# 常用工具函数

## 防抖

```
     function debounce(func, wait, immediate) {
       let res, timeout, context, args;
     
       const debounced = function () {
           context = this;
           args = arguments;
     
           if (timeout) clearTimeout(timeout);
           if (immediate) {
               var runNow = !timeout;
               timeout = setTimeout(function(){
                   timeout = null;
               }, wait)
               if (runNow) res = func.apply(context, args)
           }
           else {
               timeout = setTimeout(function(){
                   func.apply(context, args)
               }, wait);
           }
           return res;
       };
     
       debounced.cancel = function() {
           clearTimeout(timeout);
           timeout = null;
       };
     
       return debounced;
     }
```

## 节流

```
function throttle(func, wait, options = {}) {
  let timeout, context, args, previous = 0;

  const later = function() {
      previous = options.leading === false ? 0 : +new Date();
      timeout = null;
      func.apply(context, args);
      if (!timeout) context = args = null; 
  };

  const throttled = function() {
      let now = +new Date();
      if (!previous && options.leading === false) previous = now;
      let remaining = wait - (now - previous);
      context = this;
      args = arguments;
      if (remaining <= 0 || remaining > wait) {
          if (timeout) {
              clearTimeout(timeout);
              timeout = null;
          }
          previous = now;
          func.apply(context, args);
          if (!timeout) context = args = null;
      } else if (!timeout && options.trailing !== false) {
          timeout = setTimeout(later, remaining);
      }

      throttled.cancel = function() {
          clearTimeout(timeout);
          previous = 0;
          timeout = null;
      }
  };
  return throttled;
}
```

## 获取url参数

* URLSearchParams

```
    const params = new URLSearchParams("q=devpoint&page=1"); //window.location.search
    params.get("q"); // 'devpoint'
    params.get("page"); // '1'

    const params = new URLSearchParams("q=devpoint&page=1");
    const entries = params.entries();
    Object.fromEntries(entries); // {q: 'devpoint', page: '1'}

```

* URLSearchParams

```
    const url = new URL("https://stackabuse.com/search?q=devpoint&page=1");
    const searchParams = url.searchParams;
    searchParams.get("q"); // 'devpoint'
    searchParams.get("page"); // '1'

    url.href; // 'https://stackabuse.com/search?q=devpoint&page=1'
    url.origin; // 'https://stackabuse.com'
    url.protocol; // 'https:'
    url.host; // 'stackabuse.com'
    url.hostname; // 'stackabuse.com'
    url.port; // ''
    url.pathname; // '/search'
    url.search; // '?q=devpoint&page=2'
    url.hash; // ''

```

* 纯JS

```
    function getQueryParams(url) {
        const paramArr = url.slice(url.indexOf("?") + 1).split("&");
        const params = {};
        paramArr.map((param) => {
            const [key, val] = param.split("=");
            params[key] = decodeURIComponent(val);
        });
        return params;
    }
```

## 对象转url参数

```
    getParams(params) {
      let paramStr = "";
      Object.keys(params).forEach((item) => {
        if (paramStr === "") {
          paramStr = `${item}=${params[item]}`;
        } else {
          paramStr = `${paramStr}&${item}=${params[item]}`;
        }
      });

      return paramStr;
    }
```
