# Animation

## 播放动画片段

```csharp
public class MonsterManager : MonoBehaviour {

    private Animation anim; //定义一个 animation 组件

    //如果同一脚本挂了多个物体，需要分别定义Idle状态和Die状态的动画
    public AnimationClip idleClip;
    public AnimationClip dieClip;
    //撞击音效的播放器
    public AudioSource kickAudio;

    private void Awake()
    {
        //获得动画组件
        anim = gameObject.GetComponent<Animation>(); //获得物体身上的 animation 组件
        anim.clip = idleClip;
    }

    //当检测到碰撞时
    private void OnCollisionEnter(Collision collision)
    {
        //如果碰撞到的物体的标签为Bullet， 就销毁 bullet
        if (collision.collider.tag == "Bullet")
        {
            Destroy(collision.collider.gameObject);

            //播放撞击音效
            kickAudio.Play();

            //把默认的动画改为死亡动画，并播放
            anim.clip = dieClip;
            anim.Play();
            gameObject.GetComponent<BoxCollider>().enabled = false;
            StartCoroutine("Deactivate");
            //增加得分
            UIManager._instance.AddScore();
        }
    }

    //当怪物被Disable的时候，将默认的动画修改为idle动画
    private void OnDisable()
    {
        anim.clip = idleClip;
    }

    IEnumerator Deactivate()
    {
        yield return new WaitForSeconds(0.8f);
        //使当前的怪物变为未激活状态，并使整个循环重新开始
        TargetManager._intance.UpdateMonsters();
    }

}
```

