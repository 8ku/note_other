# UGUI

* TOC
{:toc}
## 使用  EventSystem 探测物体

使用 UI 事件需要先引用事件系统

```csharp
using UnityEngine.EventSystems;
```

[MonoBehaviour](MonoBehaviour) 里有一个 OnMouseDown 的类可以控制有 collider 属性的物体。

```csharp
void OnMouseDown() //可以直接建一个类
    {
        // Destroy the gameObject after clicking on it
        Destroy(gameObject);
    }
```

### UI 和 3D 物体重叠时，点击事件

MainCamera 使用 `Physics Raycaster` 组件，不要用 Graphic Raycaster`，因为后者只能对 UI 物体响应

使用 Eventsystems 里的 ` IPointerClickHandler ` 可以同时控制3D 和 2D 物体

```csharp
// 3D
using UnityEngine;
using UnityEngine.EventSystems;

public class ClickCube : MonoBehaviour,IPointerClickHandler
{
    private int _index;
    // Start is called before the first frame update
    void Start()
    {

    }

    // Update is called once per frame
    void Update()
    {

    }

    public void OnPointerClick(PointerEventData eventData)
    {
        ChangeColor();
    }

    void ChangeColor()
    {
        if (_index == 0)
        {
            GetComponent<MeshRenderer>().material.SetColor("_Color", Color.black);
        }
        else
        {
            GetComponent<MeshRenderer>().material.SetColor("_Color", Color.white);
        }
        _index = _index == 0 ? 1 : 0;
    }
}

```



```csharp
//2D
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.EventSystems;
using UnityEngine.UI;

public class ClickUI : MonoBehaviour,IPointerClickHandler
{
    private int _index;
    // Start is called before the first frame update
    void Start()
    {

    }

    public void ChangeColor()
    {
        if (_index == 0)
        {
            GetComponent<Image>().color = Color.blue;
        }
        else
        {
            GetComponent<Image>().color = Color.white;
        }
        _index = _index == 0 ? 1 : 0;
    }

    public void OnPointerClick(PointerEventData eventData)
    {
        ChangeColor();
        //ExecuteAll(eventData);
    }

    public void ExecuteAll(PointerEventData eventData)
    {
        List<RaycastResult> results = new List<RaycastResult>();
        EventSystem.current.RaycastAll(eventData, results);
        foreach (RaycastResult result in results)
        {
            if (result.gameObject != gameObject)
            {
                ExecuteEvents.Execute(result.gameObject, eventData, ExecuteEvents.pointerClickHandler);
            }
        }
    }
}
```

### 判断是否点击在UGUI上

`EventSystem.current.IsPointerOverGameObject`

```csharp
// -1表示 left mouse button" (pointerId = -1)
if (Input.GetMouseButtonDown(0) && EventSystem.current.IsPointerOverGameObject(-1) == false)
        {
            isPickedItem = false;
            PickedItem.Hide();

        }
```



## 使用Input System 探测物体

### 前置工作

-  安装input system插件
- 新建action文件, 把action文件生成 C# 文件(Actions.cs)
- 在player controller里引用 action 生成的 C# 文件(或建立一个空对象放这个文件, 为了便于控制其他 input 命令, 还是挂在player身上比较好)

### 脚本

- ```csharp
  public Actions actions;
  //要使用射线, 引入摄像机, 如果有多个摄像机, 用公开变量, 如果只有一个, 用私变量 Cam = Camera.mainCamera;
  publice Camera uiCam; 
  
  
  private void Awake(){
    //默认该文件不能修改, 所以用新建, 引用后可以用脚本调用action
    actions = new Actions();
  }
  
   private void OnEnable(){
     actions.Enable();
  }
  
  private void Disable(){
    actions.Disable();
  }
  
  private void Start(){
    // UI 是action map的名字, Click 是map下的Action名字
    action.UI.Click.started += _ => StartClicked();
    action.UI.Click.performed += _ => EndClicked();
  }
  
  private void StartClicked(){
    
  }
  
  private void EndClicked(){
    DetectObject();
  }
  
  //探测
  private void DetectObject(){
    //先在action面板里创建/使用action(name = Point), type = Pass Through, Control Type = Vector 2 Path = Position[Mouse]
    Ray ray = uiCam.ScreenPointToRay(actions.UI.Point.ReadValue<Vector2>());
    
    int layerMask = LayerMask.GetMask("UI");
    
    //3D Array Detect
    RaycastHit[] hits = Physics.RaycastAll(ray, 200, layermask);
    for (int i = 0; i < hits.Length; i++){
      if (hit[i].collider != null){
        Debug.Log(hits[i].collider.Tag);
      }
    }
    
    //2D Detect 物体上同样要加刚体
    RaycastHit2D hits2d = Physics2D.GetRayIntersection(ray);
  if (hits2d.collider != null)
     {
        Debug.Log(hits2d.collider.gameObject.name);
     }
  }
  ```

- 