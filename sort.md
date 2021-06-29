## 1. 选择排序

``` cpp
void selectSort(vector<int> &arr) {
    for (int i = 0; i < arr.size(); i++) {
        int min = i;
        for (int j = i + 1; j < arr.size(); j++) {
            if (arr[j] < arr[min]) min = j;
        }
        swap(arr, i, min);
    }
}

void swap(vector<int> &arr, int i, int j) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
```

第一次遍历找到数组中最小的数，和第一个位置的数进行交换；第二次遍历找到数组中次小的数，和第二个位置的数进行交换，如此循环往复。

时间复杂度：O(n^2)

空间复杂度：O(1)

## 2. 插入排序

``` cpp
void insertSort(vector<int> &arr) {
   
    for (int i = 1; i < arr.size(); i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && key < arr[j]) {
            arr[j + 1] = arr[j];
            --j;
        }
        arr[j + 1] = key;
    }
}
```

插入排序比较像摸扑克牌，把牌放到合适的位置。

举个例子：

用[]括起来的代表已经摆好的牌，比如摸到的牌是：

[5]，4，3

第二张牌是4，他需要和第一张牌5比较，4小于5，所以第一张牌需要放到第二章牌的位置。第一张牌前面已经没有牌了，所以第二张牌就放到第一张牌的位置，此时牌变成了：

[4, 5], 3

第三张牌是3，他需要和第二张牌比较，3小于5，所以第二张牌需要放到第三张牌的位置；第三张牌接着和第一张牌比较，3小于4，所以第一张牌需要放到第二张牌的位置。第一张牌前面已经没有牌了，所以第三张牌就放到第一张牌的位置，此时牌变成了：

[3, 4, 5]

这样就摆好了。

时间复杂度： 最好O(n)，最坏O(n^2)

空间复杂度：O(1)


## 3. 归并排序

``` rust
pub fn merge_sort(arr: &mut Vec<i32>, tmp: &mut Vec<i32>, low: usize, mid: usize, high: usize) {
    let mut i = low;
    let mut j = mid + 1;
    let mut k = 0;
    while i <= mid && j <= high {
        if arr[i] < arr[j] {
            tmp[k] = arr[i];
            i += 1;
        } else {
            tmp[k] = arr[j];
            j += 1;
        }
        k += 1;
    }

    while i <= mid {
        tmp[k] = arr[i];
        k += 1;
        i += 1;
    }
    while j <= high {
        tmp[k] = arr[j];
        k += 1;
        j += 1;
    }
    i = low;
    k = 0;
    while i <= high {
        arr[i] = tmp[k];
        i += 1;
        k += 1;
    }
}

pub fn merge(arr: &mut Vec<i32>, tmp: &mut Vec<i32>) {
    let mut mid;
    let mut size = 1;
    let mut low;
    let mut high;
    while size < arr.len() {
        low = 0;
        while low + size < arr.len() {
            mid = low + size - 1;
            high = low + 2 * size - 1;
            if high > arr.len() - 1 {
                high = arr.len() - 1;
            }
            merge_sort(arr, tmp, low, mid, high);
            low += 2 * size
        }
        size <<= 1;
    }
}
```
