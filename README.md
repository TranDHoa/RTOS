# 🚀 Kiến trúc Hệ điều hành Nhúng (RTOS) cho STM32 (ARM Cortex-M)

Dự án này tập trung vào việc xây dựng một hệ điều hành thời gian thực (RTOS) từ con số 0 trên dòng vi điều khiển STM32. Lộ trình được thiết kế trong 10 tuần, kết nối chặt chẽ giữa lý thuyết hệ điều hành và thực hành trên phần cứng ARM Cortex-M.

---

## 🏗️ Kiến trúc Hệ thống (File Structure)

Để đảm bảo tính linh hoạt và chuyên nghiệp, mã nguồn được chia làm 2 phần tách biệt:

### 1. Phần LÕI (Core - Độc lập phần cứng)
*Chỉ chứa logic C chuẩn, có thể mang sang các dòng chip khác.*
* `os_task.c / .h`: Quản lý danh sách Task (TCB) và cấp phát bộ nhớ.
* `os_kernel.c / .h`: Chứa thuật toán lập lịch (Scheduler).
* `os_ipc.c / .h`: Cơ chế giao tiếp (Semaphore, Mutex, Queue).

### 2. Phần GIAO TIẾP (Port - Phụ thuộc phần cứng)
*Can thiệp trực tiếp vào thanh ghi và kiến trúc ARM Cortex-M.*
* `os_port.c / .h`: Cấu hình SysTick, khởi tạo Stack giả (Fake Context).
* `os_port_asm.s`: Mã Assembly thực hiện chuyển ngữ cảnh (Context Switch).

---

## 📅 Lộ trình Phát triển 10 Tuần

### 🔹 Giai đoạn 1: Khởi động & Bare-Metal (Tuần 1 - 2)
**Mục tiêu:** Làm chủ quá trình Boot và Debug cơ bản.
- [ ] Tìm hiểu Vector Table và Startup file của ARM.
- [ ] Viết Driver UART (không dùng thư viện HAL quá sâu).
- [ ] Build hàm `printf()` tùy chỉnh để log dữ liệu.

### 🔹 Giai đoạn 2: Quản lý Task & Stack (Tuần 3 - 4)
**Mục tiêu:** Định nghĩa "hình hài" của một tiến trình.
- [ ] Thiết kế cấu trúc **TCB (Task Control Block)**.
- [ ] Phân chia vùng nhớ RAM thành các phân đoạn Stack riêng biệt.
- [ ] Viết hàm `port_init_stack()`: Nạp sẵn địa chỉ hàm (PC) và trạng thái (xPSR) vào Stack.



### 🔹 Giai đoạn 3: Trái tim & Bộ não OS (Tuần 5 - 6) 🚩 Cột mốc quan trọng
**Mục tiêu:** Thực hiện đa nhiệm (Multitasking).
- [ ] Cấu hình **SysTick Timer** tạo ngắt mỗi 1ms (OS Tick).
- [ ] Cài đặt thuật toán lập lịch **Round-Robin** trong `os_kernel.c`.
- [ ] Viết trình xử lý ngắt **PendSV** bằng Assembly để tráo đổi thanh ghi giữa các Task.

### 🔹 Giai đoạn 4: Đồng bộ & Giao tiếp (Tuần 7 - 8)
**Mục tiêu:** Giải quyết xung đột tài nguyên (Race Condition).
- [ ] Triển khai **Mutex** và **Semaphore** để bảo vệ tài nguyên dùng chung (như UART).
- [ ] Xây dựng hàm `task_sleep()` để đưa Task vào trạng thái *Blocked*.
- [ ] Xử lý bài toán lập lịch ưu tiên (Priority-based Scheduling).

### 🔹 Giai đoạn 5: Ứng dụng & Tối ưu (Tuần 9 - 10)
**Mục tiêu:** Hoàn thiện sản phẩm thực tế.
- [ ] Chạy Demo đa nhiệm: Task 1 (Đọc cảm biến), Task 2 (Xử lý), Task 3 (Hiển thị/LED).
- [ ] Đo lường hiệu suất CPU (CPU Utilization).
- [ ] Đóng gói thư viện và viết tài liệu hướng dẫn.

---

## 🛠️ Công cụ hỗ trợ
* **Hardware:** STM32 (Dòng F1 hoặc F4).
* **IDE/Compiler:** PlatformIO / Keil C / STM32CubeIDE.
* **Debugger:** ST-Link V2.

