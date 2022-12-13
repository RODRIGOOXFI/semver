# POC Autmoatic Versioning

## Using the semver gradle plugin 

This is a fork of the public and open source plugin found in https://github.com/dipien/semantic-version-gradle-plugin

In order to enable this plugin to work according to how we use our flow into the project wa required to created a fork 
that can be found in https://github.com/RODEVS/semantic-version-gradle-plugin this is public and specially adapted 
to what we need.

## Using the plugin 

To use the plugin into our projects we must add the plugin into the main build.gradle of the project

```
buildscript {
    repositories {
        maven {
            name = "GitHubPackages"
            url = uri("https://maven.pkg.github.com/RODEVS/semantic-version-gradle-plugin")
        }
    }
    dependencies {
        classpath("com.rodevs.semantic-version:semantic-version-gradle-plugin:2.0.0")
    }
}
```

This should only be added into the main build.gradle


After that to enable in each required project you just need to apply the plugin in each subroject build.gradle file
like so:

```
version = "5.1.0" // Assign your project version here

apply plugin: "com.rodevs.semantic-version"
```

Notice that the plugin must be apply after the version of the project; otherwise an exception will be raised by the plugin


## Using the gradle plugin

Because this plugin directly modifies the version of the project in the build.gradle file
this version can be seen any time by opening the required build.gradle project.

Keep in mind that the version should not be directly or manually modified.

### Print actual version

To print the version of the project you can just:

```
./gradlew subprojectName:printVersion
```

This is goint to print the version from the build.gradle file

```
e.g

./gradlew module-1:printVersion                                                                                                                     ✔ 

> Task :module-1:printVersion
Version: 5.0.0

BUILD SUCCESSFUL in 1s
1 actionable task: 1 executed

```

To print the version of all the subprojects just type

```
./gradlew printVersion
```


## Increase version 

The incrementVersion task increments the project version on your root build.gradle[.kts] file. The versionIncrementType option defines the type of increment: MAJOR, MINOR or PATCH

```
 // Increments the major from 1.0.0 to 2.0.0
./gradlew subproject:incrementVersion --versionIncrementType=MAJOR

// Increments the minor from 1.0.0 to 1.1.0
./gradlew subproject:incrementVersion --versionIncrementType=MINOR

// Increments the patch from 1.0.0 to 1.0.1
./gradlew subproject:incrementVersion --versionIncrementType=PATCH
```

##Using RC versions 

To use RC version you just need to use the RC icrement type, if the version is not a RC already this is going to change
to .RC.N

e.g
```
// Increments the major from 1.0.0-SNAPSHOT to 1.0.0.RC.0
./gradlew subproject:incrementVersion --versionIncrementType=RC  


// Increments the major from 1.0.0.RC.0 to 1.0.0.RC.1
./gradlew subproject:incrementVersion --versionIncrementType=RC 

// Increments the major from 1.0.0.RC.1 to 1.0.0.RC.2
./gradlew subproject:incrementVersion --versionIncrementType=RC

// Increments the major from 1.0.0.RC.2 to 1.0.0.RC.3
./gradlew subproject:incrementVersion --versionIncrementType=RC

.
.
.

```

When no other RC version is required use the versionIncrement=release

```

// Increments the major from 1.0.0.RC.2 to 1.0.0
./gradlew subproject:incrementVersion --versionIncrementType=RC

```

This is going to discard the suffix of the actual version and updated the file