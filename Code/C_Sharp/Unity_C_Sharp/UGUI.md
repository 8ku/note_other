# UGUI

使用 UI 事件需要先引用事件系统

```c#
using UnityEngin.EventSystems;
```

[MonoBehaviour](MonoBehaviour) 里有一个 OnMouseDown 的类可以控制有 collider 属性的物体。

```c#
void OnMouseDown() //可以直接建一个类
    {
        // Destroy the gameObject after clicking on it
        Destroy(gameObject);
    }
```

### UI 和 3D 物体重叠时，点击事件

MainCamera 使用 `Physics Raycaster` 组件，不要用 Graphic Raycaster`，因为后者只能对 UI 物体响应

使用 Eventsystems 里的 ` IPointerClickHandler ` 可以同时控制3D 和 2D 物体

```c#
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



```c#
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

