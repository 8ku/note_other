# Tags管理

用一个单独的脚本管理工程中的tags,把标签名常量化,这样当使用标签时,编译器会自动提示标签名,防止打字出错.

```c#
public class Tags:Monobehaviour
{
  public const string ground = "Ground";
  public const string player = "Player";
}
```

