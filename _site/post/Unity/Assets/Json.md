# 解析Json的方式

## JsonUtility

序列化方法有点僵硬,暂时不考虑

- 只能接受json对象,如果是json数组会报错

- 被转换的对象必须是可被序列化的,需标记 [System.Serializable] 属性

## LitJson

- 引用时把 dll 文件放到Plugins中

- json文件中的值需要和引用时一模一样
- json文件中不能有空值

```c#
using LitJson;
using System.IO; //读取文件必须引用IO


void Start()
{
//把文件转为字符串
string txt = File.ReadAllText(Application.dataPath+"/Item.json");
//把字符串转为对象
JsonData itemJson = JsonMapper.ToObject(txt);
//把要输出的对象字符串化
string result = (string)itemJson[0]["Consumable"][0];
Debug.Log(result);
}
```

## Newtonsoft

```c#
using UnityEngine;
using System.IO;
using Newtonsoft.Json.Linq;
using System.Text;

public class Newtonso : MonoBehaviour
{
    // Start is called before the first frame update
    void Start()
    {
        // 读取文件,返回JArray数据
        string dataJson = File.ReadAllText(Application.dataPath + "/Items.json", Encoding.UTF8);
        //转为JArray数组
        JArray jArray = JArray.Parse(dataJson);
        //把指定数组转为字符串
        string p1 = jArray[0].ToString();

        //把上述字符串放到 data 里
        JObject data = JObject.Parse(p1);


        //把指定标签的值输出
        string Consumable = data["Consumable"].ToString();

        Debug.Log(Consumable);

        //解析子标签需要再把父级数据从string转为object
        JObject hp = JObject.Parse(Consumable);

        //把子标签数据转为string输出,也可以to double 或 to single等
        Debug.Log(hp["hp"].ToString());

        //如果数组中包含数组,可以把string后的数组array,再string出来
        //JArray array = JArray.Parse(string);
        //Debug.Log(array[0][1].ToString());

        
    }
}
```

json文件

```json
[

    {
        "id": "1",
        "name": "血瓶",
        "type": "Consumable",
        "description": "加血",
        "quality": "Common",
        "capacity": 10,
        "buyPrice": 10,
        "sellPrice": 5,
        "sprite": "Sprites/Items/hp",
        "Consumable":
        {
            "hp": 10,
            "mp": 0
        }
    },
    {
        "id": "2",
        "name": "蓝瓶",
        "type": "Consumable",
        "description": "加蓝",
        "quality": "Common",
        "capacity": 10,
        "buyPrice": 10,
        "sellPrice": 5,
        "sprite": "Sprites/Items/mp",
        "Consumable":
        {
            "hp": 0,
            "mp": 10
        }
    }
  ]
```

