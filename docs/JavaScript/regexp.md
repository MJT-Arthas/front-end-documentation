# 正则

## 截取字符串中的

```
    var str = "http://pavo.elongstatic.com/i/ori/19O7SHlEuAw.jpg";

    str = str.match(new RegExp(/pavo.elongstatic.com\/i\/ori\/(\S*).jpg/))[1]; 

```
