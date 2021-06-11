#CS/Java #CS/算法 

# 参考

- [[数据结构与算法分析 java语言描述（原书第3版）.pdf]]
- [[Java]]
- [[Java数据结构]]
- [[算法]] 

# 字符串

## 两个字符串的最长重复子串

```java
public class MaximalRepeatSubStringOfTwoString {
    public String maximalRepeatSubStringOfTwoString(String s1, String s2){
        int l1 = s1.length();
        int l2 = s2.length();
        if (l1<l2) return maximalRepeatSubStringOfTwoString(s2,s1);
        int start=0,end=1;
        ArrayList<HashSet<Integer>> distribution = distributionOfS2InS1(s1,s2);
        for (int left = 0; left < l2; left++) {
            if (end-start>=l2-left) break;
            for(int i:distribution.get(left)){
                int right=left+1;
                for (int j=i+1;right<l2&&distribution.get(right).contains(j);right++,j++)
                    distribution.get(right).remove(j);
                if (right-left>end-start){
                    end=right;
                    start=left;
                }
            }
        }
        return s2.substring(start,end);
    }

    private ArrayList<HashSet<Integer>> distributionOfS2InS1(String s1, String s2) {

        ArrayList<HashSet<Integer>> distribution=new ArrayList<>();
        HashMap<Character,HashSet<Integer>> cDistribution=new HashMap<>();
        for (int i = 0; i < s2.length(); i++)
            cDistribution.put(s2.charAt(i),new HashSet<>());
        for (int i = 0; i < s1.length(); i++) {
            char c = s1.charAt(i);
            if (cDistribution.containsKey(c))
                cDistribution.get(c).add(i);
        }
        for (int i = 0; i < s2.length(); i++)
            distribution.add(new HashSet<>(cDistribution.get(s2.charAt(i))));
        return distribution;
    }
}
```

## 比较字符串

```java
public static int compare(String s1,String s2){
    int i = s1.length();
    int j = s2.length();
    int end= Math.min(i, j);
    for (int k = 0; k < end; k++) {
        if (s1.charAt(k)<s2.charAt(k)) return -1;
        else if (s1.charAt(k)>s2.charAt(k)) return 1;
    }
    return i-j;
}
```

## 字符串匹配

### KMP

```java
public static int kmpSearch(String str1, String str2, int[] next) {
    //遍历 
    for(int i = 0, j = 0; i < str1.length(); i++) {
        //需要处理 str1.charAt(i) ！= str2.charAt(j), 去调整j的大小
        //KMP算法核心点, 可以验证...
        while( j > 0 && str1.charAt(i) != str2.charAt(j)) j = next[j - 1];
        if(str1.charAt(i) == str2.charAt(j)) j++;
        //找到了 // j = 3 i 
        if(j == str2.length()) return i - j + 1;
    }
    return  -1;
}
//获取到一个字符串(子串) 的部分匹配值表
public static  int[] kmpNext(String dest) {
    //创建一个next 数组保存部分匹配值
    int[] next = new int[dest.length()];
    next[0] = 0; //如果字符串是长度为1 部分匹配值就是0
    for(int i = 1, j = 0; i < dest.length(); i++) {
        //当dest.charAt(i) != dest.charAt(j) ，我们需要从next[j-1]获取新的j
        //直到我们发现 有  dest.charAt(i) == dest.charAt(j)成立才退出
        //这时kmp算法的核心点
        while(j > 0 && dest.charAt(i) != dest.charAt(j)) j = next[j-1];
        //当dest.charAt(i) == dest.charAt(j) 满足时，部分匹配值就是+1
        if(dest.charAt(i) == dest.charAt(j)) j++;
        next[i] = j;
    }
    return next;
}
```

### 暴力匹配

```java
// 暴力匹配算法实现
public static int violenceMatch(String str1, String str2) {
    char[] s1 = str1.toCharArray();
    char[] s2 = str2.toCharArray();
    int s1Len = s1.length;
    int s2Len = s2.length;
    int i = 0; // i索引指向s1
    int j = 0; // j索引指向s2
    while (i < s1Len && j < s2Len) {// 保证匹配时，不越界
        if(s1[i] == s2[j]) {//匹配ok
            i++;
            j++;
        } else { //没有匹配成功
            //如果失配（即str1[i]! = str2[j]），令i = i - (j - 1)，j = 0。
            i = i - (j - 1);
            j = 0;
        }
    }

    //判断是否匹配成功
    if(j == s2Len) {
        return i - j;
    } else {
        return -1;
    }
}
```

# 查找

## 斐波那契查找

```java
public static int maxSize = 20;
public static int[] fib() {
    int[] f = new int[maxSize];
    f[0] = 1;
    f[1] = 1;
    for (int i = 2; i < maxSize; i++) {
        f[i] = f[i - 1] + f[i - 2];
    }
    return f;
}
public static int fibSearch(int[] a, int key) {
    int low = 0;
    int high = a.length - 1;
    int k = 0; //表示斐波那契分割数值的下标
    int mid = 0; //存放mid值
    int[] f = fib(); //获取到斐波那契数列
    //获取到斐波那契分割数值的下标
    while(high + 1> f[k]) {
        k++;
    }
    //因为 f[k] 值 可能大于 a 的 长度，因此我们需要使用Arrays类，构造一个新的数组，并指向temp[]
    //不足的部分会使用0填充
    int[] temp = Arrays.copyOf(a, f[k]);
    //实际上需求使用a数组最后的数填充 temp
    //举例:
    //temp = {1,8, 10, 89, 1000, 1234, 0, 0}  => {1,8, 10, 89, 1000, 1234, 1234, 1234,}
    for(int i = high + 1; i < temp.length; i++) {
        temp[i] = a[high];
    }

    // 使用while来循环处理，找到我们的数 key
    while (low <= high) { // 只要这个条件满足，就可以找
        mid = low + f[k - 1] - 1;
        if(key < temp[mid]) { //我们应该继续向数组的前面查找(左边)
            high = mid;
            //为甚是 k--
            //说明
            //1. 全部元素 = 前面的元素 + 后边元素
            //2. f[k] = f[k-1] + f[k-2]
            //因为 前面有 f[k-1]个元素,所以可以继续拆分 f[k-1] = f[k-2] + f[k-3]
            //即 在 f[k-1] 的前面继续查找 k--
            //即下次循环 mid = f[k-1-1]-1
            k--;
        } else if ( key > temp[mid]) { // 我们应该继续向数组的后面查找(右边)
            low = mid + 1;
            //为什么是k -=2
            //说明
            //1. 全部元素 = 前面的元素 + 后边元素
            //2. f[k] = f[k-1] + f[k-2]
            //3. 因为后面我们有f[k-2] 所以可以继续拆分 f[k-2] = f[k-3] + f[k-4]
            //4. 即在f[k-2] 的前面进行查找 k -=2
            //5. 即下次循环 mid = f[k - 1 - 2] - 1
            k -= 2;
        } else { //找到
            //需要确定，返回的是哪个下标
            return Math.min(mid, high);
        }
    }
    return -1;
}
```

