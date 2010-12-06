CROSS_COMPILE=armv5tel-redhat-linux-gnueabi-
CPU=arm926ej-s
all:
	$(CROSS_COMPILE)gcc -c -mcpu=$(CPU) -g test.c -o test.o
	$(CROSS_COMPILE)as -mcpu=$(CPU) -g startup.s -o startup.o
	$(CROSS_COMPILE)ld -Map=test.map -T test.ld test.o startup.o -o test.elf
	$(CROSS_COMPILE)objcopy -O binary test.elf test.bin

all-uboot:
	$(CROSS_COMPILE)gcc -c -mcpu=$(CPU) -g test.c -o test.o
	$(CROSS_COMPILE)as -mcpu=$(CPU) -g startup.s -o startup.o
	$(CROSS_COMPILE)ld -Map=test-uboot.map -T test-uboot.ld test.o startup.o -o test-uboot.elf
	$(CROSS_COMPILE)objcopy -O binary test-uboot.elf test-uboot.bin

clean:
	rm -f *.o *~ test.elf  test.bin test-uboot.bin test-uboot.elf flash.bin test-uboot.uimg \
		test.map test-uboot.map


test-image: all-uboot
	mkimage -A arm -C none -O linux -T kernel -d test-uboot.bin -a 0x00100000 -e 0x00100000 test-uboot.uimg
	cat u-boot.bin test-uboot.bin > flash.bin
