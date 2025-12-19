LIBRARY=libquickjs_c_bridge_plugin.so

CC=gcc
CXX=g++

FLAGS=-Wall
# FLAGS=-Wall -O2

C_SOURCES=quickjs/cutils.c quickjs/libregexp.c quickjs/libunicode.c quickjs/dtoa.c quickjs/quickjs.c
CPP_SOURCES=libfastdev_quickjs_runtime.cpp

OBJECTS=$(C_SOURCES:.c=.o) $(CPP_SOURCES:.cpp=.o)

ifdef WINDOWS
	# export PATH=$PATH:$HOME/bin_custom/cosmocc/bin

	# LIBRARY=libquickjs_c_bridge_plugin.dll
	LIBRARY=libquickjs_c_bridge_plugin-implib.dll

	# CC=cosmocc
	# CXX=cosmoc++

	# CC=x86_64-w64-mingw32-gcc
	# CXX=x86_64-w64-mingw32-g++

	CC=i686-w64-mingw32-gcc
	CXX=i686-w64-mingw32-g++
endif

# dlldir=/usr/x86_64-w64-mingw32/bin
# cross_prefix=x86_64-w64-mingw32-

dlldir=/usr/i686-w64-mingw32/bin
cross_prefix=i686-w64-mingw32-

all: $(LIBRARY)
	$(cross_prefix)strip $(LIBRARY)
	cp $(dlldir)/libwinpthread-1.dll .


$(LIBRARY): $(OBJECTS)
	$(CXX) $(FLAGS) -shared $^ -o $@ -Wl,--out-implib,$(LIBRARY:.dll=.a)

$(CPP_SOURCES:.cpp=.o): $(CPP_SOURCES)
	$(CXX) $(FLAGS) -DCONFIG_VERSION="\"2025-09-13\"" -c -fPIC $< -o $@

%.o: %.c
	$(CC) $(FLAGS) -DCONFIG_VERSION="\"2025-09-13\"" -c -fPIC $< -o $@


# BINARY_NAME=libquickjs_c_bridge_plugin
# build_windows:
# 	x86_64-w64-mingw32-gcc -DCONFIG_VERSION="\"2025-09-13\"" -Wall -O2 -shared -o $(BINARY_NAME).dll -fPIC quickjs/cutils.c quickjs/libregexp.c quickjs/libunicode.c quickjs/dtoa.c quickjs/quickjs.c libfastdev_quickjs_runtime.cpp


clean_shared_libs:
	rm *.dll *.so *.a

clean:
	rm quickjs/*.o
	rm *.o
