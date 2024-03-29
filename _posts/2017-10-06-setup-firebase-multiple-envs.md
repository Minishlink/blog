---
layout: post
title:  "Setup Firebase on iOS/Android with multiple environments"
categories: dev ios android
tags: macOS
---
# Setup Firebase on iOS/Android with multiple environments

It's pretty straightforward to install Firebase when you have only one environment.
But what if you have multiple environments, such as `dev`, `staging` and `production`?
Here's a step-by-step guide.

## Android
On Android, Firebase groups the different configurations in one file.

1. Go to the [Firebase console](https://console.firebase.google.com/)
2. Select your project
3. Click "Add an application", choose Android
4. Fill in the form (giving a name like `Staging`), click save, and close the window
5. Repeat steps 3 to 4 for all your environments
5. Download the `google-services.json` file
   1. Select one of the Android applications
   2. Click on "google-services.json"
6. Put `google-services.json` in your `app` folder (`android/app` in React-Native)
7. You might want to add `google-services.json` in your `.gitignore`

![steps]({{ site.baseurl }}/assets/articles/2017-10-06-setup-firebase-multiple-envs/firebase_android.png)

## iOS
On iOS, there is one Firebase configuration file per environment.

1. Go to the [Firebase console](https://console.firebase.google.com/)
2. Select your project
3. Click "Add an application", choose iOS
4. Fill in the form (giving a name like `Staging`), click save
5. Download the configuration file `GoogleService-Info.plist` and rename it like `GoogleService-Info.{APP_IDENTIFIER}.plist`
   * Example: for `tech.bam.myApp.staging`, `GoogleService-Info.tech.bam.myApp.staging.plist`
6. Repeat steps 3 to 5 for all your environments
7. Put your configuration files in the root of your iOS app folder (`ios` in React-Native)
8. Make sure that your app identifier is injected in your `.pbxproj`. For example, if you're using Fastlane, add a `update_app_identifier` step like:
```ruby
update_app_identifier(
  xcodeproj: xcodeproj_full_path,
  plist_path: plist_full_path,
  app_identifier: ENV['APP_IDENTIFIER']
)
```
9. In XCode, in `Build phases`, add a `Select GoogleService-Info.plist` build step before the `Copy Bundle Resources` step that contains:
```bash
cp "GoogleService-Info."$PRODUCT_BUNDLE_IDENTIFIER".plist" "GoogleService-Info.plist"
```
10. In XCode, in `Build phases`, add a `Clean GoogleService-Info.plist` build step after the `Copy Bundle Resources` step that contains:
```bash
rm "GoogleService-Info.plist"
```
11. Make sure that the `GoogleService-Info.plist` is listed in the resources of the `Copy Bundle Resources` step
12. You might want to add `GoogleService-Info.*.plist` in your `.gitignore`

![steps]({{ site.baseurl }}/assets/articles/2017-10-06-setup-firebase-multiple-envs/ios_steps.png)
