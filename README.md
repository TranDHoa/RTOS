# RTOS - Thiết kế và triển khai lõi hệ điều hành đa nhiệm thời gian thực (RTOS) từ mức thanh ghi trên vi điều khiển ARM Cortex-M ứng dụng vào điều khiển led 7 thanh và led đơn

Chào bạn! Ý tưởng tự xây dựng một RTOS từ con số 0 trên dòng ESP32  là một thử thách cực kỳ thú vị và giúp nâng trình kiến thức về System Architecture lên rất nhiều.

Dưới đây là nội dung kế hoạch 12 tuần của bạn đã được tối ưu hóa theo định dạng **Markdown (`README.md`)** chuyên nghiệp để bạn có thể đưa thẳng lên GitHub. Tôi đã bổ sung thêm 2 tuần cuối (Tuần 11-12) để hoàn thiện đúng lộ trình 12 tuần như tiêu đề bạn mong muốn.

---

# 🚀 ESP32 Custom RTOS Development Project

Dự án xây dựng Hệ điều hành thời gian thực (RTOS) từ cơ bản dành cho dòng vi điều khiển **ESP32  (ARM Cortex-M4)**.

---

## 📅 Lộ Trình Thực Hiện (12 Tuần)

### 🏗️ GIAI ĐOẠN 1: NGHIÊN CỨU NỀN TẢNG VÀ THIẾT KẾ KIẾN TRÚC (Tuần 1-3)

#### **Tuần 1: Nghiên cứu tổng quan và thiết lập môi trường**

* **Mục tiêu:** Hiểu rõ yêu cầu đề tài, chuẩn bị công cụ phát triển.
* **Nội dung:**
* Tìm hiểu khái niệm, phân loại và ứng dụng của RTOS.
* Nghiên cứu kiến trúc **ARM Cortex-M**: Tập thanh ghi, chế độ Thread mode & Handler mode.
* Đọc Datasheet/Reference Manual của **ESP32 xx**.
* Cài đặt: ESP32CubeIDE/Keil uVision, toolchain ARM GCC.
* Chuẩn bị phần cứng: Board ESP32  Discovery, LED, điện trở.


* **Sản phẩm:** * [ ] Báo cáo tổng quan RTOS & ARM.
* [ ] Môi trường phát triển hoàn chỉnh.



#### **Tuần 2: Nghiên cứu kiến trúc ARM Cortex-M chuyên sâu**

* **Mục tiêu:** Nắm vững cơ chế ngắt, ngoại lệ và quản lý bộ nhớ.
* **Nội dung:**
* Phân tích **NVIC**, **PendSV**, và **SysTick timer**.
* Nghiên cứu cơ chế **Hardware Stacking** (tự động lưu ngữ cảnh).
* Tìm hiểu giá trị `EXC_RETURN` và con trỏ ngăn xếp (**MSP**, **PSP**).
* Viết code Assembly cơ bản thao tác thanh ghi.


* **Sản phẩm:**
* [ ] Code mẫu Assembly.
* [ ] Sơ đồ hoạt động của PendSV & SysTick.



#### **Tuần 3: Thiết kế kiến trúc RTOS và viết driver LED**

* **Mục tiêu:** Xây dựng cấu trúc tổng thể và driver ngoại vi.
* **Nội dung:**
* Thiết kế kiến trúc phân lớp: Kernel -> Scheduler -> HAL.
* Định nghĩa **Task Control Block (TCB)**.
* Viết driver GPIO trực tiếp qua thanh ghi cho LED đơn & LED 7 đoạn.


* **Sản phẩm:**
* [ ] Tài liệu thiết kế (Class/Sequence diagram).
* [ ] Driver LED đơn và LED 7 đoạn hoạt động độc lập.



---

### 🧠 GIAI ĐOẠN 2: TRIỂN KHAI LÕI RTOS (Tuần 4-7)

#### **Tuần 4: Xây dựng cấu trúc dữ liệu và quản lý tác vụ**

* **Mục tiêu:** Hoàn thiện TCB và các hàm quản lý tác vụ.
* **Nội dung:**
* Triển khai `RTOS_CreateTask()`: Cấp phát và giả lập Stack ban đầu cho task.
* Xây dựng mảng quản lý TCB và hàm `RTOS_Init()`.
* Kiểm thử tạo 2 task đơn giản, in thông báo qua UART.


