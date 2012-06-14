# $Id$

OBJASM = $(GCCSDK_INSTALL_CROSSBIN)/asasm
CC = $(GCCSDK_INSTALL_CROSSBIN)/arm-unknown-riscos-gcc
LINK = $(GCCSDK_INSTALL_CROSSBIN)/

SockWatch,ffa: SockWatch.s
	$(OBJASM) -o SockWatch.o SockWatch.s
	$(CC) -nostdlib -lgcc -mmodule -o SockWatch,ffa SockWatch.o

install: SockWatch,ffa
	cp SockWatch,ffa ../!ModInst/Resources/!System/310/Modules/Network/

clean:
	rm -f SockWatch,ffa
	rm -f SockWatch.o
