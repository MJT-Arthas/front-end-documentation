# 样式

## 单行省略

```
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis; 	
```

## 多行省略

        

```        	

        display: -webkit-box;
        overflow: hidden;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical; 

        /*! autoprefixer: off*/
              -webkit-box-orient: vertical;
        /*! autoprefixer: on*/

```
