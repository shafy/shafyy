---
title: "Automate production settings for Oculus Go store (Unity)"
date: 2019-06-07T14:14:00+03:00
draft: false
---

If you're developing VR apps for the Oculus Go with Unity and want to distribute them through the Oculus Go store, you need to set up your app for production in Unity. However, Unity offers no easy way to go between development and production settings, making the process a pain in the ass and error prone.

Here's a small script I wrote that automates most of those tasks. Specifically, it:

* Adds a Menu in the Unity Editor with two buttons to switch between Dev and Production mode
* Sets your Package name
* Increments version number by 0.01 (only for Production mode)
* Increments bundle version code by 1 (only for Production mode)
* Adds or removes the store-compatible `AndroidManifest.xml
* Adds or removes the keystore[1]
* Enables or disables Oculus Platform Entitlement Check[2]


Hopefully this helps you :-)


```
using UnityEngine;
using UnityEditor;
using UnityEditor.SceneManagement;


// Sets the Build Mode
public class BuildMode {

  static string currentMode;

  [MenuItem("Kosmos/Dev Mode")]
  static void setDevMode() {
    setMode("dev");
  }

  [MenuItem("Kosmos/Prod Mode")]
  static void setProdMode() {
    setMode("prod");
  }

  static void setMode(string mode) {
    if (mode == "dev" && currentMode != "dev") {
      // set dev mode
      PlayerSettings.applicationIdentifier = "com.yourcompany.YourApp_dev";
      PlayerSettings.SetScriptingBackend(BuildTargetGroup.Android, ScriptingImplementation.Mono2x);
      OVRManifestPreprocessor.RemoveAndroidManifest();
      setKeystore(false);
      setEntitlementCheck(false);
      currentMode = "dev";
      return;
    }

    if (mode == "prod" && currentMode != "prod") {
      // set prod mode
      PlayerSettings.applicationIdentifier = "com.yourcompany.YourApp";
      PlayerSettings.SetScriptingBackend(BuildTargetGroup.Android, ScriptingImplementation.IL2CPP);
      PlayerSettings.bundleVersion = (float.Parse(PlayerSettings.bundleVersion) + 0.01f).ToString("#.00");
      PlayerSettings.Android.bundleVersionCode = PlayerSettings.Android.bundleVersionCode + 1;
      OVRManifestPreprocessor.GenerateManifestForSubmission();
      setKeystore(true);
      setEntitlementCheck(true);
      currentMode = "prod";
      return;
    }
  }

  static void setKeystore(bool isEnabled) {
    if (isEnabled) {
      PlayerSettings.Android.keystoreName = EnvKeys.KEYSTORE_NAME; // full local path
      PlayerSettings.Android.keyaliasName = EnvKeys.KEYALIAS_NAME;
      PlayerSettings.Android.keyaliasPass = EnvKeys.KEYALIAS_PASS;
      PlayerSettings.Android.keystorePass = EnvKeys.KEYSTORE_PASS;
      return;
    }
    PlayerSettings.Android.keystoreName = "";
    PlayerSettings.Android.keyaliasName = "";
    PlayerSettings.Android.keyaliasPass = "";
    PlayerSettings.Android.keystorePass = "";
  }

  // you might need to adapt this depending how you handle the entitlement check
  static void setEntitlementCheck(bool isEnabled) {
      EditorSceneManager.SaveCurrentModifiedScenesIfUserWantsTo();
      EditorSceneManager.OpenScene("Assets/Shared/Scenes/WelcomeScreen.unity");
      GameObject gameController = GameObject.Find("GameController");
      gameController.GetComponent<OculusPlatformSetup>().DoEntitlementCheck = isEnabled;
      EditorSceneManager.SaveScene(EditorSceneManager.GetActiveScene());
  }
}
```

* [1] Since I don't want to check in the keystore path and passwords to version control, I created a separate class `EnvKeys` that holds those static values (like an .env file)

* [2] For the entitlement check, I have a component called `OculusPlatformSetup` on a GameObject called `GameController` in the first scene that's loaded in the app (called `WelcomeScene`). `OculusPlatformSetup` performs the entitlement check if `DoEntitlementCheck == true`. The reason for this is that if you build locally on your device, the entitlement check doesn't pass (as of writing this, they hopefully change that in the future), so you need to skip it.
