# 自定义 package

## MenuItem

MenuItem 把任何静态方法做到菜单命令中，只有静态方法才能使用 MenuItem 。

```csharp
// MenuItem 有三种构造方法
public MenuItem(string itemName);
// isValidateFunction：是否是验证方法
public MenuItem(string itemName, bool isValidateFunction);
// priority：优先级，数值大的在下面，如果菜单项数字间隔太大，显示时会有分割线
public MenuItem(string itemName, bool isValidateFunction, int priority);

//example
[MenuItem("8ku/MenuName", false, -10)]
```



### 代码中指定快捷键

`UnityEditor` 中的 MenuItem 可设定自己的菜单，并为其指定快捷键。

| key                 | macOS         | Windows        |
| ------------------- | ------------- | -------------- |
| %                   | cmd           | control        |
| #                   | shift         | shift          |
| &                   | alt           | alt            |
| #LEFT/RIGHT/UP/DOWN | left shift... | left shift ... |
| HOME/END/PGUP/PGDN  | ...           | ...            |

```csharp
# if UNITY_EDITOR
using UnityEditor;
# endif
  
namespace Baku 
{
    public class ReuseMenuItems
    {
#if UNITY_EDITOR 
        [MenuItem("8ku/ReuseMenuItems %e")] // “%e”表示 cmd + e 菜单项快捷键,快捷键必须和菜单名之间用空格分离

        private static void MenuClicked()
        {
            // 调用复制文件名的菜单命令，并打开文件夹
            EditorApplication.ExecuteMenuItem("8ku/CopyPackageName");
            // 要使用 combine, path.combine需要引用System.IO，../表示该目录的上级目录
            Application.OpenURL("file:///" + Path.Combine(Application.dataPath, "../"));
        }
    }
#endif
}
```

## ExportPackage

用于以 unitypackage 的文件形式导出 assets 到指定目录下。

```csharp
AssetDatabase.ExportPackage(assetPathName, fileName, ExportPackageOptions.Recurse);
```

ExportPackageOptions:

| [Default](ExportPackageOptions.Default.html)                 | Default mode. Will not include dependencies or subdirectories nor include Library assets unless specifically included in the asset list. |      |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| [Interactive](ExportPackageOptions.Interactive.html)         | The export operation will be run asynchronously and reveal the exported package file in a file browser window after the export is finished. |      |
| [Recurse](ExportPackageOptions.Recurse.html)                 | Will recurse through any subdirectories listed and include all assets inside them. |      |
| [IncludeDependencies](ExportPackageOptions.IncludeDependencies.html) | In addition to the assets paths listed, all dependent assets will be included as well. |      |
| [IncludeLibraryAssets](ExportPackageOptions.IncludeLibraryAssets.html) | The exported package will include all library assets, ie. the project settings located in the Library folder of the project. |      |

## System.Obsolete

方法过时的标记，加上，之后调用该方法编译器会给出提示

```csharp
[Obsolete("方法已过时,请使用xxx方法")]
public static void functionName(){}
```

## Partial 让类可以在调用时修改

会经常调用且需要个性化的类，可以在类名中增加 partial 字段，可以让类在被调用时可添加新方法，不影响原类模板。

不需要经常修改的类不需要加 partial 。

不需要从外部调用的可以设置为 private 。

```csharp
namespace Baku
{
  public partial class ClassName
  {
    function;
  }
}
```

