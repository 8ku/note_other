# 背包系统

```csharp
void ParseItemJson()
{
  itemList = new List<Item>();
  //用Resources来读取文件,需要先创建一个Resources文件夹
  //The Resources class allows you to find and access Objects including assets.
  TextAsset itemText = Resources.Load<TextAsset>("Items");
}
```

