# Makefile for Biome-BGC MuSo v4
# invoke by issuing command "make" from this directory!
# Modified by Zoltan BARCZA and Richard KOVACS for Biome-BGC MuSo 4.0;  Nov 2016
# REMARK: on MS Windows standard compiler settings are used [no optimization for speed]
# so we decided to use un-optimized comlining here as well, in order to match settings under Linux and Windows.
# This is why Generic UNIX flags are used
# Static linking is used so 32 bit executable will run in 64 bit Linux box

ROOTDIR=${PWD}
LIBDIR=${ROOTDIR}/lib
INCDIR=${ROOTDIR}/include
VERSION=4
USER=`whoami`
HOST=`hostname`

# Not including these CFLAGS/LDFLAGS will surely break something
# So DON'T MODIFY THESE LINES. Modify the platform specific lines down below
CFLAGS_GENERIC = -I${INCDIR} -DVERS="\\\"${VERSION}\\\"" -DUSER="\\\"${USER}\\\"" -DHOST="\\\"${HOST}\\\""
LDFLAGS_GENERIC = -lm

# For Linux
# CFLAGS = -O3 -Wall -std=c99 ${CFLAGS_GENERIC} # Fully optimized and using ISO C99 features
# CFLAGS = -O3 -std=c99 -ffloat-store ${CFLAGS_GENERIC} # Use precise IEEE Floating Point
# CFLAGS = -g -Wall -ansi -pedantic -std=c89 ${CFLAGS_GENERIC} # 'standards' testing flags 
# CFLAGS = -g -Wall -ansi -pedantic -std=c99 ${CFLAGS_GENERIC} # testing with line/file reporting
LDFLAGS = ${LDFLAGS_GENERIC}
CC = gcc

# For Generic UNIX with debugging
CFLAGS = -g -Wall ${CFLAGS_GENERIC} -static
# LDFLAGS = ${LDFLAGS_GENERIC}
# CC = cc

# For Mac OSX
ifeq "$(shell uname)" "Darwin"
CFLAGS = -g -Wall -I/usr/include/malloc $(CFLAGS_GENERIC)
endif


MACROS=ROOTDIR=${ROOTDIR} LIBDIR=${LIBDIR} INCDIR=${INCDIR} \
	VERSION=${VERSION} CC=${CC} CFLAGS="${CFLAGS}" LDFLAGS="${LDFLAGS}" 

all : 
	cd src ; ${MAKE} all ${MACROS}

clean : 
	cd src; ${MAKE} clean ${MACROS}
	#-rm -f ../outputs/enf_test1* ../restart/enf_test1*

test : all
	cd ../; ./muso ini/enf_test1_spinup.ini; ./bgc ini/enf_test1.ini -a
	
diff:	all
	cd ../; ./bgc ini/enf_test1_spinup.ini

