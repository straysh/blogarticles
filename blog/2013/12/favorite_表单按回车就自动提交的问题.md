{
    "id": 15,
    "user_id": 1,
    "category_id": 5,
    "author": "straysh",
    "title": "表单按回车就自动提交的问题",
    "slug": "favorite_表单按回车就自动提交的问题",
    "hits": 121,
    "published_at": "1386928384",
    "created_at": 1386928384,
    "updated_at": 1504790961,
    "deleted_at": null
}
#### 当form表单中只有一个`<input type="text" name="name" />`时按回车键将会自动将表单提交。
```html
<form id="form1" action="post.php" method="post">   
    <input type="text" name="name" />   
</form>
```
再添加一个 `<input type="text" />`
<p>按下回车将不会自动提交，但是页面上显示一个不知所云的输入框挺别扭，后从网上搜到两个解决办法：</p>

## 1) 添加一个 `<input style="display: none;" type="text" />`
不显示输入框，然后回车之后也不会提交：
```html
<form id="form1" action="post.php" method="post">   
    <input type="text" name="name" />   
    <input style="display:none" />   
</form>
```

## 2) 添加一个onkeydown事件，然后回车之后也不会显示：
```html
<form id="form1" action="post.php" method="post">   
    <input type="text" name="name" onkeydown="if(event.keyCode==13) return false;"/>   
</form>
```
如果想添加回车事件可以在onkeydown事件中添加判断提交表单：
```html
<form id="form1" action="post.php" method="post">   
    <input style="display:none" />   
    <input type="text" name="name" onkeydown="if(event.keyCode==13){gosubmit();}" />   
</form>
```
我们有时候希望回车键敲在文本框（input element）里来提交表单（form），但有时候又不希望如此。比如搜索行为，希望输入完关键词之后直接按回车键立即提交表单，而有些复杂表单，可能要避免回车键误操作在未完成表单填写的时候就触发了表单提交。
<p>要控制这些行为，不需要借助JS，浏览器已经帮我们做了这些处理，这里总结几条规则：</p>
<p>如果表单里有一个type="submit"的按钮，回车键生效。</p>
<p>如果表单里只有一个type="text"的input，不管按钮是什么type，回车键生效。</p>
<p>如果按钮不是用input，而是用button，并且没有加type，IE下默认为type=button，FX默认为type=submit。</p>
<p>其他表单元素如textarea、select不影响，radio checkbox不影响触发规则，但本身在FX下会响应回车键，在IE下不响应。</p>
<p>type="image"的input，效果等同于type="submit"，不知道为什么会设计这样一种type，不推荐使用，应该用CSS添加背景图合适些。</p>