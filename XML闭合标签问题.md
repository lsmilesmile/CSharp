#### XML闭合标签

```xml
<setParameter>
    <radarVersion key="radarVersion" value="LCA01E"/>
    <startAngle key="startAngle" value="-75" />
    <endAngle key="endAngle" value="75" />
    <points key="points" value="10" />
  </setParameter>
```



```tex
这是闭合的标签。
一个元素如果没有内容，那么它可以写成<points></points>，也可以简写成<points/>。这都是符合规定的闭合标签。
上面的就是这样，points元素没有内容只有属性，所以不用单独写结束标签，而是在起始标签的最后加上/，表示已经闭合。
```

