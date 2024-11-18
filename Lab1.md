# LAB 1  
## PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG  

---

## 1. Đề Xuất Kiến Trúc  

Hệ thống Payroll được đề xuất sử dụng kiến trúc **client-server**, bao gồm các thành phần chính:

- **Client**:
  - Chạy trên máy tính của nhân viên.
  - Cung cấp giao diện người dùng (UI) để nhập thông tin bảng chấm công, chọn phương thức thanh toán, và xem báo cáo.
  - Kết nối với server để gửi yêu cầu và nhận dữ liệu qua giao tiếp mạng (API).

- **Server**:
  - Đảm nhiệm xử lý nghiệp vụ, tính toán lương, kiểm tra bảng chấm công, và lưu trữ dữ liệu.
  - Gồm các module chính:
    - **Authentication Module**: Xác thực người dùng và phân quyền truy cập.
    - **Timecard Management**: Xử lý logic liên quan đến bảng chấm công.
    - **Payment Management**: Xử lý logic liên quan đến thanh toán.
    - **Database Interface**: Giao tiếp với cơ sở dữ liệu để lưu trữ và truy xuất thông tin.

- **Database Server**:
  - Chứa cơ sở dữ liệu chính của hệ thống Payroll, bao gồm thông tin nhân viên, bảng chấm công, và lịch sử thanh toán.
  - Tích hợp với **Project Management Database** (DB2 trên IBM mainframe) qua giao tiếp định sẵn để truy vấn thông tin dự án.

### Giải Thích Lý Do Lựa Chọn  

Kiến trúc **client-server** được lựa chọn vì:
- **Tính phân tách rõ ràng**: Client tập trung vào giao diện người dùng, còn server đảm nhiệm xử lý nghiệp vụ.
- **Tính mở rộng tốt**: Server có thể xử lý đồng thời hàng nghìn yêu cầu từ các client.
- **Tính bảo mật cao**: Xác thực và phân quyền được xử lý tại server.
- **Dễ dàng tích hợp**: Server có thể tích hợp với các hệ thống hiện tại như Cơ Sở Dữ Liệu Quản Lý Dự Án mà không cần thay đổi logic tại client.

