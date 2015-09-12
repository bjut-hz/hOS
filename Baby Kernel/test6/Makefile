ENTRYPOINT		= 0x30400

ASM 			= nasm
CC 				= gcc
LD  			= ld
ASMFLAG  		= -f elf -o
CFLAG 			= -m32 -c -fno-builtin -o
LDFLAG 			= -m elf_i386 -s -Ttext $(ENTRYPOINT) 

hOSBOOT 		= boot.bin loader.bin
hOSKERNEL 		= kernel.bin
OBJS 			= kernel.o string.o start.o kliba.o

.PHONY : everything realclean clean all buildimg final

everything : $(hOSBOOT) $(hOSKERNEL)

all : realclean everything

final: all clean

image: final buildimg

clean:
	rm -f $(OBJS)
	
realclean:
	rm -f $(OBJS) $(hOSBOOT) $(hOSKERNEL)
	
buildimg:
	dd if=boot.bin of=a.img bs=512 count=1 conv=notrunc
	sudo mount -o loop a.img /mnt/floppy/
	sudo cp -fv loader.bin /mnt/floppy/
	sudo cp -fv kernel.bin /mnt/floppy
	sudo umount /mnt/floppy

boot.bin : boot.asm load.inc fat12hdr.inc
	$(ASM) $< -o $@ 
loader.bin : loader.asm load.inc fat12hdr.inc pm.inc
	$(ASM) $< -o $@
	
$(hOSKERNEL) : $(OBJS)
	$(LD) $(LDFLAG) -o $(hOSKERNEL) $(OBJS)

kernel.o : kernel.asm
	$(ASM) $(ASMFLAG) $@ $<

string.o : string.asm
	$(ASM) $(ASMFLAG) $@ $<

kliba.o : kliba.asm
	$(ASM) $(ASMFLAG) $@ $<

start.o : start.c type.h const.h protect.h
	$(CC) $(CFLAG) $@ $<
