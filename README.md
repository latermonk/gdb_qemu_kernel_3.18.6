## how to debug linux kernel step by step ?  ##


the answer is **Ubuntu 14.04 + gdb + qemu**

Here is how:

##step 1. Donwload the linux kernel 3.18.6
https://www.kernel.org/pub/linux/kernel/v3.x/  


##step 2. config the kernel 

####make defconfig  
generate the .config file for kernel config (location: the root directory of kernel directory)

####make menuconfig ( config the kernel in the menu way )  

in the menuconfig menu , be sure to select the option: compile the kernel with debug info .

![](https://github.com/latermonk/gdb_qemu_kernel_3.18.6/raw/master/img/00.png)
![](https://github.com/latermonk/gdb_qemu_kernel_3.18.6/raw/master/img/01.png)
![](https://github.com/latermonk/gdb_qemu_kernel_3.18.6/raw/master/img/02.png)



##step 3. compile the kernel OUTPUT:  bzImage &  vmlinux

make bzImage

##step 4. run the kernel with qemu

qemu-system-x86_64 -kernel arch/x86_64/boot/bzImage -hda linux-0.2.img -append "root=/dev/sda" -s -S

##step 5. gdb the vmlinux file and connect to qemu gdb server  
gdb vmlinux  
target remote :1234  
b start_kernel  
win  
c



