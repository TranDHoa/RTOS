# RTOS - Thiết kế và triển khai lõi hệ điều hành đa nhiệm thời gian thực (RTOS) từ mức thanh ghi trên vi điều khiển ARM Cortex-M ứng dụng vào điều khiển led 7 thanh và led đơn

Chào bạn! Ý tưởng tự xây dựng một RTOS từ con số 0 trên dòng STM32F4 là một thử thách cực kỳ thú vị và giúp nâng trình kiến thức về System Architecture lên rất nhiều.

Dưới đây là nội dung kế hoạch 12 tuần của bạn đã được tối ưu hóa theo định dạng **Markdown (`README.md`)** chuyên nghiệp để bạn có thể đưa thẳng lên GitHub. Tôi đã bổ sung thêm 2 tuần cuối (Tuần 11-12) để hoàn thiện đúng lộ trình 12 tuần như tiêu đề bạn mong muốn.

---

# 🚀 STM32 Custom RTOS Development Project

Dự án xây dựng Hệ điều hành thời gian thực (RTOS) từ cơ bản dành cho dòng vi điều khiển **STM32F4 (ARM Cortex-M4)**.

---

## 📅 Lộ Trình Thực Hiện (12 Tuần)

### 🏗️ GIAI ĐOẠN 1: NGHIÊN CỨU NỀN TẢNG VÀ THIẾT KẾ KIẾN TRÚC (Tuần 1-3)

#### **Tuần 1: Nghiên cứu tổng quan và thiết lập môi trường**

* **Mục tiêu:** Hiểu rõ yêu cầu đề tài, chuẩn bị công cụ phát triển.
* **Nội dung:**
* Tìm hiểu khái niệm, phân loại và ứng dụng của RTOS.
* Nghiên cứu kiến trúc **ARM Cortex-M**: Tập thanh ghi, chế độ Thread mode & Handler mode.
* Đọc Datasheet/Reference Manual của **STM32F4xx**.
* Cài đặt: STM32CubeIDE/Keil uVision, toolchain ARM GCC.
* Chuẩn bị phần cứng: Board STM32F4 Discovery, LED, điện trở.


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
* Viết hướng dẫn sử dụng API (API Reference).
* Quay video demo tổng quát tất cả tính năng.


* **Sản phẩm:**
* [ ] Toàn bộ Source Code & Tài liệu hướng dẫn trên GitHub.



---

## 🛠 Yêu cầu phần cứng & phần mềm

| Loại | Chi tiết |
| --- | --- |
| **Vi điều khiển** | STM32F4 Discovery (ARM Cortex-M4) |
| **Công cụ nạp** | ST-Link V2 |
| **Phần mềm** | STM32CubeIDE / Keil uVision |
| **Ngôn ngữ** | C, Assembly (ARM Cortex-M) |

---

https://github.com/jserv/mini-arm-os?fbclid=IwY2xjawQhESNleHRuA2FlbQIxMABicmlkETFwR1RtaFZVVFEyUFVJWEVSc3J0YwZhcHBfaWQQMjIyMDM5MTc4ODIwMDg5MgABHqPadw6MhEAyE_3gPT7rVmPEpyxlWzY8yGl4imvajrrF6q9OD0yE9_Fxb7Fb_aem_SHf99d-15D3CUu0KHoPBAA

https://github.com/Thanhlearningcode/RTOS-BKTECH-COUSRE?fbclid=IwY2xjawQhEUNleHRuA2FlbQIxMABicmlkETFwR1RtaFZVVFEyUFVJWEVSc3J0YwZhcHBfaWQQMjIyMDM5MTc4ODIwMDg5MgABHnLaYVlS02tGVjxDyjd1gQNNYkT7CW0X4IflkEburFLMrj-IXiW-lZEyfLzp_aem_sXy0Niaqh5lK5gnk3ygsLQ
