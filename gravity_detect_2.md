Affected Version:
gravity 0.8.5 1eb6d5ab98b9df4909513612a2bb9238a8304422

Vulnerability Description:
The vulnerability is a memory leak bug located at line 46 of the file /gravity/src/compiler/gravity_ircode.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

gravity download address:
https://github.com/marcobambini/gravity.git

Defect details:

1.In the file /gravity/src/compiler/gravity_ircode.c, a pointer variable named 'code' is defined at line 37, and a block of dynamic memory is allocated for this pointer variable by calling the function mem_alloc. The function mem_alloc is a macro definition that points to the function gravity_calloc, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_6.png)

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_5.png)

2.At line 19 of the gravity_calloc function, calloc function is used to allocate a block of dynamic memory and then returns it, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_7.png)

3.After the execution of the gravity_calloc function, at line 38 of the program, there is a check to determine whether the pointer 'code' has been allocated successfully. If the if statement at line 38 returns false (indicating successful allocation of dynamic memory for 'code'), the program proceeds to line 45, where mem_alloc is called again to allocate dynamic memory for 'code->list'. If the if statement at line 46 returns true (indicating failure to allocate dynamic memory for 'code->list'), the program returns NULL. Throughout this process, there is no deallocation of the dynamic memory allocated for 'code' at line 37, leading to a memory leak defect, as shown in the following figure:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_8.png)
