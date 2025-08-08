# Embedded Systems Demos Repository

This repository contains a collection of embedded systems demo projects. Each demo includes its own code, `Makefile`, and documentation. It’s designed for hobbyists, students, or engineers experimenting with microcontrollers like STM32, AVR, ESP32, and others.

---

## 📁 Project Structure

```
/embedded-demos
├── blink-led/
│   ├── main.c
│   ├── Makefile
│   └── README.md
├── uart-echo/
│   ├── main.c
│   ├── Makefile
│   └── README.md
└── ...
```

---

## 🚀 Getting Started

### 🔧 Prerequisites

Make sure you have the following installed:

- GCC toolchain for your target (e.g. `arm-none-eabi-gcc` for ARM Cortex-M)
- `make` utility
- Flashing tool (e.g. `openocd`, `avrdude`, or `esptool.py`)

---

### 📦 Clone the Repository

```bash
git clone https://github.com/your-username/embedded-demos.git
cd embedded-demos
```

---

### ▶️ Build and Flash a Demo

```bash
cd blink-led
make            # Compiles the source code
make flash      # Flash to your device (optional)
make clean      # Clean build artifacts
```

---

## 🛠️ Example Makefile Template

Each project contains its own `Makefile`. Here’s an example for an STM32 Cortex-M4 target using `arm-none-eabi-gcc` and `openocd`:

```makefile
# Example Makefile

PROJECT = blink-led
BUILD_DIR = build
SRC = main.c
TARGET = $(BUILD_DIR)/$(PROJECT).elf

CC = arm-none-eabi-gcc
CFLAGS = -mcpu=cortex-m4 -mthumb -Wall -O2

all: $(TARGET)

$(BUILD_DIR):
	mkdir -p $(BUILD_DIR)

$(TARGET): $(SRC) | $(BUILD_DIR)
	$(CC) $(CFLAGS) -o $@ $^

flash: $(TARGET)
	openocd -f interface/stlink.cfg -f target/stm32f4x.cfg -c "program $(TARGET) verify reset exit"

clean:
	rm -rf $(BUILD_DIR)
```

💡 Modify this template depending on your board, toolchain, or flashing method.

---

## ➕ Add a New Project

```bash
cd embedded-demos
mkdir my-demo
cd my-demo
touch main.c Makefile README.md
```

Then copy and modify the `Makefile` from another demo:
- Rename `PROJECT`
- Update `CFLAGS` for your MCU
- Change `flash` target to use your tool (e.g. `esptool.py`, `avrdude`, etc.)

---

## ✅ Supported Boards (Examples)

| Project       | MCU / Platform     | Flash Tool     |
|---------------|---------------------|----------------|
| blink-led     | STM32F401RE         | OpenOCD        |
| uart-echo     | ATmega328P (Uno)    | avrdude        |
| wifi-demo     | ESP32               | esptool.py     |

---

## 🤝 Contributions

Want to contribute?

- Fork the repo
- Add a new project folder
- Include a working `Makefile` and a short `README.md`
- Submit a pull request

---

## 📜 License

MIT License
