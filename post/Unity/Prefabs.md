# Prefab相关笔记

## Editing Environment

用于设置prefab的背景

Edit>Project Settings>Editor打开工程设置界面：

- Prefab Editing Environments
  - Regular Environment：常规环境，非UI类的都属于常规类，也就是说凡是Prefab父级是Transform的都会用这个环境。
  - UI Environment：UI类Prefab编辑环境，凡是Prefab父级是RectTransform的都会用这个环境。

## 实例

支持修改的部分：

- 属性值
- 组件增删
- 子物体的添加

*实例上的修改时，inspertor对应条目左侧有蓝条标示*

## 覆盖和恢复

Overrides(覆盖)：将实例中所做的修改覆盖到原始Prefab中，此操作会更新所有实例。

Revert(恢复)：将某个实例上的修改移除，恢复到原始Prefab上的状态。

### 方法

**方法1（最全面）**：Inspector 顶部的 Overrides 按钮

**方法2（针对组件上属性与添加和删除组件）**：Inspector 相应修改属性上右键

**方法3（针对添加子物体时的操作）**：Hierarchy 面板对象上右键 > Add GameObject（只有该对象为子对象时有此菜单）

## 嵌套Prefab

在 Hierarchy 把一堆Prefab放到一个空对象/Prefab下，形成嵌套Prefab，没有层级数量限制。

## Prefab变体

Prefab变体用于快速生成多个Prefab，同时可以给予它们不同的外观的外观与属性，又共同继承自原始的Prefab。

在Project面板中，原始Prefab右键，Creat>Prefab Variant

==在变体的Prefab Mode中，选中Prefab最上层时的Overides下覆盖按钮变成了**Apply All to Base**，此命令会使用变体的修改去覆盖原始Prefab，请千万明确此操作确实是你想要的再去点。==

## Prefab解散

1. 首先解散操作只能在实例上进行操作，也就是只能在Hierarchy中进行。所以先在Hierarchy中选中Prefab实例。
2. 然后右键，从中选择Unpack Prefab或者Unpack Prefab Completely。

- Unpack Prefab：解散Prefab与本体的关联，此时在Hierarchy面板中父级会变成灰色图标，表示不再是一个实例。在Inspector面板中Prefab相关的操作也会消失。<u>但是子级的Prefab属性还是存在的</u>。（如果子级有Prefab的话）
- UnPack Prefab Completely：完全解散Prefab，此时不管是父级还是多深的子级全部失去与各自Prefab的关联，也就是纯纯粹变成了场景中的一组对象而已。