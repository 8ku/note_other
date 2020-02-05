# 保存和读档

## 存档

### 创建一个类保存数据 - 把数据序列化存到文件

- PlayerPrefs：数据持久化方案
  - 键值对
    -  ` PlayerPrefs.SetInt(“Index”, 1);`
    - `PlayerPrefs.SetFloat(“Height”,180.5f);`
    - `PlayerPrefs.SetString(“Name”,”Tom”);`
  - 获取数据
    - `PlayerPrefs.GetInt(“Index”);`
    - `PlayerPrefs.GetFloat(“Index”);`
    - `PlayerPrefs.GetString(“Index”);`
  - 适用于使用频繁的数据，需要频繁调用
    - 药水、技能
- Serialization 序列化
  - 二进制：通过二进制格式器写入读出，简单，可读性差
  - XML，可读性强，文件庞大，冗余信息多
    - 适用于建立装备数据库
  - JSON：数据格式简单，易读写，但不直观，可读性比 XML 差
    - 适用于游戏存档
    - json 最好建立在对应不同文件夹下

```c#
//以存储角色信息为例

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using LitJson; //引用 json 类
using System.IO;
using UnityEditor;

public class Person
{
    public string Name { get; set; }
    public double HP { get; set; }
    public int Level { get; set; }
    public double Exp { get; set; }
    public int Attak { get; set; }

}
public class PersonList
{
    public Dictionary<string, string> dictionary = new Dictionary<string, string>();
}

public class Classtext : MonoBehaviour {
    /*定义一个Person对象（其属性包括，Name，HP,Level，Exp,Attak等），
     将其转会成json格式字符串并且写入到person.json的文本中，
     然后将person.json文本中的内容读取出来赋值给新的Person对象。
     */
	
    public PersonList personList = new PersonList();

    // Use this for initialization
    void Start () {
	    //初始化人物信息
        Person person = new Person();
        person.Name = "Czhenya";
        person.HP = 100;
        person.Level = 30;
        person.Exp = 999.99;
        person.Attak = 38;
		
		//调用保存方法
       Save(person);
        
    }
    /// <summary>
    /// 保存JSON数据到本地的方法
    /// </summary>
    /// <param name="player">要保存的对象</param>
    public void Save(Person player)
    {
        //打包后Resources文件夹不能存储文件，如需打包后使用自行更换目录
        string filePath = Application.dataPath + @"/Resources/JsonPerson.json";
        Debug.Log(Application.dataPath + @"/Resources/JsonPerson.json");

        if (!File.Exists(filePath))  //不存在就创建键值对
        {
            personList.dictionary.Add("Name", player.Name);
            personList.dictionary.Add("HP", player.HP.ToString());
            personList.dictionary.Add("Level", player.Level.ToString());
            personList.dictionary.Add("Exp", player.Exp.ToString());
            personList.dictionary.Add("Attak", player.Attak.ToString());

        }
        else   //若存在就更新值
        {
            personList.dictionary["Name"] = player.Name;
            personList.dictionary["HP"] = player.HP.ToString();
            personList.dictionary["Level"] = player.Level.ToString();
            personList.dictionary["Exp"] = player.Exp.ToString();
            personList.dictionary["Attak"] = player.Attak.ToString();
        }
       
        //找到当前路径
        FileInfo file = new FileInfo(filePath);
        //判断有没有文件，有则打开文件，，没有创建后打开文件
        StreamWriter sw = file.CreateText();
        //ToJson接口将你的列表类传进去，，并自动转换为string类型
        string json = JsonMapper.ToJson(personList.dictionary); 
        //将转换好的字符串存进文件，
        sw.WriteLine(json);
        //注意释放资源
        sw.Close();
        sw.Dispose();

        AssetDatabase.Refresh();

    }

    /// <summary>
    /// 读取保存数据的方法
    /// </summary>
    public void LoadPerson()
    {
        //调试用的  //Debug.Log(1);
        
        //TextAsset该类是用来读取配置文件的
        TextAsset asset = Resources.Load("JsonPerson") as TextAsset;
        if (!asset)  //读不到就退出此方法
            return;

        string strdata = asset.text;		
        JsonData jsdata3 = JsonMapper.ToObject(strdata);
		//在这里循环输出表示读到了数据，即此数据可以使用了，ToObject 把json 转成对象
        for (int i = 0; i < jsdata3.Count; i++)
        {
            Debug.Log(jsdata3[i]);
        }
        //使用foreach输出的话会以[键，值]，，，
		/*foreach (var item in jsdata3)
        {
            Debug.Log(item);
        }*/

    }
	
    private void OnGUI()
    {   //点击读取存储的文件
        if (GUILayout.Button("LoadTXT"))
        {
            LoadPerson();
        }
    }
}
```

## 参考 API

- [LitJson](https://litjson.net/api/LitJson/JsonMapper/)



