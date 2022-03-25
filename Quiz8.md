# Quiz 8: Threads and Concurrency

### Question 1  
1. Select the parts that are shared among threads (in the same process):  
    - [ ] register values  
    - [x] heap data  
    - [x] code segment  
    - [ ] call stack  
  
   
### Question 2  
2. In the race simulation homework of chapter 26, program loop.s will never have data race/race condition.  
    - [x] True
    - [ ] False


### Question 3  
3. We have two threads running the program "looping-race-nolock.s" (see in homework of chapter 26).
   The thread trace can be seen below:
```
         Thread 0                Thread 1
    1000 mov 2000, %ax
------ Interrupt ------  ------ Interrupt ------
                            1000 mov 2000, %ax
------ Interrupt ------  ------ Interrupt ------
    1001 add $1, %ax
    1002 mov %ax, 2000
------ Interrupt ------  ------ Interrupt ------
                            1001 add $1, %ax
------ Interrupt ------  ------ Interrupt ------
    1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
                            1002 mov %ax, 2000
                            1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
   1004 test $0, %bx
   1005 jgt .top
   1000 mov 2000, %ax
   1001 add $1, %ax
------ Interrupt ------  ------ Interrupt ------
                            1004 test $0, %bx
                            1005 jgt .top
                            1000 mov 2000, %ax
                            1001 add $1, %ax
------ Interrupt ------  ------ Interrupt ------
   1002 mov %ax, 2000
   1003 sub  $1, %bx
   1004 test $0, %bx
   1005 jgt .top
------ Interrupt ------  ------ Interrupt ------
                            1002 mov %ax, 2000
------ Interrupt ------  ------ Interrupt ------
   1006 halt
----- Halt;Switch -----  ----- Halt;Switch -----
                            1003 sub  $1, %bx
                            1004 test $0, %bx
------ Interrupt ------  ------ Interrupt ------
                            1005 jgt .top
                            1000 mov 2000, %ax
------ Interrupt ------  ------ Interrupt ------
                            1001 add $1, %ax
------ Interrupt ------  ------ Interrupt ------
                            1002 mov %ax, 2000
------ Interrupt ------  ------ Interrupt ------
                            1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
                            1004 test $0, %bx
                            1005 jgt .top
                            1006 halt
```
   If data race did not happen, what is the expected value of the "variable"? ________
   What is the actual value of the "variable"? ________
	
   ---  
   
   **Blank #1:** `2`    
   **Blank #2:** `5`    


### Question 4     
4. We have two threads running the program "looping-race-nolock.s (see in homework of chapter 26).
   The thread trace can be seen below:
```
       Thread 0                Thread 1
    1000 mov 2000, %ax
    1001 add $1, %ax
    1002 mov %ax, 2000
------ Interrupt ------  ------ Interrupt ------
                             1000 mov 2000, %ax
                             1001 add $1, %ax
                             1002 mov %ax, 2000
------ Interrupt ------  ------ Interrupt ------
    1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
                             1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
    1004 test $0, %bx
    1005 jgt .top
    1000 mov 2000, %ax
------ Interrupt ------  ------ Interrupt ------
                             1004 test $0, %bx
                             1005 jgt .top
                             1000 mov 2000, %ax
------ Interrupt ------  ------ Interrupt ------
    1001 add $1, %ax
    1002 mov %ax, 2000
    1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
                             1001 add $1, %ax
------ Interrupt ------  ------ Interrupt ------
    1004 test $0, %bx
    1005 jgt .top
------ Interrupt ------  ------ Interrupt ------
                             1002 mov %ax, 2000
                             1003 sub  $1, %bx
------ Interrupt ------  ------ Interrupt ------
    1006 halt
----- Halt;Switch -----  ----- Halt;Switch -----
                             1004 test $0, %bx
------ Interrupt ------  ------ Interrupt ------
                             1005 jgt .top
------ Interrupt ------  ------ Interrupt ------
                             1006 halt
```   
   If data race did not happen, what is the expectd value of the "variable"? ________  
   What is the actual value of the "variable"? ________  
   
   ---  
   
   **Blank #1:** `2`  
   **Blank #2:** `4`  


### Question 5     
5. Look at this code snippet:     
```c
int *a;  
*a = 3;  
TestAndSet(a, 2);  
   ```
   What is the return value of this TestAndSet call? ________  
   What is the value of *a after this TestAndSet call? ________  
   
   ---  
   
   **Blank #1:** `3`  
   **Blank #2:** `2`  


### Question 6  
6. Look at this code snippet:    
```c
int *a;  
*a = 3;  
CompareAndSwap(a, 2, 1);  
```
   What is the return value of this CompareAndSwamp? ________  
   What is the value of the *a after this CompareAndSwap operation? ________  
   
   ---  
   
   **Blank #1:** `3`  
   **Blank #2:** `3`  
