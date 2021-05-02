# CharacterController

## SimpleMove

- 自带重力效果

- 不受y轴影响

- 返回bool值:在角色接触地面时返回True

```csharp
private CharacterController controller;
private float speed = 3.0f;
void Start()
{
  controller = this.GetComponent<CharacterController>();
}

void Update()
{
  controller.SimpleMove(transform.forward * speed);
}

```



## Move

- 没有重力效果
- 返回碰撞对象信息