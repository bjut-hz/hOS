SRC=boot.asm
BIN=$(subst .asm,.bin,$(SRC))

.PHONY : everything

everything : $(BIN)
	dd if=$(BIN) of=a.img count=1 conv=notrunc

$(BIN) : $(SRC)
	nasm $< -o $@

