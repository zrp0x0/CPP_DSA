# S01. 연결 리스트 (Linked List)


### 1. 리스트(list)란?
- 순서를 가진 데이터의 모임(목록)
- e.g. TODO 리스트, 요일(일요일, 월요일, ..., 토요일)


### 2. 리스트의 주요 연산
- 원소의 참조, 삽입(insert), 삭제(remove), 검색(search), ...


### 3. 대표적인 리스트 구현 방법
- 배열
    - 연속된 메모리 공간
    - 원소의 삽입삭제 비효율적
    - 구현 쉬움

- 연결 리스트   
    - 임의의 메모리 공간
    - 원소의 삽입삭제 효율적
    - 구현 어려움


### 4. 연결 리스트(Linked List)란?
- 데이터와 링크로 구성된 노드(node)가 연결되어 있는 자료 구조
    - 데이터(data): 정수, 문자열, 복합 자료형 등
    - 링크(link, next): 다음 노드를 가리키는 포인터(엄밀하게 말하면 다른 노드를 가리키는 포인터)
    - 노드(node): 데이터와 링크로 이루어진 연결 리스트 구성 단위
    - ex. [Header] -> [[data][next]] -> [[data][next]] -> [[data][next]] -> NULL

    ```cpp
    struct Node
    {
        int data;
        Node* next;
    }
    ```


### 5. 연결 리스트 클래스
```cpp
struct Node
{
    int data;
    Node* next;
}

class LinkedList
{
private:
    Node* head;

public:
    LinkedList() : head(NULL) {}
    ~LinkedList();

    void push_front(int val);
    void pop_front();

    void insert(int index, Node* node); // 이건 수업 시간에 안 다룸

    void print_all();
    bool empty();
}
```


### 6. 연결 리스트 맨 앞에 노드 삽입하기
```cpp
void push_front(int val)
{
    Node* new_node = new Node {val, NULL};

    // 연결 리스트의 초기 상태 empty가 아닐 때
    if (head != NULL)
    {
        new_node->next = head;
    }
    head = new_node;
}
```


### 7. 연결 리스트 맨 앞 노드 삭제하기
```cpp
void pop_front()
{
    if (head == NULL)
        return;

    Node* delete_node = head;
    head = head->next;

    delete delete_node;
    delete_node = nullptr;
}
```


### 8. 연결 리스트 전체 데이터 출력하기
```cpp
void print_all()
{
    Node* currentNode = head;

    while (currentNode != NULL)
    {
        std::cout << currentNode->data << ", ";
        currentNode = currentNode->next;
    }
}
```


### 9. 연결 리스트 비어있는지 확인하기
```cpp
bool empty()
{
    return (head == NULL);
}
```


### 10. 연결 리스트 제거
```cpp
~LinkedList()
{
    while (!empty())
    {
        pop_front();
    }
}
```


### 11. 구현한 연결 리스트 클래스 동작 확인
```cpp
#include <iostream>

struct Node
{
    int data;
    Node* next;
};

class LinkedList
{
public:
    LinkedList() : head(NULL) {}
    ~LinkedList() 
    {
        while (!empty())
        {
            pop_front();
        }
    }

    void push_front(int val)
    {
        Node* new_node = new Node {val, NULL};

        if (head != NULL)
        {
            new_node->next = head;
        }
        head = new_node;
    }

    void pop_front()
    {
        if (head == NULL)
            return;

        Node* delete_node = head;
        head = head->next;

        delete delete_node;
        delete_node = nullptr;
    }

    void print_all()
    {
        Node* current_node = head;

        while (current_node != NULL)
        {
            std::cout << current_node->data << " ";
            current_node = current_node->next;
        }
        std::cout << std::endl;
    }

    bool empty()
    {
        return head == NULL;
    }

public:
    Node* head;
};

int main()
{
    LinkedList ll;

    ll.push_front(10);
    ll.push_front(20);
    ll.push_front(30);

    ll.print_all(); // 30 20 10

    ll.pop_front();
    ll.pop_front();

    ll.print_all(); // 10

    return 0;
}
```


### 12. 연결 리스트의 장단점
- 장점
    - 임의의 위치에 원소의 삽입/삭제가 효율적: O(1) - 이거 위치를 알고 있을때임!!
    - 크기 제한이 없음

- 단점
    - 임의의 원소 접근이 비효율적: O(N) - 이거 때문에 삭제할 위치를 찾는 과정은 비효율적임
    - 링크를 위한 여분의 공간 사용: next 포인터
    - 구현이 복잡


---
# S02. 이중 연결 리스트
