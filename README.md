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
