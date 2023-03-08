# assign01kernelprog-AyeshaIrshad1337
## Ayesha Irshad 21K-4734
I have worked on ubuntu 16.04 and used these following commands:  
Prerequisites:  
• sudo apt-get install gcc  
• sudo apt-get install libncurses5-dev  
• sudo apt-get install bison  
• sudo apt-get install flex  
• sudo apt install make  
• sudo apt-get install libssl-dev  
• sudo apt-get install libelf-dev  
• sudo add-apt-repository "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) main uiverse"  
• sudo apt-get update  
• sudo apt-get upgrade  
as my laptop was hagging alot I wasn't able to take screenshot of every steps  
# Downloading the Kernel  
I downloaded the kernel from kernel.org and extracted it on the Desktop  
![image](https://user-images.githubusercontent.com/104616632/223098173-411a7580-4292-4e46-a1f3-debe775a0c2b.png)
  
![image](https://user-images.githubusercontent.com/104616632/223097711-af709d3a-2f28-4ec7-b812-ea0b7fee20cf.png)  
# Making A new Folder called Hello:
![image](https://user-images.githubusercontent.com/104616632/223098016-9b3b7409-71cc-4c0a-80a8-daa393658012.png)  
# Adding a .C file with the following Code:  
**"gedit hello.c"** in the directory of hello folder created in the extracted kernel file.  
![image](https://user-images.githubusercontent.com/104616632/223098501-be402aab-12c7-4100-8a47-0bbd827722cc.png)    
**Code Explanation**  
a. We used #include <linux/kernel> because we are building a system call for our linux
kernel.  
b. Amslinkage simply means that the arguments for this function will be on the stack
instead of the CPU registers.  
c. Printk is used instead of printf because we are going to print in the kernel’s log file.  
d. If the code is run and it returns 0, then it will mean that our program ran successfully and Hello world is written to out kernel’s log file.  
# Creating a Makefile for the C code:  
Creating a make file by using the following command:  
**gedit Makefile**   
![image](https://user-images.githubusercontent.com/104616632/223810797-4895b42b-c7d9-4ee4-a95b-6a1a8d583d52.png)

and then add the following lines  
**obj-y :=heelo.o**  
![image](https://user-images.githubusercontent.com/104616632/223099463-fe83ebd5-991f-4fc8-b60b-78409f58125a.png)  
# adding the new code into the system table file:  
run the following command:    
**gedit /arch/x86/entry/syscalls/syscall_64.tbl**  
before using it check your system type by using the following command:  
**uname -m**  
if your system is 32 use this syscall_32.tbl instead of syscall_64.tbl  
We add **"64 hello"** and ** "sys_hello"** at line 335  
![image](https://user-images.githubusercontent.com/104616632/223100338-9fabf5b2-4bba-41d6-afe0-3803a4ce90d0.png)  
# Adding the prototype of the system call into the system calls header file:  
And to access the system call header file run this command:
**gedit include/linux/syscalls.h"  
then go to the end of the file and add the prototype of the function you created on the hello.c file.  
![image](https://user-images.githubusercontent.com/104616632/223101818-89a52705-6953-49fe-92f9-acc0050ea1d5.png)  
# Changing version and adding the hello folder in the kernels Makefile:  
Now we have to add our roll number at the extraversion of the kernels make file and we have to add the new module that we created into out kerrnels make file.  
For this, we open the Makefile of the kernel. After changing the extraversion do ctrl F and find core-y and go on its second instance which is under KBUILD_EXTMOD and add our new module hello.    
**"gedit Makefile"**  
![image](https://user-images.githubusercontent.com/104616632/223102953-49c3b9a3-60b0-4ba1-99ec-767e0f3eeb29.png)  
# Now we have to  create a config for our kernel:  
**“ls /boot | grep config”** 
**"pwd"**  Copy the path 
**“cp /boot/config-4.19.0-275-generic [copied path]"**  
**“yes "" | make oldconfig -j2”**  
before putting check your processor first mine was 2 you can check by the following command  
**"lscpu"**  
# Cleaning and Compiling the kernel:  
**" sudo su "**  
**" make clean -j2 "**  
**" make -j2 "**  
After this you will find the following lines which means your kernel is successfully complied.  
![image](https://user-images.githubusercontent.com/104616632/223104903-eeb9fd0e-7c7e-494c-a9c3-9c65e074f4ef.png)  
# Installing Modulues:  
**" make modules_install install "**  
after that shutdown and while restart press shift.  
**" shutdown -r now "**  
# Output:  
![image](https://user-images.githubusercontent.com/104616632/223105300-f5bb3da5-1dd0-4f4d-b033-073273f916f9.png)  
