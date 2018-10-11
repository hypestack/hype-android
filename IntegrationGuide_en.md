


## Hypestack SDK Integration Guide (Android, v1.0.0)



#### *“Ads you and your users will love.”*



### Overview

Hypestack works uniquely in chat and is driven by user-expressed intent from their actual conversations.  Work with us to grow your revenue in chat while providing the next level of excellent user experience.  User privacy is protected because conversations are processed on-device by our local SDK and users have full control over their expressed intent.

This guide provides instructions for incorporating the Hypestack Android SDK into your app.  To request access to the Hype SDK (hype-sdk-1.0.x.jar), please email us at partner@hypestack.io.

### Quick Start

**Step 1:  Clone the SDK repository (copy all jars from /lib)**

```
git clone https://github.com/hypestack/hype-android
```

**Step 2: Setup your gradle build  (we recommend as a third-party library)**
```
api fileTree(include: ['*.jar'], dir: 'lib')      
```
**Step 3: Initialize the Hype SDK (call this in your top-level activity)**

```
public class MyActivity extends Activity {
   protected void onCreate(Bundle bundle) {
      Hype.init(getContext());
   }
}
```

**Step 4: Process each message  (this does not send the message)**

```
HypeMessage msg = Hype.monetize(Context(), to, text);
```

**Step 5: Render the message (matched intent will appear as links)**

```
Spannable span = Hype.render(getContext(), msg);
...
view.setMovementMethod(LinkMovementMethod.getInstance());
view.setText(span, TextView.BufferType.SPANNABLE);
```


### API Overview


#### Hype Initialization

```
/** 
* Initialize the Hypestack SDK.
* @param context - Context 
* @note this method is non-blocking
*/
public void init(Context ctx)
```

#### Message Process
```
/** 
* Takes in a message text, determines intent, and returns a HypeMessage. A
* HypeMessage contains an EMMessage that may be sent by the ChatManager 
* and which contains metadata for rendering it in the UI. 
* If HypeMessage.echo() returns true, the message starts with a “#”
* and should be saved locally for the current user, not sent.
* @param ctx- Context
* @param to - username
* @param text - message text
* @returns HypeMessage (get() returns the EMMessage) 
* @see HypeMessage 
*/
public HypeMessage monetize(Context ctx, String to, String text);
```

#### Link Decoration
```
/** 
* Takes a HypeMessage and creates spannable text to be rendered in 
* the UI for current user. The Spannable already contains metadata for 
* rendering the link in a View, but may be used as a CharSequence.
* @param context - Context 
* @param HypeMessage (get() returns the EMMessage) 
*/
public Spannable render(Context ctx, HypeMessage msg);
```

#### *TextView Render (optional, for convenience only)*
```
/** 
* Takes a HypeMessage and a TextView for rendering the message. If a 
* different component is desired, use the Spannable directly.
* @param context - Context 
* @param msg - HypeMessage
* @param view - TextView 
*/
public void render(Context ctx, HypeMessage msg, TextView view);
```

#### Activity Registration

To enable WebView support, include the following activity in your AndroidManifest.xml:

```
<activity
android:name="com.hypestack.android_sdk.ui.WebActivity"
android:screenOrientation="portrait"
android:theme="@style/horizontal_slide"
android:hardwareAccelerated="true">
</activity>
```

#### Manifest Permissions

To enable geolocation, add the following permissions to your AndroidManifest.xml:

```
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```
This will trigger the appropriate consent when the user installs the upgrade. If the user already has the permissions, no consent will be required.


#### Android SDK & JDKs

The Hype SDK is currently targeting API 26 (Oreo), JDK 1.8, and uses the following support libraries:

```
com.android.support:appcompat-v7:26.1.0
com.android.support.constraint:constraint-layout:1.1.3
```

### Hypestack Support

Please do not hesitate to ask us questions at support@hypestack.io.

###### Copyright (c) by Hypestack, Inc. All Rights Reserved.

