#	Makefile	4.10	83/07/09
#
DESTDIR=
CFLAGS=	-O

# Programs that live in subdirectories, and have makefiles of their own.
#
SUBDIR=	lib2648 libF77 libI77 libU77 libcurses libdbm libg libln \
	libm libmp libnm libpc libplot libtermlib lpr sendmail

# Shell scripts that need only be installed and are never removed.
#
SCRIPT=	makewhatis

# C programs that live in the current directory and do not need
# explicit make lines.
#
STD=	atrun getNAME makekey

# C programs that live in the current directory and need explicit make lines.
#
NSTD=	

all:	${SUBDIR} ${STD} ${NSTD}

${SUBDIR}: /tmp
	cd $@; make ${MFLAGS}

${STD}:
	cc ${CFLAGS} -o $@ $@.c

install:
	for i in ${SUBDIR}; do \
		(cd $$i; make ${MFLAGS} DESTDIR=${DESTDIR} install); done
	for i in ${SCRIPT}; do (install -c $$i.sh ${DESTDIR}/usr/lib/$$i); done
	for i in ${STD} ${NSTD}; do (install $$i ${DESTDIR}/usr/lib/$$i); done
	install -c lib.b ${DESTDIR}/usr/lib/lib.b

clean:
	rm -f a.out core *.s *.o
	for i in ${SUBDIR}; do (cd $$i; make ${MFLAGS} clean); done
	rm -f ${STD} ${NSTD}

depend:
	cat </dev/null >x.c
	for i in ${STD} ${NSTD}; do \
		(echo $$i: $$i.c >>makedep; \
		/bin/grep '^#[ 	]*include' x.c $$i.c | sed \
			-e '/\.\.\/h/d' \
			-e 's,<\(.*\)>,"/usr/include/\1",' \
			-e 's/:[^"]*"\([^"]*\)".*/: \1/' \
			-e 's/\.c//' >>makedep); done
	echo '/^# DO NOT DELETE THIS LINE/+2,$$d' >eddep
	echo '$$r makedep' >>eddep
	echo 'w' >>eddep
	cp Makefile Makefile.bak
	ed - Makefile < eddep
	rm eddep makedep x.c
	echo '# DEPENDENCIES MUST END AT END OF FILE' >> Makefile
	echo '# IF YOU PUT STUFF HERE IT WILL GO AWAY' >> Makefile
	echo '# see make depend above' >> Makefile

# Files listed in ${NSTD} have explicit make lines given below.

# DO NOT DELETE THIS LINE -- make depend uses it

atrun: atrun.c
atrun: /usr/include/stdio.h
atrun: /usr/include/sys/param.h
atrun: /usr/include/sys/dir.h
atrun: /usr/include/sys/time.h
atrun: /usr/include/sys/stat.h
getNAME: getNAME.c
getNAME: /usr/include/stdio.h
makekey: makekey.c
# DEPENDENCIES MUST END AT END OF FILE
# IF YOU PUT STUFF HERE IT WILL GO AWAY
# see make depend above
