NAME = play
MODULES = 

CS107E= ../../../../cs107e
CFLAGS = -g -Wall -Og -std=c99 -ffreestanding -I$(CS107E)/include
LDFLAGS = -nostdlib -T memmap -L$(CS107E)/lib 
LDLIBS = -lpiextra -lpi -lgcc

all : $(NAME).list $(NAME).bin 

%.bin: %.elf
	arm-none-eabi-objcopy $< -O binary $@

%.elf: %.o $(MODULES) start.o cstart.o
	arm-none-eabi-gcc $(LDFLAGS) $^ $(LDLIBS) -o $@

%.o: %.c
	arm-none-eabi-gcc $(CFLAGS) -c $< -o $@

%.o: %.s
	arm-none-eabi-as $< -o $@

%.list: %.o
	arm-none-eabi-objdump -d $< > $@

install: $(NAME).bin
	rpi-install.py $(NAME).bin

clean:
	rm -f *.o *.bin *.elf *.list

.PHONY: all clean

.PRECIOUS: %.o %.elf
