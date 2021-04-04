# Bolt笔记

经常查询https://ludiq.io/bolt/manual/units

## Variables

每个variable都有 ``name``,``type``和``value``组成。

Bolt里有6种variables.

| kind        | description                                                  |
| ----------- | ------------------------------------------------------------ |
| flow        | 流变量                                                       |
| Graph       | 局部变量                                                     |
| Object      | 属于游戏对象，可共享使用                                     |
| Scene       | 在本游戏场景可用的变量                                       |
| Application | 在App退出后重置，可以在场景间共享                            |
| Saved       | 公共组件，独立于游戏或场景<br />- Initial:使用后为新游戏自动载入的变量<br />- Saved:保存到电脑中，可单独编辑 |

## Graphs

Graphs是逻辑可视化，Bolt的核心。分为两种。

| Flow Grahps                                           | State Grahps                                              |
| ----------------------------------------------------- | --------------------------------------------------------- |
| 流程图                                                | 状态机（if...then...else）                                |
| low-level logic                                       | high-level logic                                          |
| when this happens,what should I do,and in what order? | what is my current behaviour,and when should that change? |

## Machines

是Graph的载体，分为两种：``Flow Machine`` and ``State Machine``.

### Source

|        | Embed                                                        | Macro                                                |
| ------ | ------------------------------------------------------------ | ---------------------------------------------------- |
| 关系   | 嵌在machine本身                                              | 作为asset引用到machine上                             |
| 可复用 | 不可复用，但可转成prefab复用                                 | 可复用                                               |
| 持久性 | 删除不可恢复，如果切换为macro也会被删除                      | 从machine里移除不会删除本身，切换为embed也不会被删除 |
| 场景   | 只要不被转成prefab，可用于当前场景中的游戏对象               | 不属于任何场景，所以不能refer to本场景的游戏对象     |
| 预制件 | The machine should not be used if you instantiate your prefab while in the editor. | The machine can safely be used on all prefabs.       |

## Groups

按住Cmd/Ctrl，按住鼠标左键打组

按住Alt拖动画布

## Flow Graphs

### Units：指代码的node和actions

**连接节点的方式：**

- Control Connection: △ 端口连接
- Value Connection: ◯ 条件连接

删除连接的方式：右键

**Super Units**

- 类似自定义unit
  - key不可以为null或空
  - port的key必须在整个graph里唯一
  - 如果改了key，所有这个端口的连接都会被移除
  - 所有input和output的value必须有type

## State Graphs

### State：告诉对象什么时候要做什么的一组行为，经常用于AI或对象行为或控制场景状态

**Flow States**

包含嵌套流程的流程图。

- 你可以右键把任何state（块）选择为开始状态（Toggle Start），开始状态可以允许设置为多个
- Any State：可使用『任何状态』触发到其他状态的转换，但此状态不能接收任何转换或执行任何操作

**Make Self Transitiion**

自循环，例如，希望每3秒敌人会改变目的地进行巡逻。

- 右键选择``Make Self Transition``

**Super States**

可复用的包含别一套流程的流程图，和Flow States很接近，主要的区别在包含的graph不是flow graph，是state graph.

**Multiple Transitions**

两个状态之前可以多种条件，多种条件没有优先级。

**State Units**

和``super units``很像，但里面包的是状态流程图，而不是flow流程图。

## 脚本
### 导入自定义type到bolt里
可以从 ``Tools > Bolt > Unit Options Wizard`` 里添加

### 在脚本里引用bolt
using Luciq;
using Bolt;
 https://ludiq.io/bolt/manual/scripting/events


## little useful features

- Dim：半透明未选择的Units（组件）
- Relations-units:显示unit流转关系
- 如果unit有错误，颜色会变橙色
- 如果unit缺少必要组件，颜色会变黄色
- 运行时，活动的节点为蓝色，出错的unit为红色
- 在state graphs里，右键（或按住cmd/ctrl拉出）make transition可以指向空白，指向空白并松开鼠标时，会自动创建一个新的状态
- transition也是一个flow graph，你可以使用任何unit，例如事件或分支
- 默认有一个``trigger transition``作为出口，这个特殊的unit是为了告诉父级state必须要走这个分支

## 英文对照

| 英文        | 中文                                                        |
| ----------- | ----------------------------------------------------------- |
| prefab      | 预制件                                                      |
| node        | 节点                                                        |
| asset       | 资产？                                                      |
| port        | 端口                                                        |
| transitions | 连接条件（state graphs中的连接线，右键选择make transition） |

​	