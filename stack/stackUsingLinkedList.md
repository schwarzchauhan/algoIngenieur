# ***STACK*** 

FILO
---
first in last out 

⮩ `push`
---
element inserted in stack  

⮩ `pop`
---
element removed from top of stack  

⮩ Underflow
---
pop out an empty stack  

⮩ Overflow
---
push out an empty stack


⮩ Exceptions 
---
* pop on an empty stack ***throws an exception***
* push an element in a full stack ***throws an exception***

⮩ Implementation 
===
* defining a struct type *`with name node`* 
* `isEmpty()` to check if stack is *empty or not*
* `push()` to insert element in the stack, exception overflow 
* `pop()` to remove the top ele from the stack * returns the value of the ele popped, exception : underflow 
* `peek()` prints the ele on the top of the stack

```c++

#include<bits/stdc++.h> 
using namespace std;
#define ll long long int
#define co cout<<


struct node{
    int data;
    struct node* prev;     //ptr to the previous top ele of stack
};
struct node* create(){      // returns the pointer(NULL by  default) to the top ele of the newly created stack
    return NULL;
}
bool isEmpty(struct node* top){
    return top==NULL;
}
void push(struct node** top, int x ){   //pass by reference

    //allocating memory to the ptr of stuct node data type
    struct node* temp;
    temp = (struct node*)malloc(sizeof(struct node));  

    // updating the ptr top (to point to the  new top of stack)
    temp ->data = x;        
    temp -> prev = *top;    
    *top = temp;            
}
int pop(struct node** top){     //pass by reference

    int x;
    struct node *temp;

    // check if stack is already empty
    if(isEmpty(*top)){
        cout<<"underflow";
        return -1;
    }
  
    //popping the top of the stack
    temp = *top;
    x    =  temp -> data; 
    *top =  temp -> prev;
    free(temp);             //deallocating memory(to free memory space not required anymore)
    return x;

}
void peek(struct node *top){        //pass by address 
    if(top == NULL){
        cout<<"Empty Stack";
    }else{
        cout <<"ele at the  top is : " << top->data<<"\n";
    }
}
int main(){
    struct node* stk = create();   // stk is pointer to the top of the stacck
    push(&stk,8);
    peek(stk);
    push(&stk,9);
    peek(stk);
    push(&stk,5);
    peek(stk);
    push(&stk,2);
    peek(stk);
    push(&stk,10);
    peek(stk);
    cout<<"ele popped : " << pop(&stk)<<"\n";
    peek(stk);
    cout<<"ele popped : " << pop(&stk)<<"\n";
    peek(stk);
    cout<<"ele popped : " << pop(&stk)<<"\n";
    peek(stk);
    cout<<"ele popped : " << pop(&stk)<<"\n";
    peek(stk);
    cout<<"ele popped : " << pop(&stk)<<"\n";
    peek(stk);
    return 0;
}



```



