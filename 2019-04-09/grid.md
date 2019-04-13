[https://juejin.im/post/5c997ab05188252d6534581e](https://juejin.im/post/5c997ab05188252d6534581e)

##### Grid Container 的全部属性

<code>display
grid-template-columns
grid-template-rows
grid-template-areas
grid-template
grid-column-gap
grid-row-gap
grid-gap
justify-items
align-items</code>
justify-content
align-content
grid-auto-columns
grid-auto-rows
grid-auto-flow
grid

##### Grid Items 的全部属性

grid-column-start
grid-column-end
grid-row-start
grid-row-end
grid-column
grid-row
grid-area
justify-self
align-self


属性justify-items 和 justify-self 以行轴为参照对齐项目，属性align-items 和 align-self 以列轴为参照对齐项目。

属性justify-items 和 align-items 是网格容器的属性，并支持如下这些值：

    auto
    normal
    start
    end
    center
    stretch
    baseline
    first baseline
    last baseline 


项目可以用属性align-self 和 justify-self定义自己的对齐方式，是网格元素的属性，并支持如下这些属性值：

    auto
    normal
    start
    end
    center
    stretch
    baseline
    first baseline
    last baseline
    
    
属性align-content用于定义网格轨道延着行的轴线的对齐方式，而属性justify-content用于定义网格轨道沿着列的轴线的对齐方式。并分别支持如下属性：

    normal
    start
    end
    center
    stretch
    space-around
    space-between
    space-evenly
    baseline
    first baseline
    last baseline
    
