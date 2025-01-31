---
title: 矩阵快速幂
tags:
  - 算法
  - 矩阵
  - 快速幂
categories:
  - 算法
mathjax: true
pubDate: 2022-03-28 16:00:41
---



### 引例（洛谷P3390）

#### 题目描述

给定一个$n \times n$的矩阵$A$，求$A^k$。

#### 输入格式

第一行两个整数 $n,k$ 接下来 $n$ 行，每行 $n$ 个整数，第 $i$ 行的第 $j$ 的数表示 $A_{i,j}$。

#### 输出格式

输出$A^k$

共 $n$行，每行 $n$ 个数，第 $i$ 行第 $j$ 个数表示 $(A^k)_{i,j}$，每个元素对$10^9+7$取模。

#### 输入输出样例

##### 输入 #1

```
2 1
1 1
1 1
```

##### 输出 #1

```
1 1
1 1
```

#### 数据范围

对于 $100$% 的数据：$1 \le n \le 100,0 \le k \le 10^{12}, |A_{i,j}| \le 1000$

### 完整代码

``` java
import java.io.*;

/**
 * P3390 【模板】矩阵快速幂
 */
@SuppressWarnings("all")
public class P3390 {

    private static long[][] matrix;

    private static int n;

    private static long k;

    private static final int MOD = 1000000007;

    public static void main(String[] args) throws Exception {
        n = nextInt();
        k = nextLong();
        matrix = new long[n][n];
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                matrix[i][j] = nextInt();
            }
        }
        
        long[][] ans = quickPow(k);
        for (int i = 0; i < ans.length; i++) {
            for (int j = 0; j < ans[i].length; j++) {
                pw.print(ans[i][j] + " ");
            }
            pw.println();
        }
        
        pw.flush();
    }

    private static long[][] quickPow(long k) throws Exception {
        long[][] res = new long[n][n];
        // 单位矩阵
        for (int i = 0; i < n; i++) {
            res[i][i] = 1;
        }
        while (k > 0) {
            if ((k & 1) > 0) {
                res = matrixMultiplication(res, matrix);
            }
            k >>= 1;
            matrix = matrixMultiplication(matrix, matrix);
        }
        return res;
    }

    private static long[][] matrixMultiplication(long[][] A, long[][] B) throws Exception {
        int rowA = A.length, columnA = A[0].length, rowB = B.length, columnB = B[0].length;
        if (columnA != rowB) {
            throw new Exception("第一个矩阵的列数必须等于第二个矩阵的行数！");
        }
        long[][] C = new long[rowA][columnB];
        for (int i = 0; i < rowA; i++) {
            for (int j = 0; j < columnB; j++) {
                for (int k = 0; k < columnA; k++) {
                    C[i][j] += A[i][k] * B[k][j];
                    C[i][j] %= MOD;
                }
            }
        }
        return C;
    }

    private static BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

    private static StreamTokenizer st = new StreamTokenizer(br);

    private static PrintWriter pw = new PrintWriter(new OutputStreamWriter(System.out));

    private static int nextInt() throws IOException {
        st.nextToken();
        return (int) st.nval;
    }

    private static long nextLong() throws IOException {
        st.nextToken();
        return (long) st.nval;
    }

}

```

