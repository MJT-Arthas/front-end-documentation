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
