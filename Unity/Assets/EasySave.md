# Easy Save

## 保存文件

以字典的方式保存，key : value

### 数据保存路径

- setiing
  -  location：建议用 PersistentDataPath（持久数据路径），在各平台都可以正常储存

### 数据分类保存

```c#
//保存到默认路径下的默认文件中
ES3.Save<int>("ChinaInt",666);
//保存到默认路径下 ChinaFile.es3 文件中
ES3.Save<int>("ChinaInt",777,"ChinaFile.es3");
//保存到默认路径下 ChinaFolder 文件夹下的 ChinaFile.es3 文件中
ES3.Save<int>("ChinaInt",888,"ChinaFolder/ChinaFile.es3");
//保存到指定路径下 ChinaFolder 文件夹下的 ChinaFile.es3 文件
ES3.Save<int>("ChinarInt", 999, "C:/Users/Administrator/Desktop/ChinarFile.es3");
```

### 把数据直接赋值给指定对象

`ES3.LoadInto<T>()`

```c#
//保存cube1的数据，赋值给Cub2
void Start()
{
    //保存cube1的数据
    ES3.Save<Transform>("Cube1",Cube1.transform);
    //读取cube1数据赋值给cube2
    ES3.LoadInto("Cube1",Cube2.transform);
}
```

### 删除

```c#
void Start()
{
    // 从文件中删除一个键
    ES3.DeleteKey("Chinar_Key", "ChinarFolder/ChinarFile3.es3"); 
    // 删除整个文件
    ES3.DeleteFile("ChinarFolder/ChinarFile3.es3");    
    // 删除一个目录及其包含的所有文件
    ES3.DeleteDirectory("ChinarFolder/"); 
}
```

## 加密

### 动态加密

```c#
void Start()
{
    //第一步：声明一个 ES3Settings 对象
    ES3Settings settings = new ES3Settings();
    //第二步：设置加密方式为AES
    settings.encryptionType = ES3.EncryptionType.AES;
    //第三部：设置密码：密码要求为`string`类型
    settings.encryptionPassword = "ChinarPassword";
    //第四步：使用 settings 对象的设置信息，进行加密保存
    ES3.Save<Transform>("Chinar_Cube1", Cube1.transform, Application.dataPath + "/ChinarFile4.es3", settings);
}
```





