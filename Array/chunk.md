## lodash.js->Array->chunk

### 用法
> 将数组拆分为等长的若干个新数组组成的二维数组，如果无法被分割成全部都等长的新数组，那么最后剩下的数组元素将组成最后一个数组。

### 例子

```javascript
    _.chunk([1,2,3,4,5,6],3)
    //==>[[1,2,3],[4,5,6]];
    //3为等长的长度参数，取消参数则默认长度为1
```

### 源码理解
```javascript
    function chunk(array, size, guard) {
      if ((guard ? isIterateeCall(array, size, guard) : size === undefined)) {
        size = 1;
      } else {
        size = nativeMax(toInteger(size), 0);
      }
      var length = array ? array.length : 0;
      if (!length || size < 1) {
        return [];
      }
      var index = 0,
          resIndex = 0,
          result = Array(nativeCeil(length / size));

      while (index < length) {
        result[resIndex++] = baseSlice(array, index, (index += size));
      }
      return result;
    } 

    `guard意思是守卫`

    1.直接看核心代码
     var index = 0,
         resIndex = 0,
         result = Array(nativeCeil(length / size));

      while (index < length) {
        result[resIndex++] = baseSlice(array, index, (index += size));
      }
      return result;
      (a).初始化原数组下标index,新二维数组下标resIndex,新二维数组result，并占位
      (b).无限循环剪切index开始，index+size结束的数组元素并填入result，直到末位
```
### 延申
    Ceil(length/size)从0开始向上取整，完美的得到了新数组的下标

    取2数组前三组成新数组
    return _.chunk(a,3).concat(_chunk(b,3));
