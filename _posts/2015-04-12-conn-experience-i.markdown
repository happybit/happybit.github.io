---
layout: post
title: "Conn Experience I"
date: 2015-04-12 20:40
comments: true
categories: Others
---

Conn的核心操作不过是自动toggle data connection。可以将`ConnectivityManager`中的`setMobileDataEnabled`方法reflection出来使用。

<!--more-->

~~~ java
{% highlight java %}
final ConnectivityManager conman = (ConnectivityManager)  context.getSystemService(Context.CONNECTIVITY_SERVICE);
final Class conmanClass = Class.forName(conman.getClass().getName());
final Field connectivityManagerField = conmanClass.getDeclaredField("mService");
connectivityManagerField.setAccessible(true);
final Object connectivityManager = connectivityManagerField.get(conman);
final Class connectivityManagerClass =  Class.forName(connectivityManager.getClass().getName());
final Method setMobileDataEnabledMethod = connectivityManagerClass.getDeclaredMethod("setMobileDataEnabled", Boolean.TYPE);
setMobileDataEnabledMethod.setAccessible(true);

setMobileDataEnabledMethod.invoke(connectivityManager, enabled);
{% endhighlight %}
~~~

同时，在`AndroidManifest.xml`中添加下列两行，需要获取这两项权限：

    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />


年初手机升级5.0后，突然发现应用无法使用，出错信息提示“NoSuchMethodException”。搜了一圈，发现Android Lollipop之后，该方法已从`ConnectivityManager`中移除了。在AOSP论坛里，开发人员已经[哀嚎一片](https://code.google.com/p/android/issues/detail?can=2&start=0&num=100&q=&colspec=ID%20Type%20Status%20Owner%20Summary%20Stars&groupby=&sort=&id=78084)。短期内看来，Google不会有进一步的反应。应该也有考虑第三方apps偷偷打开数据连接偷流量的风险。

无奈，再寻找work-around。现阶段找到的一个是通过`su` command直接操作，动作是糙了点，而且这种方式下device必需要rooted。不过还好有效。

~~~ java
{% highlight java %}
String state = (enabled) ? "enable" : "disable";
String command = String.format("svc data " + state + "\n");

try{
    Process su = Runtime.getRuntime().exec("su");
    DataOutputStream outputStream = new DataOutputStream(su.getOutputStream());

    outputStream.writeBytes(command);
    outputStream.flush();

    outputStream.writeBytes("exit\n");
    outputStream.flush();
    try {
        su.waitFor();
    } catch (InterruptedException e) {
        e.printStackTrace();
    }

    outputStream.close();
}catch(IOException e){
    e.printStackTrace();
}
{% endhighlight %}
~~~

详细调用情况请参看[这里](https://github.com/happybit/Conn/blob/master/app/src/main/java/me/pzheng/conn/DataConn.java)。




