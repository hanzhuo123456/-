### 让图片与文字的间隔为0

- 首先确保所有的默认样式已经移除，如body的padding等

- 将父元素的font-size设置为0， 再在子元素下设置font-size即可

  ```stylus
    .header
      color: #fff
      background: #000
      .content-wrapper
          padding: 24px 12px 18px 24px
          font-size: 0    <----
          .avatar
            display: inline-block
          .content
            display: inline-block
            font-size:15px   <-----
  ```

- 以上就会将content-wrapper里的图片与文字间隔设置为0了,如果发现还有间隔怎么办?此时就可以考虑是换行导致的间隔了, 可以将让两个标签不换行

### 设置模糊效果

```
filter: blur(10px)
```

### css Sticky footer

[布局博客](https://www.cnblogs.com/shicongbuct/p/6487122.html)

### Flex布局

- 阮一峰老师的文章

### padding-top黑科技

- [使用padding-top实现响应式背景图片](https://www.jianshu.com/p/1c1d55575e86)
- [padding-top黑科技](https://blog.csdn.net/helianthus5/article/details/79052510)

```css
    .image-header
      position: relative
      width: 100%
      height: 0
      padding-top: 100%
      img
        position: absolute
        top:0
        left:0
        width: 100%
        height:100%
```

