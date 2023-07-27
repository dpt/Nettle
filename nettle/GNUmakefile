#
# Makefile for cross-compiling Nettle
#

CC ?= /home/riscos/gccsdk/cross/bin/arm-unknown-riscos-gcc
NATIVE_CC ?= /usr/bin/gcc
CFLAGS = -c -D_BSD_SOURCE -std=c9x -Wall -mpoke-function-name -I/home/riscos/gccsdk/env/include
CONFIG = -DWITH_SSH

LIBS = -L/home/riscos/gccsdk/env/lib -lssh2 -lgcrypt -lgpg-error -lcrypto
OBJS = chardefn.o choices.o dnslib.o globals.o init.o keyboard.o lineedit.o \
       main.o misc.o hotlist.o nettle.o process.o socket.o quit.o seln.o \
       wimp.o zapgen.o fortify.o sockwatch.o messages.o termlist.o url.o \
       wimputil.o spool.o mouse.o scripts.o processesc.o processiac.o \
       procesescx.o
HEADERS = chardefn.h choices.h dnslib.h fortify.h generic.h globals.h \
	  graphics.h hotlist.h init.h keyboard.h lineedit.h main.h messages.h \
	  misc.h mouse.h nettle.h process.h quit.h scripts.h seln.h socket.h \
	  sockwatch.h spool.h templ.h termlist.h ufortify.h url.h wimp.h \
	  wimputil.h zapredraw.h
TEMPLATES = !Nettle/Resources/UK/Templates,fec

all:	!Nettle/!RunImage,ff8

!Nettle/!RunImage,ff8: !Nettle/!RunImage,e1f
	@echo " ELF2AIF:" $@
	@/home/riscos/gccsdk/cross/bin/elf2aif $< $@
	@rm !Nettle/!RunImage,e1f

!Nettle/!RunImage,e1f: $(OBJS)
	@echo "    LINK:" $@
	@$(CC) -static -o $@ $(OBJS) $(LIBS)

$(OBJS): $(HEADERS) GNUmakefile

%.o: %.c
	@echo " COMPILE:" $<
	@$(CC) $(CFLAGS) $(CONFIG) -o $@ $<

# intentionally compiled using native compiler
templheadr: templheadr.c
	@$(NATIVE_CC) -o $@ $(LINKFLAGS) $?

templ.h: templheadr $(TEMPLATES)
	./templheadr $(TEMPLATES) $@

# convert RISC OS style c and h directories into extensions using symlinks
%.h: h/%
	@ln -s $< $@
%.c: c/%
	@ln -s $< $@

clean:
	rm --force --verbose *.o *.h *.c templ.h templheadr
	rm --force --verbose !Nettle/!RunImage,e1f !Nettle/!RunImage,ff8

