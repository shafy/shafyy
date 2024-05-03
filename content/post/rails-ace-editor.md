---
title: "Adding the Ace code editor with Importmap to Rails 7"
date: 2024-05-03T08:35:00+02:00
draft: false
---

The other day I wanted to integrate the [Ace code editor](https://ace.c9.io/) into a Rails 7 project I was working on. Rather than loading it from a CDN, I wanted to serve Ace from the same server and integrate it with [Rails Importmap](https://github.com/rails/importmap-rails). What I thought would be a two-minute walk in the park turned into a day-long struggle. In the end, my stubbornes and absoute disregad for the efficiency of my use of time led to a victorious outcome. Here's a quick guide how I did so that others who embark upon the same journey can sail more smoothly.

### 1. Download the required files from Ace
You need to get the required files and save them to your Rails project. In this example, we want syntax highlighting and hints for JavaScript as well as the Monokai theme. The [Ace Builds repo](https://github.com/ajaxorg/ace-builds/) offers 4 different versions of the library. We're going to go with the `src-min-noconflict` version (but it shouldn't matter which one you use, I think). Download the following files from the [src-min-noconflict repo](https://github.com/ajaxorg/ace-builds/tree/master/src-min-noconflict) and save them to the `vendors/javascript/ace/` directory in your Rails project.

```bash
ace.js
theme-monokai.js
mode-javascript.js
worker-javascript.js
```

### 2. Pin the files
In order for Rails to create an import map, you need to pin the newly downloaded files in the `importmap.rb` file. You can do that easily with one command: `pin_all_from "vendor/javascript"`. Your `importmap.rb` might now look like this:

```ruby
# importmap.rb

# these lines are probably already here
pin "application"
pin "@hotwired/turbo-rails", to: "turbo.min.js"
pin "@hotwired/stimulus", to: "stimulus.min.js"
pin "@hotwired/stimulus-loading", to: "stimulus-loading.js"
pin_all_from "app/javascript/controllers", under: "controllers"

# add this line
pin_all_from "vendor/javascript"
```

### 3. Import the files in your controller
Pinning the files does not import them yet, it just creates the import map. In my case, I set up a Stimulus controller to initiate the Ace code editor. But you can also import them directly in your `*.html.erb` files, of course.

My `ace_controller.js` looks like this:

```javascript
import { Controller } from "@hotwired/stimulus"

import "ace/ace";
import "ace/theme-monokai"
import "ace/mode-javascript";

export default class extends Controller {
  static values = { workerJavascriptUrl: String }

  connect() {
    // manually set the module URL for the javascript worker
    ace.config.setModuleUrl("ace/mode/javascript_worker", this.workerJavascriptUrlValue);
    
    // initialize ace editor
    this.editor = ace.edit("ace-editor");
    this.editor.setTheme("ace/theme/monokai");
    this.editor.session.setMode("ace/mode/javascript");
  }
}
```

And herein lied the problem that almost drove me insane. You see, I thought that the three Ace imports at the top would have been enough to run Ace. But then I learned that the JavaScript mode also automatically requires the JavaScript worker file. And by default it tries to load it from `/worker-javascript.js`. And of course, this returns a 404 because that route is not mapped to the file.

My next hunch was to add an import for the JavasScript worker with `import "ace/worker-javascript"`. After all, this also worked for the theme file. However, importing it that way led to a `window not defined` error.

After almost losing my shit, I came across a way to set the module URLs manually, and that's what you see in the first line of code in the `connect()` method above. `this.workerJavascriptUrlValue` is defined in my `*.html.erb` file as `asset_path("ace/worker-javascript.js"` – so basically just the current digested asset path to the `worker-javascript.js` file (for example looking like this: `/assets/ace/worker-javascript-916a4d168406b6aa01acd6944dd62328434ff765.js`). Since the `asset_path` method is Ruby, I need to call it in my template file and then pass the value to my JavaScript controller.

Again, you could also do all this in the template file directly. For example by using the `javascript_import_module_tag` helper from Rails Importmap like this: `<%= javascript_import_module_tag "ace/ace" %>`.


Hopefully this is helpful to others and let me know if you find an even better way to add the Ace editor to your Rails project with Importmaps.
