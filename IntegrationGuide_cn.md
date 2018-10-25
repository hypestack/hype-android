## Hypestack SDK集成指南 （Android，V1.0.0）

#### *“您和您的用户一定会喜欢的广告.”*

### 概述

Hypestack独特性的技术通过用户的实际对话去了解他们的意图。与我们合作您能在聊天窗口
中增加财政收入的同时也提供更好的用户体验。您的用户隐私将会受到保护，因为我们的SDK是在本地设备上处理对话和让用户完全控制其表达的意图。

本指南提供了 Hypestack Android SDK 集成应用说明。


### 快速集成指引


**步骤1：设置gradle构建  （我们建议作为第三方库）**
```
api fileTree（包括：['* .jar']， dir： 'lib'）
```

**步骤2：初始化Hype SDK （在顶层活动中调用此公共类）**
```
public class MyActivity extends Activity {
   protected void onCreate(Bundle bundle) {
      Hype.init(getContext());
   }
}
```

**步骤3：处理的每个消息  （这不发送消息）**

```
HypeMessage msg = Hype.monetize（Context（），to，text）;
```

**步骤4：装饰消息 （匹配意图将显示为链接）**
```
Spannable span =.render Hype（getContext（），msg）;
...
view.setMovementMethod（LinkMovementMethod.getInstance（））;
view.setText（span，TextView.BufferType.SPANNABLE）;
```





### API概述


#### 初始化
```
/**
* Initialize Hypestack SDK。
* @param context  -  Context
* @note此方法是非阻塞的
*/
public void init（Context ctx）
```

#### 消息处理
```
/**
* 接收消息文本，确定intent，并返回HypeMessage。
* HypeMessage包含可由ChatManager发送的EMMessage，其中包含用于在UI中呈现它的元数据。
* 如果HypeMessage.echo（）返回true，则消息以“＃”开头，
* 并且应该在本地保存给当前用户，而不是发送。
* @param ctx- Context
* @param to  -  username
* @param text  -  message text
* @returns HypeMessage（get()返回EMMessage）
* @see HypeMessage
* /
public HypeMessage monetize(Context ctx, String to, String text);
```

#### 链接装饰
```
/**
* 采用HypeMessage并创建可在呈现的可跨越文本 当前用户的UI中。 Spannable已经包含用于元数据
* 在视图中呈现链接的，但可以用作CharSequence。
* @param context  -  Context
* @param HypeMessage（get() 返回EMMessage）
*/
public Spannable render（Context ctx，HypeMessage msg）;
```

#### *TextView 装饰 （可选，仅为方便起见)*
```
/**
* 使用HypeMessage和TextView呈现消息。如果需要不同的组件，请直接使用Spannable。
* @param context  -  Context
* @param msg  -  HypeMessage
* @param view  -  TextView
*/
public void render（Context ctx，HypeMessage msg，TextView view）;
```

#### Activity 注册

要启用WebView支持，请在AndroidManifest.xml中包含以下活动：

```
<activity
android：name =“com.hypestack.android_sdk.ui.WebActivity”
android：screenOrientation =“portrait”
android：theme =“@ style/ horizo​​ntal_slide “
android：hardwareAccelerated =”true“>
</ activity>
```

#### Manifest 权限

要启用地理位置，请将以下权限添加到AndroidManifest.xml：

```
<uses-permission android：name =”android.permission.ACCESS_COARSE_LOCATION“/>
<uses-permission android：name =“android.permission.ACCESS_FINE_LOCATION”/>
```

这将在用户安装升级时触发相应的同意。如果用户已拥有权限，则不需要同意。


#### Android SDK和JDK

Hype SDK目前面向API 26（Oreo），JDK 1.8，并使用以下支持库：:

```
com.android.support:appcompat-v7:26.1.0
com.android.support.constraint:constraint-layout:1.1.3
```

### 技术咨询

如果您有任何问题，请不要客气向我们提问 @ support@hypestack.io

###### Copyright (c) by Hypestack, Inc. All Rights Reserved.



