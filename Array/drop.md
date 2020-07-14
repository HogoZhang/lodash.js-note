## lodash.js->Array->drop

### 用法
> 从头开始，切除array一定长度的元素,返回切除后的数组。

### 例子

```javascript
    _.drop([1,2,3,4,5,6],3)
    //==>[4,5,6];
    //3为等长的长度参数，取消参数则默认长度为1
```

### 源码理解
```javascript
    function drop(array, n, guard) {
      var length = array ? array.length : 0;
      if (!length) {
        return [];
      }
      n = (guard || n === undefined) ? 1 : toInteger(n);
      return baseSlice(array, n < 0 ? 0 : n, length);
    }

    `guard意思是守卫`

    1.直接看核心代码
      return baseSlice(array, n < 0 ? 0 : n, length);

     判断array长度是否大于1，大于1从下标n开始剪切，长度为数组的长度，array长度为0返回空数组
```
### 延申
    从12个月的数据中只取最近三个月的数据

    return _.drop([array(12)],9);
