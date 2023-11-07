## Unity如何往XCode的PlistInfo中加字段

在Unity中，你可以使用PostProcessBuildAttribute来在构建后自动修改Xcode的Info.plist文件。以下是一个简单的示例：

```
#if UNITY_IOS
using UnityEditor;
using UnityEditor.Callbacks;
using UnityEditor.iOS.Xcode;
using System.IO;

public class PostBuildProcessor
{
    [PostProcessBuildAttribute(1)]
    public static void OnPostprocessBuild(BuildTarget target, string pathToBuiltProject)
    {
        if (target == BuildTarget.iOS)
        {
            string plistPath = pathToBuiltProject + "/Info.plist";
            PlistDocument plist = new PlistDocument();
            plist.ReadFromString(File.ReadAllText(plistPath));

            PlistElementDict rootDict = plist.root;
            rootDict.SetString("YourKey", "YourValue");

            File.WriteAllText(plistPath, plist.WriteToString());
        }
    }
}
#endif
```

在这个示例中，你需要将"YourKey"和"YourValue"替换为你想要添加的键值对。这段代码会在Unity构建iOS项目后自动运行，将你指定的键值对添加到Info.plist文件中。
注意，这段代码需要放在Unity项目的Editor文件夹下，否则Unity不会执行它。同时，你需要在Unity中安装iOS Build Support组件以使用UnityEditor.iOS.Xcode命名空间。

