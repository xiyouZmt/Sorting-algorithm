## 排序算法

```java
public class Sort{

    /**
     * 选择排序
     */
    public static void selectSort(int [] array){
        for (int i = 0; i < array.length - 1; i++) {
            int k = i, j;
            for (j = i + 1; j < array.length; j++) {
                if(array[k] > array[j]){
                    k = j;
                }
            }
            if(k != i){
                int temp = array[i] ^ array[k];
                array[i] = temp ^ array[i];
                array[k] = temp ^ array[k];
            }
        }
    }

    /**
     * 冒泡排序
     */
     public static void bubbleSort(int [] array){
         boolean flag = true;
         for (int i = 0; i < array.length - 1 && flag; i++) {
             flag = false;
             for (int j = 0; j < array.length - i - 1; j++) {
                 if(array[j] > array[j + 1]){
                     int temp = array[j] ^ array[j + 1];
                     array[j] = temp ^ array[j];
                     array[j + 1] = temp ^ array[j + 1];
                     flag = true;
                 }
             }
         }
     }

    /**
     * 直接插入排序
     */
    public void insertSort(int [] l){  
        if(l != null && l.length != 0){  
            for (int i = 2; i < l.length; i++) {  
                if(l[i] < l[i - 1]){  
                    l[0] = l[i];  
                    int j;  
                    for (j = i - 1; l[0] < l[j]; j--){  
                        l[j + 1] = l[j];  
                    }  
                    l[j + 1] = l[0];  
                }  
            }  
        }  
    }  

    /**
     * 折半插入排序
     */
    public void binaryInsertSort(int [] l){  
        if(l != null && l.length != 0){  
            int j;  
            int low, high, mid;  
            for (int i = 2; i < l.length; i++) {  
                if(l[i] < l[i - 1]){  
                    l[0] = l[i];  
                    low = 1; high = i - 1;  
                    while (low <= high){  
                        mid = (low + high)/2;  
                        if(l[0] < l[mid]){  
                            high = mid - 1;  
                        } else {  
                            low = mid + 1;  
                        }  
                    }  
                    for(j = i - 1; j >= low; j--){  
                        l[j + 1] = l[j];  
                    }  
                    l[low] = l[0];  
                }  
            }  
            System.out.println(Arrays.toString(l));  
        }  
    }  

    /**
     * Shell Sort
     */
    private static void ShellSort(int [] l, int [] dk){  
        for (int aDk : dk) {  
            insertSort(l, aDk);  
        }  
    }  
      
    private static void insertSort(int [] l, int dk){  
        if(l != null && l.length != 0){  
            for (int i = dk + 1; i < l.length; i++) {  
                if(l[i] < l[i - dk]){  
                    l[0] = l[i];  
                    int j;  
                    for (j = i - dk; j > 0 && l[j] > l[0] ; j -= dk) {  
                        l[j + dk] = l[j];  
                    }  
                    l[j + dk] = l[0];  
                }  
            }  
            System.out.println(Arrays.toString(l));  
        }  
    } 

    /**
     * QuickSort
     */ 
    public static void QuickSort(int [] r, int low, int high){  
        int temp;  
        if(low < high){  
            temp = QuickPass(r, low, high);  
            QuickSort(r, low, temp - 1);  
            QuickSort(r, temp + 1, high);  
        }  
        System.out.println(Arrays.toString(r));  
    }  

    public int QuickPass(int [] r, int low, int high){  
        int temp = r[low];  
        while (low < high){  
            while (low < high && r[high] >= temp){  
                high --;  
            }  
            r[low] = r[high];  
            while (low < high && r[low] < temp){  
                low ++ ;  
            }  
            r[high] = r[low];  
        }  
        r[low] = temp;  
        return low;  
    }

    /**
     * MergeSort
     */
    public static void mergeSort(int [] l, int [] result, int left, int right){  
        if(left < right){  
            int middle = (left + right)/2;  
            mergeSort(l, result, left, middle);  
            mergeSort(l, result, middle + 1, right);  
            merge(l, result, left, right, middle);  
        }  
    }  
      
    public static void merge(int [] l, int [] result, int left, int right, int middle){  
        int p1, p2;  
        int i = p1 = left;  
        System.arraycopy(l, 0, result, 0, l.length);  
        p2 = middle + 1;  
        while (p1 <= middle && p2 <= right){  
            if(result[p2] >= result[p1]){  
                l[i] = result[p1];  
                p1 ++;  
            }  
            else{  
                l[i] = result[p2];  
                p2 ++;  
            }  
            i ++;  
        }  
        while (p1 <= middle){  
            l[i] = result[p1];  
            i ++;  
            p1 ++;  
        }  
        while (p2 <= middle){  
            l[i] = result[p2];  
            i ++;  
            p2 ++;  
        }  
    }

    /**
     * HeapSort
     */
    private static void heapSort(int[] arr) {
        // 将待排序的序列构建成一个大顶堆
        for (int i = arr.length / 2; i >= 0; i--){
            heapAdjust(arr, i, arr.length);
        }

        // 逐步将每个最大值的根节点与末尾元素交换，并且再调整二叉树，使其成为大顶堆
        for (int i = arr.length - 1; i > 0; i--) {
            swap(arr, 0, i); // 将堆顶记录和当前未经排序子序列的最后一个记录交换
            heapAdjust(arr, 0, i); // 交换之后，需要重新检查堆是否符合大顶堆，不符合则要调整
        }
    }

    /**
     * 构建堆的过程
     * @param arr 需要排序的数组
     * @param i 需要构建堆的根节点的序号
     * @param n 数组的长度
     */
    private static void heapAdjust(int[] arr, int i, int n) {
        int child;
        int father;
        for (father = arr[i]; leftChild(i) < n; i = child) {
            child = leftChild(i);
            // 如果左子树小于右子树，则需要比较右子树和父节点
            if (child != n - 1 && arr[child] < arr[child + 1]) {
                child++; // 序号增1，指向右子树
            }

            // 如果父节点小于孩子结点，则需要交换
            if (father < arr[child]) {
                arr[i] = arr[child];
            } else {
                break; // 大顶堆结构未被破坏，不需要调整
            }
        }
        arr[i] = father;
    }

    // 获取到左孩子结点
    private static int leftChild(int i) {
        return 2 * i + 1;
    }

    // 交换元素位置
    private static void swap(int[] arr, int index1, int index2) {
        int tmp = arr[index1];
        arr[index1] = arr[index2];
        arr[index2] = tmp;
    }

    /**
     * RadixSort
     */
    public class Radix {  
  
        private int value;  
        private Radix next;  
      
        private int getValue() {  
            return value;  
        }  
      
        private void setValue(int value) {  
            this.value = value;  
        }  
      
        private Radix getNext() {  
            return next;  
        }  
      
        private void setNext(Radix next) {  
            this.next = next;  
        }  
      
        public static void main(String [] args){  
            int [] l = {46, 25, 68, 33, 33, 19, 12, 80};  
            RadixSort(l);  
        }  
      
        private static void RadixSort(int [] l){  
            Radix[] linkedArray = new Radix[10];  
            Radix radix = initLinkedArray(l);  
            /** 
             *将元素按个位大小添加到元素数组中 
             */  
            digit(radix, linkedArray, 0);  
            print(linkedArray);  
            int maxLength = maxLength(l);  
            for (int i = 1; i < maxLength; i++) {  
                Radix[] newLinkedArray = new Radix[10];  
                for (Radix aLinkedArray1 : linkedArray) {  
                    radix = aLinkedArray1;  
                    digit(radix, newLinkedArray, i);  
                }  
                linkedArray = newLinkedArray;  
                print(linkedArray);  
            }  
        }  
      
        private static Radix initLinkedArray(int [] l){  
            Radix radix = new Radix();  
            Radix temp = radix;  
            radix.setValue(l[0]);  
            for (int i = 1; i < l.length; i ++) {  
                Radix t1 = new Radix();  
                t1.setValue(l[i]);  
                temp.setNext(t1);  
                temp = t1;  
            }  
            return radix;  
        }  
      
        /** 
         * 根据第i位数字的大小添加元素到数组位置 
         * @param radix 
         * @param newLinkedArray 
         * @param i 
         */  
        private static void digit(Radix radix, Radix[] newLinkedArray, int i){  
            while (radix != null) {  
                int value = radix.getValue();  
                String str = String.valueOf(value);  
                int c;  
                if (i < str.length()) {  
                    c = str.charAt(str.length() - i - 1) - 48;  
                } else {  
                    c = 0;  
                }  
                Radix newRadix = new Radix();  
                newRadix.setValue(radix.getValue());  
                if (newLinkedArray[c] == null) {  
                    newLinkedArray[c] = newRadix;  
                } else {  
                    Radix radix1 = newLinkedArray[c];  
                    while (radix1.getNext() != null) {  
                        radix1 = radix1.getNext();  
                    }  
                    radix1.setNext(newRadix);  
                }  
                radix = radix.getNext();  
            }  
        }  
      
        private static void print(Radix[] linkedArray){  
            for (Radix aLinkedArray : linkedArray) {  
                if(aLinkedArray == null){  
                    System.out.print("null");  
                }  
                while (aLinkedArray != null){  
                    System.out.print(aLinkedArray.getValue() + "    ");  
                    aLinkedArray = aLinkedArray.getNext();  
                }  
                System.out.println("");  
            }  
            System.out.println("----------------------------");  
        }  
      
        private static int maxLength(int [] l){  
            int max = l[0];  
            for (int i : l) {  
                if(i > max){  
                    max = i;  
                }  
            }  
            return String.valueOf(max).length();  
        }  
    }
}
```
### 目前包括 选择排序，冒泡排序， 插入排序（直接插入和折半插入），希尔排序，快速排序，堆排序，归并排序，基数排序。
