# SoundManager

- 单例化声音管理脚本,可直接在别的脚本调用,不用用每次先找游戏物体,再找身上的脚本的方式来调用
- 把声音片段序列化, 让private的属性在inspector面板上可见

```c#
public class SoundManager:MonoBehaviour
{
  //单例化
  public static SoundManager instance;
  
  public AudioSource audioSource;
  //序列化声音片段
  [SerializeField]
  private AudioClip buttonClick,jumpSound;
  
  //实例化单例模式脚本
  private void Awake()
  {
    instance = this;
  }
  
  public void ButtonClick()
  {
    audioSource.clip = buttonClick;
    audioSource.Play();
  }
  
  public void JumpSound()
  {
    audioSource.clip = jumpSound;
    audioSource.Play();
  }
}
```

