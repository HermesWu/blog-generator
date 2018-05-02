---
title: Tween.js
date: 2018-05-02 18:20:26
tags: Tween.js
categories: Tweenjs
---

# Tweenjs

页面缓动效果时，用到Tweenjs，记录下demo

## 一、CDN引入Tweenjs

## 二、demo如下

```
        let currentTop = window.scrollY // 初始位置
        let targetTop = document.querySelector(e.currentTarget.getAttribute('href')).offsetTop - 70 //目标位置
        let s = targetTop - currentTop
        let t = Math.abs((s/100)*300)
        if(t>500) {t=500}
        function animate(time) {
            requestAnimationFrame(animate);
            TWEEN.update(time);
        }
        requestAnimationFrame(animate);

        var coords = { x: currentTop }; 
        var tween = new TWEEN.Tween(coords) 
                .to({ x: targetTop}, t) 
                .easing(TWEEN.Easing.Cubic.InOut) 
                .onUpdate(function() {
                  window.scroll(0, coords.x)
                })
                .start(); 
                // window.scroll(0, top)
              }
            }
```