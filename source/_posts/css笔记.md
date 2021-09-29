---
title: css笔记
date: 2020-10-01 15:54:23
categories: css
tags:
 - 日常笔记
 - css
---

# 定位

## 1.粘性定位

用于快速实现滚动吸顶的效果，似乎兼容性不是特别优秀，特别是移动端

```
position： sticky
```

1、父元素不能**overflow:hidden**或者**overflow:auto**属性。

2、必须指定**top**、**bottom**、**left**、**right**4个值之一，否则只会处于相对定位

3、父元素的高度不能低于sticky元素的高度

4、sticky元素仅在其父元素内生效