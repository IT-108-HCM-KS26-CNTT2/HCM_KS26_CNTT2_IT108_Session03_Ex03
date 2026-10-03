## **Ràng buộc & Bẫy dữ liệu**

- Điều gì xảy ra nếu sinh viên cố gắng kết thúc (End Task) một tiến trình (Process) có tên là **System**?

\-> Tiến trình system là tiến trình của hệ điều hành đại diện cho nhân của hệ điều hành (Kernel), nên khi bấm end task thì thường máy tính sẽ báo lỗi hoặc không hiển thị nút end task. Nhưng nếu vẫn tìm cách để end task thì máy tính sẽ ngay lập tức bị sập và khởi động lại nếu dữ liệu chưa lưu thì sẽ bị mất.

- Dự đoán sự khác biệt về hiệu suất khi RAM đầy nếu máy sử dụng ổ SSD so với HDD (liên quan đến Swap file).
- Khi máy sử dụng quá nhiều tài nguyên và dẫn đến bị tràn RAM lúc này dữ liệu trên RAM sẽ được đưa vô phân vùng RAM ảo từ ổ cứng SSD hoặc HDD lúc này sẽ xảy ra hiện tượng giật lag. Tuy nhiên ổ SSD sẽ đỡ lag hơn ổ HDD vì ổ HDD có tốc độ đọc thông tin rất thấp chỉ từ 80MB-160MB/s còn ổ SSD đọc nhanh hơn rất nhiều từ 500MB-7300MB/s tuỳ loại phân khúc SATA(phân khúc thấp) hay NVme(phân khúc cao cấp).

**Yêu cầu đầu ra**

- **Báo cáo phân tích:** Giải thích hiện tượng giật lag dựa trên chức năng Quản lý tiến trình và Quản lý bộ nhớ của hệ điều hành.

\->

\- Quản lý bộ nhớ:Chrome khi bật lên nhiều tab thì máy tính phân cấp phân vùng RAM cho nó và còn chạy thêm các tiện ít, VS Code khi chạy phải cấp phân vùng RAM để chạy và còn chạy thêm các tiện ít. Hai phần mềm này vốn tốn RAM, cộng với dịch vụ nền của Windows nên RAM lên 95%. Khi RAM gần cạn, Kernel buộc phải dùng swap file, nên dữ liệu liên tục bị chuyển giữa RAM và ổ đĩa.

\- Quản lý tiến trình: có quá nhiều tiến trình cùng chờ CPU và CPU không thể xử lý cùng 1 lúc nên sẽ chia nhỏ thời gian CPU cho từng tiến trình và tiến trình thường xuyên bị chặn để chờ dữ liệu từ ổ đĩa nên thao tác của người dùng bị phản hồi trễ.

- **Sơ đồ:** Vẽ sơ đồ phân tầng (Architecture Layers) từ User đến Hardware cho hành động

Tầng 1: Khi click đúp vào biểu tượng trình duyệt

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR4XmP4//8/AwAI/AL+GwXmLwAAAABJRU5ErkJggg==)

Tầng 2: Shell: Nhận yêu cầu và dịch cho hệ tầng dưới biết yêu cầu chạy file

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR4XmP4//8/AwAI/AL+GwXmLwAAAABJRU5ErkJggg==)

Tầng 3: kernel: Quản lý tiến trình: tạo Process, xếp CPU-> Quản lý bộ nhớ: cấp RAM, swap file -> File System: tìm file .exe của trình duyệt (ví dụ: chrome.exe) trên ổ đĩa -> Device Drivers: giao tiếp phần cứng

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR4XmP4//8/AwAI/AL+GwXmLwAAAABJRU5ErkJggg==)

TẦNG 4: HAL (Hardware Abstraction Layer): Che giấu khác biệt giữa các loại phần cứng

![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR4XmP4//8/AwAI/AL+GwXmLwAAAABJRU5ErkJggg==)

TẦNG 5: HARDWARE: CPU, RAM, SSD/HDD, GPU, Màn hình