* **Sản phẩm:**
* [ ] Code hoàn chỉnh TCB & Task Creation.



#### **Tuần 5: Triển khai bộ lập lịch (Scheduler) cơ bản**

* **Mục tiêu:** Xây dựng thuật toán lập lịch **Round-Robin**.
* **Nội dung:**
* Xây dựng **Ready Queue**.
* Viết hàm `Scheduler_GetNextTask_RoundRobin()`.
* Quản lý trạng thái Task: `READY`, `RUNNING`, `BLOCKED`.


* **Sản phẩm:**
* [ ] Code bộ lập lịch hoạt động ổn định trên mô phỏng.



#### **Tuần 6: Xây dựng cơ chế chuyển đổi tác vụ (Context Switching)**

* **Mục tiêu:** Triển khai cơ chế chuyển đổi ngữ cảnh bằng Assembly.
* **Nội dung:**
* Viết **PendSV Handler**: Lưu và phục hồi các thanh ghi R4-R11.
* Sử dụng SysTick để kích hoạt PendSV định kỳ.
* Xử lý chuyển đổi giữa các stack (PSP).


* **Sản phẩm:**
* [ ] Kernel có khả năng nhảy qua lại giữa 2 task.
* [ ] Video demo chuyển đổi task qua LED.



#### **Tuần 7: Hoàn thiện Kernel và RTOS_Start()**

* **Mục tiêu:** Tích hợp và chạy Kernel lần đầu tiên.
* **Nội dung:**
* Viết hàm `RTOS_Start()`: Cấu hình `CONTROL` register để dùng PSP.
* Triển khai hàm `RTOS_Delay()` cơ bản dựa trên SysTick.
* Tối ưu hóa thời gian Context Switch.


* **Sản phẩm:**
* [ ] Bản Kernel v1.0 chạy được đa nhiệm.



---

### 🛠️ GIAI ĐOẠN 3: ỨNG DỤNG VÀ MỞ RỘNG (Tuần 8-12)

#### **Tuần 8 & 9: Phát triển ứng dụng thực tế**

* **Tuần 8:** Task LED đơn nhấp nháy 1Hz bằng `RTOS_Delay()`.
* **Tuần 9:** Task LED 7 đoạn quét động, hiển thị số đếm 0-9 đồng thời với LED đơn.
* **Sản phẩm:**
* [ ] Hệ thống đa nhiệm hoàn chỉnh điều khiển song song các loại LED.



#### **Tuần 10: Mở rộng tính năng nâng cao**

* **Nội dung:**
* Cài đặt **Priority-based Scheduling**.
* Thêm cơ chế đồng bộ: **Semaphore** & **Mutex**.
* Xử lý vấn đề Priority Inversion (Nghịch đảo độ ưu tiên).



#### **Tuần 11: Tối ưu hóa và Kiểm tra lỗi (Stress Test)**

* **Mục tiêu:** Đảm bảo hệ thống vận hành bền bỉ.
* **Nội dung:**
* Kiểm tra Stack Overflow cho từng Task.
* Đo đạc thời gian đáp ứng ngắt (Interrupt Latency).
* Fix lỗi tranh chấp tài nguyên khi chạy nhiều task cường độ cao.


* **Sản phẩm:**
* [ ] Báo cáo đánh giá hiệu năng hệ thống.



#### **Tuần 12: Hoàn thiện tài liệu và Đóng gói**

* **Mục tiêu:** Chuẩn bị bàn giao và trình bày.
* **Nội dung:**
* Hoàn thiện mã nguồn (Comment sạch sẽ theo chuẩn Doxygen).
# Lộ trình 12 tuần: Tự xây dựng RTOS từ Bare-metal đến Multi-threading

> Mục tiêu: Tự tay xây dựng một RTOS (Real-Time Operating System) hoàn chỉnh từ con số 0, hiểu sâu kiến trúc ARM Cortex-M, cơ chế context switch, bộ lập lịch và ứng dụng thực tế.

---

## Phần 1: Nền tảng Bare-metal & Khởi động (Tuần 1–3)

### Tuần 1: Môi trường & Semihosting

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Cài đặt toolchain `arm-none-eabi-gcc`, OpenOCD, trình debug (ST-Link/J-Link) | ✅ Build và debug thành công chương trình trên hardware thực |
| ✅ Viết chương trình C tối giản in "Hello World" qua semihosting | ✅ File `main.c`, `startup.s`, `linker.ld` được kiểm soát hoàn toàn |
| ✅ Đọc và giải thích từng phần của linker script (`.ld`) | ✅ Giải thích được luồng: reset vector → `Reset_Handler` → `main()` |

