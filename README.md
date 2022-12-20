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
clang -w -D_OS='"Darwin"' -D_CPU='"x86_64"' sysdefs.c  &&  ./a.out > ../lib/sysdefs  &&  rm ./a.out
opt -O3   -opaque-pointers -o base.bc base.ll
clang -O3 -w -c -o lib.bc -D_OS='"Darwin"' -D_CPU='"x86_64"' -I/usr/local/opt/libffi/include -I/usr/local/opt/readline/include -emit-llvm lib.c
llvm-link -o picolisp.bc base.bc lib.bc
mkdir -p ../bin ../lib
llc picolisp.bc -o picolisp.s
clang picolisp.s -o ../bin/picolisp -lm -ldl -lreadline -lffi -lncurses -L/usr/local/opt/readline/lib
strip ../bin/picolisp
clang -O3 -w -o ../bin/balance balance.c
strip ../bin/balance
clang -O3 -w -o ../bin/ssl ssl.c -lssl -lcrypto -L/usr/local/opt/openssl/lib -I/usr/local/opt/openssl/include
strip ../bin/ssl
clang -O3 -w -o ../bin/httpGate httpGate.c -lssl -lcrypto -L/usr/local/opt/openssl/lib -I/usr/local/opt/openssl/include
strip ../bin/httpGate
#
```
