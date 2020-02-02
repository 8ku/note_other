# DOTween一些笔记

## [官方文档](http://dotween.demigiant.com/documentation.php)

## Note

- 给序列添加间隔

  ```c#
  Sequence quence = DOTween.Sequence(); //创建一个序列
  	.Append(transform.DOMove(Vector3.one, 2));
  	.AppendInterval(1); //Adds the given interval to the end of the Sequence.
  //Insert a scale tween for the whole duration of the Sequence
  	.Insert(0, tranform.DOScale(new Vector3(3,3,3),quence.Duration()));
  ```

  