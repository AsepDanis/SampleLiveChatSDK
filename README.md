# Live Chat SDK by Sociomile

### Required

* Programming language Kotlin
* Minimum Android SDK 21 (Android 5.0 - 5.0.2 Lollipop)

### Download

1. Add jcenter, maven central and jitpack to the root build.gradle file of your project at the end of repositories.
```
allprojects {
  repositories {
    ...
    jcenter()
    mavenCentral()
    maven { url 'https://jitpack.io' }
  }
}
```

2. Add into the root local.properties file of your project.
```
# credential for download library live chat sdk request to admin sociomile
ext.user = /* your userid */
ext.key = /* your personal token */
```

3. Add into app/build.gradle file of your project.
```
plugins {
    ...
}

Properties properties = new Properties()
properties.load(project.rootProject.file("local.properties").newDataInputStream())
repositories {
    maven {
        name = "GitHubPackages"
        url = uri("https://maven.pkg.github.com/AsepDanis/LiveChatSDK")
        credentials {
            username = properties.getProperty("ext.user")
            password = properties.getProperty("ext.key")
        }
    }
}

android {
    ...
}
``` 

4. Add the dependency
```
implementation "org.sociomile.livechat.sdk:core:1.0.5"
``` 

### Usage
Usage is very simply, you only need to do following:

#### Add this widget into your xml layout:

```xml
<org.sociomile.livechat.sdk.ChatFab
    android:id="@+id/fab"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="bottom|end"
    android:layout_margin="16dp"
    app:themeColor="red|blue"/>
```

#### Configuration

* your set clientId already registered in sociomile:
```
SocketManager.clientId = "/* your clientId set in here */"
```

* your create `CoroutineEvent.registerEvent` for handle event:
```
CoroutineEvent.registerEvent(String::class.java) { event ->
    when(event) {
        SocketManager.TAG_RESET -> {
            binding.fab.count = 0
        }
        SocketManager.TAG_UPDATE -> {
            binding.fab.increase()
        }
    }
}
```
