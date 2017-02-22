# 快速排序算法

```
def quick_sort(a_list):
  quick_sort_helper(a_list, 0, len(a_list)-1)

def quick_sort_helper(a_list, start, end):
  if start < end:
    split_point = partition(a_list, start, end)
    quick_sort_helper(a_list, start, split_point-1)
    quick_sort_helper(a_list, split_point+1, end)

def partition(a_list, start, end):
  pivot_value = a_list[start]
  left_mark, right_mark, done = start, end, False
  while not done:
    while left_mark <= right_mark and a_list[left_mark] <= pivot_value:
      left_mark += 1
    while left_mark <= right_mark and a_list[right_mark] >= pivot_value:
      right_mark -=1
    if left_mark < right_mark:
      done = True
    else:
      a_list[left_mark], a_list[right_mark] = a_list[right_mark], a_list[left_mark]
  a_list[start], a_list[right_mark] = a_list[right_mark], pivot_value
  return right_mark
```
