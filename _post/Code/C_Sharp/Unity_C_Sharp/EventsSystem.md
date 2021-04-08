# Events System

## WorkFlow

### Events Manager

- 在一个空对象上挂脚本 `EventsManager`

- ```c#
  using System;
  using System.Collections;
  using System.Collections.Generic;
  using UnityEngine;
  
  public class EventsManager : MonoBehaviour
  {
      //实例化 
      public static EventsManager current;
  
      private void Awake()
      {
          current = this;
      }
  
      public event Action onPickupTriggerEnter;
  
      public void OnPickupTriggerEnter()
      {
          if (onPickupTriggerEnter != null)
          {
              onPickupTriggerEnter();
          }
      }
  
      public event Action onPickupTriggerExit;
      public void OnPickupTriggerExit()
      {
          if (onPickupTriggerExit != null)
          {
              onPickupTriggerExit();
          }
      }
  
      //如果同一个事件要分配给多个物体,根据物体不同单独执行事件, 给事件编号
      public event Action<int> onOpen;
      public void OnOpen(int id)
      {
          if (onOpen != null)
          {
              onOpen(id);
          }
      }
  }
  ```

- 在检测物体上挂脚本(物品, 武器等), 调用 Events manager

- ```c#
  using System;
  using System.Collections;
  using System.Collections.Generic;
  using UnityEngine;
  
  public class Food : MomoBehaviour
  {
       public int id;//在面板上修改
  		 private void Start()
       {
          // sign in , use +=
         	EventsManager.current.onPickupTriggerEnter += OnPickFoodOn;
          EventsManager.current.onPickupTriggerExit += OnPickFoodOut;
         
          EventsManager.current.onOpen += OnOpen;
       }
    
    	private void OnPickFoodOn()
      {
        some method();
      }
    
    	private void OnPickFoodOut()
      {
        some method();
      }	 
    
    	//根据int编号调用
    	private void OnOpen(int id)
      {
        	if (id == this.id)
          {
          		OpenDoor();  
          }
      }
    
    	//物体销毁时, 事件检测也要销毁, 用-=
    	private void OnDestrory()
      {
        	EventsManager.current.onPickupTriggerEnter -= OnPickFoodOn;
          EventsManager.current.onPickupTriggerExit -= OnPickFoodOut;
         
          EventsManager.current.onOpen -= OnOpen;
        
      }
  }
  ```

- 在物体下挂个空物体, 加上碰撞体, 勾选is trigger, 放脚本 `TriggerArea`

- ```c#
  public class TriggerArea : MonoBehaviour
  {
    public int id;//在面板上修改
    
    private void OnTriggerEnter(Collider other)
    {
      EventsManager.current.OnPickupTriggerEnter(); 
    }
    
    private void OnTriggerExit(Collider other)
    {
      EventsManager.current.OnPickupTriggerExit(); 
    }
    
    private void OnTriggerStya(Collider other)
    {
      	EventsManager.current.OnOpen(id);
    }
    
    // set this to private so it can't be accidentally assigned twice
    private Func<List<GameObject>> onRequestListOfTriggers;
    public void SetOnRequestListOfTriggers(Func<List<GameObject>> returnEvent )
    {
      	onRequestListOfTriggers = returnEvent;
      
    }
    
    public List<GameObject> RequestListOfTriggers()
    {
      	if (onRequestListOfTriggers != null)
        {
          return onRequestListOfTriggers();
          
        }
      
    }
      
    
  }
  ```

  



