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