### Biểu Đồ Package Mô Tả Kiến Trúc  
![Biểu Đồ Package Kiến Trúc Hệ Thống Payroll](https://www.planttext.com/api/plantuml/svg/X93D2e904CVl-nI3fpg8qB53M7a93Cg83k5XMWVPqdNRNGE9dgn3ZzGhf4QH47MScT__WxbVRxwng6sPPumfv0TC2Pnf9aXQ2B4YxS2P0MpNivXTFf0LwHFf3Z9MAXCShIWaX4KgU5SHeCKEtonsQ2XkXeKkziGjp57MTDx4l-xG2oQ3VclMr03N7NqBWo54T2p9M2yYemffY7t3MlaxkrLXucsqi3_u__LgesL9kWBrH0rZp2UPr9zz0000__y30000)

---

## 2. Cơ Chế Phân Tích  

Dưới đây là các cơ chế được đề xuất để giải quyết yêu cầu của hệ thống:

- **Persistency**: Lưu trữ và duy trì dữ liệu của nhân viên, timecard, và thông tin thanh toán.
- **Communication**: Đảm bảo giao tiếp giữa client và server qua giao thức từ xa.
- **Transaction Management**: Quản lý giao dịch, đặc biệt là xử lý các thao tác thanh toán để đảm bảo tính toàn vẹn dữ liệu.
- **Security**: Đảm bảo an toàn thông tin, ngăn chặn truy cập trái phép vào timecard hoặc thông tin nhân viên.
- **Redundancy**: Đảm bảo tính dự phòng để hệ thống hoạt động liên tục.
- **Legacy Interface**: Giao tiếp với cơ sở dữ liệu DB2 hiện tại.

## 3. Phân Tích Ca Sử Dụng: Select Payment Method  

### Xác Định Các Lớp Phân Tích  

Các lớp phân tích cho ca sử dụng này bao gồm:
- **Employee**: Đại diện cho nhân viên, lưu trữ thông tin cá nhân.
- **PaymentMethod**: Đại diện cho phương thức thanh toán. 
- **PaymentManager**: Chịu trách nhiệm xử lý logic thay đổi phương thức thanh toán.
- **DatabaseHandler**: Kết nối với cơ sở dữ liệu để lưu thông tin thanh toán.

### Biểu Đồ Sequence  
![Biểu Đồ Sequence cho Select Payment Method](https://www.planttext.com/api/plantuml/svg/Z9512i8m44NtESNGlHTm8Lsek154wG76PB2590tf5EdPN7Wahs3Isgh1WjlCU_zdaiVjdZUCdbkZ1KgkFMoCqtL795muhcJbq38Si3DaUOyMB-I_HcjaF6D3ExHA9xDH8ovh9SGO3OjLaWXBo4waIJ9Oke8RXc1wCHC97FIaDVf7GWMozJwQQKBAVzoW9sB0bbYMizq3DbVDhRV_bBtNVJagiByMdDuge8KB54tnELaL_-i9003__mC0)

### Nhiệm Vụ của Từng Lớp  

- **Employee**: Cung cấp thông tin cá nhân và yêu cầu thay đổi phương thức thanh toán.
- **PaymentMethod**: Lưu thông tin về các phương thức thanh toán.
- **PaymentManager**: Xử lý logic liên quan đến thay đổi phương thức thanh toán.
- **DatabaseHandler**: Xử lý thao tác đọc và ghi dữ liệu vào cơ sở dữ liệu.

### Biểu Đồ Lớp Mô Tả Phân Tích  
![Biểu Đồ Lớp cho Select Payment Method](https://www.planttext.com/api/plantuml/svg/Z5BB3W4n5DttAneh5c9l8HCPmeA8nmTSUiCaVKpQ8XFnPHO-oI_eLCbq2BhhkVUSS-zfRvThOYneknUSR3WOGmSYvwf0f2T2tLbOdSajnO2EMHML8B1wpw4GAEq4xKuz6WrotDXP5M-so9a4iwWGEmgFnNuFRFfqtUSCBFuK1mbRr47zCwUi781dN_LIiB06WoEGZBy4DGABA4EjHDeFeaUTrHINoXUTwYlfTgy-QvSs5ZwvPwHXzGQfDJfgVIp7dRkPEjxw3txy1ewzyX6zCHEKhFmcTm000F__0m00)

---

## 4. Phân Tích Ca Sử Dụng: Maintain Timecard  

### Xác Định Các Lớp Phân Tích  

Các lớp phân tích cho ca sử dụng này bao gồm:
- **Employee**: Đại diện cho nhân viên, nhập thông tin giờ làm việc.
- **Timecard**: Đại diện cho bản ghi giờ làm việc của nhân viên.
- **ProjectManager**: Quản lý và cung cấp danh sách mã số dự án.
- **TimecardManager**: Xử lý logic tạo và cập nhật timecard.
- **DatabaseHandler**: Kết nối với cơ sở dữ liệu để lưu timecard.

### Biểu Đồ Sequence  
![Biểu Đồ Sequence cho Maintain Timecard](https://www.planttext.com/api/plantuml/svg/R9712i8m38RlVOgmko_WGGGLl0YYWkVOHgrkwSmon6Vpu2Fv2dRer9NTIl9_-KZwl3_6bQ9eNUG6hGQ1ML7cuKPaobZsrfV82XjVa4Ln2sGya7HwKrJSOKLpP9SdlPRh59SIJcIrdMLQ8mn6gGY6aCrOu-CQvEpv0CTGIvMPD1VHxjY6ND6bfagXV7V01aUHJOBzrXLfBPoYFTfa_ORTYbS2_MJ1nKHcqjoVjc7MyVO_fjVqlLECJmBllHG_2R7ABJDZOjVyvGi00F__0m00)

### Nhiệm Vụ của Từng Lớp  

- **Employee**: Nhập thông tin giờ làm việc vào timecard.
- **Timecard**: Lưu trữ thông tin giờ làm việc và mã số dự án của nhân viên.
- **ProjectManager**: Tích hợp với cơ sở dữ liệu kế thừa để lấy danh sách mã số dự án.
- **TimecardManager**: Xử lý logic liên quan đến timecard, bao gồm việc kiểm tra và cập nhật.
- **DatabaseHandler**: Xử lý thao tác đọc và ghi dữ liệu vào cơ sở dữ liệu.

### Biểu Đồ Lớp Mô Tả Phân Tích  
![Biểu Đồ Lớp cho Maintain Timecard](https://www.planttext.com/api/plantuml/svg/V591JiCm4Bpx5LPES43SEQ0AMg27IXMK1opsAWGSErexL0ZnCWuyYI-mJXs7X41k7itCpkxaw-DpuGDGQ6iZb07lvQfkZ7j5b6z2ydSNgBAbn8IkzK_KGetT6sr0sbKrAY1zT2pUHNBhiR5RI6XoMq90sSM8z052gpEGb0sv9rJXqka3t3QQcNEJjmVc1YoKIEFvKvSImtQ0_Dm2Onz5E1uRmHSmrLzfU1zu08ytOBN9DkoYU_OLkNfvaQpsL0q-EzVXx9MxEJd_5UnC5glOWjmxUevBFhgMV26cF9PEmx3qbfESTbDpERFIt2ThxhlR_y-VjC2gQmpz_QMArox4WekEF-0t0000__y30000)

---

## 5. Hợp Nhất Kết Quả Phân Tích  

### Biểu Đồ Lớp Tổng Hợp  
Kết quả hợp nhất:
- Lớp chính: `Employee`, `Timecard`, `PaymentMethod`.
- Lớp xử lý nghiệp vụ: `TimecardManager`, `PaymentManager`.
- Lớp tích hợp: `ProjectManager` (giao tiếp với DB2).
- Lớp xử lý dữ liệu: `DatabaseHandler`.

![Biểu Đồ Lớp Tổng Hợp](https://www.planttext.com/api/plantuml/svg/Z5JBJiCm4BpxAwoSu82uSq0Lj3mEe8YM3rZYLHk8xSXsg2h4bt7Wa_W57CTEOZUqv9ICTsRMEwlyV7tFj05b6bwHeWAjwOBNbTmXqWz2xRCqgXHhYXwzPsDK0CVnTmqxZi8yeDd8hb1ZXON9n_Z9AVaatYmwY1svmsA_3diChatDmE1HSH2mHkNLfpdjoJjKvK6zEHXu0Ort85ZL2oe45b5kbEJpAo-wLMMYk9Bki5TTbHmBKCdjZKVz_QqrKXTKMpv0A5WFX0oKVBKZlvPiFAJWCkKS3wYm5uhgnxEPaiaxmrZbZsRMQF81qfrClt5dbsbc5pHRkWqAg-LN82D9eQMcyLZkaytct4Nm3twyYvRzx2QtnnotcuxGiXR2s9UjL6_j03QoKJeZQTtHTaF-azH-POOc3zOd2LdMBPgG3ItQ938oixlK_WL-0G00__y30000)

### Giải Thích  

Các lớp phân tích chính như `Employee`, `Timecard` và `PaymentMethod` cung cấp nền tảng lưu trữ và quản lý dữ liệu cốt lõi của hệ thống. Các lớp xử lý như `PaymentManager` và `TimecardManager` chịu trách nhiệm thực thi logic nghiệp vụ, đảm bảo tính nhất quán của dữ liệu và bảo mật hệ thống.

--- 

