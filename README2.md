# 基本类型与控制流

## Question 1
1 == True 不能通过编译，在Java中True未定义。
1 == true 不能通过编译，int类型和bool类型无法直接比较。
0 == false 不能通过编译，int类型和bool类型无法直接比较。
2 + "ab" 可以，表达式类型为String,表达式的值为"2ab",原因是int类型的2会被转成字符串类型，再进行拼接。
2.3 + "ab" 可以，表达式类型为String,表达式的值为"2.3ab",原因是int类型的2会被转成字符串类型，再进行拼接。
2 + 'a' 可以，表达式类型为int,表达式的值为99,原因是'a'会把char转成int类型进行相加。
2 * "ab" 不能，*无法用于int和String之间的运算。
2 * 'a' 可以，表达式类型为int,表达式的值为194,原因是'a'会把char转成int类型进行相乘。
1 + 1.0 可以，表达式类型为double,表达式的值为2.0，int类型的1会提升成为double类型的1.0进行运算。
1/3 可以，表达式类型为int,表达式的值为0，int除int，结果还是int，会舍去小数部分。
1.0/3，可以，表达式类型是double,表达式的值为0.3333333333333333,原因1.0为double,运算结果也为double。

## Question 2
System.out.println(a); 2147483647 正常输出。
System.out.println(a + 1); -2147483648 加一发生溢出。
System.out.println(2 - a); -2147483645正常输出。
System.out.println(-2 - a); 2147483647 发生溢出，二进制计算后得到该结果。
System.out.println(2 * a); -2 发生溢出，二进制计算后得到该结果。
System.out.println(4 * a); -4 发生溢出，二进制计算后得到该结果。

## Question 3
false 因为Math.sqrt()返回的是近似值，两个近似值相乘的结果由于double的精度限制和2不相等。

## Question 4
```java
public class a{
    public static void main(String[] args){
        double x1=Double.parseDouble(args[0]);
        double y1=Double.parseDouble(args[1]);
        double x2=Double.parseDouble(args[2]);
        double y2=Double.parseDouble(args[3]);
        double dx=x2-x1;
        double dy=y2-y1;
        double distance=Math.sqrt(dx*dx+dy*dy);
        System.out.println(distance);
    }
}
```

## Question 5
```java
public class a{
    public static void main(String[] args){
        for(int i=0;i<=11;i++){
            int x=(int)Math.pow(2,i);
            double a= Math.log(x)/Math.log(2);
            double b= x*a;
            double c= x*x;
            double d= x*x*x;
            System.out.println("当数字为"+x+"时");
            System.out.println("logx的值为"+a);
            System.out.println("xlogx的值为"+b);
            System.out.println("x2的值为"+c);
            System.out.println("x3的值为"+d);
        }
    }
}
```

## Question 6
```java
import java.util.Scanner;
public class Sqrt{
    public static void main(String[] args){
       Scanner sc=new Scanner(System.in);
       System.out.print("请输入一个1~2的数");
       double num=sc.nextDouble();
       double eps=1e-10;
       double x=1.0;
       while(Math.abs(x*x-num)>eps){
            x=0.5*(x+num/x);
       }
       System.out.println(x);
    }
}
```

## Question 7
```java
public class Mid{
    public static void main(String[] args){
        if(args.length !=5){
            System.out.println("请输入五个参数：");
            return;
        }
        int[] nums= new int[5];
        for(int i=0;i<5;i++){
            nums[i]=Integer.parseInt(args[i]);
        }
        for(int i=0;i<5;i++){
            for(int j=i+1;j<5;j++){
                if(nums[j]>nums[i]){
                    int temp=nums[i];
                    nums[i]=nums[j];
                    nums[j]=temp;
                }
            }
        }
        System.out.println(nums[2]);
    }
}
```

## Question 8
false 因为==比较的是地址是否相同，而a,b是两个数组，地址不同，所以不相同。

## Question 9
```java
import java.util.Scanner;
public class Had{
    public static void main(String args[]){
        Scanner sc=new Scanner(System.in);
        System.out.print("请输入一个数");
        int num=sc.nextInt();
        int[][] result=get(num);
        printhad(result);
    }
    public static int[][] get(int n){
        if(n==1){
            return new int[][]{{1}};
        }
        int[][] prev=get(n-1);
        int size=prev.length;
        int newsize = size*2;
        int [][] p=new int[newsize][newsize];
        for(int i=0;i<size;i++){
            for(int j=0;j<size;j++){
                p[i][j]=prev[i][j];
                p[i][j+size]=prev[i][j];
                p[i+size][j]=prev[i][j];
                p[i+size][j+size]=1-prev[i][j];
            }
        }
        return p;
    }
    public static void printhad(int[][] p){
        for(int []row: p){
            for(int num: row){
                System.out.print(num+" ");
            }
            System.out.println();
        }
    }
}
```

