# 希尔排序算法

```
function shellSort(arr) {
  var len = arr.length;
  var gap = 1;
  var tmp;
  while(gap < len/5) {
    gap = gap*5 + 1;
  }
  for(; gap>0; gap=Math.floor(gap/5)) {
    for(var i=gap; i<len; i++) {
      tmp = arr[i];
      for(var j=i-gap; j>=0 && arr[j]>tmp; j-=gap) {
        arr[j+gap] = arr[j];
      }
      arr[j+gap] = tmp;
    }
  }
  return arr;
}
```
