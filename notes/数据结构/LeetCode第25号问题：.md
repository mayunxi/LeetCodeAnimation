
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

template <class T1>
class List
{
public:
    List(){
        head = NULL;
        tail = NULL;
    }
    void push_back(Node<T1> *node)
    {
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
    void push_fornt(Node<T1> *node)
    {
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
    int size()
    {
        return length;
    }

    Node<T1> *head;
    Node<T1> *tail;
private:
    int length = 0;
};
int main(int argc, char *argv[])
{
    Node<int> node;
    List<int> linkList;

    linkList.push_back(node);
    node = new Node(2);
    linkList.push_back(node);
    node = new Node(3);
    linkList.push_back(node);

    printf("head:%d,tail:%d\n",linkList.head->data,linkList.tail->data);
    return 0;
}

