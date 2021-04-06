# Random

## 随机生成敌人

```c#
public class TargetManager : MonoBehaviour {
    public static TargetManager _intance;

    public GameObject[] monsters;
    public GameObject activeMonster = null;

    private void Awake()
    {
        _intance = this;
    }
    private void Start()
    {
        foreach(GameObject monster in monsters)
        {
            monster.GetComponent<BoxCollider>().enabled = false;
            monster.SetActive(false);
        }
        //调用协程
        StartCoroutine("AliveTimer");
    }

    //随机激活怪物
    private void ActivateMonster()
    {
        int index = Random.Range(0, monsters.Length);
        activeMonster = monsters[index];
        activeMonster.SetActive(true);
        activeMonster.GetComponent<BoxCollider>().enabled = true;
        //调用死亡时间的协程
        StartCoroutine("DeathTimer");
    }

    //迭代器方法，设置生成的等待时间
    IEnumerator AliveTimer()
    {
        //等待1-4秒后执行ActivateMonster方法
        yield return new WaitForSeconds(Random.Range(1, 5));
        ActivateMonster();
    }

    //使激活状态的怪物变为未激活状态
    private void DeActivateMonster()
    {
        if (activeMonster != null)
        {
            activeMonster.GetComponent<BoxCollider>().enabled = false;
            activeMonster.SetActive(false);
            activeMonster = null;
        }
        //调用激活时间的协程，达到一个反复激活和死亡的循环
        StartCoroutine("AliveTimer");
    }

    //迭代器，设置死亡的等待时间
    IEnumerator DeathTimer()
    {
        yield return new WaitForSeconds(Random.Range(3, 8));
        DeActivateMonster();
    }

    //更新生命周期。当子弹击中怪物时，停止所有的协程
    //将当前处于激活状态的怪物变为未激活状态，清空activeMonster
    //重新开始AliveTimer的协程（随机激活怪物）
    public void UpdateMonsters()
    {
        StopAllCoroutines();
        if (activeMonster != null)
        {
            activeMonster.SetActive(false); 
            activeMonster = null;         
        }
        StartCoroutine("AliveTimer");
    }
}

```

