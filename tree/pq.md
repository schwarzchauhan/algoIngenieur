# __Priority Queue__


## Application
+ job scheduling 
+ prim
+ dijkstra
+ data compression - huffman
+ event driven simulation
+ selection - find kth smallest ele 

ascending priority queue - ele with smallest key has highest priority
descending priority queue - ele with largest key has highest priority


# Operations 
+ insert(key, data)
+ deleteMin()
+ getMinimum()


# Binary heap implementation

## Heap Propt 
+ value of node must be ≥ or ≤ than its child node
+ heap should be completer binary tree

### Min heap - value of the node must be ≤ its child nodes  
### Max heap - value of the node must be ≥ its child nodes  

# Max priority queue implementation

+ type = 1 , for max pq
+ type = 0, for min pq 


createHeap() : to create & return heap  

delHeap()  

parent(h,i)  :  returns index of parent of nodei, otherwise returns -1 invalid case   

leftChild() :  returns index of left child of node i, otherwise returns -1 in invalid case  

rightChild() :  returns index of right child of node i, otherwise returns -1 ininvalid case  

extractHighPriorityEle() : returns -1 if stack is empty , otherwise returns value of high priority ele  

heapify()

```
assuming that the both left & right subtree of index i satisfies the heap propt
we may slide the ele at ind  i downward if it's not consistent with its's child w.r.t. heap propt
also called percolate down ,
O(lgn), in worst case we start at root and go downward to leave , equal to height of tree which is lgn
```

ins()

del() : to delete the highest priority ele

print()

main() : driver pgm


```C++
#include<bits/stdc++.h>
using namespace std;
#define ll long long int
#define co cout<<

// assuming 0-based indexing

struct heap{
    int *a, *ind;         // array 
    int hs;             //  hs of ele in heap
    int cap;            //  maxm size of heap aintowed
    int type;          // min heap - 0 or max heap - 1
};



struct heap*  createHeap(int cap, int type){    // O(1)
    struct heap *h = (struct heap *)malloc(sizeof(struct heap));   // allocating memory
    if( h == NULL){        // ~~
        cout << " memory error ";
        return NULL;
    }

    h -> hs = 0;
    h -> cap = cap;
    h -> type = type;

    h ->  a = (int *)malloc(sizeof(int) * (h->cap) );       // allocating memory to array
    if( h -> a == NULL ){    // ~~
        cout << " memory error ";
        return NULL;
    }

    return h;
}

int parent(struct heap *h, int i){       
    return ( i <= 0 || i >= h->hs )? -1 : (i-1)/2;
}

int leftChild(struct heap *h, int i) {
    return ((2*i+1) < (h->hs)) ? (2*i+1) : -1;
}

int rightChild(struct heap *h, int i){
    return ((2*i+2) < (h->hs)) ? (2*i+2) : -1;
}

int extractHighPriorityEle(struct heap *h){
    return ( h->hs == 0 )? -1 : h->a[0];
}

void heapify(struct heap *h, int i) {
    if( i >= h->hs  || i < 0 ){
        return;
    }

    int lc = leftChild(h, i), rc = rightChild(h, i), largest = i;
    if( h->type == 0 ){
        /* code */
    }
    else {  // max priority 
        if( h->a[largest] < h->a[lc] && lc != -1 ){
            largest = lc;
        }
        if( h->a[largest] < h->a[rc] && rc != -1 ){
            largest = rc;
        }
        if( largest != i){
            swap( h->a[i], h->a[largest]);
            heapify(h, largest);
        }
    }
}


int del(struct heap *h) {   // O(lgn)
    if( h->hs == 0  /*  h->hs <=0 */){
        cout << "heap already empty"<<endl;
        return -1;
    }

    int ele = h->a[0];

    h -> a[0] = h -> a[h->hs-1];
    h -> hs   = h -> hs - 1;
    heapify(h, 0);              // new value at root node may not satisfy heap propt , hence we heapify from root

    return ele;
}

void ins(struct heap *h, int data)     // O(lgn), in worst case we r traversing heap linearly from leave to root, which is equal to the height of tree i.e. lgn
{
    if( h->type == 0){
        /* code*/
    }
    else{
        if( h -> hs == h -> cap /*  h -> hs >= h -> cap */ ) {
            /* resize */
            cout << "heap is fully occupied"<<endl;
        }
        else 
        {
            int i = h->hs;
            h -> a[i] = data;
            h -> hs  = h-> hs + 1;

            int p = parent(h , i);
            while( i > 0 && (h->a[p] <  h -> a[i])){    // alternatively while(p != -1)        // bottom up approach used
                swap( h->a[p], h->a[i] );
                i = p;
                p = parent(h, i);
            }
        }
    }
}

void print(struct heap *h){
    for (int i = 0; i < h->hs; i++){
        cout << h->a[i]<<" ";
    }cout << endl;
}

void delHeap(struct heap* h){
    if ( h == NULL)
        return;
    free( h -> a);
    free(h);
    h = NULL;
}

void buildMinHeap(struct heap *h, ll a[], ll n){
    for (ll i = 0; i < n; i++){
        h -> a[i] = a[i];
    }
    h->hs = n;

    for (int i = (n - 1)/2 ; i >= 0; i--){
        heapify(h, i);
    }
    print(h);
}


int main(){

    // #ifndef ONLINE_JUDGE
    //     freopen("input.txt", "r", stdin);
    //     freopen("output.txt", "w", stdout);
    // #endif

    // int T;
    // cin>>T;
    // for (int tc = 0; tc < T; tc++){
        struct heap *h;
        h = createHeap(50, 1);

        cout <<h->hs<<endl;
        cout <<h->cap<<endl;
        cout <<h->type<<endl;

        int data,c;
        bool u = true;

        cout <<"1)ins \t 2)del \t 3)peek \t 4)heapSize \t 5)capacity \t 6)index \t 7)print \t 8)exit"<<endl;
        while(u == true)
        {
            cout <<"Choice : ";
            cin >> c;
            if(c == 1)
            {
                cout << "enter the data : "; 
                cin>>data; 
                ins(h,data);
            }
            else if( c == 2 )
                del(h);
            else if( c == 3 )
                cout <<extractHighPriorityEle(h)<<endl;
            else if( c == 4)
                cout  << h->hs<<endl;
            else if( c == 5 )
                cout << h-> cap<<endl;
            else if(c == 6){
                cout <<"enter index : ";
                cin >> c;
                if ( c >= h->hs){
                    cout <<"invalid posn"<<endl;
                }else{
                    cout << h-> a[c]<<endl;
                }
            }
            else if( c == 7 )
                print(h);
            else
                u = false;

            cout <<"ok"<<endl;
        }
    // }

    return 0;
}

/*

Sample input

Sample output

*/
```
