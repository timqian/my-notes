---
layout: post
title: javascript 识别用户对触屏的上下左右滑动(touch event)
tags: 
- javascript
---

这个技术是为我的在线贪吃蛇大战准备的

## 资料

[识别上下](http://stackoverflow.com/questions/13278087/determine-vertical-direction-of-a-touchmove)

[w3c touch doc](http://www.w3.org/TR/touch-events/#widl-TouchEvent-changedTouches)

[a gist for up and down](https://gist.github.com/localpcguy/1373518)

Note: It's important to note that in many cases, both touch and mouse events get sent 
(in order to let non-touch-specific code still interact with the user).
If you use touch events, you should call `event.preventDefault()` to keep the mouse event from being sent as well.
