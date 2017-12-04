libFLAC for Vita
-------

Build instructions for Vita build:

- install VitaSDK
- Download this repository and extract it to some folder
- run the following command from inside that folder
```
bash
sed -ie 's/#include <memory.h>/\/\/#include <memory.h>/g' src/libFLAC/cpu.c
export CFLAGS="-Wl,-q -O3 -mfpu=neon -mcpu=cortex-a9 -march=armv7-a -mfloat-abi=hard -mvectorize-with-neon-quad"
export CXXFLAGS=$CFLAGS
./configure --host=arm-vita-eabi --prefix="" --disable-shared --enable-static --without-pic
make -C src/libFLAC
make -C src/libFLAC++
make -C src/libFLAC DESTDIR=$VITASDK/arm-vita-eabi install
make -C src/libFLAC++ DESTDIR=$VITASDK/arm-vita-eabi install
make -C include DESTDIR=$VITASDK/arm-vita-eabi install
exit
```