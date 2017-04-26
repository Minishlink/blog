---
layout: post
title:  "How to compile your React-Native or Android app with the latest Android build-tools"
categories: dev
tags: android react-native gradle
---
# How to compile your React Native or Android app with the latest Android build-tools
With the release of Gradle 3 and the great performance boost it comes with, it's very tempting to update like so:
 
1. in your root `build.gradle`, update the Gradle plugin so that it uses Gradle 3+: 
```gradle
...
dependencies {
    classpath 'com.android.tools.build:gradle:2.3.0'
...
```

2. in your `app/build.gradle`, update the build tools to the latest (25), because it's mandatory to support Gradle 3+:
```gradle
...
android {
    compileSdkVersion 23
    buildToolsVersion "25.0.2"
...
```

Sadly, you'll very much likely encounter this sort of error: 
`The SDK Build Tools revision (23.0.1) is too low for project ':react-native-vector-icons'. Minimum required is 25.0.0`.
That's because one of your dependency (here, react-native-vector-icons) uses an old build tools version.

The process of updating the dependency (make a PR, be reviewed, be merged, and be published) can take a long time.
Fortunately, you can overwrite the build tools version of your dependencies. To do so, add in your root `build.gradle`:

```
ext {
    compileSdkVersion = 23
    buildToolsVersion = '25.0.2'
}

subprojects { subproject ->
    afterEvaluate{
        if((subproject.plugins.hasPlugin('android') || subproject.plugins.hasPlugin('android-library'))) {
            android {
                compileSdkVersion rootProject.ext.compileSdkVersion
                buildToolsVersion rootProject.ext.buildToolsVersion
            }
        }
    }
}
```

And in your `app/build.gradle`:
```
...
android {
    compileSdkVersion rootProject.ext.compileSdkVersion
    buildToolsVersion rootProject.ext.buildToolsVersion
...
```
