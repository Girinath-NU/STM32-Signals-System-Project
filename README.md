# GAS Value Display using STM32 and OLED

This project reads analog gas sensor data, converts it to digital, and displays it on an SSD1306 OLED using an STM32 microcontroller. The output is also used to show a status message depending on the PPM (parts per million) value.

## 🧠 Features

- Reads digital gas data from GPIO pins
- Displays real-time PPM values on SSD1306 OLED
- Shows status messages like `PPM is Very High` or `(PPM is Low)`
- Uses interrupt-based data acquisition for accuracy
- Simple PWM configuration for future scalability

## 🛠️ Hardware Components

- STM32 Microcontroller (Tested on STM32F103C8T6 - Blue Pill)
- SSD1306 128x64 I2C OLED Display
- Gas Sensor (with SOC, EOC, OE signals)
- Jumper Wires and Breadboard/PCB

## 🔌 Pin Configuration

| STM32 Pin | Connected To     | Description            |
|-----------|------------------|------------------------|
| GPIOA[0-7] | Data Pins D0-D7  | 8-bit digital data     |
| PBx       | `SOC`            | Start of conversion    |
| PBx       | `OE`             | Output enable          |
| EOC Pin   | EXTI Interrupt   | End of conversion signal|

> Note: Replace `PBx` with your exact GPIO pin used for `SOC` and `OE`.

## 🖥️ OLED Output

The OLED displays:
- "GAS values" as a heading
- The 3-digit PPM value
- A status message depending on the value:
  - `"PPM is Very High"` when value > 90
  - `"(PPM is Low)"` otherwise

## 📁 File Structure

- `main.c`: Contains the main application logic
- `main.h`, `stm32f1xx_hal_*`: Standard STM32 peripheral headers
- `fonts.h`, `ssd1306.h`: OLED library files

## ⏱️ Timing & Delay

- Uses `HAL_Delay(1)` for small delays during data reading
- Adds a delay of 2 seconds between each reading

## 📷 Preview

*(Add an image of your hardware setup or OLED output if possible)*

## 📦 Dependencies

- STM32CubeMX generated code
- HAL drivers
- SSD1306 OLED library
- `fonts.h` for font rendering on OLED

## 🧠 How it Works

1. SOC signal is triggered to start ADC conversion.
2. MCU waits for `EOC` signal using EXTI interrupt.
3. Once `flag` is set, MCU enables output by setting `OE`.
4. 8-bit data is read from GPIOA and shown on OLED.
5. OLED shows real-time gas concentration in PPM format.

---

📌 Maintained by [Girinath NU](https://github.com/girinath-nu)

