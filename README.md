# Blinkande LED på Raspberry Pi Pico W

Denna guide beskriver hur du får den inbyggda LED-lampan på en Raspberry Pi Pico W att blinka med både MicroPython och C/C++.

## Förberedelser
### Hårdvara
- Raspberry Pi Pico W
- USB-kabel (USB-A till micro-USB)
- Dator (Windows, macOS eller Linux)

### Programvara
- **MicroPython**
  - Thonny IDE (rekommenderat)
  - MicroPython firmware
- **C/C++**
  - Raspberry Pi Pico SDK
  - CMake och GNU Make
  - Compiler (arm-none-eabi-gcc)

## Alternativ 1: Blinkande LED med MicroPython

### Steg 1: Installera MicroPython på Pico
1. Ladda ner den senaste MicroPython UF2-filen från:
   - [https://micropython.org/download/rp2-pico-w/](https://micropython.org/download/rp2-pico-w/)
2. Håll in **BOOTSEL**-knappen på din Pico och anslut den till datorn via USB.
3. Släpp knappen när enheten monteras som en enhet med namnet **RPI-RP2**.
4. Dra och släpp UF2-filen till **RPI-RP2**-enheten.
5. Pico startar om och kör MicroPython.

### Steg 2: Skriv och kör programmet
1. Öppna **Thonny IDE**.
2. Välj **Raspberry Pi Pico** som interpreter under **Run** > **Select Interpreter**.
3. Skriv följande kod:

```python
from machine import Pin, Timer

led = Pin("LED", Pin.OUT)
timer = Timer()

def blink(timer):
    led.toggle()

timer.init(freq=1, mode=Timer.PERIODIC, callback=blink)
```

4. Klicka på **Run** för att köra programmet. LED-lampan ska nu blinka en gång per sekund.

---

## Alternativ 2: Blinkande LED med C/C++

### Steg 1: Installera och konfigurera Raspberry Pi Pico SDK
1. Installera **CMake**, **GNU Make** och **arm-none-eabi-gcc**.
2. Klona och konfigurera Pico SDK:

```sh
git clone -b master https://github.com/raspberrypi/pico-sdk.git
cd pico-sdk
export PICO_SDK_PATH=$(pwd)
```

### Steg 2: Skriv blink-programmet
Skapa en fil `blink.c`:

```c
#include "pico/stdlib.h"

int main() {
    gpio_init(PICO_DEFAULT_LED_PIN);
    gpio_set_dir(PICO_DEFAULT_LED_PIN, GPIO_OUT);

    while (1) {
        gpio_put(PICO_DEFAULT_LED_PIN, 1);
        sleep_ms(500);
        gpio_put(PICO_DEFAULT_LED_PIN, 0);
        sleep_ms(500);
    }
}
```

### Steg 3: Bygg och ladda upp programmet
1. Skapa en `CMakeLists.txt`:

```cmake
cmake_minimum_required(VERSION 3.13)
include(pico_sdk_import.cmake)

project(blink C CXX ASM)
pico_sdk_init()

add_executable(blink blink.c)
target_link_libraries(blink pico_stdlib)
pico_add_extra_outputs(blink)
```

2. Bygg projektet:

```sh
mkdir build
cd build
cmake ..
make
```

3. Ladda upp `.uf2`-filen till Pico genom att hålla in **BOOTSEL**, ansluta USB och kopiera filen till **RPI-RP2**.

### Steg 4: Starta programmet
När Pico startar om, ska LED-lampan blinka en gång per sekund.

---

## Felsökning
- Kontrollera att Pico är korrekt ansluten och i BOOTSEL-läge vid behov.
- Se till att rätt firmware används (MicroPython eller C/C++ SDK).
- Om det inte fungerar i C/C++, dubbelkolla att rätt verktyg är installerade och `PICO_SDK_PATH` är satt.

## Avslutning
Nu har du fått den inbyggda LED-lampan på en Raspberry Pi Pico W att blinka! 🚀

