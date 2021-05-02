## TextAsset

**Text Assets** are a format for imported text files. When you drop a text file into your Project Folder, it will be converted to a Text Asset. The supported text formats are:

- **.txt**
- **.html**
- **.htm**
- **.xml**
- **.bytes**
- **.json**
- **.csv**
- **.yaml**
- **.fnt**

```csharp
//定义一个显示文本的text组件
public Text textLabel;
//定义一个显示说话人头像的image
public Image faceImage;
//定义一个放入对话文本的TextAsset组件
public TextAsset textFile;
//定义一个用于给对话文本读行计数的int
public int index;

//定义一个list放对话文本change to string的空间
List<string> textList = new List<string>();

//4. 初始化时载入文本文件
private void Awake()
{
  GetTextFromFile(textFile);
}

//3. awake之后载入textlist的第一条文本
private void OnEnable()
{
  textLable.text = textList[index]; //index=0
  index++; //index=1,如果不加这行，每一次按 R 键会停留在 0 行上
}

//2. 每次刷新时按index序号把textList里的字符串输出到textLabel
private void Update()
{
  //如果计数=textList的行数，说明文本被显示完
  if (Input.GetKeyDown(KeyCode.R) && index == textList.Count)
  {
    gameObject.SetActive(false); //把对话框隐藏
    index = 0;
    return; //跳出if语句
  }
  if (Input.GetKeyDown(KeyCode.R))
  {
    textLable.text = textList[index]; //按下 R 键时，在textLabel中按index计数显示textList中的字符串
    index++;
  }
    
}


//1. 转换文本文件
void GetTextFromFile(TextAsset file) //把文本文件做为参数传入
{
  textList.Clear(); //每次转换前要清空列表，不然文本会一直累加
  index = 0; //把文本行数计数清0
  
  var lineData = file.text.Split('\n'); //把文本文件中的文本按换行切分
  
  foreach (var line in lineData)
  {
    textList.Add(line); //遍历切分好的文本，加入textList列表中
  }
}


```

