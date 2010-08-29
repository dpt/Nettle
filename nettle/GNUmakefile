#
# Makefile for cross-compiling Nettle
#

CC = /home/riscos/cross/bin/arm-unknown-riscos-gcc
CFLAGS = -c -std=c9x -Wall -mpoke-function-name -I/home/riscos/env/include

LIBS = -L/home/riscos/env/lib -lssh2 -lgcrypt -lgpg-error
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

!Nettle/!RunImage,ff8: RunImage,e1f
	@echo " ELF2AIF:" $@
	@/home/riscos/cross/bin/elf2aif $< $@

RunImage,e1f: $(OBJS)
	@echo "    LINK:" $@
	@$(CC) -o $@ $(OBJS) $(LIBS)

$(OBJS): $(HEADERS)

%.o: %.c
	@echo " COMPILE:" $<
	@$(CC) $(CFLAGS) -o $@ $<

# intentionally compiled using native compiler
templheadr: templheadr.c
	gcc -o $@ $(LINKFLAGS) $?

templ.h: templheadr $(TEMPLATES)
	./templheadr $(TEMPLATES) $@

# convert RISC OS style c and h directories into extensions using symlinks
%.h: h/%
	ln -s $< $@
%.c: c/%
	@ln -s $< $@

clean:
	rm --force --verbose *.o templ.h templheadr
	rm --force --verbose RunImage,e1f !Nettle/!RunImage,ff8