## 插值查找

```java
public static int insertValueSearch(int[] arr, int left, int right, int findVal) { 

    if (left > right || findVal < arr[0] || findVal > arr[arr.length - 1]) {
        return -1;
    }

    int mid = left + (right - left) * (findVal - arr[left]) / (arr[right] - arr[left]);
    int midVal = arr[mid];
    if (findVal > midVal) {
        return insertValueSearch(arr, mid + 1, right, findVal);
    } else if (findVal < midVal) { 
        return insertValueSearch(arr, left, mid - 1, findVal);
    } else {
        return mid;
    }
}
```

## 二分查找

### 循环方式

```java
public static int binarySearch(int[] arr, int target) {

    int left = 0;
    int right = arr.length - 1;
    while(left <= right) { //说明继续查找
        int mid = (left + right) / 2;
        if(arr[mid] == target) {
            return mid;
        } else if ( arr[mid] > target) {
            right = mid - 1;//需要向左边查找
        } else {
            left = mid + 1; //需要向右边查找
        }
    }
    return -1;
}
```

### 递归方式

```java
public static List<Integer> binarySearch2(int[] arr, int left, int right, int findVal) {
    // 当 left > right 时，说明递归整个数组，但是没有找到
    if (left > right) {
        return new ArrayList<>();
    }
    int mid = (left + right) / 2;
    int midVal = arr[mid];
    if (findVal > midVal) { // 向 右递归
        return binarySearch2(arr, mid + 1, right, findVal);
    } else if (findVal < midVal) { // 向左递归
        return binarySearch2(arr, left, mid - 1, findVal);
    } else {
        List<Integer> resIndexlist = new ArrayList<>();
        //向mid 索引值的左边扫描，将所有满足 1000， 的元素的下标，加入到集合ArrayList
        int temp = mid - 1;
        //退出
        while (temp >= 0 && arr[temp] == findVal) {
            //否则，就temp 放入到 resIndexlist
            resIndexlist.add(temp);
            temp -= 1; //temp左移
        }
        resIndexlist.add(mid);  //
        //向mid 索引值的右边扫描，将所有满足 1000， 的元素的下标，加入到集合ArrayList
        temp = mid + 1;
        //退出
        while (temp <= arr.length - 1 && arr[temp] == findVal) {
            //否则，就temp 放入到 resIndexlist
            resIndexlist.add(temp);
            temp += 1; //temp右移
        }
        return resIndexlist;
    }
}
```

## 线性查找

```java
public static int seqSearch(int[] arr, int value) {
    // 线性查找是逐一比对，发现有相同值，就返回下标
    for (int i = 0; i < arr.length; i++) {
        if(arr[i] == value) {
            return i;
        }
    }
    return -1;
}
```

# 排序

## 冒泡排序

```java
public void bubbleSort(int[] arr){
    boolean flag=true;
    int temp=0;
    for (int i=0;i<arr.length-1;i++){
        for (int j=0;j<arr.length-1-i;j++){
            if (arr[j]>arr[j+1]){
                flag=false;
                temp=arr[j];
                arr[j]=arr[j+1];
                arr[j+1]=temp;
            }
        }
        if (flag) break;
        else flag=true;
    }
}
```

## 选择排序

```java
public void selectSort(int[] arr) {
    for (int i = 0; i < arr.length - 1; i++) {
        int minIndex = i;
        int min = arr[i];
        for (int j = i + 1; j < arr.length; j++) {
            if (min > arr[j]) {
                min = arr[j]; 
                minIndex = j;
            }
        }
        if (minIndex != i) {
            arr[minIndex] = arr[i];
            arr[i] = min;
        }
    }
}
```

## 插入排序

```java
public static void insertSort(int[] arr){
    for(int i=1;i<arr.length;i++){
        int current=arr[i];
        int j=i-1;
        while(j >= 0 && current < arr[j]) {
            arr[j+1]=arr[j];
            j--;
        }
        arr[j+1]=current;
    }
}
```

## shell排序

```java
//插入式shell排序
public static void shellSort(int[] arr) {
    for (int gap = arr.length / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < arr.length; i++) {
            int j = i;
            int temp = arr[j];
            if (arr[j] < arr[j - gap]) {
                while (j - gap >= 0 && temp < arr[j - gap]) {
                    arr[j] = arr[j - gap];
                    j -= gap;
                }
                arr[j] = temp;
            }
        }
    }
}
```

## 快速排序

```java
public static void quickSort(int[] arr,int left, int right) {
    if (left>=right)return;
    int l=left;
    int r=right;
    int base=arr[left];
    int temp;
    while (l<r){
        while (r>l && arr[r]>=base) --r;
        while (l<r && arr[l]<=base) ++l;
        if (l<r) {
            temp=arr[l];
            arr[l]=arr[r];
            arr[r]=temp;
        }
    }
    if(r>left){
        arr[left]=arr[r];
        arr[r]=base;
    }
    quickSort(arr, left, --r);
    quickSort(arr, ++l, right);
}
```

## 归并排序

```java
public static void mergeSort(int[] arr, int left, int right, int[] temp) {
    if(left < right) {
        int mid = (left + right) / 2; 
        mergeSort(arr, left, mid, temp);
        mergeSort(arr, mid + 1, right, temp);
        merge(arr, left, mid, right, temp);
    }
}
public static void merge(int[] arr, int left, int mid, int right, int[] temp) {
    int i = left; 
    int j = mid + 1; 
    int t = 0;
    while (i <= mid && j <= right) {
        if(arr[i] <= arr[j]) temp[t++] = arr[i++];
        else temp[t++] = arr[j++];
    }
    while( i <= mid) temp[t++] = arr[i++];
    while( j <= right) temp[t++] = arr[j++];
    t = 0;
    while(left <= right) arr[left++] = temp[t++];
}
```

## 桶排序

```java
public static void radixSort(int[] arr) {
    int max = arr[0];
    for(int i = 1; i < arr.length; i++) 
        if (arr[i] > max)
            max = arr[i];
    int maxLength = (max + "").length();
    int[][] bucket = new int[10][arr.length];
    int[] bucketElementCounts = new int[10];
    for(int i = 0 , n = 1; i < maxLength; i++, n *= 10) {
        for (int value : arr) {
            int digitOfElement = value / n % 10;
            bucket[digitOfElement][bucketElementCounts[digitOfElement]++] = value;
        }
        int index = 0;
        for(int k = 0; k < bucketElementCounts.length; k++) {
            if(bucketElementCounts[k] != 0)
                for (int l = 0; l < bucketElementCounts[k]; l++) 
                    arr[index++] = bucket[k][l];
            bucketElementCounts[k] = 0;
        }
    }
}
```

