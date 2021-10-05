## Axure连接Google Analytics

### 把事件发送到GA上

- GA添加跟踪代码

- 在 axure cloud 文件的 plugin 里把GA的gtag.js粘贴

- axure：

  - 在需要打点的按钮上添加点击事件 `Click or Tap --> Open Link`

    - 选择 Link to external URL

    - 在输入框中输入事件代码

    - ```javascript
      javascript:this.gtag('event', 'eventName', {'event_label':'label_name'});
      ```



### 使用自定义维度给用户分组

- 在`GA --> 设置 --> 媒体资源 --> 自定义定义 --> 自定义维度`中添加新维度

- 修改 axure cloud 文件的 plugin 里GA的gtag.js

  - ```javascript
    <!-- Global site tag (gtag.js) - Google Analytics -->
    <script async src="from GA"></script>
    <script>
      window.dataLayer = window.dataLayer || [];
      function gtag(){dataLayer.push(arguments);}
      gtag('js', new Date());
    
    gtag('config', 'your view code',{
    	'custom_map': {'dimension1': 'dimension_name'}
    	});
    </script>
    ```

  - 在Axure点击事件中传**全局变量**的值

    - ```javascript
      javascript:
      $axure.internal(function($ax){
      $ax.public.getGlobalVariable = $ax.getGlobalVariable = function(name) {
      return $ax.globalVariableProvider.getVariableValue(name);
      };
      });
      var vraag1 = $axure.getGlobalVariable("client_id");
      //alert (vraag1); //弹窗显示结果，测试用
      this.gtag('event', vraag1, {'client_id': vraag1});
      $axure.getGlobalVariable('');
      throw new error('No global Variable');
      ```
    
  - 显示局部变量
  
    - ```javascript
      javascript:
      var vraag1 = '[[LVAR1]]'; //LVAR1 为局部变量
      alert (vraag1);
      ```
  
  
  
  

## 父框架注入代码

- 新建全局变量，变量名随意，变量值写入js代码  `<script> code here</script>`
- 或者css样式 `<style> #topPanel{display:none;} /*隐藏顶部工具栏*/</style>`

