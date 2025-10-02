# Dự án điều khiển LED với nút nhấn sử dụng thư viện OneButton

## 1. Giới thiệu
Trong ví dụ này, chúng ta sẽ sử dụng **ESP32** (hoặc có thể thay bằng Arduino Uno/Nano/MEGA) kết hợp với thư viện **OneButton** để điều khiển LED thông qua một nút nhấn duy nhất.  
Nhờ thư viện này, chỉ với 1 nút bấm ta có thể tạo ra nhiều chức năng khác nhau như **nhấn 1 lần (single click)** hoặc **nhấn 2 lần (double click)**.

## 2. Phần cứng cần chuẩn bị
- 01 bo mạch ESP32 hoặc Arduino tương đương.  
- 01 đèn LED rời (không sử dụng LED tích hợp sẵn trên board).  
- 01 điện trở 220Ω – 330Ω để hạn dòng cho LED.  
- 01 nút nhấn (button).  
- Dây cắm và Breadboard.  

### Sơ đồ nối dây
- LED → nối với **GPIO4 (ESP32)**, đầu còn lại qua điện trở xuống GND.  
- Nút nhấn → nối với **GPIO35 (ESP32)** ở chế độ **INPUT_PULLUP**:  
  - Một chân nối GPIO35.  
  - Chân còn lại nối GND.  

## 3. Phần mềm cần cài đặt
- Visual Studio Code kèm extension **PlatformIO**.  
- Thư viện **OneButton** cài trong PlatformIO.  

## 4. Các chức năng của chương trình
- **Nhấn 1 lần**: bật/tắt LED.  
- **Nhấn 2 lần liên tiếp**: LED chuyển sang chế độ nhấp nháy (chu kỳ 0.5 giây sáng/tắt).  
- Khi LED đang nhấp nháy, nhấn double click lần nữa → thoát chế độ nháy, LED tắt hẳn.  

## 5. Cách hoạt động
Thư viện **OneButton** cung cấp sẵn các hàm xử lý sự kiện từ một nút bấm:  
- `attachClick()` để xử lý nhấn 1 lần.  
- `attachDoubleClick()` để xử lý nhấn 2 lần.  

Chương trình sử dụng một biến trạng thái `blinking` để kiểm soát việc LED có đang nháy hay không.  
Trong vòng lặp `loop()`, nếu `blinking = true`, LED sẽ thay đổi trạng thái sau mỗi 500ms nhờ sử dụng hàm **millis()**.
