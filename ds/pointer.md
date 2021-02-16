

# Pass by value & Pass by reference

```C++
#include<bits/stdc++.h>
using namespace std;
#define ll long long int
#define co cout<<


void fn1 (int *a ){      //   pass by reference
    *a = 9;
}
void fn2 (int b ){       //   pass by value
    b = 9;
}
int main(){

    // #ifndef ONLINE_JUDGE
    //     freopen("input.txt", "r", stdin);
    //     freopen("output.txt", "w", stdout);
    // #endif

    // int T;
    // cin>>T;
    // for (int tc = 0; tc < T; tc++){

        int a = 89;
        cout <<a<<endl;
        fn1(&a);             // pass by reference
        cout <<a<<endl;

        int b = 70;
        cout <<b<<endl; 
        fn2(b);             // pass by value
        cout <<b<<endl; 
    
    // }

    return 0;
}
```

![passBy*Illustration](passByValueReference.jpg)


# Memory Allocation / Deallocation basics 
```C++
    free(ptr); // to deallocate the memory assigned to the ptr

    int *a;
    a = (int *)malloc(sizeof(int) * n);     // to allocate memory to ptr to an array of size n

    struct node *h;
    h = (struct node*)malloc(sizeof(struct node));      // to allocate memory to an ptr(*h) pointing to ele of struct node type
```


# struct
+  user can use struct to make their own data type
```C++

struct student{
    int rollno;
    char grade;
    int age;
};

/*
now if we make ptr of struct student type 
then we can easily access its all attributes
*/

struct student *ram;

ram = (struct student *)malloc(sizeof(struct student));     // allocating memory to store value  of data types(int,chr,int) mentioned, 

ram -> rollno = 89;
ram -> grade = 'B';
ram -> age = 14;

free(ram);      // deallocate all memory space for student ram, i.e. delete everydata related to ram
```

Node in Complete Binary Tree
```C++
struct node{
    ll data;
    struct node *lc, *rc;
};

struct node* createNode(ll data){
    struct node* newNode;

    newNode = (struct node*)malloc(sizeof(struct node));

    newNode -> data = data;
    newNode -> lc   = NULL;
    newNode -> rc   = NULL;

    return newNode;
}
```