---

### Tuần 2: Giao tiếp ngoại vi nguyên thủy

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Viết driver USART chỉ bằng thao tác thanh ghi (không HAL/LL) | ✅ Module `uart.c` và `uart.h` tự viết |
| ✅ Cấu hình RCC bật xung cho USART, GPIO | ✅ Hiểu và vẽ được sơ đồ Clock Tree cho USART |
| ✅ Gửi chuỗi "UART works\r\n" ra console (115200 bps) | ✅ Debug thành công giao tiếp UART |

---

### Tuần 3: Kiến trúc ARM Cortex-M & Assembly

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Viết lại file `startup.s` thủ công (vector table, Reset_Handler) | ✅ File `startup.s` tự viết, biên dịch và chạy đúng |
| ✅ Sử dụng assembly Thumb-2 để thực hiện phép tính và gọi hàm C | ✅ Hiểu rõ cách CPU lấy vector table, thiết lập SP, nhảy vào `main` |
| ✅ Chuẩn bị nền tảng cho context switch | ✅ Sẵn sàng cho các tuần tiếp theo |

---

## Phần 2: Cấu trúc Hệ điều hành & Đa nhiệm (Tuần 4–6)

### Tuần 4: Phân quyền & Lời gọi hệ thống

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Phân biệt Thread mode (unprivileged) và Handler mode (privileged) | ✅ Hiểu rõ cơ chế phân quyền qua CONTROL register |
| ✅ Viết lệnh SVC bằng assembly inline | ✅ Chương trình có `SVC_Handler` xử lý đúng |
| ✅ Thực hiện lệnh đặc quyền (ví dụ: ghi NVIC) | ✅ Hiểu rõ cơ chế system call trong RTOS |

---

### Tuần 5: Đa nhiệm hợp tác – Cooperative Multitasking

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Tạo hai task chạy luân phiên qua hàm `yield()` | ✅ Hai task in ký tự xen kẽ, chạy ổn định |
| ✅ Thực hiện context saving cơ bản (lưu R4–R11) | ✅ Hiểu rõ điểm khác biệt giữa cooperative và preemptive |

---

### Tuần 6: Trái tim của RTOS – Ngắt định thời SysTick

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Cấu hình SysTick timer ngắt mỗi 1ms | ✅ Đo và xác nhận chính xác tần số 1ms bằng oscilloscope/toggle GPIO |
| ✅ Trong handler, tăng `os_tick_count` và đặt cờ | ✅ Hệ thống có nền tảng thời gian cho bộ lập lịch |

---

## Phần 3: Ứng dụng phần cứng & Bộ lập lịch (Tuần 7–9)

### Tuần 7: Ứng dụng thực tế – Quét LED

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Cấu hình GPIO cho LED đơn và LED 7 thanh | ✅ Phần cứng hiển thị ổn định, không nhấp nháy |
| ✅ Đưa thuật toán quét LED vào `SysTick_Handler` (không dùng `delay()`) | ✅ Hiểu cách RTOS quản lý tác vụ thời gian thực |
| ✅ LED đơn nhấp nháy, LED 7 thanh hiển thị số thay đổi | ✅ Hoàn chỉnh ứng dụng đa nhiệm trên phần cứng |

---

### Tuần 8: Lập lịch ưu tiên – Preemptive Scheduling

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Kích hoạt ngắt PendSV để thực hiện context switch | ✅ Hai task chạy xen kẽ tự động, không cần `yield()` |
| ✅ Trong `SysTick_Handler`, kích hoạt PendSV | ✅ Hiểu rõ cơ chế: SysTick → PendSV → Context Switch |
| ✅ `PendSV_Handler` thực hiện chuyển task | ✅ Bộ lập lịch ưu tiên hoạt động ổn định |

---

### Tuần 9: Tối ưu hóa Context Switch bằng Assembly

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Viết lại `PendSV_Handler` hoàn toàn bằng assembly | ✅ Context switch tối ưu chu kỳ xung nhịp |
| ✅ Push/pop đầy đủ R0–R3, R12, LR, PC, xPSR (hardware-stacked) và R4–R11 (software-stacked) | ✅ Hoạt động ổn định, đảm bảo atomic bằng `CPSID`/`CPSIE` |
| ✅ Sẵn sàng mở rộng quản lý nhiều task | ✅ Nền tảng vững chắc cho RTOS hoàn chỉnh |

