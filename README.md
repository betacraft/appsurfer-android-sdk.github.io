# AppSurfer Android SDK

AppSurfer's Android SDK makes it easy for you to integrate AppSurfer into your Android apps.


## Adding SDK to your project
### Gradle (Android Studio)
* Add AppSurfer maven repository to your applications build.gradle.

![alt Help](https://github.com/betacraft/appsurfer-android-sdk.github.io/blob/master/example/images/gradle_file.png)

```groovy
    repositories {
        ...
        maven { url 'http://maven.appsurfer.com'}
    }
```
* And then add AppSurfer SDK as dependency.
```groovy
dependencies {
    compile "com.appsurfer.android:sdk:1.0.+"
}
```
__Important__ 
> We are using Android Build Tool version : 23.0.1, Min SDK Version : 16, Target SDK version 23 and Compile SDK version 23. 

> Check your build.gradle for the project and module to check if you are on the build tool version >= 23.0.1. 

### Maven
Add following dependency and repository to your pom.xml
```xml
<project ...>
<dependecies>
    ...
    <dependency>
        <groupId>com.appsurfer.android</groupId>
        <artifactId>sdk</artifactId>
        <version>LATEST</version>
    </dependency>
</dependencies>

<repositories>
    <repository>
      <id>com.appsurfer</id>
      <url>http://maven.appsurfer.com</url>
    </repository>
 </repositories>
</project>
```

## Update your AndroidManifest.xml
In AndroidManifest.xml of your application project add the following permission (if it's already not there).
```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
<!-- Required for application that uses location -->
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
```

## Initialization
```java
/**
 * For initializing AppSurfer SDK
 *
 * @param application       Current {@link Application} instance
 * @param registrationId    registration id
 */
Appsurfer.init(application, registrationId);
```
> We do not store any reference to `application` parameter, so there is no possibility of cyclic reference. We just store the `ApplicationContext` which will be used for starting new activities.

### Set User
```java
/**
 * Set User's email address and phone number
 *
 * @param email         user email address
 * @param phone         user phone number
 */
Appsurfer.setUser(email, phone);
```

## Launch AppSurfer's appviewer

```java
AppSurferApp app = new AppSurferApp(packageName);
app.addParam(key, value)
AppSurfer.launch(app, new ApplicationLaunchStatusListener() {
    /**
     * Called when application launch is successful
     */
    void onSuccess(){
    }
    
    /**
     * Called when application launch is unsuccessful
     *
     * @param throwable reason of the exception. Use throwable.getMessage() to show user readable error
     */
    void onError(final Throwable throwable){
    }
});
```

