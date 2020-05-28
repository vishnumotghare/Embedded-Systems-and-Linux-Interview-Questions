# C Interview questions and answers

 
## Questions On Storage Class Specifier

### 1. What are storage class specifier?

   Storage class specifiers in C language tells the compiler where to store a variable, how to store the variable, what is the initial value of the variable and life time of the variable.
   
   **Syntax:** `storage_specifier data_type variable _name`

   Types of storage class specifier in c :
   
   There are four storage class specifier in C Language. They are,
   
   1. Automatic
   2. Register
   3. Static
   4. Extern
   
   
   Storage Specifier | Storage Place | Initial /Default value | Scope | Life Time |
   ----------------- | ------------- | ---------------------- | ----- | --------- |
     Auto | CPU Memory | garbage value | local | within block |
     static | CPU Memory | zero | local | Retains the value of the variable between different function calls. | 
     register | CPU Memory | garbage | local | within block | 
     extern | CPU Memory | zero | global | Till the end of the main program. Variable definition might be anywhere in the C program  |
     
   **Note:**
   
   * For faster access of a variable, it is better to go for register specifiers rather than auto specifiers.
   * Because, register variables are stored in register memory whereas auto variables are stored in main CPU memory.
   * Only few variables can be stored in register memory. So, we can use variables as register that are used very often in a C program.

 
### 2. What is static variable?

There are 3 main uses for the static variable.

1. If it declares within a function:
  * It retains the value between function calls.
1. If it is declared for a function name:
  * By default function is extern, so it will be visible from other files if the function declaration is as static, it is invisible for the outer files.
1. Static for global variables:
  * By default we can use the global variables from outside files If it is static global..that variable is limited to with in the file.
  
### 3. What is difference between static and extern?
 
#### Static:
  
   * The static storage class is used to declare an identifier that is a local variable either to a function or a file and that exists and   retains its value after control passes from where it was declared.
   * This storage class has a duration that is permanent.
   * A variable declared of this class retains its value from one call of the function to the next.
   * The scope is local. A variable is known only by the  function it is declared within or if declared globally in a file, it is known or seen only by the functions within that file. This storage class guarantees that declaration of the variable also initializes the variable to zero or all bits off.

#### Extern:
  
  * The extern storage class is used to declare a global variable that will be known to the functions in a file and capable of being known to all functions in a program.
  * This storage class has a duration that is permanent. Any variable of this class retains its value until changed by another assignment.
  * The scope is global.
  * A variable can be known or seen by all functions within a program.
  
  
### 4. What is difference between static local and static global variable?

#### Static global :
 * Static variable has scope only in the file in which it is declared. it can't be accessed in any other file but its value remains intact if code is running in some other file means lifetime is in complete program .

#### Static local:
 * static local variable has scope in that function in which it is declared means it can't be used in other functions in the same file also, means scope is limited to the function in which it is declared while its life time is also through out the program.

### 5. Can we declare static variable in header file?
* You can’t declare a static variable without defining it as well (this is because the storage class modifiers static and extern are mutuallyexclusive). A static variable can be defined in a header file, but this would cause each source file that included the header file to have its own private copy of the variable, which is probably not what was intended.

### 6. Can we declare main() function as static?
 * No. The C spec actually says somewhere in it  that the main function cannot be static.