---

## Phần 4: Hoàn thiện & Chuẩn hóa (Tuần 10–12)

### Tuần 10: Quản lý luồng cấp cao – Threads

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Định nghĩa cấu trúc `TCB` (sp, priority, state, next) | ✅ Hệ thống chạy 3–4 task độc lập, chuyển đổi Round-Robin |
| ✅ Xây dựng bộ lập lịch Round-Robin với danh sách liên kết | ✅ Cấu trúc RTOS rõ ràng, dễ mở rộng |
| ✅ API `os_create_task()` tạo task mới | ✅ Quản lý task chuyên nghiệp |

---

### Tuần 11: Trừu tượng hóa phần cứng với CMSIS

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Tích hợp CMSIS-Core vào project | ✅ Code sạch, ít phụ thuộc vào STM32 cụ thể |
| ✅ Refactor code thao tác thanh ghi sang CMSIS API (`NVIC_SetPriority`, `SysTick_Config`, ...) | ✅ Dễ dàng port sang các chip Cortex-M khác (LPC, nRF, ...) |

---

### Tuần 12: Tổng duyệt & Mở rộng hướng IoT

| Yêu cầu | Kết quả |
|---------|--------|
| ✅ Kiểm tra hệ thống hoạt động ổn định 24h | ✅ RTOS hoàn chỉnh, ổn định, sẵn sàng cho dự án thực tế |
| ✅ Phân tích stack usage, độ trễ context switch bằng debugger | ✅ Hiểu sâu về hiệu năng và tài nguyên |
| ✅ Thiết kế ứng dụng IoT nhỏ (cảm biến + radio + LED) chạy trên RTOS tự viết | ✅ Nắm vững cách RTOS giải quyết vấn đề trong hệ thống phức tạp, tránh treo khi xử lý đa luồng |

---

## 📌 Tổng kết

Sau 12 tuần, bạn sẽ có:

- ✅ Một RTOS **hoàn chỉnh, tự viết 100%** từ bare-metal
- ✅ Hiểu sâu **kiến trúc ARM Cortex-M, assembly, cơ chế ngắt, context switch**
- ✅ Khả năng **port RTOS sang các vi điều khiển Cortex-M khác**
- ✅ Nền tảng vững chắc để phát triển **firmware phức tạp, IoT nodes, hệ thống thời gian thực**

---

## 🛠️ Công nghệ sử dụng

| Thành phần | Công nghệ |
|------------|-----------|
| Vi điều khiển | STM32 (Cortex-M3/M4) |
| Toolchain | `arm-none-eabi-gcc`, OpenOCD, Makefile |
| Ngôn ngữ | C, Assembly (Thumb-2) |
| Thư viện | CMSIS (tuần 11 trở đi) |
| Debug | Semihosting, UART, OpenOCD, GDB |

---

## 📁 Cấu trúc dự án (dự kiến)
<img width="348" height="683" alt="image" src="https://github.com/user-attachments/assets/8169adc9-92a7-40ec-a34e-a200ff8cae64" />

---

https://github.com/jserv/mini-arm-os?fbclid=IwY2xjawQhESNleHRuA2FlbQIxMABicmlkETFwR1RtaFZVVFEyUFVJWEVSc3J0YwZhcHBfaWQQMjIyMDM5MTc4ODIwMDg5MgABHqPadw6MhEAyE_3gPT7rVmPEpyxlWzY8yGl4imvajrrF6q9OD0yE9_Fxb7Fb_aem_SHf99d-15D3CUu0KHoPBAA

https://github.com/Thanhlearningcode/RTOS-BKTECH-COUSRE?fbclid=IwY2xjawQhEUNleHRuA2FlbQIxMABicmlkETFwR1RtaFZVVFEyUFVJWEVSc3J0YwZhcHBfaWQQMjIyMDM5MTc4ODIwMDg5MgABHnLaYVlS02tGVjxDyjd1gQNNYkT7CW0X4IflkEburFLMrj-IXiW-lZEyfLzp_aem_sXy0Niaqh5lK5gnk3ygsLQ
