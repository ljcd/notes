# 冒泡排序算法

```
function bubbleSort(arr) {
  var i = arr.length - 1;
  var isSwap = true;
  while(i>0 && isSwap) {
    isSwap = false;
    for(var j=0; j<i; j++) {
      if(arr[j] > arr[j+1]) {
        var tmp = arr[j+1];
        arr[j+1] = arr[j];
        arr[j] = tmp;
        isSwap = true;
      }
    }
    i--;
  }
  return arr;
}
```
