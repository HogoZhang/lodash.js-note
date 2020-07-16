## lodash.js->Array->findIndex

### 用法
> 传递一个方法/对象/属性名，通过条件查找第一个符合条件的元素的下标。

### 例子

```javascript
    var gods = [
      { 'name': '韩立', 'fairy': false },
      { 'name': '林凡', 'fairy': false },
      { 'name': '王林', 'fairy': true }
    ];
    
    _.findIndex(gods, function(god) { return god.name === '林凡'; });
    // => 1
    _.findIndex(gods, { 'name': '林凡', 'fairy': false });
    // => 1
    _.findIndex(gods, ['fairy', false]);
    // => 0
    _.findIndex(gods, 'active');
    // => 2
```

### 源码理解
```javascript

    function findIndex(array, predicate) {
      return (array && array.length)
        ? baseFindIndex(array, getIteratee(predicate, 3))
        : -1;
    }

    function baseFindIndex(array, predicate, fromRight) {
      var length = array.length,
      index = fromRight ? length : -1;

      while ((fromRight ? index-- : ++index < length)) {
        if (predicate(array[index], index, array)) {
          return index;
        }
      }
      return -1;
    }

    1.直接看核心代码
      while ((fromRight ? index-- : ++index < length)) {
        if (predicate(array[index], index, array)) {
          return index;
        }
      }
      return -1;

     findIndex未传递参数fromRight;所以循环条件为：++index<length;
     -1->length-1递增，即循环array，直到出现第一个满足predicate()条件的元素出现；
     循环完毕还没找到满足条件的元素，则返回 -1;
```
### 延申
  
  使用较少，js原生API中已提供find和findIndex；此处做熟练和练习使用。
