# KMO - Kernel Memory Overwrite

KMO is a bug that allows you to write to kernel memory, utilizing a buffer overflow in add_module. 

Inside of add_module, there is already buffer overflow protection; for modules.

It does not check if is_mod is overflowing. 

is_mod stores the ports of modules, for a lookup table.

So, if you keep overwriting any module, 131072 times, (or 131072 - the amount of current modules, aka is_mod_count) you will be able to overwrite kernel memory. 

# Step 1 - Prepare modules.

First, set a module 131072 times. (or 131072 - the amount of current modules, aka is_mod_count)

Second, make sure is_mod_count is 131072. If so, go on to Step 2. 

# Step 2 - Overwrite Memory

Now, add a module, with the port as the 1 or 2 bytes you would like to write, after is_mod. 

Repeat, for as many bytes as you like! 

# PoC

This repository contains a kernel exploit, in exploit.c. 

Simply run prepare_kernel, to prepare the kernel. 

Now run write_bytes for every 2 bytes you would like to write.

To only write 1 byte, just run write_bytes with only 1 byte. 

Make sure the bytes are in int form, not a char array.
