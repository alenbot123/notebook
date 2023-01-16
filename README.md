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
    string msgContent{ "明天下午3点钟有个会" };
    Message* msg{ new Message(12,34,msgContent) };
    msg->SendMessage();
    delete msg;
    auto c = getchar();
}
