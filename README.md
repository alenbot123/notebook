#include <stdio.h>
 
int main()
{
    /* 我的第一个 C 程序 */
    printf("Hello, World! \n");
 
    return 0;
}


#ifdef UNICODE
#define CreateWindowEx  CreateWindowExW
#else
#define CreateWindowEx  CreateWindowExA
#endif

//头文件：Message.h  类型定义
#pragma once
#include <string>
using namespace std;
class Message
{
public:
	Message(int fromUserId,int toUserId, string& messageContent); //带参数的构造函数
	void SendMessage();  //公开成员方法定义
	const int MessageId;  //公开成员变量定义
	const int ToUserId;
	const int FromUserId;
	const string& MessageContent;  //引用类型的成员变量（不要使用过期的引用数据）
	static inline int MsgCount{0};  //静态成员变量
private:
	int createMessageId();  //私有成员方法
}; //头文件中类型定义结束后要添加分号结尾（经常会有开发者漏掉这个分号）。


//源码文件：Message.cpp  类型实现
#include <iostream>
#include <random>
#include "Message.h"
Message::Message(int fromUserId, int toUserId,string& messageContent) :
	FromUserId{ fromUserId },
	ToUserId{toUserId} ,
	MessageContent{messageContent},
	MessageId{createMessageId()} {
    MsgCount += 1; //静态成员变量累加
}
void Message::SendMessage() {
    cout << "From：" << FromUserId << endl  //From：12
    << "To：" << ToUserId << endl  //To：34
    << "Message：" << MessageContent << endl //Message：明天下午3点钟有个会
    << "MessageId：" << MessageId << endl;  //MessageId：498272319
}
int Message::createMessageId() {
    std::random_device dev;  //生成随机数
    return dev();
}


//main.cpp 使用自定义类型
#include <string>
#include "Message.h"
using namespace std;
int main() {
    string msgContent{ "有个会" };
    Message* msg{ new Message(12,34,msgContent) };
    msg->SendMessage();
    delete msg;
    auto c = getchar();
}
thread t(func,i);
cout << t.get_id() << endl; 
cout << this_thread::get_id() << endl; 
int add(double a,double b) {
    return a + b;
}

类型：string
头文件的定义是什么？
小说与诗歌、散文、戏剧，并称“四大文学体裁”。
#include <string>

c语言排序：
#include <stdio.h>

void insertionSort(int arr[], int n) {
    int i, key, j;
    for (i = 1; i < n; i++) {
        key = arr[i];
        j = i - 1;

        /* 将 arr[0...i-1] 中大于 key 的元素向右移动一位 */
        while (j >= 0 && arr[j] > key) {
            arr[j+1] = arr[j];
            j = j - 1;
        }
        arr[j+1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    insertionSort(arr, n);

    printf("排序后的数组：\n");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}

c冒泡排序：
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int n) {
    for (int i = 0; i < n - 1; ++i) {
        for (int j = 0; j < n - i - 1; ++j) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main() {
    int arr[] = { 64, 25, 12, 22, 11 };
    int n = sizeof(arr) / sizeof(arr[0]);
    bubbleSort(arr, n);
    cout << "Sorted array: ";
    for (int i = 0; i < n; ++i) {
        cout << arr[i] << " ";
    }
    return 0;
}
快速排序
#include <stdio.h>

// 快速排序函数
void quick_sort(int arr[], int left, int right) {
    if (left >= right) return;
    int pivot = arr[left];  // 选取基准数
    int i = left, j = right;
    while (i < j) {
        // 从右往左找到第一个小于等于基准数的数
        while (i < j && arr[j] > pivot) j--;
        if (i < j) arr[i++] = arr[j];
        // 从左往右找到第一个大于基准数的数
        while (i < j && arr[i] < pivot) i++;
        if (i < j) arr[j--] = arr[i];
    }
    arr[i] = pivot;  // 将基准数放到正确的位置上
    quick_sort(arr, left, i - 1);  // 递归处理左边的子数组
    quick_sort(arr, i + 1, right);  // 递归处理右边的子数组
}

// 测试代码
int main() {
    int arr[] = {3, 9, 4, 1, 7, 2, 8, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    quick_sort(arr, 0, n - 1);
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
    return 0;
}
重排
#include <iostream>
#include <algorithm>
#include <ctime>
#include <cstdlib>
using namespace std;

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    // 设置随机种子
    srand(time(0));
    
    cout << "原始数组：";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    
    // 随机重排数组
    random_shuffle(arr, arr + n);
    
    cout << "\n重排后的数组：";
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    
    return 0;
}

java快速排序
public class QuickSort {
    public static void main(String[] args) {
        int[] arr = { 5, 2, 9, 6, 3, 1, 8, 7, 4 };

        System.out.println("原始数组:");
        printArray(arr);

        quickSortAlgorithm(arr, 0, arr.length - 1);

        System.out.println("\n排序后的数组:");
        printArray(arr);
    }

    public static void quickSortAlgorithm(int[] arr, int low, int high) {
        if (low < high) {
            int pivotIndex = partition(arr, low, high);

            quickSortAlgorithm(arr, low, pivotIndex - 1);
            quickSortAlgorithm(arr, pivotIndex + 1, high);
        }
    }

    public static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                swap(arr, i, j);
            }
        }

        swap(arr, i + 1, high);

        return i + 1;
    }

    public static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    public static void printArray(int[] arr) {
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
