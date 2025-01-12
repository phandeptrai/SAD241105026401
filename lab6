# 📑Phân Tích Thiết Kế Hệ Thống **Payroll System**

## 1. Phân Tích Các Lớp Và Mối Quan Hệ

### 1.1. Subsystem: User Management
- **Chức năng:** Quản lý thông tin người dùng, xác thực và phân quyền truy cập.
- **Các lớp chính:**
  - **`User`**  
    Chứa thông tin đăng nhập của người dùng (username, password).  
  - **`UserProfile`**  
    Chứa thông tin cá nhân của người dùng (tên, địa chỉ, số điện thoại).  
  - **`AuthenticationManager`**  
    Xử lý xác thực người dùng và kiểm tra quyền hạn.

- **Mối quan hệ:**
  - `User` có mối quan hệ **1-1** với `UserProfile`.
  - `AuthenticationManager` sử dụng `User` để xác thực và quản lý quyền.

---

### 1.2. Subsystem: Payroll Processing
- **Chức năng:** Tính toán và quản lý bảng lương của nhân viên.  
- **Các lớp chính:**
  - **`PayrollRecord`**  
    Chứa thông tin lương như: lương cơ bản, thưởng, khấu trừ, tổng lương.  
  - **`PayrollCalculator`**  
    Tính toán bảng lương dựa trên thời gian làm việc và quy tắc khấu trừ.  
  - **`PayrollManager`**  
    Quản lý việc tạo và cập nhật các bản ghi bảng lương.  

- **Mối quan hệ:**
  - `PayrollCalculator` tạo ra các `PayrollRecord`.
  - `PayrollManager` quản lý và cập nhật các `PayrollRecord`.

---

### 1.3. Subsystem: Timecard Management
- **Chức năng:** Ghi nhận và quản lý thông tin chấm công của nhân viên.  
- **Các lớp chính:**
  - **`Timecard`**  
    Lưu trữ thông tin chấm công của từng nhân viên theo ngày, giờ làm việc.  
  - **`TimecardManager`**  
    Quản lý việc ghi nhận và truy xuất dữ liệu chấm công.  

- **Mối quan hệ:**
  - `TimecardManager` sử dụng `Timecard` để ghi nhận và quản lý thời gian làm việc.  
  - `Timecard` kết nối với `PayrollCalculator` để tính toán lương dựa trên giờ làm.

---

### 1.4. Subsystem: Reporting
- **Chức năng:** Tạo và xuất báo cáo về lương, giờ làm và hiệu suất làm việc.  
- **Các lớp chính:**
  - **`Report`**  
    Đại diện một báo cáo chứa dữ liệu đã tổng hợp.  
  - **`ReportManager`**  
    Quản lý việc tạo báo cáo và lập lịch xuất báo cáo.  

- **Mối quan hệ:**
  - `ReportManager` tạo các `Report` dựa trên dữ liệu từ `PayrollRecord` và `Timecard`.

---

### 1.5. Subsystem: Security
- **Chức năng:** Quản lý quyền truy cập và bảo mật hệ thống.  
- **Các lớp chính:**
  - **`Permission`**  
    Đại diện các quyền truy cập trong hệ thống.  
  - **`SecurityManager`**  
    Xử lý xác thực, mã hóa dữ liệu và kiểm tra quyền truy cập.  

- **Mối quan hệ:**
  - `SecurityManager` sử dụng `Permission` để đảm bảo chỉ người dùng hợp lệ có thể truy cập dữ liệu.

---

### 1.6. Subsystem: Data Management
- **Chức năng:** Quản lý lưu trữ và đồng bộ dữ liệu.  
- **Các lớp chính:**
  - **`DatabaseManager`**  
    Quản lý việc lưu trữ và truy cập dữ liệu hệ thống (nhân viên, lương, chấm công).  
  - **`SynchronizationManager`**  
    Xử lý việc đồng bộ hóa dữ liệu với các hệ thống khác (ngân hàng, báo cáo).  

- **Mối quan hệ:**
  - `DatabaseManager` lưu trữ dữ liệu từ `PayrollRecord`, `Timecard`, và các lớp khác.
  - `SynchronizationManager` đảm bảo dữ liệu luôn đồng bộ giữa các hệ thống.

---

## 2. Biểu Đồ Lớp Tổng Quan

![2](https://www.planttext.com/plantuml/svg/T5HBZjim3Dth589N2T1Sm2W6CssMKpIOJD4r8tDYTMGf9QKftA8dww97wXKAsR8ZVx8poCV7H_B9__xy5VViWNneZ506cEKNHfA_X9HI1aQoq60fZvwqFNV12p3_S5IDmTyYgpoGUz464y6Y6AgAa7bAM3kBIxQ7u6kqNYlmsjbFOE4y2ZFkhEqcoYkxhjjIVd3E8DWkhMfKhmUaHZDhPpb3lfE4x0AfiMDME_O-G4lEc2TKZghKymICHp10RIdtBfmCzc5d0qyY5LP1HStJi0AZWW6Fpyw3sMp7vBphnmHqmxHZvSRh1XN4tJ-dhsqv5RjWcovE4OB7bDfWSp6kHIppqzrc77echWeybd8Flf-lTe7ugwDNh9QZ3QLJDHnEZVP3Rcsw3dR64PEVyghtKRD_Fq3khbsVyEB8fsPdj4ZWiGzkAl1Goi-dRwZyTkc-7hMsl5IlI7ia3PcD-ioLuuWgaFRjb0MjelRYz-0XYHW9iaVn1aR71JyeXPnFlMRNo1NjETikl67M9OtQfLxGgxhBVGyO3JrAw57P3ArLDJchVwuyGswjwbYsiQ3xSUnsTvF_G2cB6hWGwwzvG4SON178XLW-XWWUBLZA8d26oncdhxUKHTCbkH1p6-vcbBqXkH3JyqTOyb8fYzu6N8ZvVVDfXljn8URNMPN8tj4jy4HXmjsuIuJFAM9LQnKNGjoZhK9Z_WC00F__0m00)
