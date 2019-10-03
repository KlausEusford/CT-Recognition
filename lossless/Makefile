
#
# Makefile for lossless wavelet compression software
#
# This makefile assumes that the Microsoft environment has
# been enhanced with the cygwin UNIX utilities for Win32.
# These are available from Red Hat (which purchased Cygnus).
#
# Command:
#    nmake -f Makefile
#

DEBUG     = -Zi
BROWSE    = -FR

CFLAGS    = $(BROWSE) $(DEBUG) -DWIN32 -Tp
OBJ       = obj
EXE       = .exe

TOPINC = ..\include

DOXYPATH = e:/doxygen/bin

INCLUDE = -Iinclude -I$(TOPINC) -I..\data\include -I "d:\Program Files\Microsoft Visual Studio\Vc98\Include"

PACKET_OBJ = blockpool.$(OBJ) packtree_base_int.$(OBJ) packtree_int.$(OBJ) invpacktree_int.$(OBJ) costwidth.$(OBJ) support.$(OBJ) yahooTS.$(OBJ)

all: compresstest


compresstest: compresstest$(EXE) 


compresstest$(EXE): $(PACKET_OBJ) compresstest.$(OBJ) 
	$(CC) $(PACKET_OBJ) compresstest.$(OBJ) $(DEBUG) -o compresstest$(EXE)

#
# clean-up for Microsoft object and browser files and emacs temps
#
clean:
	rm -f *.obj *.pdb *.sbr *.ilk *.exe 
	rm -f include/*~
	rm -f src/*~


$(TOPINC)\costbase.h: $(TOPINC)\packnode.h

include\costwidth.h: $(TOPINC)\costbase.h

include\line_int.h: $(TOPINC)\liftbase.h

$(TOPINC)\packdata.h: $(TOPINC)\blockpool.h

include\invpacktree_int.h: $(TOPINC)\packdata.h

$(TOPINC)\packnode.h: $(TOPINC)\packdata.h

$(TOPINC)\packdata_list.h: $(TOPINC)\fifo_list.h $(TOPINC)\packdata.h

$(TOPINC)\packcontainer.h: $(TOPINC)\packnode.h

$(TOPINC)\queue.h: $(TOPINC)\fifo_list.h $(TOPINC)\packnode.h

include\packtree_base_int.h: $(TOPINC)\packnode.h $(TOPINC)\liftbase.h

include\packtree_int.h: include\packtree_base_int.h $(TOPINC)\packcontainer.h $(TOPINC)\liftbase.h

include\invpacktree_int.h: $(TOPINC)\liftbase.h $(TOPINC)\list.h $(TOPINC)\packcontainer.h $(TOPINC)\packdata.h $(TOPINC)\packdata_list.h

packtree_base_int.$(OBJ): src\$*.cpp include\$*.h
	$(CC) -c $(INCLUDE) $(CFLAGS) src\$*.cpp


packtree_int.$(OBJ): src\$*.cpp include\$*.h $(TOPINC)\queue.h $(TOPINC)\packcontainer.h $(TOPINC)\blockpool.h
	$(CC) -c $(INCLUDE) $(CFLAGS) src\$*.cpp


invpacktree_int.$(OBJ): src\$*.cpp include\$*.h $(TOPINC)\blockpool.h
	$(CC) -c $(INCLUDE) $(CFLAGS) src\$*.cpp

blockpool.$(OBJ): ..\src\$*.cpp ..\include\$*.h
	$(CC) -c $(INCLUDE) $(CFLAGS) ..\src\$*.cpp

costwidth.$(OBJ): src\$*.cpp include\$*.h
	$(CC) -c $(INCLUDE) $(CFLAGS) src\$*.cpp

support.$(OBJ): src\$*.cpp include\$*.h
	$(CC) -c $(INCLUDE) $(CFLAGS) src\$*.cpp

yahooTS.$(OBJ): ..\data\src\$*.cpp ..\data\include\$*.h
	$(CC) -c $(INCLUDE) $(CFLAGS) ..\data\src\$*.cpp

compresstest.$(OBJ): src\$*.cpp include\line_int.h $(TOPINC)\packnode.h $(TOPINC)\packcontainer.h include\packtree_int.h include\invpacktree_int.h 
	$(CC) -c $(INCLUDE) $(CFLAGS) src\$*.cpp

