{
    "id": 54,
    "user_id": 1,
    "category_id": 12,
    "author": "straysh",
    "title": "移动开发规范",
    "slug": "mobile_web_spec",
    "hits": 112,
    "published_at": "1445321476",
    "created_at": 1445321476,
    "updated_at": 1504930818,
    "deleted_at": null
}
#### 字体设置
使用无衬线字体
```
body {
    font-family: "Helvetica Neue", Helvetica, STHeiTi, sans-serif;
}
```

iOS 4.0+ 使用英文字体 Helvetica Neue，之前的iOS版本降级使用 Helvetica。中文字体设置为华文黑体STHeiTi。 需补充说明，华文黑体并不存在iOS的字体库中(http://support.apple.com/kb/HT5878)， 但系统会自动将华文黑体 STHeiTi 兼容命中系统默认中文字体黑体-简或黑体-繁
```
Heiti SC Light 黑体-简 细体 （iOS 7后废弃）
Heiti SC Medium 黑体-简 中黑
Heiti TC Light 黑体-繁 细体
Heiti TC Medium 黑体-繁 中黑
```

原生Android下中文字体与英文字体都选择默认的无衬线字体
```
4.0 之前版本英文字体原生 Android 使用的是 Droid Sans，中文字体原生 Android 会命中 Droid Sans Fallback
4.0 之后中英文字体都会使用原生 Android 新的 Roboto 字体
其他第三方 Android 系统也一致选择默认的无衬线字体
```

#### 基础交互
设置全局的CSS样式，避免图中的长按弹出菜单与选中文本的行为
```
a, img {
    -webkit-touch-callout: none; /* 禁止长按链接与图片弹出菜单 */
}
html, body {
    -webkit-user-select: none;   /* 禁止选中文本（如无文本选中需求，此为必选项） */
    user-select: none;
}
```

参考资料:
* [CSS选择器-火狐开发文档](http://www.w3.org/TR/selectors/#selectors)
* [CSS选择器](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Getting_started/Selectors)