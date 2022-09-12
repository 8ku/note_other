# 动画控制

## 细节技术

### 脚不沾地

在fbx导入 - Animation - Root Transform Position(Y) 下, **调整Offset的数值, 大约是0.05~0.1之间**

**注意<u>不要</u>勾选Root Transform Position(XZ) - Bake Into Pose**

### 后脚跟不沾地

- 导入fbx时, rig 使用Humanoid
- 打开Animator编辑器, 点击Layers - Base Layer 右侧的齿轮, 勾选 IK Pass, 这样可以在脚本里调用IK组件
- 在需要控制的角色中加入脚本

```c#
using UnityEngine;


[RequireComponent(typeof(Animator))]
public class CharacterIK : MonoBehaviour
{

    protected Animator animator;

    [Range(0, 1)]
    public float DistanceToGround;

    public LayerMask layerMask;

    void Start()
    {
        animator = GetComponent<Animator>();
    }

    // Update is called once per frame
    void Update()
    {

    }

    private void OnAnimatorIK(int layerIndex)
    {
        if (animator)
        {
            //把IK的重量重置为1, 避免之前设置为其他值
            animator.SetIKPositionWeight(AvatarIKGoal.LeftFoot, 1f);
            animator.SetIKRotationWeight(AvatarIKGoal.LeftFoot, 1f);

            animator.SetIKPositionWeight(AvatarIKGoal.RightFoot, 1f);
            animator.SetIKRotationWeight(AvatarIKGoal.RightFoot, 1f);

            //Left Foot
            RaycastHit hit;
            //从脚发射一个向下的射线
            Ray ray = new Ray(animator.GetIKPosition(AvatarIKGoal.LeftFoot) + Vector3.up, Vector3.down);
            Debug.DrawRay(animator.GetIKPosition(AvatarIKGoal.LeftFoot), Vector3.down, Color.red);

            //如果射线碰撞到Player以外的所有层, 此时需要在面板上把角色设置为Player层, 并在此脚本的下拉选项中把Player层取消勾选
            if (Physics.Raycast(ray, out hit, DistanceToGround + 1f, layerMask))
            {
                //把可行走的地面Tag修改为Walkable
                if (hit.transform.tag == "Walkable")
                {
                    Vector3 footPosition = hit.point;
                    footPosition.y += DistanceToGround; //使脚接触到地面
                    animator.SetIKPosition(AvatarIKGoal.LeftFoot, footPosition);
                    animator.SetIKRotation(AvatarIKGoal.LeftFoot, Quaternion.FromToRotation(Vector3.up, hit.normal) * transform.rotation);
                }
            }

            //Right foot
            ray = new Ray(animator.GetIKPosition(AvatarIKGoal.RightFoot) + Vector3.up, Vector3.down);
            Debug.DrawRay(animator.GetIKPosition(AvatarIKGoal.RightFoot), Vector3.down, Color.red);

            if (Physics.Raycast(ray, out hit, DistanceToGround + 1f, layerMask))
            {
                //把可行走的地面Tag修改为Walkable
                if (hit.transform.tag == "Walkable")
                {
                    Vector3 footPosition = hit.point;
                    footPosition.y += DistanceToGround; //使脚接触到地面
                    animator.SetIKPosition(AvatarIKGoal.RightFoot, footPosition);
                    animator.SetIKRotation(AvatarIKGoal.RightFoot, Quaternion.FromToRotation(Vector3.up, hit.normal) * transform.rotation);
                }
            }

        }

    }
}
```

## 创建人物动画

- 在人物角色(model)下创建 Animator 组件

- 在 **Assets** 下新建一个 **Animator Controller**

- 角色的 Animator- Controller：放入上一步新建的 controller

- 打开 Animator 菜单
  
  - Create State - From New Blend Tree，双击 Blend Tree
    - Add motion - Add Motion Field
    - | Motion | Pos X | Pos Y |
      | ------ | ----- | ----- |
      | idle   | 0     | 0     |
      | Walk   | 0     | 0.5   |
      | Run    | 0     | 1     |

- 编辑 `AnimaotrHandler.cs`

### [使用blend混合动画](https://docs.unity3d.com/Manual/class-BlendTree.html)

- 在Animator里右键 Create State --> From New Blend Tree
- 双击新建的 blend tree 进入编辑界面
- 在右侧添加 motin 动画(或在blend tree上点击右建新建)
- 

## 动作

- **IDLE：待命状态**
  - defalt 状态，静止状态，可以做呼吸动画
- **walk**
- **run**

## 骨骼绑定

- 方式
  - 使用assets的模型改造
  - 从3D建模软件中导入，支持`.fbx` 文件，因为模型导入可能被重构，最好的方法是在3D软件中制作好部件，导入U3D中拼接
  - Animation Rigging 技术
  - 注意比例：Unity3D中默认 1单位距离 = 1米。
- **导入模型的技术要求：**
  - 法线要正确：Unity3D中不可以修改多边形法线方向，所以如果错了就必须返回Maya进行修改再重新导入；
  - 比例要正确：如果按照Maya默认1单位=1厘米，那么1米高的物体在Maya中就应该高100个单位，同时导入时`Scale Factor`设置为0.01；
  - Pivot Point要提前设置好；
  - 位移归零位置要在坐标原点（但初始位置不一定要在原点）；
  - 不能有构造历史（导出FBX的时候会自动统一清空构造历史，所以不要有任何依赖于构造历史的修改变化）；
  - UV都放在(0,1)象限内，且保持UV正向（Maya中显示为蓝色为正向）；
  - 单一mesh的UV不要有重叠；
  - 只使用smooth bind进行绑定；
  - 动画必须全部由动画曲线关键帧控制；
  - 骨骼命名最好提前做好。
  - 关键词：3d 动画绑定 unity   [参考](https://www.jianshu.com/p/e2aa4d898fb7)
- 插件
  - 2D
    - `2D Animation  `  `2D PSD Importer`  安装后可导入<u>PSB</u>文件
    - 第3方插件 `puppet 2D`
  - 3D
    - 第3方插件 `puppet 3D`

## 绘制2D 地图

- 新建 2D Project - Tilemap
- Windows - 2D - Tile Patette
- 把地图元素用 Sprite Editor 切好
- 在 Tile Patette 中新建 palette ，把切好的元素拖入，点击保存

## 创建动画的快捷方法

在素材中直接把切好的图拖入 Hierarchy