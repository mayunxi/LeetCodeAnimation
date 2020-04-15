
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
