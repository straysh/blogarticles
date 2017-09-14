{
    "id": 39,
    "user_id": 1,
    "category_id": 12,
    "author": "straysh",
    "title": "js动画",
    "slug": "js_animation",
    "hits": 56,
    "published_at": "1438670725",
    "created_at": 1438670725,
    "updated_at": 1504982672,
    "deleted_at": null
}
游戏动画，Flash动画里一个比较重要的概念是 帧频 ，即每秒播放多少帧动画，一般动画是30帧/秒，单位为fps（frames per second）。

对于匀速运动来说：如果一个动画的持续时间duration为500ms，帧频frequence为30fps，则总帧数frames为 (500/1000)*30 = 15 ，即该动画过程有15个“画面”，每走一帧，都计算出一个画面： 画面当前位置 = 开始位置 + (当前帧/总帧数)(结束位置-开始位置) ，如果当前帧是最后一帧，则动画结束。其中setTimeout或setInterval每隔 (500/15)ms 时间段调用一次函数，即计算一个画面。

来看下线性运动Linear缓动算法函数，t表示当前帧，b表示开始位置，c表示发生偏移的距离值，即当前位置-开始位置，d表示总帧数，符合上面的推理解释，对于其他的算法函数，道理其实都是一样，只不过在运动过程中的曲线不同，有些呈现抛物线，有些呈现线性指数，对于数学感兴趣的可以研究下这些算法函数，我也是略知皮毛：

```js
Linear: function (t, b, c, d) {
  return c * t / d + b;
}
```