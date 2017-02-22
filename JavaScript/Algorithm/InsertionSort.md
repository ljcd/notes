# 插入排序算法

```
function insertionSort(arr) {
  var len = arr.length;
  var left, right, mid, key;
  for(var i=1; i<len; i++) {
    left = 0;
    right = i-1;
    key = arr[i];
    while(left<=right) {
      mid = parseInt((left + right)/2);
      if(arr[mid] > key) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    }
    for(var j=i; j>left; j--) {
      arr[j] = arr[j-1];
    }
    arr[left] = key;
  }
  return arr;
}
```
