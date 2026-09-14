---
tags:
  - android
  - compose
---
# Official
## HorizontalPager 翻页，轮播
横向平滑组件

> [!关键点]
> page 默认是占屏幕宽度
> 当你想让当前page 的额外剩余空间 显示 下一个page的部分内容，可以使用contentPadding
> contentPadding 可以控制item的左右边距 ，就可以让左右两边的元素显示在当前页面


``` kotlin
@Composable  
fun PlaceSection() {  
    val placeList by remember {  
        mutableStateOf(  
            listOf(  
                R.mipmap.place1,  
                R.mipmap.place1,  
                R.mipmap.place1,  
                R.mipmap.place1,  
                R.mipmap.place1,  
            )  
        )  
    }  
    val pagerState = rememberPagerState(pageCount = { placeList.size })  
    HorizontalPager(  
        state = pagerState,  
        contentPadding = PaddingValues(start = 16.dp, end = 100.dp),  
        pageSpacing = 20.dp,  
        modifier = Modifier  
            .fillMaxWidth()  
    ) { page ->  
        PlaceItem(placeList[page])  
    }  
}

```


---


## BoxWithConstraints 带有size

> [!NOTE] important
> 可以确定容器的宽度和高度，内部是使用了 **SubcomposeLayout**



## SubcomposeLayout

在measure 和 layout 之间，可以获取到布局的宽高



## LazyVerticalGrid 网格布局
```kotlin
LazyVerticalGrid(  
    columns = GridCells.Adaptive(50.dp),  
    verticalArrangement = Arrangement.spacedBy(16.dp),  
    horizontalArrangement = Arrangement.spacedBy(30.dp),  
    modifier = Modifier  
        .fillMaxWidth()  
) {  
    items(usualToolItemList) { item ->  
        UsualToolItem(  
            icon = item.first,  
            label = item.second  
        )  
    }  
}
```




# Other