## 堆排序

```java
public static void heapSort(int[] arr) {
    int min = 0;
    //从后往前调整所有的父节点，循环结束后所有父节点都比子节点大
    for(int i = arr.length / 2 -1; i >=0; i--)
        adjustHeap(arr, i, arr.length);
    //将最大值放在最后，然后再找出数组前面部分的最大值
    for(int j = arr.length-1;j >0; j--) {
        min = arr[j];
        arr[j] = arr[0];
        arr[0] = min;
        //交换后除了根节点以外父节点都比子节点大
        adjustHeap(arr, 0, j); 
    }
}
public  static void adjustHeap(int[] arr, int i, int length) {
    int root = arr[i];
    for(int k = i * 2 + 1; k < length; k = k * 2 + 1) {
        if(k+1 < length && arr[k] < arr[k+1]) k++;//获取左右子节点较大者
        if(arr[k] > root) {//如果子节点中较大者大于根节点，就将此子节点上移
            arr[i] = arr[k];
            i = k;
        } else break;
    }
    arr[i] = root;//将根节点放在其应该(按所有父节点都比子节点大规则)所处的位置
}
```

# 递归

- 用到递归的[[Java算法#排序]]算法
  1. [[Java算法#快速排序]]
  2. [[Java算法#归并排序]]
- 用到递归的[[Java算法#查找]]算法
  1. [[Java算法#二分查找]]
  2. [[Java算法#插值查找]]
- 与[[Java算法#树]]相关的算法
  1. [[Java算法#霍夫曼编码]]

## 汉诺塔

```java
public static void hanoiTower(int num, char a, char b, char c) {
    //如果只有一个盘
    if(num == 1) {
        System.out.println("第1个盘从 " + a + "->" + c);
    } else {
        //如果我们有 n >= 2 情况，我们总是可以看做是两个盘 1.最下边的一个盘 2. 上面的所有盘
        //1. 先把 最上面的所有盘 A->B， 移动过程会使用到 c
        hanoiTower(num - 1, a, c, b);
        //2. 把最下边的盘 A->C
        System.out.println("第" + num + "个盘从 " + a + "->" + c);
        //3. 把B塔的所有盘 从 B->C , 移动过程使用到 a塔  
        hanoiTower(num - 1, b, a, c);

    }
}
```

## 字符串的全排列

```java
public class Arrange {
    public static void main(String[] args) {
        new Arrange().arrangeString(new char[]{'a', 'b', 'c'},0,3);
    }

    public void arrangeString(char[] arr,int left,int length){
        if (left==length) {
            for (int j = 0; j < length; j++) {
                System.out.print(arr[j]);
            }
            System.out.println();
        }else {
            for (int j = left; j < length; j++) {
                swap(arr,j,left);
                arrangeString(arr,left+1,length);
                swap(arr,j,left);
            }
        }
    }

    private void swap(char[] arr, int j, int i) {
        char temp=arr[j];
        arr[j]=arr[i];
        arr[i]=temp;
    }
}
```

## 篮子放球

```java
public int count(int baskets, int capacity, int balls){
    if (baskets*capacity<balls) return 0;
    //为了减少递归,单独考虑以下简单情况，更复杂的情况用递归更好
    if (balls==0||baskets==1) return 1;//没球或者只有一个篮子
    if (balls==1) return baskets;//球数为1，篮子里只能放一个，放哪个篮子就是一种放法
    //复杂情况
    int sum = 0;
    int maxBalls= Math.min(balls, capacity);//确定最大球数
    for (int i = 0; i <= maxBalls; i++)
        sum += count(baskets - 1, capacity, balls - i);
    return sum;
}
```

## 迷宫

```java
public static boolean setWay(int[][] map, int i, int j) {
    if(map[6][5] == 2) { // 通路已经找到ok
        return true;
    } else {
        if(map[i][j] == 0) { //如果当前这个点还没有走过
            //按照策略 下->右->上->左  走
            map[i][j] = 2; // 假定该点是可以走通.
            if(setWay(map, i+1, j)) {//向下走
                return true;
            } else if (setWay(map, i, j+1)) { //向右走
                return true;
            } else if (setWay(map, i-1, j)) { //向上
                return true;
            } else if (setWay(map, i, j-1)){ // 向左走
                return true;
            } else {
                //说明该点是走不通，是死路
                map[i][j] = 3;
                return false;
            }
        } else { // 如果map[i][j] != 0 , 可能是 1， 2， 3
            return false;
        }
    }
}
```

## 八皇后

```java
public class Queue8 {

    //定义一个max表示共有多少个皇后
    int max = 8;
    //定义数组array, 保存皇后放置位置的结果,比如 arr = {0 , 4, 7, 5, 2, 6, 1, 3} 
    int[] array = new int[max];
    static int count = 0;
    static int judgeCount = 0;
    public static void main(String[] args) {
        //测试一把 ， 8皇后是否正确
        Queue8 queue8 = new Queue8();
        queue8.check(0);
        System.out.printf("一共有%d解法", count*2);
        System.out.printf("一共判断冲突的次数%d次", judgeCount); // 1.5w

    }



    //编写一个方法，放置第n个皇后
    //特别注意： check 是 每一次递归时，进入到check中都有  for(int i = 0; i < max; i++)，因此会有回溯
    private void check(int n) {
        if(n == max) {  //n = 8 , 其实8个皇后就既然放好
            print();
            return;
        }
        int end=max;
        if (n==0){
            end=4;
        }
        //依次放入皇后，并判断是否冲突
        for(int i = 0; i < end; i++) {
            //先把当前这个皇后 n , 放到该行的第1列
            array[n] = i;
            //判断当放置第n个皇后到i列时，是否冲突
            if(judge(n)) { // 不冲突
                //接着放n+1个皇后,即开始递归
                check(n+1); //  
            }
            //如果冲突，就继续执行 array[n] = i; 即将第n个皇后，放置在本行得 后移的一个位置
        }
    }

    //查看当我们放置第n个皇后, 就去检测该皇后是否和前面已经摆放的皇后冲突
    /**
     * 
     * @param n 表示第n个皇后
     * @return
     */
    private boolean judge(int n) {
        judgeCount++;
        for(int i = 0; i < n; i++) {
            // 说明
            //1. array[i] == array[n]  表示判断 第n个皇后是否和前面的n-1个皇后在同一列
            //2. Math.abs(n-i) == Math.abs(array[n] - array[i]) 表示判断第n个皇后是否和第i皇后是否在同一斜线
            // n = 1  放置第 2列 1 n = 1 array[1] = 1
            // Math.abs(1-0) == 1  Math.abs(array[n] - array[i]) = Math.abs(1-0) = 1
            //3. 判断是否在同一行, 没有必要，n 每次都在递增
            if(array[i] == array[n] || Math.abs(n-i) == Math.abs(array[n] - array[i]) ) {
                return false;
            }
        }
        return true;
    }

    //写一个方法，可以将皇后摆放的位置输出
    private void print() {
        count++;
        for (int value : array) {
            System.out.print(value + " ");
        }
        System.out.println();
    }

}
```

# 链

## 反转单链表

```java
public static <T> void reverseList(HeroNode<T> head) {
    if(head.next == null || head.next.next == null) {
        return ;
    }
    HeroNode<T> cur = head.next;
    HeroNode<T> next = null;
    HeroNode<T> reverseHead = new HeroNode<>();
    while(cur != null) { 
        next = cur.next;
        cur.next = reverseHead.next;
        reverseHead.next = cur; 
        cur = next;
    }
    head.next = reverseHead.next;
}
```

# 栈

## 后缀表达式计算器

```java
public class PolandNotation {

    public static void main(String[] args) {


        //完成将一个中缀表达式转成后缀表达式的功能
        //说明
        //1. 1+((2+3)×4)-5 => 转成  1 2 3 + 4 × + 5 –
        //2. 因为直接对str 进行操作，不方便，因此 先将  "1+((2+3)×4)-5" =》 中缀的表达式对应的List
        //   即 "1+((2+3)×4)-5" => ArrayList [1,+,(,(,2,+,3,),*,4,),-,5]
        //3. 将得到的中缀表达式对应的List => 后缀表达式对应的List
        //   即 ArrayList [1,+,(,(,2,+,3,),*,4,),-,5]  =》 ArrayList [1,2,3,+,4,*,+,5,–]

        String expression = "1+((2+3)*4)-5";//注意表达式 
        List<String> infixExpressionList = toInfixExpressionList(expression);
        System.out.println("中缀表达式对应的List=" + infixExpressionList); // ArrayList [1,+,(,(,2,+,3,),*,4,),-,5]
        List<String> suffixExpreesionList = parseSuffixExpreesionList(infixExpressionList);
        System.out.println("后缀表达式对应的List" + suffixExpreesionList); //ArrayList [1,2,3,+,4,*,+,5,–] 

        System.out.printf("expression=%d", calculate(suffixExpreesionList)); // ?



        /*

        //先定义给逆波兰表达式
        //(30+4)×5-6  => 30 4 + 5 × 6 - => 164
        // 4 * 5 - 8 + 60 + 8 / 2 => 4 5 * 8 - 60 + 8 2 / + 
        //测试 
        //说明为了方便，逆波兰表达式 的数字和符号使用空格隔开
        //String suffixExpression = "30 4 + 5 * 6 -";
        String suffixExpression = "4 5 * 8 - 60 + 8 2 / +"; // 76
        //思路
        //1. 先将 "3 4 + 5 × 6 - " => 放到ArrayList中
        //2. 将 ArrayList 传递给一个方法，遍历 ArrayList 配合栈 完成计算

        List<String> list = getListString(suffixExpression);
        System.out.println("rpnList=" + list);
        int res = calculate(list);
        System.out.println("计算的结果是=" + res);

        */
    }



    //即 ArrayList [1,+,(,(,2,+,3,),*,4,),-,5]  =》 ArrayList [1,2,3,+,4,*,+,5,–]
    //方法：将得到的中缀表达式对应的List => 后缀表达式对应的List
    public static List<String> parseSuffixExpreesionList(List<String> ls) {
        //定义两个栈
        Stack<String> s1 = new Stack<>(); // 符号栈
        //说明：因为s2 这个栈，在整个转换过程中，没有pop操作，而且后面我们还需要逆序输出
        //因此比较麻烦，这里我们就不用 Stack<String> 直接使用 List<String> s2
        //Stack<String> s2 = new Stack<String>(); // 储存中间结果的栈s2
        List<String> s2 = new ArrayList<>(); // 储存中间结果的Lists2

        //遍历ls
        for(String item: ls) {
            //如果是一个数，加入s2
            if(item.matches("\\d+")) {
                s2.add(item);
            } else if (item.equals("(")) {
                s1.push(item);
            } else if (item.equals(")")) {
                //如果是右括号“)”，则依次弹出s1栈顶的运算符，并压入s2，直到遇到左括号为止，此时将这一对括号丢弃
                while(!s1.peek().equals("(")) {
                    s2.add(s1.pop());
                }
                s1.pop();//!!! 将 ( 弹出 s1栈， 消除小括号
            } else {
                //当item的优先级小于等于s1栈顶运算符, 将s1栈顶的运算符弹出并加入到s2中，再次转到(4.1)与s1中新的栈顶运算符相比较
                //问题：我们缺少一个比较优先级高低的方法
                while(s1.size() != 0 && Operation.getValue(s1.peek()) >= Operation.getValue(item) ) {
                    s2.add(s1.pop());
                }
                //还需要将item压入栈
                s1.push(item);
            }
        }

        //将s1中剩余的运算符依次弹出并加入s2
        while(s1.size() != 0) {
            s2.add(s1.pop());
        }

        return s2; //注意因为是存放到List, 因此按顺序输出就是对应的后缀表达式对应的List

    }

    //方法：将 中缀表达式转成对应的List
    //  s="1+((2+3)×4)-5";
    public static List<String> toInfixExpressionList(String s) {
        //定义一个List,存放中缀表达式 对应的内容
        List<String> ls = new ArrayList<>();
        int i = 0; //这时是一个指针，用于遍历 中缀表达式字符串
        StringBuilder str; // 对多位数的拼接
        char c; // 每遍历到一个字符，就放入到c
        do {
            //如果c是一个非数字，我需要加入到ls
            if((c=s.charAt(i)) < 48 ||  (c=s.charAt(i)) > 57) {
                ls.add("" + c);
                i++; //i需要后移
            } else { //如果是一个数，需要考虑多位数
                str = new StringBuilder(); //先将str 置成"" '0'[48]->'9'[57]
                while(i < s.length() && (c=s.charAt(i)) >= 48 && (c=s.charAt(i)) <= 57) {
                    str.append(c);//拼接
                    i++;
                }
                ls.add(str.toString());
            }
        }while(i < s.length());
        return ls;//返回
    }

    //将一个逆波兰表达式， 依次将数据和运算符 放入到 ArrayList中
    public static List<String> getListString(String suffixExpression) {
        //将 suffixExpression 分割
        String[] split = suffixExpression.split(" ");
        return new ArrayList<String>(Arrays.asList(split));

    }

    //完成对逆波兰表达式的运算
    /*
     * 1)从左至右扫描，将3和4压入堆栈；
        2)遇到+运算符，因此弹出4和3（4为栈顶元素，3为次顶元素），计算出3+4的值，得7，再将7入栈；
        3)将5入栈；
        4)接下来是×运算符，因此弹出5和7，计算出7×5=35，将35入栈；
        5)将6入栈；
        6)最后是-运算符，计算出35-6的值，即29，由此得出最终结果
     */

    public static int calculate(List<String> ls) {
        // 创建给栈, 只需要一个栈即可
        Stack<String> stack = new Stack<String>();
        // 遍历 ls
        for (String item : ls) {
            // 这里使用正则表达式来取出数
            if (item.matches("\\d+")) { // 匹配的是多位数
                // 入栈
                stack.push(item);
            } else {
                // pop出两个数，并运算， 再入栈
                int num2 = Integer.parseInt(stack.pop());
                int num1 = Integer.parseInt(stack.pop());
                int res = switch (item) {
                    case "+" -> num1 + num2;
                    case "-" -> num1 - num2;
                    case "*" -> num1 * num2;
                    case "/" -> num1 / num2;
                    default -> throw new RuntimeException("运算符有误");
                };
                //把res 入栈
                stack.push("" + res);
            }

        }
        //最后留在stack中的数据是运算结果
        return Integer.parseInt(stack.pop());
    }

}

//编写一个类 Operation 可以返回一个运算符 对应的优先级
class Operation {
    private static final int ADD = 1;
    private static final int SUB = 1;
    private static final int MUL = 2;
    private static final int DIV = 2;

    //写一个方法，返回对应的优先级数字
    public static int getValue(String operation) {
        int result = 0;
        switch (operation) {
            case "+" -> result = ADD;
            case "-" -> result = SUB;
            case "*" -> result = MUL;
            case "/" -> result = DIV;
            default -> System.out.println("不存在该运算符" + operation);
        }
        return result;
    }

}
```

# 树

## 复制树

采用从上到下从左到右的方式复制一颗树并打印

```java
class Tree{
    int value;
    Tree left;
    Tree right;
    public Tree(int value) {
        this.value=value;
    }
    public void list(){
        LinkedList<Tree> list=new LinkedList<>();
        list.add(this);
        while (list.size()>0) {
            Tree current = list.remove();
            if (current.left!=null) list.add(current.left);
            if (current.right!=null) list.add(current.right);            
            System.out.print(current.value+"\t");
        }
        System.out.println();
    }
    public Tree copy() {
        Tree newtree=new Tree(value);

        LinkedList<Tree> list1=new LinkedList<>();
        list1.add(this);

        LinkedList<Tree> list2=new LinkedList<>();
        list2.add(newtree);

        while (list1.size()>0) {
            Tree originTree = list1.remove();
            Tree copyTree = list2.remove();
            if (originTree.left!=null) {
                copyTree.left=new Tree(originTree.left.value);
                list1.add(originTree.left);
                list2.add(copyTree.left);
            }
            if (originTree.right!=null) {
                copyTree.right=new Tree(originTree.right.value);
                list1.add(originTree.right);
                list2.add(copyTree.right);
            }
        }
        return newtree;        
    }
}
```

## 霍夫曼编码

```java
public class HuffmanCode {

    public static void unZipFile(String zipFile, String dstFile) {


        InputStream is = null;

        ObjectInputStream ois = null;

        OutputStream os = null;
        try {

            is = new FileInputStream(zipFile);

            ois = new ObjectInputStream(is);

            byte[] huffmanBytes = (byte[])ois.readObject();

            Map<Byte,String> huffmanCodes = (Map<Byte,String>)ois.readObject();

            byte[] bytes = decode(huffmanCodes, huffmanBytes);

            os = new FileOutputStream(dstFile);

            os.write(bytes);
        } catch (Exception e) {
            // TODO: handle exception
            System.out.println(e.getMessage());
        } finally {

            try {
                assert os != null;
                os.close();
                ois.close();
                is.close();
            } catch (Exception e2) {
                // TODO: handle exception
                System.out.println(e2.getMessage());
            }

        }
    }

    public static void zipFile(String srcFile, String dstFile) {


        OutputStream os = null;
        ObjectOutputStream oos = null;

        FileInputStream is = null;
        try {

            is = new FileInputStream(srcFile);

            byte[] b = new byte[is.available()];

            is.read(b);

            byte[] huffmanBytes = huffmanZip(b);

            os = new FileOutputStream(dstFile);

            oos = new ObjectOutputStream(os);

            oos.writeObject(huffmanBytes);
            oos.writeObject(huffmanCodes);


        }catch (Exception e) {
            // TODO: handle exception
            System.out.println(e.getMessage());
        }finally {
            try {
                assert is != null;
                is.close();
                assert oos != null;
                oos.close();
                os.close();
            }catch (Exception e) {
                // TODO: handle exception
                System.out.println(e.getMessage());
            }
        }

    }

    private static byte[] decode(Map<Byte,String> huffmanCodes, byte[] huffmanBytes) {

        StringBuilder stringBuilder = new StringBuilder();
        String str;
        for(int i = 0; i < huffmanBytes.length-2; i++) {
            byte b = huffmanBytes[i];
            str = byteToBitString(b);
            //System.out.println("此次添加："+str);
            stringBuilder.append(str);
        }

        int temp=huffmanBytes[huffmanBytes.length - 2];
        str=Integer.toBinaryString(temp);
        if (temp>=0) str="0".repeat(Math.max(0, huffmanBytes[huffmanBytes.length - 1]))+str;
        else str=str.substring(str.length() - 8);
        //System.out.println("此次添加："+str);
        stringBuilder.append(str);

        System.out.println("解码结果："+stringBuilder);
        Map<String, Byte>  map = new HashMap<>();
        for(Map.Entry<Byte, String> entry: huffmanCodes.entrySet()) {
            map.put(entry.getValue(), entry.getKey());
        }

        List<Byte> list = new ArrayList<>();

        for(int  i = 0; i < stringBuilder.length(); ) {
            int count = 1;
            Byte b = null;
            String key;
            for(Map.Entry<String, Byte> entry: map.entrySet()) {
                key=entry.getKey();
                count=key.length();
                if (i + count<=stringBuilder.length()&&
                        key.equals(stringBuilder.substring(i, i + count))){
                    b=entry.getValue();
                    break;
                }
            }
            list.add(b);
            i += count;
        }
        byte[] b = new byte[list.size()];
        for(int i = 0;i < b.length; i++) b[i] = list.get(i);
        return b;
    }

    private static String byteToBitString(byte b) {
        int temp = b;
        temp |= 256;
        String str = Integer.toBinaryString(temp);
        return str.substring(str.length() - 8);

    }

    private static byte[] huffmanZip(byte[] bytes) {
        List<Node> nodes = getNodes(bytes);
        Node huffmanTreeRoot = createHuffmanTree(nodes);
        Map<Byte, String> huffmanCodes = getCodes(huffmanTreeRoot);
        return zip(bytes, huffmanCodes);
    }

    private static byte[] zip(byte[] bytes, Map<Byte, String> huffmanCodes) {

        StringBuilder stringBuilder = new StringBuilder();

        for(byte b: bytes) {
            stringBuilder.append(huffmanCodes.get(b));
        }
        //System.out.println("二进制字符串："+stringBuilder);
        int len;
        if(stringBuilder.length() % 8 == 0) {
            len = stringBuilder.length() / 8;
        } else {
            len = stringBuilder.length() / 8 + 1;
        }
        byte[] huffmanCodeBytes = new byte[len+1];
        int index = 0;
        int count=0;//补0的数目
        for (int i = 0; i < stringBuilder.length(); i += 8) {
            String strByte;
            if(i+8 > stringBuilder.length()) strByte = stringBuilder.substring(i);
            else strByte = stringBuilder.substring(i, i + 8);
            //转换最后一个字节时，需要计算开头0的数目，将count放在最后一个bite
            if(i+8>=stringBuilder.length()){
                //如果全是0的话不用计算最后一个0
                for (int j = 0; j < strByte.length()-1; j++) {
                    if (strByte.charAt(j)=='0'){
                        ++count;
                    }else break;
                }
            }
            huffmanCodeBytes[index] = (byte)Integer.parseInt(strByte, 2);
            index++;
        }
        huffmanCodeBytes[index]= (byte) count;
        return huffmanCodeBytes;
    }

    static Map<Byte, String> huffmanCodes = new HashMap<>();

    static StringBuilder stringBuilder = new StringBuilder();

    private static Map<Byte, String> getCodes(Node root) {
        if(root == null) {
            return null;
        }
        getCodes(root.left, "0", stringBuilder);
        getCodes(root.right, "1", stringBuilder);
        return huffmanCodes;
    }

    private static void getCodes(Node node, String code, StringBuilder stringBuilder) {
        StringBuilder stringBuilder2 = new StringBuilder(stringBuilder);
        stringBuilder2.append(code);
        if(node != null) {
            if(node.data == null) {
                getCodes(node.left, "0", stringBuilder2);
                getCodes(node.right, "1", stringBuilder2);
            } else huffmanCodes.put(node.data, stringBuilder2.toString());
        }
    }

    private static List<Node> getNodes(byte[] bytes) {

        ArrayList<Node> nodes = new ArrayList<>();

        Map<Byte, Integer> counts = new HashMap<>();

        for (byte b : bytes) counts.merge(b, 1, Integer::sum);

        for(Map.Entry<Byte, Integer> entry: counts.entrySet())
            nodes.add(new Node(entry.getKey(), entry.getValue()));

        return nodes;
    }

    private static Node createHuffmanTree(List<Node> nodes) {
        while(nodes.size() > 1) {
            Collections.sort(nodes);
            Node leftNode = nodes.get(0);
            Node rightNode = nodes.get(1);
            Node parent = new Node(null, leftNode.weight + rightNode.weight);
            parent.left = leftNode;
            parent.right = rightNode;
            nodes.remove(0);
            nodes.remove(0);
            nodes.add(parent);
        }
        return nodes.get(0);
    }
}

class Node implements Comparable<Node>  {

    Byte data;
    int weight;
    Node left;
    Node right;

    public Node(Byte data, int weight) {
        this.data = data;
        this.weight = weight;
    }

    @Override
    public int compareTo(Node o) {
        return this.weight - o.weight;
    }

    public String toString() {
        return "Node [data = " + data + " weight=" + weight + "]";
    }

    public void preOrder() {
        System.out.println(this);
        if(this.left != null) this.left.preOrder();
        if(this.right != null) this.right.preOrder();
    }
}
```

# 图

## Kruskal解决公交问题

```java
public class KruskalCase {

    private int edgeNum; //边的个数
    private final char[] vertexs; //顶点数组
    private final int[][] matrix; //邻接矩阵
    //使用 INF 表示两个顶点不能连通
    private static final int INF = Integer.MAX_VALUE;

    public static void main(String[] args) {
        char[] vertexs = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        //克鲁斯卡尔算法的邻接矩阵  
          int[][] matrix = {
          /*A*//*B*//*C*//*D*//*E*//*F*//*G*/
    /*A*/ {   0,  12, INF, INF, INF,  16,  14},
    /*B*/ {  12,   0,  10, INF, INF,   7, INF},
    /*C*/ { INF,  10,   0,   3,   5,   6, INF},
    /*D*/ { INF, INF,   3,   0,   4, INF, INF},
    /*E*/ { INF, INF,   5,   4,   0,   2,   8},
    /*F*/ {  16,   7,   6, INF,   2,   0,   9},
    /*G*/ {  14, INF, INF, INF,   8,   9,   0}}; 
          //大家可以在去测试其它的邻接矩阵，结果都可以得到最小生成树.

          //创建KruskalCase 对象实例
          KruskalCase kruskalCase = new KruskalCase(vertexs, matrix);
          //输出构建的
          kruskalCase.print();
          kruskalCase.kruskal();

    }

    //构造器
    public KruskalCase(char[] vertexs, int[][] matrix) {
        //初始化顶点数和边的个数
        int vlen = vertexs.length;

        //初始化顶点, 复制拷贝的方式
        this.vertexs = new char[vlen];
        System.arraycopy(vertexs, 0, this.vertexs, 0, vertexs.length);

        //初始化边, 使用的是复制拷贝的方式
        this.matrix = new int[vlen][vlen];
        for(int i = 0; i < vlen; i++) {
            System.arraycopy(matrix[i], 0, this.matrix[i], 0, vlen);
        }
        //统计边的条数
        for(int i =0; i < vlen; i++) {
            for(int j = i+1; j < vlen; j++) {
                if(this.matrix[i][j] != INF) {
                    edgeNum++;
                }
            }
        }

    }
    public void kruskal() {
        int index = 0; //表示最后结果数组的索引
        int[] ends = new int[edgeNum]; //用于保存"已有最小生成树" 中的每个顶点在最小生成树中的终点
        //创建结果数组, 保存最后的最小生成树
        EData[] rets = new EData[edgeNum];

        //获取图中 所有的边的集合 ， 一共有12边
        EData[] edges = getEdges();
        System.out.println("图的边的集合=" + Arrays.toString(edges) + " 共"+ edges.length); //12

        //按照边的权值大小进行排序(从小到大)
        sortEdges(edges);

        //遍历edges 数组，将边添加到最小生成树中时，判断是准备加入的边否形成了回路，如果没有，就加入 rets, 否则不能加入
        for(int i=0; i < edgeNum; i++) {
            //获取到第i条边的第一个顶点(起点)
            int p1 = getPosition(edges[i].start); //p1=4
            //获取到第i条边的第2个顶点
            int p2 = getPosition(edges[i].end); //p2 = 5

            //获取p1这个顶点在已有最小生成树中的终点
            int m = getEnd(ends, p1); //m = 4
            //获取p2这个顶点在已有最小生成树中的终点
            int n = getEnd(ends, p2); // n = 5
            //是否构成回路
            if(m != n) { //没有构成回路
                ends[m] = n; // 设置m 在"已有最小生成树"中的终点 <E,F> [0,0,0,0,5,0,0,0,0,0,0,0]
                rets[index++] = edges[i]; //有一条边加入到rets数组
            }
        }
        //<E,F> <C,D> <D,E> <B,F> <E,G> <A,B>。
        //统计并打印 "最小生成树", 输出  rets
        System.out.println("最小生成树为");
        for(int i = 0; i < index; i++)
            System.out.println(rets[i]);
    }

    //打印邻接矩阵
    public void print() {
        System.out.println("邻接矩阵为: \n");
        for(int i = 0; i < vertexs.length; i++) {
            for(int j=0; j < vertexs.length; j++)
                System.out.printf("%12d", matrix[i][j]);
            System.out.println();//换行
        }
    }

    /**
     * 功能：对边进行排序处理, 冒泡排序
     * @param edges 边的集合
     */
    private void sortEdges(EData[] edges) {
        for(int i = 0; i < edges.length - 1; i++)
            for (int j = 0; j < edges.length - 1 - i; j++)
                if (edges[j].weight > edges[j + 1].weight) {//交换
                    EData tmp = edges[j];
                    edges[j] = edges[j + 1];
                    edges[j + 1] = tmp;
                }
    }
    /**
     * 
     * @param ch 顶点的值，比如'A','B'
     * @return 返回ch顶点对应的下标，如果找不到，返回-1
     */
    private int getPosition(char ch) {
        for(int i = 0; i < vertexs.length; i++)
            if(vertexs[i] == ch) //找到
                return i;
        //找不到,返回-1
        return -1;
    }
    /**
     * 功能: 获取图中边，放到EData[] 数组中，后面我们需要遍历该数组
     * 是通过matrix 邻接矩阵来获取
     * EData[] 形式 [['A','B', 12], ['B','F',7], .....]
     * @return EData[]
     */
    private EData[] getEdges() {
        int index = 0;
        EData[] edges = new EData[edgeNum];
        for(int i = 0; i < vertexs.length; i++)
            for(int j=i+1; j <vertexs.length; j++)
                if(matrix[i][j] != INF)
                    edges[index++] = new EData(vertexs[i], vertexs[j], matrix[i][j]);
        return edges;
    }
    /**
     * 功能: 获取下标为i的顶点的终点(), 用于后面判断两个顶点的终点是否相同
     * @param ends ： 数组就是记录了各个顶点对应的终点是哪个,ends 数组是在遍历过程中，逐步形成
     * @param i : 表示传入的顶点对应的下标
     * @return 返回的就是 下标为i的这个顶点对应的终点的下标, 一会回头还有来理解
     */
    private int getEnd(int[] ends, int i) { // i = 4 [0,0,0,0,5,0,0,0,0,0,0,0]
        while(ends[i] != 0)
            i = ends[i];
        return i;
    }

}

//创建一个类EData ，它的对象实例就表示一条边
class EData {
    char start; //边的一个点
    char end; //边的另外一个点
    int weight; //边的权值
    //构造器
    public EData(char start, char end, int weight) {
        this.start = start;
        this.end = end;
        this.weight = weight;
    }
    //重写toString, 便于输出边信息
    @Override
    public String toString() {
        return "EData [<" + start + ", " + end + ">= " + weight + "]";
    }


}
```

## prime算法解决修路问题

```java
public class PrimAlgorithm {
    public static void main(String[] args) {
        //测试看看图是否创建ok
        char[] data = new char[]{'A','B','C','D','E','F','G'};
        int verxs = data.length;
        //邻接矩阵的关系使用二维数组表示,10000这个大数，表示两个点不联通
        int [][]weight=new int[][]{
            {10000,5,7,10000,10000,10000,2},
            {5,10000,10000,9,10000,10000,3},
            {7,10000,10000,10000,8,10000,10000},
            {10000,9,10000,10000,10000,4,10000},
            {10000,10000,8,10000,10000,5,4},
            {10000,10000,10000,4,5,10000,6},
            {2,3,10000,10000,4,6,10000},};
        //创建MGraph对象
        MGraph graph = new MGraph(verxs);
        //创建一个MinTree对象
        MinTree minTree = new MinTree();
        minTree.createGraph(graph, verxs, data, weight);
        //输出
        //minTree.showGraph(graph);
        //测试普利姆算法
        for (int i = 0; i < data.length; i++) {
            minTree.prim(graph,i);
        }
    }
}

//创建最小生成树->村庄的图
class MinTree {
    //创建图的邻接矩阵
    /**
     * @param graph 图对象
     * @param vertexs 图对应的顶点个数
     * @param data 图的各个顶点的值
     * @param weight 图的邻接矩阵
     */
    public void createGraph(MGraph graph, int vertexs, char[] data, int[][] weight) {
        int i, j;
        for(i = 0; i < vertexs; i++) {//顶点
            graph.data[i] = data[i];
            for(j = 0; j < vertexs; j++) {
                graph.weight[i][j] = weight[i][j];
            }
        }
    }

    //显示图的邻接矩阵
    public void showGraph(MGraph graph) {
        for(int[] link: graph.weight) {
            System.out.println(Arrays.toString(link));
        }
    }

    //编写prim算法，得到最小生成树
    /**
     * 
     * @param graph 图
     * @param v 表示从图的第几个顶点开始生成'A'->0 'B'->1...
     */
    public void prim(MGraph graph, int v) {
        //visited[] 标记结点(顶点)是否被访问过
        int[] visited = new int[graph.vertexs];
        //visited[] 默认元素的值都是0, 表示没有访问过
//        for(int i =0; i <graph.verxs; i++) {
//            visited[i] = 0;
//        }

        //把当前这个结点标记为已访问
        visited[v] = 1;
        //h1 和 h2 记录两个顶点的下标
        int h1 = -1;
        int h2 = -1;
        int minWeight = 10000; //将 minWeight 初始成一个大数，后面在遍历过程中，会被替换
        int sum=0;
        //因为有 graph.vertexs 顶点，普利姆算法结束后，有 graph.vertexs-1 边
        for(int k = 1; k < graph.vertexs; k++) {
            //这个是确定每一次生成的子图 ，和哪个结点的距离最近
            // i结点表示被访问过的结点
            for(int i = 0; i < graph.vertexs; i++)
                if (visited[i] == 1)
                    //j结点表示还没有访问过的结点
                    for (int j = 0; j < graph.vertexs; j++)
                        if (visited[j] == 0 && graph.weight[i][j] < minWeight) {
                            //替换 minWeight (寻找已经访问过的结点和未访问过的结点间的权值最小的边)
                            minWeight = graph.weight[i][j];
                            h1 = i;
                            h2 = j;
                        }
            //找到一条边是最小
            System.out.println("边<" + graph.data[h1] + "," + graph.data[h2] + "> 权值:" + minWeight);
            sum+=minWeight;
            //将当前这个结点标记为已经访问
            visited[h2] = 1;
            //minWeight 重新设置为最大值 10000
            minWeight = 10000;
        }
        System.out.println(sum);
    }
}

class MGraph {
    int vertexs; //表示图的节点个数
    char[] data;//存放结点数据
    int[][] weight; //存放边，就是我们的邻接矩阵

    public MGraph(int vertexs) {
        this.vertexs = vertexs;
        data = new char[vertexs];
        weight = new int[vertexs][vertexs];
    }
}
```

# 其他

## 产生一组不同随机数

### 利用数组回溯

```java
  int[] a=new int[5];
  for (int i=5; i>0 ;i--){
      int b=(int)(Math.random()*10)+1;
      int j;
      for(j=0;j<5-i;j++){
          if(a[j]==b){
              i++;
              break;
          }
      }
      if(j==5-i){
          a[j]=b;
      }
  }
```

### 利用list去重

```java
  List list1= new ArrayList();
  List list2= new ArrayList();
  for(int i=0;i<m;i++){
      list1.add(i+1);
  }
  for(int i=m;i>n;i--){
      int a=(int)(Math.random()*i);
      list2.add(list1.get(a));
      list1.remove(a);
  }
```

## 背包问题

```java
public class KnapsackProblem {
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        int[] oW = {1,2,3};//物品的重量
        int[] oVal = {900,1900,2800}; //物品的价值 这里val[i] 就是前面讲的v[i]
        int[] maxNumber=new int[oW.length];

        int m = 4; //背包的容量
        int n = 0; //物品的个数

        //物品数目无限时，求出每个物品最大可放数目
        for (int i = 0; i < maxNumber.length; i++) {
            maxNumber[i]=m/oW[i];
            n+=maxNumber[i];
        }
        //添加重复物品
        int k=0;
        int[] val=new int[n];
        int[] w=new int[n];
        for (int i = 0; i < maxNumber.length; i++)
            for (int j = maxNumber[i]; j >0 ; j--) {
                val[k]=oVal[i];
                w[k]=oW[i];
                k++;
            }
        //创建二维数组，
        //v[i][j] 表示在前i个物品中能够装入容量为j的背包中的最大价值
        int[][] v = new int[n+1][m+1];
        //为了记录放入商品的情况，我们定一个二维数组
        int[][] path = new int[n+1][m+1];

        //初始化第一行和第一列, 这里在本程序中，可以不去处理，因为默认就是0
        //将第一列设置为0
        for (int i = 0; i < v.length; i++) v[i][0] = 0;
        //将第一行设置0
        Arrays.fill(v[0], 0);


        //根据前面得到公式来动态规划处理
        //不处理第一行 i是从1开始的
        for(int i = 1; i < v.length; i++)
            for (int j = 1; j < v[0].length; j++) {//不处理第一列, j是从1开始的
                //公式
                // 因为我们程序i 是从1开始的，因此原来公式中的 w[i] 修改成 w[i-1]
                //说明:
                //因为我们的i 从1开始的， 因此公式需要调整成
                //v[i][j]=Math.max(v[i-1][j], val[i-1]+v[i-1][j-w[i-1]]);
                //v[i][j] = Math.max(v[i - 1][j], val[i - 1] + v[i - 1][j - w[i - 1]]);
                //为了记录商品存放到背包的情况，我们不能直接的使用上面的公式，需要使用if-else来体现公式
                if (w[i - 1] > j) v[i][j] = v[i - 1][j];
                else if (v[i - 1][j] < val[i - 1] + v[i - 1][j - w[i - 1]]) {
                    v[i][j] = val[i - 1] + v[i - 1][j - w[i - 1]];
                    //把当前的情况记录到path
                    path[i][j] = 1;
                } else {
                    v[i][j] = v[i - 1][j];
                }
            }

        //输出一下v 看看目前的情况
        for (int[] ints : v) {
            for (int anInt : ints)
                System.out.print(anInt==0?"0    ":(anInt+" "));
            System.out.println();
        }

        System.out.println("============================");
        //输出最后我们是放入的哪些商品
        //遍历path, 这样输出会把所有的放入情况都得到, 其实我们只需要最后的放入
//        for(int i = 0; i < path.length; i++) {
//            for(int j=0; j < path[i].length; j++) {
//                if(path[i][j] == 1) {
//                    System.out.printf("第%d个商品放入到背包\n", i);
//                }
//            }
//        }

        //动脑筋
        int i = path.length - 1; //行的最大下标
        int j = path[0].length - 1;  //列的最大下标
        HashMap<Integer, Integer> pack = new HashMap<>();
        while(i > 0 && j > 0 ) { //从path的最后开始找
            if(path[i][j] == 1) {
                //确定商品数目
                int x=i-1;
                int t=0;
                while (x>=0) x-=maxNumber[t++];
                if (!pack.containsKey(t)) pack.put(t,0);
                pack.put(t,pack.get(t)+1);
                j -= w[i-1]; //w[i-1]
            }
            i--;
        }
        //输出结果
        for (Integer key : pack.keySet()) 
            System.out.println("放了" + pack.get(key) + "个" + key + "号商品到背包中");

    }
}
```

## 约瑟夫问题

```java
public <T> void josef(ArrayList<T> list, int start, int count){
    if (start <= 0 || list==null || list.isEmpty()) return;
    int size=list.size();
    if(start > size) return;
    count=count-1;
    start=start-1;
    while (size!=0){
        int out=(start+count)%size;
        System.out.println(list.remove(out));
        start=out;
        --size;
    }
}
```

## 输出一个集合的所有子集构成的集合

```java
Set<Set<Object>> SubSet(Set<Object> org){
    Set<Set<Object>> set=new HashSet<>();
    set.add(new HashSet<>());//添加空集
    for (Object l:org){
        Set<Set<Object>> set1= new HashSet<>(set);//复制前面元素构成的集合的子集集合
        for(Set<Object> s:set1){//遍历前面元素构成的集合的子集
            Set<Object> s1= new HashSet<>(s);//复制子集
            s1.add(l);//将后面元素添加到子集
            set.add(s1);//将新的子集加入总子集
        }
    }
    return set;
}
```

[c++](../c++/c++.md)

