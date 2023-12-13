## Sorting 정렬

### Bubble Sort
- 인접한 두 자료를 비교하며 자리 교환하여 정렬
```Java
    public static void bubbleSort(int[] array) {
        int length = array.length;
        for (int i = 0; i < length; i++) {
        for (int j = 0; j < length - 1; j++) {
            if (array[j] > array[j + 1]) {
                int temp = array[j];
                array[j] = array[j + 1];
                array[j + 1] = temp;
            }
        }
        }
    }
    public static void main(String[] args) {
        int[] array = {36, 12, 18, 15, 41, 19};
        bubbleSort(array);
        System.out.println(Arrays.toString(array));
    }
```

### Selection Sort
- 자료들 중 제일 작은 숫자를 골라 앞으로 정렬
```Java
    public static void selectionSort (int[] array){
        int length = array.length;

        for (int j = 0; j < length; j++) {
            int minIndex = j;
            for (int i = j + 1; i < length; i++) {
                if (array[i] < array[minIndex]){
                    minIndex = i;
                }
            }
            int temp = array[minIndex];
            array[minIndex] = array[j];
            array[j] = temp;
        }
    }
    
    public static void main(String[] args) {
        int[] array = new int[] {11, 31, 29, 16, 20, 1, 5, 8};
        selectionSort(array);
        System.out.println(Arrays.toString(array));
    }
```

### Counting Sort
- 각 자료가 몇 개 존재하는지를 먼저 정리하고 정렬
```Java
public static void countingSort(int[] array){
        int[] counts = new int[6]; // max를 찾았다고 가정함
        for (int data : array){
            counts[data]++;
        }
        for (int i = 0; i < 5; i++) {
            counts[i + 1] += counts[i];
        }
        int[] output = new int[array.length];
        for (int i = array.length - 1; i >= 0; i--) {
            counts[array[i]]--;
            int position = counts[array[i]];
            output[position] = array[i];
        }
        for (int i = 0; i < array.length; i++) {
            array[i] = output[i];
        }
    }

    public static void main(String[] args) {
        int[] array = new int[]{0, 1, 4, 4, 3, 0, 5, 2, 5, 1};
        countingSort(array);
        System.out.println(Arrays.toString(array));
 }
```

### Binary Search
 - 이진 탐색
 - 이미 정렬된 원소의 나열에서 어떤 특정한 원소를 찾기 위한 검색 알고리즘
 ```Java
     public static int binarySearch(int[] array, int target) {
        int left = 0;
        int right = array.length - 1;

        while (left <= right) {
            int mid = (right - left) / 2 + left;

            if (array[mid] == target) {
                return mid;
            } else if (array[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }
        public static void main (String[]args){
            int[] array = new int[]{1, 5, 8, 11, 16, 20, 29, 31};
            System.out.println(binarySearch(array, 5));
        }
    }
 ```
