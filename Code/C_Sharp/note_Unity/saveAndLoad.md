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



## 读档

### 从文件中读取数据反序列化 - 加载到类中





