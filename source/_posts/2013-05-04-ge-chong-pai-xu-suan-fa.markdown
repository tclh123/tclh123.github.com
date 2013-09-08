---
layout: post
title: "各种排序算法"
date: 2013-05-04 15:31
comments: true
categories: Algorithm, sort
---

这篇东西其实是当时为了找实习而复习排序弄的，面试官无聊就喜欢问你个排序，如果你连插入排序跟选择排序都分不清楚的话还是别去找虐了。

##几种排序

大致按算法难度、类型从上到下排。

*算法描述都按升序排序，复杂度都指平均复杂度。*

- 冒泡排序
    
    模拟**气泡**浮上来的过程，n-1趟float，时间复杂度O( n^2 )

- 选择排序，一般指简单选择排序
    
    每次在无序区中**选择**出最大的元素，然后放到有序区跟无序区间，n-1趟，时间复杂度O( n^2 )

- 插入排序，一般指直接插入排序，还有折半插入排序、2-路插入排序、表插入排序等

    本质：元素插入到有序列。

    左边有序区，右边无序区（待排），每次将无序区最左边的元素**插入**到有序区中合适的位置（故涉及到元素的右移），n-1次，时间复杂度O( n^2 )

- 希尔排序，对直接插入排序的改进

    简单来说，就是取不同步长，进行多次插入排序，最后步长为1，就是以此直接插入排序。重点在于步长的选择，原始版本步长为n/( 2^i )，最坏复杂度O( n^2 )。现在最好的步长可以达到O( n(logn)^2 )，仅次于O(nlogn)的排序。

    [可以想象成取不同的行宽，按列进行插入排序。](http://zh.wikipedia.org/wiki/%E5%B8%8C%E5%B0%94%E6%8E%92%E5%BA%8F)

    当刚开始元素很无序的时候，步长最大，所以插入排序的元素个数很少，速度很快；当元素基本有序了，步长很小，插入排序对于有序的序列效率很高。

- 基数排序

    这篇文章的唯一一个非比较型排序算法。基数（Radix），即数的进制。之所以能够不进行比较，是因为它按数位将数分配到Radix个桶中，再顺序进行收集。

    有LSD（Least significant digital）、MSD（Most significant digital）两种方式。需要进行k(数据中最大位数)趟，每趟分配要O(n)，收集要O(radix)，所以总复杂度O(k(n+radix))。

- 归并排序，一般指2-路归并排序，还有非递归归并排序、自然归并排序等。

    本质：分治，有序列合并。

    二分需要O(logn)，合并需要O(n)，总时间复杂度O(nlogn)。需要O(n)的额外空间，用于存放合并有序列的临时结果。

- 快速排序

    本质：分治，Patition。

    难点在于Patition，要做到O(n)的时间复杂度。简单来说，就是选最左边的作为pivot，并维护值，然后两个指针，从右往左扫，从左往右扫，遇到不合适的，则换到另一边。直到两个指针相遇。

    总平均时间复杂度O(nlogn)。

- 堆排序

    本质：堆（分治）

    升序排列的话需要借助大顶堆，涉及max_heapify、sift_down两个子操作。其中sift_down类似直接插入排序中的数组右移。

    其实说白了就是二叉堆上的插入排序。

###归类

冒泡、选择、插入，都可以认为是将元素划分为有序区、无序区，都要n-1趟处理（无序区拓展到有序区），时间复杂度都是O( n^2 )。

希尔，实现起来很简单，采用最佳步长的话，复杂度可以达到O( n(logn)^2 )，仅次于O(nlogn)的排序。而且插入排序在元素基本有序的情况下时间复杂度接近O(n)。在一些情况下还是很有优势的。

基数，非比较型排序算法，类似的还有桶排序等。在数据有一定限制（比如都在0~1000间），数据量很大（比较型算法最快也要O(nlogn)）的情况下，可以考虑非比较型算法，可以O(n)完成。

归并、快速、堆排，都应用了分治思想，平均复杂度都是O(nlogn)。这也是基于比较的排序算法的极限了。

##具体实现

我希望用最简洁的代码实现算法。

因为面试一般不让写伪代码，而且是在纸上写，所以我就不用宏定义写得标准一点了。

*Ps. 我原来写swap是这样写，`inline int swap(int &x, int &y) { x^=y; y^=x; x^=y; }`，结果被坑了，why？试想x、y地址一样的话...*

``` cpp
#include <cstdio>
#include <cstring>
#include <iostream>
#include <list>
using namespace std;
inline int swap(int &x, int &y) { int t = x; x = y; y = t; }
inline int max(int x, int y) { return (x>y)? x: y; }
inline int min(int x, int y) { return (x<y)? x: y; }
#define bug(s) cout<<#s<<"="<<s<<" "

// 冒泡，O(n^2)
void bubble_sort(int *a, int n) {
    for(int k=0; k<n-1; k++) {
        for(int i = 0; i<n-1-k; i++) {
            if(a[i]>a[i+1])
                swap(a[i], a[i+1]);
        }
    }
}

// 简单选择，O(n^2)
void selection_sort(int *a, int n) {
    for(int k=0; k<n-1; k++) {
        int maxi = 0;
        for(int i=1; i<n-k; i++) {
            if(a[maxi] < a[i])
                maxi = i;
        }
        swap(a[maxi], a[n-1-k]);
    }
}

// 直接插入，O(n^2)
void insert_sort(int *a, int n) {
    for(int i=1, j; i<n; i++) {
        int t = a[i];
        for(j=i-1; j>=0 && a[j]>t; j--) a[j+1] = a[j];
        a[j+1] = t;
    }
}

// 希尔，O(n^2)
void shell_sort(int *a, int n) {
    for(int gap = n/2; gap>0; gap/=2) {
        for(int i=gap, j; i<n; i++) {
            int t = a[i];
            for(j=i-gap; j>=0 && a[j]>t; j-=gap) a[j+gap] = a[j];
            a[j+gap] = t;
        }
    }
}

// 基数，O(k*(n+r))，假设radix=10, k=5
void radix_sort(int *a, int n) {
    list<int> l[10];
    int r = 10, k = 5;
    for(int i=0, e=1; i<k; i++, e*=10) {
        for(int j=0; j<n; j++) {
            l[a[j]/e%10].push_back(a[j]);
        }
        for(int j=0, m=0; j<r; j++) {
            while(!l[j].empty()) {
                a[m++] = l[j].front();
                l[j].pop_front();
            }
        }
    }
}

// 归并，O(nlog(n))
void merge(int *a, int l, int mid, int r, int *t) {
    int i, j, c = 0;
    for(i=l, j=mid+1; i<=mid && j<=r;) {
        if(a[i]<a[j]) t[c++] = a[i++];
        else t[c++] = a[j++];
    }
    while(i<=mid) t[c++] = a[i++];
    while(j<=r) t[c++] = a[j++];
    for(c=0; c<r-l+1; c++) a[l+c] = t[c];
}
void m_sort(int *a, int l, int r, int *t) {
    if(l<r) {
        int mid = (l+r)>>1;
        m_sort(a, l, mid, t);
        m_sort(a, mid+1, r, t);
        merge(a, l, mid, r, t);
    }
}
void merge_sort(int *a, int n) {
    int *t = (int*)malloc(sizeof(int)*n);   // 统一用一个临时空间
    m_sort(a, 0, n-1, t);
    free(t);
}

// 快速排序，O(nlogn)
int patition(int *a, int l, int r) {
    int t = a[l];   //pivot
    while(l<r) {
        while(l<r && a[r]>=t) r--;
        a[l] = a[r];
        while(l<r && a[l]<=t) l++;
        a[r] = a[l];
    }
    a[l] = t;
    return l;
}
void q_sort(int *a, int l, int r) {
    if(l<r) {
        int q = patition(a, l, r);
        q_sort(a, l, q-1);
        q_sort(a, q+1, r);
    }
}
void quick_sort(int *a, int n) {
    q_sort(a, 0, n-1);
}

// 堆排序，O(nlogn)
#define lson(e) (e)<<1|1
void sift_down(int *a, int n, int i) {  // 类似直接插入排序的sift
    int t = a[i];
    for(int j=lson(i); j<n; i=j, j=lson(i)) {
        if(j+1<n && a[j]<a[j+1]) j++;   // 取较大的节点
        if(t>a[j]) break;
        a[i] = a[j];
    }
    a[i] = t;
}
void max_heapify(int *a, int n) {
    for(int i=n/2-1; i>=0; i--) {
        sift_down(a, n, i);
    }
}
void heap_sort(int *a, int n) {
    max_heapify(a, n);
    for(int i=n-1; i>=1; i--) {
        swap(a[0], a[i]);
        sift_down(a, i, 0);
    }
}

int main() {
    int a[] = {5,4,3,1,6,8,9,16,15};
    int n = sizeof(a)/sizeof(a[0]);
    // bubble_sort(a, n);
    // selection_sort(a, n);
    // insert_sort(a, n);
    // shell_sort(a, n);
    // radix_sort(a, n);
    // merge_sort(a, n);
    // quick_sort(a, n);
    heap_sort(a, n);
    for(int i=0; i<n; i++) {
        printf("%d ", a[i]);
    }
    // 1 3 4 5 6 8 9 15 16
}
```