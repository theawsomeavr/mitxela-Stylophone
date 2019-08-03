MCU=attiny85
F_CPU=16000000
CC=avr-gcc
OBJCOPY=avr-objcopy
CFLAGS=-Wall -g -Os -mmcu=${MCU} -DF_CPU=${F_CPU} -I.
TARGET=main
SRCS=main.cpp

all:
	${CC} ${CFLAGS} -o ${TARGET}.o -c ${SRCS}
	${CC} ${CFLAGS} -o USB_Stylocard/usbdrv.o -c USB_Stylocard/usbdrv.c
	${CC} ${CFLAGS} -x assembler-with-cpp -o USB_Stylocard/usbdrvasm.o -c USB_Stylocard/usbdrvasm.S
	${CC} ${CFLAGS} -o USB_Stylocard/oddebug.o -c USB_Stylocard/oddebug.c
	${CC} ${CFLAGS} -o USB_Stylocard/osccal.o -c USB_Stylocard/osccal.c
	${CC} ${CFLAGS} -o ${TARGET}.elf USB_Stylocard/usbdrv.o USB_Stylocard/usbdrvasm.o USB_Stylocard/oddebug.o USB_Stylocard/osccal.o main.o
	${OBJCOPY} -j .text -j .data -O ihex ${TARGET}.elf ${TARGET}.hex

flash:
	avrdude -Cavrdude.conf -p ${MCU} -c usbtiny -U flash:w:${TARGET}.hex:i 

clean:
	rm -f *.bin *.hex *.elf *.o