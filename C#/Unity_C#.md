# Unity中的C#语法

基本格式：

~~~c#
using System.Collections;
using UnityEngige;

public class DemoScript:MonoBehaviour {
	void Start() {
        
    }
    void Update() {
        
    }
}
~~~

- 不需要带Main方法

### 使用Debug来显示操作情况

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class BasicController : MonoBehaviour
{
    // Update is called once per frame
    void Update()
    {
        Debug.Log("Horizontal Input = " + Input.GetAxis("Horizontal")); //使用Debug来打印横向坐标
    }
}
```

- 把skybox加到camera下，可以把自定义的skybox材质放进去，在不影响编辑模式的skybox前提下显示自定义skybox
- 

