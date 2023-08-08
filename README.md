# pil21-macos

Lets install picolisp on Macos
```
# install BREW package manager
# brew install git libffi llvm ncurses openssl readline pkg-config
# add /usr/local/opt/llvm/bin to $PATH 
# git clone https://git.envs.net/mpech/pil21
# cp pil21-macos/Makefile.macos pil21/src
# cd pil21/src
# make -f Makefile.macos
$ make -f Makefile.macos
../pil   lib/llvm.l main.l -bye > base.ll
mv base.map ../lib/map
opt -O3   -opaque-pointers -o base.bc base.ll
clang -O3 -w -c -o lib.bc -D_OS='"Darwin"' -D_CPU='"x86_64"' `pkg-config --cflags libffi` -I/usr/local/opt/libffi/include -I/usr/local/opt/readline/include -emit-llvm lib.c
llvm-link -o picolisp.bc base.bc lib.bc
mkdir -p ../bin ../lib
llc picolisp.bc -relocation-model=pic -o picolisp.s
clang picolisp.s -o ../bin/picolisp -L/usr/local/opt/readline/lib -lncurses -rdynamic -lc -lutil -lm -ldl -lreadline -lffi
true ../bin/picolisp
../pil   lib/llvm.l ext.l -bye > ext.ll
opt -O3   -opaque-pointers -o ext.bc ext.ll
llc ext.bc -relocation-model=pic -o ext.s
clang ext.s -o ../lib/ext.so -dynamiclib -undefined dynamic_lookup
true ../lib/ext.so
../pil   lib/llvm.l ht.l -bye > ht.ll
opt -O3   -opaque-pointers -o ht.bc ht.ll
llc ht.bc -relocation-model=pic -o ht.s
clang ht.s -o ../lib/ht.so -dynamiclib -undefined dynamic_lookup
true ../lib/ht.so

#
```
