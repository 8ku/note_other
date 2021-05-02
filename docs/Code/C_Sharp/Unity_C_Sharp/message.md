# 消息机制

要在 Unity 里使用 Action 要 using system。

消息机制有三个动作：

1. 注册事件
2. 发送事件
3. 注销事件

## 建立步骤

1. 定义一个字典用于存放消息内容

   Action 封装一个方法，该方法只有一个参数且不返回值。

   ```csharp
   // 用 Action<object> 可以覆盖 .NET 下的所有类，Action 用于委托
   private static Dictionary<string, Action<object>> RegisteredMsgs = new Dictionary<string, Action<object>>();
   ```

   | key                | value                      |
   | ------------------ | -------------------------- |
   | Dictionary<string> | Dictionary<Action<object>> |

   

   ​	

2. 设定注册方法

   ```csharp
   // 往字典中添加数据
   public static void Register(string msgName, Action<object> onMsgReceived)
   {
     RegisteredMsgs.Add(msgName, onMsgReceived);
   }
   ```

3. 设定发送方法

   ```csharp
   // 把字典中 key 值为 msgName 的 value 发送出去
   public static void Send(string msgName, object data)
   {
     RegisteredMsgs[msgName](data);
   }
   ```

4. 设定注销方法

   ```csharp
   // 从字典中移除 key 值
   public  static void UnRegister(string msgName)
   {
     RegisteredMsgs.Remove(msgName);
   }
   ```

5. 使用

   ```csharp
   // 注册
   Register("msg1",)
   ```

   