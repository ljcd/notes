# 选择排序算法

```
function selectionSort(arr) {
  var len = arr.length;
  var minIndex, tmp;
  for(var i=0; i<len-1; i++) {
    minIndex = i;
    for(var j=i+1; j<len; j++) {
      if(arr[j] < arr[minIndex]) {
        minIndex = j;
      }
    }
    if(i !== minIndex) {
      tmp = arr[minIndex];
      arr[minIndex] = arr[i];
      arr[i] = tmp;
    }
  }
  return arr;
}
```
