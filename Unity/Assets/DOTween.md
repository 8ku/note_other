# DOTween一些笔记

## [官方文档](http://dotween.demigiant.com/documentation.php)

## [常见问题](https://blog.csdn.net/zcaixzy5211314/article/details/85749734)

## Note

一个用于设置动画的插件，例如设置位置、旋转、缩放、变色等。

- 给序列添加间隔，插入动画

  ```c#
  Sequence quence = DOTween.Sequence(); //创建一个序列
  
  quence.Append(transform.DOMove(Vector3.one, 2));
  	// the scale will be played with the movement tween
  	.Join(transform.DOScale(Vector3.one*2, 2));
  	.AppendInterval(1); //Adds the given interval to the end of the Sequence.
//Insert a scale tween for the whole duration of the Sequence,from first frame
  	.Insert(0, tranform.DOScale(new Vector3(3,3,3),quence.Duration()));
  ```
  
- 预添加：后加的会先执行，会在 append 前执行

  ```c#
  Sequence quence = DOTween.Sequence(); //创建一个序列
  
  quence.Append(transform.DOMove(Vector3.one, 2)); //third
  	.Join(transform.DOScale(Vector3.one*2, 2)); //fourth
  	.AppendInterval(1); //fifth
  	.PrependInterval(1); //first
  	.Prepend(transform.DOMove(Vector3.one, 2)); //second
  	.Insert(0, tranform.DOScale(new Vector3(3,3,3),quence.Duration())); //third
  ```

- 移动、旋转、缩放

- shake：物体或摄像机

- 混合 Blend ：颜色、透明度、运动、旋转、缩放、时间缩放、文字

- Text：打字机效果、富文本（pro）、颜色、透明度

- 动画队列（添加、插入、暂停、回调函数、预添加、循环）

- 设置参数

  - 循环、起点、延迟、以什么速度为基准（From, SetDelay, SetSpeedBased）
  - 设置 ID (SetId)，设置内部 id (字符串)，调用时直接传入内部 id。
  - 设置增量动画（SetRelative）

- 设置曲线 （SetEase）

- 回调函数（onComplete、OnKill、OnPlay、OnStart、OnStepCompete、OnUpdate、OnRewind）