## Question 10
```java
import java.util.Random;
import java.util.Scanner;

public class Rumor {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入总人数（包含Alice）：");
        int totalPeople = scanner.nextInt();
        System.out.print("请输入模拟次数：");
        int simulations = scanner.nextInt();
        scanner.close();

        int successCount = 0;
        long totalHeardCount = 0;
        Random random = new Random();

        for (int i = 0; i < simulations; i++) {
            boolean[] heard = new boolean[totalPeople];
            heard[1] = true; 
            int current = 1; 
            int heardCount = 1;
            while (true) {
                int nextPerson;
                do {
                    nextPerson = random.nextInt(totalPeople);
                } while (nextPerson == current || nextPerson == 0);
                if (heard[nextPerson]) {
                    break; 
                }
                heard[nextPerson] = true;
                heardCount++;
                current = nextPerson;
            }
            boolean allKnow = true;
            for (int j = 1; j < totalPeople; j++) {
                if (!heard[j]) {
                    allKnow = false;
                    break;
                }
            }
            if (allKnow) successCount++;
            totalHeardCount += heardCount;
        }
        double probability = (double) successCount / simulations;
        double expectedCount = (double) totalHeardCount / simulations;
        System.out.printf("所有人（除Alice）都知道谣言的概率：%.4f%n", probability);
        System.out.printf("听到谣言人数的期望值：%.4f%n", expectedCount);
    }
}
```

## Question 11
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Permu {
    public static List<List<Integer>> func(int n) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), new boolean[n + 1], n);
        return result;
    }

    private static void backtrack(List<List<Integer>> result, List<Integer> current, boolean[] used, int n) {
        if (current.size() == n) {
            result.add(new ArrayList<>(current));
            return;
        }
        for (int i = 1; i <= n; i++) {
            if (!used[i]) {
                used[i] = true;
                current.add(i);
                backtrack(result, current, used, n);
                used[i] = false;
                current.remove(current.size() - 1);
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入整数N：");
        int N = scanner.nextInt();
        scanner.close();

        List<List<Integer>> permutations = func(N);
        
        System.out.println("1~" + N + "的所有排列：");
        for (List<Integer> perm : permutations) {
            System.out.println(perm);
        }
    }
}
```

## Question 12
```java
import java.util.Scanner;
public class Inverse{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入置换的长度n:");
        int n=sc.nextInt();
        int[] s = new int [n];
        System.out.println("请输入1~n的排列:");
        for(int i=0;i < n;i++){
            s[i]=sc.nextInt();
        }
        int[] inverse=new int[n];
        for(int i=0;i<n;i++){
            inverse[s[i]-1]=i+1;
        }
        for(int i=0;i<n;i++){
            System.out.print(inverse[i]);
            if(i<n-1){
                System.out.print(", ");
            }
        }
        sc.close();
    }
}
```

## Question 13
```java
import java.util.Scanner;
public class Queen{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        System.out.print("请输入棋盘的大小N");
        int n=sc.nextInt();
        int[] perm = new int[n];
        System.out.println("请输入1~N的排列：");
        for(int i=0;i<n;i++){
            perm[i]=sc.nextInt();
        }
        boolean a=true;
        for(int i=0;i<n && a;i++){
            for(int j=i+1;j<n;j++){
                if(Math.abs(i-j)==Math.abs(perm[i]-perm[j])){
                    a=false;
                    break;
                }
            }
        }
        if(a){
            System.out.println("该棋盘是安全的");
        }
        else{
            System.out.println("该棋盘是不安全的");
        }
    }
}
```

## Question 14
```java
 import java.util.Scanner;
public class Spiral{
    public static int[][] func(int n) {
        int[][] matrix = new int[n][n];
        int num = 1;
        int top = 0, bottom = n - 1;
        int left = 0, right = n - 1;

        while (num <= n * n) {
            for (int i = left; i <= right; i++) matrix[top][i] = num++;
            top++;
            for (int i = top; i <= bottom; i++) matrix[i][right] = num++;
            right--;

            if (top <= bottom) {
                for (int i = right; i >= left; i--) matrix[bottom][i] = num++;
                bottom--;
            }

            if (left <= right) {
                for (int i = bottom; i >= top; i--) matrix[i][left] = num++;
                left++;
            }
        }
        return matrix;
    }

