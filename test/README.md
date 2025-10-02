# Dự án điều khiển LED bằng nút nhấn sử dụng thư viện OneButton

## 1. Giới thiệu
Dự án này minh họa cách sử dụng **ESP32** (hoặc Arduino) kết hợp với thư viện **OneButton** để điều khiển LED bằng một nút nhấn duy nhất.  
Chúng ta có thể thực hiện nhiều chức năng khác nhau dựa trên **cách bấm nút** (single click, double click).

## 2. Yêu cầu phần cứng
- 01 board ESP32 (hoặc Arduino Uno/Nano/MEGA).
- 01 LED rời (không dùng LED tích hợp).
- 01 điện trở 220Ω – 330Ω (dùng hạn dòng cho LED).
- 01 nút nhấn (button).
- Dây nối Breadboard.

## 3. Sơ đồ kết nối
- LED → chân GPIO4 (ESP32) + điện trở hạn dòng nối về GND.
- Nút nhấn → chân GPIO5 (ESP32), sử dụng INPUT_PULLUP.

## 4. Code mẫu
```cpp
#include <OneButton.h>

#define LED_PIN 4
#define BUTTON_PIN 5

OneButton button(BUTTON_PIN, true);

void singleClick() {
  digitalWrite(LED_PIN, !digitalRead(LED_PIN));
}

void doubleClick() {
  for (int i = 0; i < 5; i++) {
    digitalWrite(LED_PIN, HIGH);
    delay(200);
    digitalWrite(LED_PIN, LOW);
    delay(200);
  }
}

void setup() {
  pinMode(LED_PIN, OUTPUT);
  button.attachClick(singleClick);
  button.attachDoubleClick(doubleClick);
}

void loop() {
  button.tick();
}
