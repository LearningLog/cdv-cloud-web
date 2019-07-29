## 富文本编辑器[Tinymce](https://github.com/tinymce/tinymce)

- 由于目前使用 npm 安装 Tinymce 方法比较复杂而且还有一些问题(日后可能会采用该模式

  )且会大大增加编译的时间所以暂时不准备采用
  
- 目前使用异步加载 CDN 的引入方式，如果想修改 cdn 地址或者 tinymce 的版本只需在 
  
  src/components/Tinymce 中找到 tinymce 的 cdn 地址进行修改就可以了。它会通过dynamicLoadScript自动注入的 
  
  index.html 中。
  
- 使用: 由于富文本不适合双向数据流，所以只会 watch 传入富文本的内容一次变化，之后
  
  传入内容的变化就不会再监听了，如果之后还有改变富文本内容的需求。
  
  可以通过 **this.refs.xxx.setContent()** 手动来设置。
  
  源码也很简单，有任何别的需求都可以在 src/components/Tinymce 中自行修改。
  
### 属性

| 属性 | 描述 | 类型 | 默认值 | 可选值 | 是否必填（默认false） |
| --- | --- | --- | --- | --- | ------------- |
| id | 富文本唯一标识 | <span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">String</span></span></span> | <span class="colour" style="color:rgb(230, 219, 116)"></span>onair-tinymce-时间戳 |  |  |
| value | 文本内容 | <span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">String</span></span></span></span> | 只监视一次更改，可以通过 <span class="font" style="font-family:Consolas">this.refs.xxx.setContent()</span><br><span class="font" style="font-family:Consolas"></span>手动来设置富文本内容 |  |  |
| <span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">toolbar</span></span></span> | 工具栏 | <span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">Array</span></span></span> | [] | src/components/Tinymce/toolbar.js |  |
| <span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">menubar</span></span></span></span> | 顶部菜单栏 | <span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">String</span></span></span></span> | <span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">'file edit insert view format table'</span></span></span></span> | <span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">file ，edit，insert，view，format，table</span></span></span></span> |  |
| <span class="colour" style="color:rgb(253, 179, 131)"></span>plugins | 菜单栏配置项 | <span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">Array</span></span></span> | [] | src/components/Tinymce/plugins.js |  |
| height | 富文本高度 | <span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px"><span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">Number, String</span></span></span></span>r</span></span></span> | 360 |  |  |
| <span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">width</span></span></span></span> | 富文本宽度 | <span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px"></span></span></span><span class="highlight" style="background-color:rgb(246, 248, 250)"><span class="colour" style="color:rgb(44, 62, 80)"><span class="font" style="font-family:-apple-system, BlinkMacSystemFont, &quot;Segoe UI&quot;, Roboto, Oxygen, Ubuntu, Cantarell, &quot;Fira Sans&quot;, &quot;Droid Sans&quot;, &quot;Helvetica Neue&quot;, sans-serif"><span class="size" style="font-size:16px">Number, String</span></span></span></span> | auto~~~~ |  |  |

### 图片上传

- 采用elementUI 上传组件

### API

- this.refs.xxx.setContent() // 设置富文本内容