    public static void printMatrix(int[][] matrix) {
        for (int[] row : matrix) {
            for (int num : row) {
                System.out.print(num + " "); // 仅用空格分隔
            }
            System.out.println();
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("请输入 N: ");
        int n = scanner.nextInt();
        
        if (n > 0) {
            printMatrix(func(n));
        }
        scanner.close();
    }
}
```

## Question 15
```java
public class Statistic{
    public static double max(double[] a) {
        double maxVal = a[0];
        for (double num : a) {
            if (num > maxVal) maxVal = num;
        }
        return maxVal;
    }

    public static double min(double[] a) {
        double minVal = a[0];
        for (double num : a) {
            if (num < minVal) minVal = num;
        }
        return minVal;
    }


    public static double mean(double[] a) {
        double sum = 0;
        for (double num : a) sum += num;
        return sum / a.length;
    }

    public static double variance(double[] a){
        double avg = mean(a);
        double sum=0;
        for(double num: a)
            sum+=Math.pow(num-avg, 2);
        return sum / a.length;
    }

    public static double select(double[] a, int k){
        double[] sorted = a.clone();
        java.util.Arrays.sort(sorted);
        return sorted[sorted.length - k];
    }

    public static int[] histogram(double[] a){
        int num = a.length;
        int k=1;
        int[] c= new int [num];
        int[] b= new int [num];
        for(int i=0;i<num;i++){
            if(c[i]==1){
                continue;
            }
            int[] d=new int[num];
            int p=0;
            for(int j=i+1;j<num;j++){
                if(a[j]==a[i]){
                    c[j]=1;
                    k++;
                    d[p]=j;
                    p++;
                }
            }
            b[i]=k;
            for(int q=0;q<=p;q++){
                int h=d[q];
                b[h]=k;
            }
            k=1;
            d=null;
        }
        c=null;
        return b;
    }
}
```

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class Compute {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new FileReader(args[0]));
        double[] a = new double[1000];
        int n = 0;
        String line;

        while ((line = br.readLine()) != null) {
            a[n++] = Double.parseDouble(line.trim());
        }
        br.close();

        double[] data = new double[n];
        for (int i = 0; i < n; i++) data[i] = a[i];

        double mean = Statistic.mean(data);
        double var = Statistic.variance(data);
        double std = Math.sqrt(var);
        double median = Statistic.select(data, (data.length + 1) / 2);
        int[] hist = Statistic.histogram(data);

        int mode = 0;
        for(int i=0;i<hist.length;i++){
            if(a[0]<a[i]){
                a[0]=a[i];
                mode=i;
            }
        }
        double mode1=data[mode];

        // 最接近均值
        double close = data[0];
        double minD = Math.abs(data[0] - mean);
        for (double v : data) {
            double d = Math.abs(v - mean);
            if (d < minD) {
                minD = d;
                close = v;
            }
        }

        // 范围统计
        int c1 = 0, c2 = 0, c3 = 0;
        for (double v : data) {
            double d = Math.abs(v - mean);
            if (d < std) c1++;
            if (d < 2 * std) c2++;
            if (d < 3 * std) c3++;
        }

        System.out.println("均值：" + mean);
        System.out.println("中位数：" + median);
        System.out.println("众数：" + mode1);
        System.out.println("最接近均值：" + close);
        System.out.println("<1倍标准差：" + c1);
        System.out.println("<2倍标准差：" + c2);
        System.out.println("<3倍标准差：" + c3);
    }
}
```

## 补充实验
```java
import java.io.*;
import java.util.ArrayList;
public class Main {
    public static void main(String[] args) {
        FileIO.writeStringToFile("《老人与海》这本小说是根据真人真事写的。第一次世界大战结束后，海明威移居古巴，认识了老渔民格雷", "test.txt", false);
        FileIO.writeStringToFile("1930年，海明威乘的船在暴风雨中沉没，富恩特斯搭救了他。从此，海明威与富恩特斯结下了深厚的友谊。", "test.txt", true);
        FileIO.writeStringToFile("The novel The Old Man and the Sea is based on a real story. After the end of World War I in 1930,", "test.txt", true);
        FileIO.writeStringToFile("Hemingway was rescued by Fuentes when his boat sank in a storm. From then on,", "test.txt", true);

        char ch = FileIO.getCharFromFile("test.txt", 5);
        System.out.println("第5个字符是：" + ch);

        String line3 = FileIO.getLineFromFile("test.txt", 3);
        System.out.println("第3行内容是：" + line3);

        List<String> allLines = FileIO.getAllLinesFromFile("test.txt");
        System.out.println("所有行：");
        for (int i = 0; i < allLines.size(); i++) {
            System.out.println((i + 1) + ": " + allLines.get(i));
        }
    }
}
```


## 补充git实验
！[](1.jpg)

! [](2.jpg)