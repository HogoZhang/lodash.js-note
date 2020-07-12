## lodash.js->Array->difference

### 用法
> 返回一个去重后的数组，每个值不包含在其他数组参数中。结果值的顺序是由第一个数组中的顺序确定。

### 例子

```javascript
    _.difference([1,2,3],[3],[1,5])
    //==>[2];
```

### 源码理解
```javascript
    difference(array, values, iteratee, comparator) {
      var index = -1,
          includes = arrayIncludes,
          isCommon = true,
          length = array.length,
          result = [],
          valuesLength = values.length;

      if (!length) {
        return result;
      }
      if (iteratee) {
        values = arrayMap(values, baseUnary(iteratee));
      }
      if (comparator) {
        includes = arrayIncludesWith;
        isCommon = false;
      }
      else if (values.length >= LARGE_ARRAY_SIZE) {
        includes = cacheHas;
        isCommon = false;
        values = new SetCache(values);
      }
      outer:
      while (++index < length) {
        var value = array[index],
            computed = iteratee ? iteratee(value) : value;

        if (isCommon && computed === computed) {
          var valuesIndex = valuesLength;
          while (valuesIndex--) {
            if (values[valuesIndex] === computed) {
              continue outer;
            }
          }
          result.push(value);
        }
        else if (!includes(values, computed, comparator)) {
          result.push(value);
        }
      }
      return result;
    }


    1.核心代码
      outer:
      while (++index < length) {
        var value = array[index],
            computed = iteratee ? iteratee(value) : value;

        if (isCommon && computed === computed) {
          var valuesIndex = valuesLength;
          while (valuesIndex--) {
            if (values[valuesIndex] === computed) {
              continue outer;
            }
          }
          result.push(value);
        }
        else if (!includes(values, computed, comparator)) {
          result.push(value);
        }
      }
      return result;
      `思路：`将除array之外的数组参数合并去重，得到values,再使用includes方法，判断array中的元素是否存在于values中，若不存在即将value放进新数组result中，最后返回result。
```
### 延申
    假设有一需求，重点展示本月在本年没有出现过的新出现的天气类型:
    difference(month12,month1,month2.....);
