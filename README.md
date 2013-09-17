## AppSurfer Android SDK ##
This documentation helps in Integrating AppSurfer SDK with your Android project:

## Build Systems ##
We support 3 build systems for Android.

1. JAR :
If you use Ant as your build system for Android project then you just simply have to add AppSurferViewer.jar into your   libraries and you are good to go. As we do not use any resources inside the library (till version 0.1), so you need not to worry about adding the entire source code into your project.

2. MAVEN: If you are using maven build system, then add following code to your pom.xml
    2.1 Add AppSurfer repository into <repositories></repositories> tag
```java
    <repositories>
        <id>AppSurfer viewer</id>
        <url>http://www.appsurfer.com/appsurfer_viewer_mvn_repo/</url>
    </repositories>
```

    2.2 Add AppSurferViewer dependency into the code.
```java
    <dependency>
        <groupId>com.appsurfer</groupId>
        <version>0.1.0</version>
    	<packaging>jar</packaging>
    	<artifactId>viewer-sdk</artifactId>
    </dependency>
```
3. Gradle: Gradle can use [maven repo](http://www.gradle.org/docs/current/userguide/maven_plugin.html).

## Using AppSurfer viewer ##

### Permissions ###

```java
    <uses-permission android:name="android.permission.WAKE_LOCK"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
```

### Code ###

1. First of all you need to initialize AppSurferViewer SDK in your Application or make sure that you perform init on AppSurferViewer before you start working with it.
```java
    package main.java.com.appsurfer.viewer.sample;

    import android.app.Application;
    import main.java.com.appsurfer.viewer.AppSurferViewerApplication;

    public class SampleApplication extends Application {

        @Override
        public void onCreate() {
            super.onCreate();
            AppSurferViewerApplication.init(getApplicationContext());
        }

        @Override
        public void onTerminate() {
            super.onTerminate();
        }
    }
```

2. You can directly use replace or add for AppSurferViewerFragment with fragment manager.
```java
     // 1 is app id
     Fragment fragment = AppSurferViewerApplication.getAppSurferViewerFragment(1);
     FragmentTransaction t = getSupportFragmentManager().beginTransaction();
     t.replace(R.id.main_layout, fragment);
     t.commit();
```
3. AppSurferViewer fragment supports callbacks so that you can handle various events.
```java
    viewerFragment.setAppSurferSessionEventListener(new AppSurferSessionEventListener() {
            @Override
            public void onAppSurferSessionCloseClickedEvent() {               
            }

            @Override
            public void onAppSurferSessionInstallClickedEvent() {              
            }

            @Override
            public void onAppSurferSessionStartedEvent() {
            }

            @Override
            public void onAppSurferSessionConnectedEvent() {                
            }

            @Override
            public void onAppSurferSessionTimeoutOutEvent() {         
            }

            @Override
            public void onAppSurferSessionClosedEvent() {               
            }

            @Override
            public void onAppSurferSessionExceptionEvent(main.java.com.appsurfer.viewer.exceptions.AppSurferException exception)         
            {
            }
        });
```
