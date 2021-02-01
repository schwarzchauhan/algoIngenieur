# ***QUEUE***
* FIFO ,first-in-first-out
* LILO ,last-in-last-out
* for example people standing in a queue to buy train tickets

## ⮩ Operations's
---

### enQueue
to insert element in a queue 

### deQueue
to remove element from a queue

## ⮩ Exception's
---

### Underflow 
deQueueing from a empty queue

### Overflow 
inserting in a full(memory full) queue's

## ⮩ Application
---
* used in OS to schedule jobs
* in real world , we make queue to buy ticket at a counter


## ⮩ Implementation
---
* enqueue() : to insert ele in the queue
* deque() : to remove front ele of the queue & return the value of the removed ele
* isEmpty() : returns true if the queue is empty otherwise false
* front() : returns value of the front ele of the queue

```C++
#include<bits/stdc++.h> 
using namespace std;

/*
    queue implementation using linked list
*/

struct node{
    int data;
    struct node* next;
};

struct Queue{
    struct node* front;
    struct node* rear;
};

struct Queue* create(){
    return NULL;
}

bool isEmpty(struct Queue* q){
    return q == NULL;
}

int front(struct Queue** q){
    if(isEmpty(*q)==true){
        cout<<"queue is empty";
        return -1;
    }else{
        struct Queue* h;
        h = *q;
        return h->front->data;
    }
}

void enqueue(struct Queue** q, int x){

    struct node* temp;
    temp = (struct node*)malloc(sizeof(struct node));       // allocating memory
    temp -> data = x;
    temp -> next = NULL; 

    struct Queue* h;

    if( isEmpty(*q) == true ){

        h = (struct Queue*)malloc(sizeof(struct Queue));
        h -> front = temp;
        h -> rear  = temp;

    }else{

        h   =  *q;
        struct node* tmp;
        tmp =   h -> rear;
        tmp -> next = temp;

        h -> rear = temp;

    }
    *q = h;
}

int dequeue(struct Queue** q){

    struct Queue* h;
    if( isEmpty(*q) == true ){
        cout<<"exception : underflow";
        return -1;
    }else{

        h = *q;

        struct node* tmp;
        tmp   = h   -> front;
        int x = tmp -> data;

        if(h-> front == h->rear){  // case when queue has only 1 element
            h = NULL;
        }else{
            h -> front = tmp -> next;
        }
        *q = h;
        free(tmp);
        
        return x;
    }
}

int main(){

    #ifndef ONLINE_JUDGE
        freopen("input.txt", "r", stdin);
        freopen("output.txt", "w", stdout);
    #endif

    int n, a;
    cin>>n;

    struct Queue* q;
    q = create();
    enqueue(&q, 7);
    cout<<front(&q)<<"\n";

    enqueue(&q, 5);
    cout<<front(&q)<<"\n";

    enqueue(&q, 78);
    cout<<front(&q)<<"\n";

    enqueue(&q, 6);
    cout<<front(&q)<<"\n";

    enqueue(&q, 34);
    cout<<front(&q)<<"\n";

    int d = dequeue(&q);
    cout<<front(&q)<<"\n";

    d = dequeue(&q);
    cout<<front(&q)<<"\n";

    d = dequeue(&q);
    cout<<front(&q)<<"\n";

    d = dequeue(&q);
    cout<<front(&q)<<"\n";

    d = dequeue(&q);
    cout<<front(&q)<<"\n";

    d= dequeue(&q);


    return 0;
}


/*
Sample input :- 

Sample output :- 
7
7
7
7
7
5
78
6
34
queue is empty-1
exception : underflow

*/


```




 
