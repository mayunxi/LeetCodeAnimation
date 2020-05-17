####链表的优缺点
链表的优点如下：
* 链表能灵活地分配内存空间；
* 能在O(1)时间内删除或者添加元素，前提是该元素的前一个元素已知，当然也取决于是单链表还是双链表，在双链表中，如果已知该元素的后一个元素，同样可以在O(1)时间删除或者添加该元素。

链表的缺点：
* 不像数组那样可以通过下标迅速读取元素，每次都要从链表头开始一个一个读取;
* 查询第K个元素需要O(k)时间


```
#include <iostream>
using namespace std;

template<typename T>
class Node{
public:
    Node(T d)
    {
        data = d;
    }
    Node<T> *prev=NULL;
    Node<T> *next=NULL;
    T data;
};

template <class T>
class List
{
public:
    List(){
        head = NULL;
        tail = NULL;
    }
    void push_back(T data)
    {
        Node<T> *node = new Node<T>(data);
        if (length == 0)
        {
            head = node;
            tail = node;
        }
        else
        {
            tail->next=node;
            node->prev=tail;
            tail=node;
        }
        length++;
    }
    void push_fornt(T data)
    {
        Node<T> *node = new Node<T>(data);
        if (length == 0)
        {
            head = node;
            tail = node;
        }
        else
        {
            head->prev = node;
            node->next = head;
            head = node;
        }
    }
    Node<T> * operator[](int i)
    {
        Node<T> * current;
        current = head;
        while(i--)
        {
            current = current->next;
        }
        return current;
    }
    int size()
    {
        return length;
    }

    Node<T> *head;
    Node<T> *tail;
private:
    int length = 0;
};

int main(int argc, char *argv[])
{
    List<int> linkList;

    linkList.push_back(1);
    linkList.push_back(2);
    linkList.push_back(3);
    linkList.push_back(4);
    linkList.push_back(5);
    printf("size:%d,head:%d,tail:%d,data:%d\n",linkList.size(),linkList.head->data,linkList.tail->data,linkList[1]->data);

    int k=2;
    int cycleCnt = linkList.size() / 2;
    int lastCnt = linkList.size() % 2;

    for (int i = 1;i <= cycleCnt;i++)
    {
        for (int j = i*k-1;j >= (i-1)*k ;j--)
        {
            if (j != (i-1)*k)
            {
                linkList[j]->next = linkList[j-1];
            }
            else
            {
                if (lastCnt != 0)
                    linkList[j]->next = linkList[i*k+1];
            }

        }
    }
    printf("%d\n",linkList[1]->data);
    return 0;
}
```
