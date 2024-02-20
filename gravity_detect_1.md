Affected Version:
gravity 0.8.5 1eb6d5ab98b9df4909513612a2bb9238a8304422

Vulnerability Description:
The vulnerability is a memory leak bug located at line 440 of the file /gravity/src/compiler/gravity_parser.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

gravity download address:
https://github.com/marcobambini/gravity.git

Defect details:

1.In line 436 of the file gravity_parser.c located in the /gravity/src/compiler directory, a pointer variable named 'list' is defined, and a dynamic memory area is allocated for this pointer by calling the function cstring_array_create, as shown in the diagram below:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_1.png)

2.At line 29 of the cstring_array_create function, a pointer named 'r' is defined, and a dynamic memory area is allocated for this pointer using a function call to mem_alloc, which is a macro defined to point to the gravity_calloc function. Then, at line 31, this pointer is returned, as illustrated below:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_2.png)

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_5.png)

3.At line 19 of the gravity_calloc function, a dynamic memory area is allocated by calling calloc, and this allocated memory area is returned, as shown in the following diagram:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_3.png)

4.When the if statement at line 440 evaluates to true, the program returns NULL. During this process, the pointer 'list' is neither used nor freed, thereby constituting a memory leak defect, as shown in the diagram below:

![image](https://github.com/LuMingYinDetect/gravity_defects/blob/main/gravity_4.png)
