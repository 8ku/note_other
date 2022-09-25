# Items

## Weapon

### 调整左右手武器位的对齐

- 在左右手 prefab 下各建一个子物体-空对象 `left/right hand override`

- 在武器prefab上再建两个父对象，整个打包替代原来的 prefab：

  - Weapon
    - Weapon Pivot
      - Weapon prefab

- 在左右手挂脚本 `Weapon Holder Slot`，把 `left/right hand override` 拖入 `Parent override`槽位

- 创建脚本 `ScriptableObject: Item`，**可存储数据的脚本**

- ```csharp
  public class Item: ScriptableObject
  {
    [Header("Item Information")]
    public Sprite itemIcon;
    public string itemName;
  }
  ```

  - 创建派生类 `WeaponItem : Item`

    - ```csharp
      [CreateAssetMenu(menuName="Items/Weapon Item")]
      public class WeaponItem : Item 
      {
        public GameObject modelPrefab;
        public bool isUnarmed;
      }
      ```

    - **Tips**: 在类名上添加 `[CreateAssetMenu(menuName="Items/Weapon Items")]` 可以在右键创建菜单中直接创建这个类

- 新建一个 `Weapon Item`，（命名为“Sword”）把 prefab 拖入 `GameObject`

-  **Player** 挂载脚本 `Player Inventory`

  - 把 `Weapon Item(Sword)` 拖入左右手槽位

- Play，调整武器和手的位置

  - 左手
    - 点击暂停，选择 **Weapon Pivot**，调整到合适的位置
    - 右键 `Transfom - Copy - Copy Component`
    - 取消演示，在 `Weapon Prefab - Weapon Pivot`中粘贴上一步复制的信息
  - 右手
    - 演示模式下暂停，选择 **RightHand Override**，调整到合适的位置
    - 右键 `Transfom - Copy - Copy Component`
    - 取消演示，在 **RightHand Override** 中粘贴上一步复制的信息
