MYPRINT = myprint.asm
CHOOSE = choose.c
MYPRINT_O = $(subst .asm,.o,$(MYPRINT))
CHOOSE_O = $(subst .c,.o,$(CHOOSE))
PROGRAM = test

.PHONY = everything

everything : $(MYPRINT_O) $(CHOOSE_O)
	ld -m elf_i386 -s -o $(PROGRAM) $(MYPRINT_O) $(CHOOSE_O)

clean :
	rm -f $(PROGRAM) $(MYPRINT_O) $(CHOOSE_O)
	
$(MYPRINT_O) : $(MYPRINT)
	nasm -f elf -o $@ $<
$(CHOOSE_O) : $(CHOOSE)
	gcc -m32 -c $< -o $@