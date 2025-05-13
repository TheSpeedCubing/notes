# Pointer
### ```*``` 
declare a pointer variable
```c
int a = 5;
int* ptr = &a;
```
dereference a pointer
```
int a2 = *ptr; // 5
```

### ```&```
obtain address
```c
int* ptr = &a;
```

### double pointer
```c 
int a = 5;   // just-a-value
int* ptr = &a;    // value a's address
int** ptr2 = &ptr; // ptr pointer's address
```

## Pointer as Method Parameters
### ```*``` (Pointer)
```c
void a(int* ptr) {
    *ptr = 10;  //dereference, modify value
}

int r = 1;
a(&r);
```
### ```**``` (Pointer of Pointer)
```c
void a(int** ptr) {
    *ptr = new int(20);  //deference, modify pointer
}

int* r = NULL;
a(&r);
```

### ```*&``` (Reference to Pointer)
```c
void a(int*& ptr) {
    ptr = new int(20);  //modify pointer without dereference it
}

int* r = NULL;
a(r);
```


# Struct
```c
Node* n = new Node;
```
```c
Node* n = malloc(sizeof(Node));
````
allocated memory in heap space.
created a pointer n pointed to the allocated space.
the object must be deleted.

```c
Node n;
```

```c
Node n = {a,b,c...};
```
allocated memory in stack space.
will be deleted out of the scope.


### Constructor
```c
struct Node {
  int value;
  Node* next;
  
  Node(int v): value(v) { // assign v to value
     //constructor
     next = NULL;
  }  
}
```