手上有一个工程非常古老，是unity 5.4.5版本的，最近心血来潮，对这个工程进行Unity版本升级，一口气升级到Unity 2019，期间遇到不少问题，于是记录下来分享给大家。

‘GUITexture’ is obsolete: ‘GUITexture has been removed. Use UI.Image instead.’
修改方法：

添加命名空间： using UnityEngine.UI；

将GUITexture替换为Image

Didn’t find class “com.unity3d.player.UnityPlayerNativeActivity”
修改方法：

把 Manifest 

<activity android:name=”com.unity3d.player.UnityPlayerNativeActivity” … >

中的 UnityPlayerNativeActivity 修改为 UnityPlayerActivity:

<activity android:name=”com.unity3d.player.UnityPlayerActivity” … >

‘Image’ does not contain a definition for ‘texture’
修改方法：

Image.texture改为Image.material.mainTexture

‘PBXProject.GetUnityTargetName()’ is obsolete: ‘This function is deprecated

```C#
#if UNITY_2019_3_OR_NEWER
string targetId = project.GetUnityFrameworkTargetGuid();
#else
string targetId = project.TargetGuidByName(PBXProject.GetUnityTargetName());
#endif
```
