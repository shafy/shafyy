---
title: "A better CSV import"
date: 2022-05-07T09:59:09Z
draft: false
---

If you ever had to import data from a CSV file in a web app, there's a high chance that your experience wasn't great. You need to prepare a file with the required columns, export to .csv and make sure to get the delimiter right. (Ironically, even though CSV stands for *comma* separated values, the delimiter can be a different character like a semicolon or tab). The fun doesn't stop there. If there are any errors in your data, such as wrong formatting or missing values, the app will tell you to fix it before continuing. Now, you need to go back to Excel or Google Sheets and find the erroneous cells. Rinse and repeat.

When building the bulk location import feature for [Mapzy](https://mapzy.io), our open-source and self-hostable store finder, we wanted to provide a better import experience for our users. We wanted to spare them the pain of dealing with exporting files and choosing delimiters, and we wanted to make it simple for them to fix any import errors.

In an innovation that can only be likened to the invention of the first iPhone, we came up with the following: In the import screen, we provide an embedded spreadsheet that already has the correct headers filled out. Instead of choosing a file from their computer, users just copy and paste their CSV data into this spreadsheet and press the big red button. If there are any errors, we simply highlight the relevant cells in the spreadsheet. This way, users can easily fix them right then and there without needing to fiddle with a separate file and go through the whole process again.

Ladies and gentlemen, without further ado, I present to you - the Mapzy location importer:

<video width="100%" controls>
  <source src="/videos/mapzy_bulk_import_demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

If there are errors, we handle them like this:

<video width="100%" controls>
  <source src="/videos/mapzy_bulk_import_error_demo.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

For those who are interested in the technical background, more details follow.

For the spreadsheet, we use the excellent [Jspreadsheet](https://github.com/jspreadsheet/ce) library. If there are no errors, the import happens in two steps because importing a lot of locations requires a lot of calls to the Mapbox geocoding API (geocoding is converting an address to longitude and latitude), which is rate limited.

In the first step, we only validate if the information is all there and correctly formatted. For example, if a location name is missing, we highlight that error in the spreadsheet. If everything looks good, we save the locations to the database using the awesome [Activerecord-Import](https://github.com/zdennis/activerecord-import) library, but skip calling the geocoding API. Rather, we mark these locations as "to be geocoded".

In the second step, we then start a background job (with Sidekiq and Redis) that goes through the database and checks all locations that are related to the given map and geocodes their addresses if necessary. If a geocoding attempt is not successful, we later ask the user to correct the address from their Mapzy dashboard.

If you're interested in the code, have a look at [location_imports_controller.rb](https://github.com/mapzy/mapzy/blob/main/app/controllers/dashboard/location_imports_controller.rb), [location_import.rb](https://github.com/mapzy/mapzy/blob/main/app/models/location_import.rb), and [batch_geocode_worker.rb](https://github.com/mapzy/mapzy/blob/main/app/workers/batch_geocode_worker.rb).

An added technical bonus of this approach is that we don't need to deal with mapping columns from a CSV file to our data models, which can be a whole can of worms in itself.