# Linked List

+ we can grow or shrink size 
+ last node points to NULL 
+ each node points to its next node

| Linked List | Array |
| ---         |  ---  |
| elements access in worst case O(n), hence **access time is more** | elements **can be accessed in constant time** O(1)  |
| memory *allocated only when element is inserted* | *memory needs to preallocated*, i.e. **fixed size** |
| hence **memory saved** | hence **memory wasted** |

## __Dynamic Array__

+ growable & shrinkable
+ size is doubled when no of ele 🠅es to more than half the size
+ size is halved  when no of ele 🠇es to less than half the size


## __Implementation__
```C++
#include<bits/stdc++.h>
using namespace std;
#define ll long long int
#define co cout<<


/*
    head " pts to the first ele in the linked list
    temp, prev : temporary variable 
    assuming 1-based indexing
*/


struct node{
    int data;
    struct node*  next;         // *next points to next node,(pts to NULL in case their is no next ele) 
};


struct node* createList()
{
    return NULL;
}

// O(n) for traversing linked list & returns total no of ele in the list
// space complexity - O(1) for creating tempory variable
int size(struct node* head)
{
    if(head == NULL){
        cout << "list is empty"<<endl;
        return 0;
    }
    struct node* temp = head;
    int l = 0;
    while(temp != NULL)
    {
        //cout<<temp->data<<" ";
        l++;
        temp = temp -> next;
    }
    //cout<<endl;
    return l;
}

void print(struct node *head)
{
    if(head == NULL){
        cout << "list is empty"<<endl;
        return;
    }
    struct node* temp = head;
    while(temp != NULL)
    {
        cout<<temp->data<<" ";
        temp = temp -> next;
    }
    cout<<endl;
}


//to insert a node at position p
// O(n) in worst case when we r inserting at the end
//O(1) - space complexity to create temporary variable
void insert(struct node **head, int value, int p) // pass by reference , hence we used double pointer
{
    int length = size(*head);

    if(p < 1 || p > length+1)
    {
        cout<<"invalid position"<<endl;
        return;
    } 

    // creating new node
    struct node* newNode;
    newNode = (struct node*)malloc(sizeof(struct node));
    newNode -> data = value;

    if(p == 1 )                     // we need to insert new node __at beginning__ & update head
    {
        newNode -> next = *head;
        *head = newNode;
    }
    else if( p == length +1 )       // 1. we need to insert new node __at the end__ & 2. update next ptr of last node(currently) to pt to the newNode 
    {
        
        struct node* temp;
        temp = *head;
        while(temp -> next != NULL)  // loop to traverse to last ele of the linked list
        {
            temp = temp -> next;
        }
        newNode -> next = NULL;
        temp    -> next = newNode;
    }
    else                // we need to insert new node somewhere inside the linked list
    {
        struct node* temp;
        temp = *head;

        
        for (int i = 1; i <= p-2; i++)  //loop to reach (p-1)th position
        {
            temp = temp -> next;
        }

        newNode -> next = temp -> next;
        temp    -> next = newNode;
    }
}


// to delete a node at postiton p
void del(struct node** head, int p)     // pass by reference , hence we used double pointer
{
    int length = size(*head);

    if(p < 1 || p > length)
    {
        cout<<"invalid position"<<endl;
        return;
    } 

    if(p ==1 )      //delete 1st node
    {
        struct node* temp;
        temp = *head;

        *head = temp ->next;    //updating head
        free(temp);             //deallocating memory to free space
    }
    else if( p == length )  //delete last node
    {
        struct node *prev, *temp;
        prev = *head;
        temp = prev -> next;

            for(int i = 1; i<=p-2; i++)
            {
                prev = temp;
                temp = temp->next;
            }

        /*
            alternatively
            if( p != 2)
            {
                while(temp -> next != NULL)
                {
                    prev = temp;
                    temp = temp -> next;
                }
            }
        */

        // now our temp node is at tail of linked list ,, prev node is located previous to tail node
        prev -> next = NULL;
        free(temp);
    }
    else            // delete a node present intermdiate linked list
    {
        struct node *prev, *temp;
        prev = *head;
        temp = prev -> next;

        for(int i = 1; i<=p-2; i++)
        {
            prev = temp;
            temp = temp->next;
        }

        prev -> next = temp -> next;
        free(temp);
    }
}

void deleteList(struct node **head)
{
    struct node *temp;
    temp = *head;

    while((*head) != NULL )
    {
        *head = (*head) -> next;    // don't use *head = *head -> next;(precedence issue)
        //cout << temp ->data <<" ";
        free(temp);
        temp = *head;
    }

}


int main(){

    // #ifndef ONLINE_JUDGE
    //     freopen("input.txt", "r", stdin);
    //     freopen("output.txt", "w", stdout);
    // #endif

    // ll T;
    // cin>>T;
    // for (ll tc = 0; tc < T; tc++){
        struct node *h;
        h = createList();
        int choice, d, p ;
        while(true)
        {
            cout <<"enter choice 1) insert 2) delete 3) deleteLinkedList 4) exit ~~~ ";
            cin>>choice;
            switch(choice)
            {
                case 1 :    cout <<"enter <data> <position> : ";
                            cin>> d >>p;
                            insert(&h, d, p);
                            print(h);
                        break;
                case 2 :    cout <<"enter <position> : ";
                            cin >>p;
                            del(&h, p);
                            print(h);
                        break;

                case 3 :    deleteList(&h);
                            print(h);
                        break;
                case 4 :    print(h);
                            cout << "breaking out of pgm "<<endl;
                        break;
                default : cout <<"invalid choice"<<endl;
                        break;
            }
            if(choice == 4)
            {
                break;
            }
        }

    // }

    return 0;
}

/*

Sample input 

Sample output 

*/
```


