# CYB-SimpleArrays
Listing 29 CYB-SimpleArrays Page 56

## 7.2 Arrays of references to objects

Arrays of objects do not exist in Java (as they _do_ exist in C++). Instead, we can create arrays of _references_ (pointers) to objects. If not initialized otherwise, all elements of such an array will initially be `null`:  

```java
public class ArrStrings {
    public static void main (String[] args) {
      String[] arr = null;
        // prints: null
      System.out.println(arr);

      arr = new String[4];
        // prints: null null null null
      for (String s : arr) System.out.print(s + " ");
      System.out.println();

      arr[0] = arr[2] = "Ala";
        // prints: Ala null Ala null
      for (String s : arr) System.out.print(s + " ");
      System.out.println();
    }
}
```

## 7.3 Multi-dimensional arrays  

Strictly speaking, there are no multi-dimensional arrays in Java. However, it is possible that elements of an array are references to arrays of some type. Therefore, after 

```java
int[][] b = { {1,2,3}, {4,5,6,7}, {11,12} };
```

the variable `b` is the reference to an array of references to arrays of `int`s. In particular, the type of `b[1]` is _reference to array of_ `int`s, in this case the array `{4,5,6,7}`. 

Expression `b.length` is 3, as there are three references to arrays in `b`, while `b[1].length` is 4, as `b[1]` is the reference to array of `int`s with four elements. 

The type `int[][]` is _reference to array of references to arrays_ of `int`s.  

Note also, that all elements of a ‘two-dimensional’ array are references to ‘normal’
arrays of the same type, but not necessarily of the same length (as shown in the above
example). Such arrays, where rows are of different lengths, are called jagged arrays
(or ‘ragged arrays’).
However, very often they do have the same length: we call such
2D arrays rectangular arrays, as we can visualize them as ‘rectangles’ of elements
(called matrices in mathematics):

```java
int[][] arr = { {  1,  2,  3,  4},
                { 11, 22, 33, 44},
                { -1, -2, -3, -4} };
```

Individual arrays (`{1,2,3,4}`, `{11,22,33,44}` and `{-1,-2,-3,-4}` in this example) are called rows of this array — they correspond to `arr[0]`, `arr[1]`, `arr[2]`. 

Elements with the same _second_ index are called **columns**: in the above example elements `arr[i][1]` where i=0, 1, 2, are the second (with index 1) column of the array (these are numbers 2, 22, -2).

In particular, the number of columns in a rectangular array may be equal to the number of rows — it is then a **square array**.

For example, the following array is a square array 4 × 4:

```java
int[][] squ = { { 1,  2,  3,   4},
                { 5,  6,  7,   8},
                { 9, 10, 11,  12},
                { 13, 14, 15, 16} };
```

For square arrays it makes sense to talk about its diagonals. The **main diagonal** (or just ‘diagonal’) consists of the elements for which the row and column indices are the same, or in other words these are elements on the diagonal going from the upper-left
corner to the lower-right one (in the example above, these are elements 1, 6, 11, 16).  

The **antidiagonal** are elements for which the sum of row and column indices is fixed and equal to `size-1`, where `size` is the number of columns (equal to the number of rows).  

In other words, these are elements on the diagonal going from the upper-right corner to the lower-left one (in the example above, these are elements 4, 7, 10, 13).

Let us consider another example:

# Listing 29 CYB-SimpleArrays/SimpleArrays.java  

```java
 
public class SimpleArrays {
    public static void main(String[] args) {

        // ================================================
        int[] a = {1,2,3};
        System.out.println("a.length = " + a.length);
        for (int i = 0; i < a.length; ++i)
            a[i] = (i+1)*(i+1);
        for (int i = 0; i < a.length; ++i)
            System.out.print(a[i]+" ");
        System.out.println('\n');

        // ================================================
        int[][] b = { {1,2,3}, {4,5,6,7,8}, {11,12} };
        System.out.println("b.length = " + b.length);
        for (int row = 0; row < b.length; ++row)
            System.out.println("b["+row+"].length = " +
                                         b[row].length);
        System.out.println();

        for (int row = 0; row < b.length; ++row) {
            for (int col = 0; col < b[row].length; ++col)
                System.out.print(b[row][col]+" ");
            System.out.println();
        }
        System.out.println('\n');

        // ================================================
        int[] c = new int[]{1,2,3}; // <- size inferred
        System.out.println("c.length = " + c.length);
        for (int i = 0; i < c.length; ++i)
            System.out.print(c[i]+" ");
        System.out.println('\n');

        // ================================================
        int[] d = new int[5];       // <- elements are 0
        System.out.println("d.length = " + d.length);
        for (int i = 0; i < d.length; ++i)
            System.out.print(d[i]+" ");
        System.out.println('\n');

        // ================================================
        int[][] e = new int[3][2];  // <- a 3x2 matrix
        System.out.println("e.length = " + e.length);
        for (int row = 0; row < e.length; ++row)
            for (int col = 0; col < e[row].length; ++col)
                e[row][col] = row+col;

        // ================================================
        int[][] f = new int[3][];
        for (int row = 0; row < f.length; ++row)
            System.out.print(f[row]+" ");
        System.out.println();

        for (int row = 0; row < f.length; ++row)
            f[row] = new int[row*row+2];

        for (int row = 0; row < f.length; ++row) {
            System.out.println("f["+row+"].length = " +
                                         f[row].length);
            for (int col = 0; col < f[row].length; ++col)
                f[row][col] = row+col;
        }
        System.out.println();

        for (int row = 0; row < f.length; ++row) {
            for (int col = 0; col < f[row].length; ++col)
                System.out.print(f[row][col]+" ");
            System.out.println();
        }
    }
}
```

Note that the array b has rows of different lengths, so, in the loop which prints its elements, we have to use, in the inner loop, `col < b[row].length`.

Note also the array `f`. It is a 2D array, that is _one-dimensional_ array of references to one-dimensional arrays. Therefore, in order to create it, we have to specify only number of its elements (that is number of ‘rows’); all these elements have initially the value `null`, and their type is _reference to an array of_ `int`s. Of course, we can later assign to them references to any arrays of integers (of any lengths).  