The reason for this is that static means "don't let anything outside this source file use this object". The benefit is that it protects against name collisions in C when you go to link (it would be bad bad bad if you had two globals both named "is_initialized" in different files... they'd get silently merged, unless you made them static). It also allows the compiler to perform certain optimizations that it wouldn't be able to otherwise. These two reasons are why static is a nice thing to have.
Since you can't access static functions from outside the file, how would the OS be able to access the main function to start your program? That's why main can't be static.
Some compilers treat "main" specially and might silently ignore you when you declare it static.

### 7. Draw memory layout of C program?
Refer This link:   http://cinterviewquestionandanswer.blogspot.in/2014/01/memory-layout-of-c-programs.html

### 8. What is volatile variable means?
 * volatile has nothing to deal with storage class.
 * volatile just tells the compiler or force the compiler to "not to do the optimization" for that variable. so compiler would not optimize the code for that variable and reading the value from the specified location, not through interal register which holds the previous value.
 * So, by declaring variable as volatile.. it gives garrantee that you will get the latest value, which may be alterred by an external event.
 * your code may be work fine if haven't declare that variable as volatile, but there may be chance of not getting correct value sometimes, so to avoid that we should declare variable as volatile.
volatile is generally used when dealing with external events, like interrupts of hardware related pins.

`Example. reading adc values`

 * const voltile means you can not modify or alter the value of that variable in code. only external event can change the value.
controller pins are generally defines as volatile. may be by declaring variable as volatile controller will do "read by pin" not "read by latch"... this is my assumtion. may be wrong...
but still there is lots of confusion when to choose variable as volatile..
A variable should be declared volatile whenever its value could change unexpectedly. In practice, only three types of variables could change:
Memory-mapped peripheral registers
Global variables modified by an interrupt service routine
Global variables within a multi-threaded application

### 9. What does keyword const means?
 * The const qualifier explicitly declares a data object as something that cannot be changed. Its value is set at initialization. You cannot use const data objects in expressions requiring a modifiable lvalue. For example, a const data object cannot appear on the lefthand side of an assignment statement
int const volatile var

### 10. What do the following declaration means?

```c
const int a;
int const a;
const int *a;
int * const a;
int const * a const;
```

### 11. Can we use const keyword with volatile variable?

Yes. The const modifier means that this code cannot change the value
of the variable, but that does not mean that the value cannot be
changed by means outside this code. For instance, in the example  the timer structure was accessed through a volatile const pointer. The function itself did not change the value of the timer, so it was declared const. However, the value was changed by hardware on the computer, so it was declared volatile. If a variable is both const and volatile, the two modifiers can appear in either order.

### 12. What are pointers?

A pointer is a variable whose value is the address of another variable, i.e., direct address of the memory location. Like any variable or constant, you must declare a pointer before you can use it to store any variable address. The general form of a pointer variable declaration is:

`type *var-name;`

Here, type is the pointer's base type; it must be a valid C data type and var-name is the name of the pointer variable. The asterisk * you used to declare a pointer is the same asterisk that you use for multiplication. However, in this statement the asterisk is being used to designate a variable as a pointer. Following are the valid pointer declaration:
`int    *ip;`    /* pointer to an integer */
`double *dp;`    /* pointer to a double */
`float  *fp;`    /* pointer to a float */
`char   *ch`     /* pointer to a character */

The actual data type of the value of all pointers, whether integer, float, character, or otherwise, is the same, a long hexadecimal number that represents a memory address. The only difference between pointers of different data types is the data type of the variable or constant that the pointer points to.

### 13. What is dangling pointer?

A dangling pointer points to memory that has already been freed. The storage is no longer allocated. Trying to access it might cause a Segmentation fault.

Common way to end up with a dangling pointer:

```c
char* func()
{
   char str[10];
   strcpy(str,"Hello!");
   return(str); 
}
```

//returned pointer points to str which has gone out of scope. 
You are returning an address which was a local variable, which would have gone out of scope by the time control was returned to the calling function. (Undefined behaviour)
Another common dangling pointer example is an access of a memory location via pointer, after free has been explicitly called on that memory.

```c
int *c = malloc(sizeof(int));
free(c);
*c = 3; //writing to freed location!
```

### 14. What is NULL pointer?

Null pointer is special reserved value of a pointer. A pointer of any type has such a reserved value. Formally, each specific pointer type (int*, char*) has its own dedicated null-pointer value. Conceptually, when a pointer has that null value it is not pointing anywhere.

### 15. What is void Pointer?

Void pointer or generic pointer is a special type of pointer that can be pointed at objects of any data type. A void pointer is declared like a normal pointer, using the void keyword as the pointer’s type.

Pointers defined using specific data type cannot hold the address of the some other type of variable i.e., it is incorrect in C++ to assign the address of an integer variable to a pointer of type float.

Example:
```
float *f; //pointer of type float
int i;  //integer variable
f = &i; //compilation error
```
The above problem can be solved by general purpose pointer called void pointer.

Void pointer can be declared as follows:

`void *v ` // defines a pointer of type void

The pointer defined in this manner do not have any type associated with them and can hold the address of any type of variable.

Example:

```
void *v;
int *i;
int ivar;
char chvar;
float fvar;
v = &ivar; // valid
v = &chvar; //valid
v = &fvar; // valid
i = &ivar; //valid
i = &chvar; //invalid
i = &fvar; //invalid  
```
5. What is memory leakage? How can we avoid it?
Ans :
Memory leak occurs when programmers create a memory in heap and forget to delete it.
Memory leaks are particularly serious issues for programs like daemons and servers which by definition never terminate.
/* Function with memory leak */
#include 

void f()
{
   int *ptr = (int *) malloc(sizeof(int));

   /* Do some work */

   return; /* Return without freeing ptr*/
}
To avoid memory leaks, memory allocated on heap should always be freed when no longer needed.
/* Function without memory leak */
#include ;

void f()
{
   int *ptr = (int *) malloc(sizeof(int));

   /* Do some work */

   free(ptr);
   return;
}

### 16. What is the size of pointer in 32 bit machine?

Sizeof  of pointer in 32 bit machine is always 4 bytes.

### 17. Write a program to find weather machine is 32 bit or 64 bit?

```c
int main()
{
    int *p = NULL;
    if(sizeof(p) == 4)
        printf("Machine is 32 bit\n");
    else
        printf("Machine is 64 bit\n");
    return 0;
}
```

### 18. What is array?

In C programming, one of the frequently arising problem is to handle similar types of data. For example: If the user want to store marks of 100 students. This can be done by creating 100 variable individually but, this process is rather tedious and impracticable. These type of problem can be handled in C programming using arrays.
An array is a sequence of data item of homogeneous value(same type).

### 19. What is difference between array and pointer?

An array is an array and a pointer is a pointer, but in most cases array names are converted to pointers.
Here is an array:
`int a[7]`
a contains space for seven integers, and you can put a value in one of them with an assignment, like this:
`a[3] = 9;`
Here is a pointer:
`int *p;`
p doesn't contain any spaces for integers, but it can point to a space for an integer. We can for example set it to point to one of the places in the array a, such as the first one:
`p = &a[0];`
What can be confusing is that you can also write this:
`p = a;`
This does not copy the contents of the array a into the pointer p (whatever that would mean). Instead, the array name a is converted to a pointer to its first element. So that assignment does the same as the previous one.
Now you can use p in a similar way to an array:
`p[3] = 17;`
The reason that this works is that the array dereferencing operator in C, "[ ]", is defined in terms of pointers. x[y] means: start with the pointer x, step y elements forward after what the pointer points to, and then take whatever is there. Using pointer arithmetic syntax, x[y] can also be written as *(x+y).
For this to work with a normal array, such as our a, the name a in a[3] must first be converted to a pointer (to the first element in a). Then we step 3 elements forward, and take whatever is there. In other words: take the element at position 3 in the array. (Which is the fourth element in the array, since the first one is numbered 0.)
So, in summary, array names in a C program are (in most cases) converted to pointers. One exception is when we use the sizeof operator on an array. If a was converted to a pointer in this contest, sizeof(a) would give the size of a pointer and not of the actual array, which would be rather useless, so in that case a means the array itself.

### 20. Can we increment the base address of array? Justify your answer.
 
No, Because once we initialize the array variable, the pointer points base address only & it's fixed  and constant pointer.

### 21.  What is the output of program ?
int a[5] = {1,2,3,4,5};
int *ptr = (int*) (&a +1);
int *ptr = (int*) (a+1); 

you see, for your program above, a and &a will have the same numerical value,and I believe that's where your whole confusion lies.You may wonder that if they are the same,the following should give the next address after a in both cases,going by pointer arithmetic:

`(&a+1) and (a+1)`

But it's not so!!Base address of an array (a here) and Address of an array are not same! a and &a might be same numerically ,but they are not the same type. a is of type int* while &a is of type int (*)[5],ie , &a is a pointer to (address of ) and array of size 5.But a as you know is the address of the first element of the array.Numerically they are the same as you can see from the illustration using ^ below.
But when you increment these two pointers/addresses, ie as (a+1) and (&a+1), the arithmetic is totally different.While in the first case it "jumps" to the address of the next element in the array, in the latter case it jumps by 5 elements as that's what the size of an array of 5 elements.
 

### 22. What is output of the program?

```c
int main()
{
 int arr[10];
 int *ptr = arr;
 ptr++;
 arr++;
 return 0;
}
```
  
The statement `arr++` will give you lvalue error. Because hear you are trying to increment base address of array and by default base address of array is constant pointer(constant value) so,
`arr  =  arr+1;`
i.e according to rule on LHS of assignment operator there always should be lvalue i.e variable not constant.

### 23. What is string?

The string in C programming language is actually a one-dimensional array of characters which is terminated by a null character '\0'. Thus a null-terminated string contains the characters that comprise the string followed by a null.

### 24. What is difference between these two,

char ptr[] = "string";
char *ptr = "string";

The two declarations are not the same.
First one is the array of character i.e. string and second one is the string literals.
char ptr[] = "string"; declares a char array of size 7 and initializes it with the characters s ,t,r,i,n,g and \0. You are allowed to modify the contents of this array.
char *ptr = "string"; declares ptr as a char pointer and initializes it with address of string literal "string" which is read-only. Modifying a string literal is an undefined behavior. What you saw(seg fault) is one manifestation of the undefined behavior.

### 25. Write a program to find size of variable without using sizeof operator?

```c
#define sizeof(var)     ( (char*)(&var+1) - (char*) (&var))
int main()
{
    int val;
    printf("size of = %d\n", SIZEOF(val));
    return 0;
}
```

### 26. Write a program to find sizeof structure without using size of operator?

```c
#define SIZEOF(var)     ( (char*)(&var+1) - (char*) (&var))
int main()
{
 struct s {
  int a;
  char b;
  int c;
 };
 struct s obj[1];
 
 printf("size of = %ld\n", SIZEOF(obj));
 
 return 0;
}
```

### 27. What is the output of following program?

```c
int main()
{
  char str[] = "vishnu";
  printf("%d %d\n",sizeof(str),strlen(str));
}
```
Ans:
7 6

Here char str[] = " 'v'. 'i' ,'s','h','n',u','\0' ";

so sizeof operator always count null character whereas strlen skip null character.

### 28. Write a program to implement strlen(), strcpy(),strncpy(), strrev(),strcmp() function"?

#### 1. strlen:

```c
int my_strlen(const char * str)
{
    int count;
    while(* str != '\0') {
        count++;
        str++;
    }
    return 0;
}
```

#### 2. strcpy:

```c
void my_strcpy(char * dest, const char* src)
{
    while(* src != '\0') {
        *dest = *src;
        dest++;
        src++;
    }
    *dest = '\0';
}
```

### 3. strrev:

```c
void my_strrev(char *str,size)
{
    int i;
    char temp;
    for(i=0;i<=size/2;i++) {
        temp = str[i];
        str[i] = str[size-i];
        str[size-i] = temp;
    }
}
int main()
{
    char str[10] = "vishnu";
    int len;
    len = strlen(str);
    my_strrev(str,len-1);
    printf("strrev = %s\n",str);
    return 0;
}
```

#### 4. strcmp :

```c
void my_strcmp(char * dest, const char* src)
{
     while(*str != '\0' && *dest != '\0') {
        str++;
        dest++;
    }
    return (*src - *dest);
}

int main()
{
    char str[10];
    char dest[10];
    int i;
    i = my_strcmp(dest,src);
    if(i == 0 )
        printf("strings are equal\n");
    if(i < 0)
        printf(" string1 is less than string2\n");
    if(i > 0)
        printf("string2 is greter than string1\n");
    return 0;
} 
```

#### 5. strncpy

```c
void my_strncpy(char * dest, const char* src,int n)
{
    while(*src != '\0' && n != 0) {
        *dest = *src;
        dest++;
        src++;
        n--;
    }
    while(n) {
        *dest = '\0';
        n--;
    }
}
```
