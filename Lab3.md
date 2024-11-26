# **Biểu đồ ngữ cảnh hệ thống con - PrintService**

## **Các thành phần chính trong sơ đồ**

### **1. Bộ điều khiển tiền lương (<<control>>)**  
- **PayrollController** là thành phần khởi tạo của quy trình tính lương.  
- Tương tác với **IPrintService** qua phương thức `printPaycheck(aPaycheck: Paycheck)` để yêu cầu in phiếu lương.  
- Điều phối toàn bộ quy trình tính lương, bao gồm:  
  - Xác định thời điểm cần in phiếu lương.  
  - Truyền dữ liệu phiếu lương đến **PrintService**.  

---

### **2. IPrintService (<<Giao diện>>)**  
- Là giao diện định nghĩa hoạt động giao tiếp giữa **PayrollController** và **PrintService**.  
- **Hoạt động chính**:  
  - `printPaycheck(aPaycheck: Paycheck)`:  
    - Được gọi bởi **PayrollController** để bắt đầu quy trình in.  
    - Được triển khai bởi **PrintService** để thực hiện các thao tác in thực tế.  
- Cho phép kết nối lỏng lẻo để thay đổi hoặc mở rộng **PrintService** mà không cần sửa đổi **PayrollController**.  

---

### **3. PrintService (<<Proxy hệ thống con>>)**  
- **PrintService** là hệ thống con thực hiện các tác vụ in phiếu lương.  
- Triển khai giao diện **IPrintService**.  
- Chịu trách nhiệm:  
  - Xử lý thông tin từ **PayrollController** và **Paycheck** để in.  
  - Quản lý việc gửi lệnh in đến **Printer**.  
- Đóng vai trò là lớp trung gian để che giấu sự phức tạp của các tương tác in ấn.  

---

### **4. Paycheck (<<Thực thể>>)**  
- Đại diện cho dữ liệu phiếu lương của nhân viên.  
- **Nội dung chính**:  
  - Thông tin về nhân viên, lương, các khoản khấu trừ và tổng tiền.  
- Được **PrintService** sử dụng để trích xuất thông tin in ra phiếu lương.  

---

### **5. Printer (<<Thực thể>>)**  
- Biểu thị phần cứng hoặc hệ thống in bên ngoài (ví dụ: máy in vật lý).  
- **PrintService** gửi lệnh đến **Printer** để in phiếu lương thực tế.  
- **Hoạt động chính**: Nhận dữ liệu từ **PrintService** và chuyển thành bản in.

---

## **Các mối quan hệ và tương tác**

| Thành phần            | Quan hệ                                | Miêu tả tương tác                                                                                   |
|-----------------------|----------------------------------------|-----------------------------------------------------------------------------------------------------|
| **PayrollController** | -> **IPrintService**                  | Gọi phương thức `printPaycheck(aPaycheck: Paycheck)` để in phiếu lương.                             |
| **IPrintService**     | -> **PrintService**                   | **PrintService** triển khai giao diện **IPrintService**, cung cấp logic xử lý in.                   |
| **PrintService**      | -> **Paycheck**                       | Lấy thông tin từ thực thể **Paycheck** để in các chi tiết lương nhân viên.                          |
| **PrintService**      | -> **Printer**                        | Gửi lệnh đến máy in để tạo phiếu lương vật lý dựa trên dữ liệu từ **Paycheck**.                     |


---

### **Quy trình tương tác cụ thể**
1. **PayrollController** khởi chạy quy trình in bằng cách gọi `printPaycheck(aPaycheck: Paycheck)` từ giao diện **IPrintService**.  
2. **IPrintService** chuyển tiếp yêu cầu đến **PrintService**, nơi logic thực tế được thực hiện.  
3. **PrintService**:
   - Lấy thông tin từ thực thể **Paycheck** để trích xuất các chi tiết in (ví dụ: tên nhân viên, lương, v.v.).  
   - Gửi dữ liệu và lệnh đến thực thể **Printer** để tạo phiếu lương vật lý.  
4. **Printer** thực hiện in phiếu lương và hoàn thành quy trình.  

---

### **Biểu đồ ngữ cảnh**
![Diagram](https://www.planttext.com/api/plantuml/png/Z971Ri8m38RlVWeVuH1nHr65D2wx8V44MJ0GaQQLup8gs9Fjm2Fn2aiBZIZJfEKInx_pvRTp-xukeXYMflGWJZpXklc8RHGgyQqAGYV1fJCxDYKgNB4BiYO-Eai0rfiOSMLQhhplYhkTM6jxZui2pu1fpMR8JS3wNZcPmXT00X5lZILyVwO-RY3MNJAnxPxiOMA6Q8v3r5CU5fu1MiVSGStLgSqs_Wkba2RHvbm-S-yPu5V7g3RLPr35IolplzwRmhXGNzJBR4UoyhILHC-6nYgxtRwN1tyB2flkFty0003__mC0)

# **Biểu đồ ngữ cảnh hệ thống con - ProjectManagementDatabase**

## **Các thành phần chính**

### **1. Employee (<<actor>>)**  
- Người dùng chính của hệ thống, đại diện cho nhân viên tương tác với các hệ thống con:
  - Quản lý các nhiệm vụ thông qua **TimeManagementSystem**.
  - Yêu cầu báo cáo thông qua **ReportGenerator**.

---

### **2. TimeManagementSystem (<<control>>)**  
- Thành phần chịu trách nhiệm quản lý và xử lý nhiệm vụ của nhân viên.  
- **Chức năng chính**:  
  - Tạo, cập nhật và gửi các **TaskCard**.

---

### **3. ReportGenerator (<<control>>)**  
- Thành phần đảm nhận việc tạo và lưu báo cáo phân tích.
- **Chức năng chính**:  
  - Tạo báo cáo từ dữ liệu nhiệm vụ và lưu thông tin vào cơ sở dữ liệu.

---

### **4. TaskCard (<<entity>>)**  
- Đại diện cho thông tin chi tiết về nhiệm vụ mà nhân viên thực hiện.  
- **Thông tin chứa**:  
  - Giờ làm việc (taskHours).  
  - Chi tiết nhiệm vụ (taskDetails).  
  - Trạng thái (status).  

---

### **5. AnalysisReport (<<entity>>)**  
- Đại diện cho các báo cáo phân tích được tạo bởi **ReportGenerator**.  
- **Thông tin chứa**:  
  - Loại báo cáo (reportCategory).  
  - Khung thời gian (timeFrame).  
  - Các nhiệm vụ liên quan (relatedTasks).  

---

### **6. ProjectManagementDatabase (<<subsystem proxy>>)**  
- Hệ thống con quản lý cơ sở dữ liệu, hỗ trợ xử lý và lưu trữ dữ liệu từ các nhiệm vụ và báo cáo.  
- **Chức năng chính**:  
  - Lưu và truy xuất dữ liệu nhiệm vụ từ **TaskDetails**.  
  - Lưu dữ liệu báo cáo được tạo bởi **ReportGenerator**.

---

### **7. TaskDetails (<<entity>>)**  
- Lưu trữ thông tin chi tiết liên quan đến các nhiệm vụ như:
  - Mã nhiệm vụ (taskID).
  - Thông tin dự án liên quan (projectInfo).

---

## **Các mối quan hệ và tương tác**

| Thành phần                  | Quan hệ                                  | Miêu tả tương tác                                                                     |
|-----------------------------|------------------------------------------|---------------------------------------------------------------------------------------|
| **Employee**                | -> **TimeManagementSystem**             | Quản lý và theo dõi nhiệm vụ thông qua **TaskCard**.                                  |
| **Employee**                | -> **ReportGenerator**                  | Yêu cầu tạo báo cáo phân tích dựa trên dữ liệu nhiệm vụ.                               |
| **TimeManagementSystem**    | -> **TaskCard**                         | Tạo, cập nhật và gửi dữ liệu nhiệm vụ.                                                |
| **ReportGenerator**         | -> **AnalysisReport**                   | Tạo và lưu báo cáo phân tích.                                                         |
| **TimeManagementSystem**    | -> **ProjectManagementDatabase**        | Truy xuất hoặc lưu trữ dữ liệu nhiệm vụ từ/đến cơ sở dữ liệu.                          |
| **ReportGenerator**         | -> **ProjectManagementDatabase**        | Lấy hoặc lưu thông tin báo cáo phân tích.                                             |
| **ProjectManagementDatabase** | -> **TaskDetails**                    | Lưu và truy xuất chi tiết thông tin nhiệm vụ cho hệ thống con khác.                   |

---

## **Quy trình tương tác cụ thể**

1. **Employee** khởi tạo tác vụ bằng cách tương tác với **TimeManagementSystem**.  
2. **TimeManagementSystem** quản lý các **TaskCard** và lưu dữ liệu vào **ProjectManagementDatabase**.  
3. **Employee** yêu cầu báo cáo từ **ReportGenerator**.  
4. **ReportGenerator** lấy dữ liệu từ **ProjectManagementDatabase**, tạo báo cáo và lưu nó dưới dạng **AnalysisReport**.  
5. Tất cả dữ liệu nhiệm vụ được lưu trong **TaskDetails**, đảm bảo thông tin sẵn sàng cho các quy trình sau.

---

![Diagram](https://www.planttext.com/api/plantuml/png/V59BJiCm4Dtx5Du1YzoWYeeIFbqW8TeBJDkX61mxcfcWHgWdOy6Hk0BEnmqD3LbvVc_UUvFlpwyv2v1KXLLYnA9ULckkMR3GcNU2Uz6vWHr1eHFzIFuLD_803dPOe9CS1DR0gDJ60hE-AKhhQqGzcy56FALfhAnCWSFSijlGrvwmz2Htw90W36cbGekHMg-0tpAWhVvGklaanFU-8Xx270MCxHD1YbIi3aU0QmUsPiFTXWX3RPI1uCvJtMC5VhT19SOM6yhRXa2Brn6Tr1_qyj6talo-JjDXcv31TrmDR2-l8bzFe_pXH7oV_wr_aNVlikEoSC--6Re8BWRAnZj-CIMhuoMI99qm_wJbpmtEphHWyIXgFDDKHuvFmqnxUHRtd_RfKgGRRLHgZcxR_Ei_0000__y30000)


# Ánh xạ các lớp phân tích đến các phần tử thiết kế





## Subsystem: PrintService

| **Analysis Class**    | **Design Element**     |
|------------------------|------------------------|
| PayrollController      | PayrollController      |
| IPrintService          | IPrintService          |
| PrintService           | PrintService           |
| Paycheck               | Paycheck               |
| Printer                | Printer                |

---

## Subsystem: ProjectManagementDatabase

| **Analysis Class**        | **Design Element**        |
|----------------------------|---------------------------|
| Employee                  | Employee                 |
| TimeManagementSystem      | TimeManagementSystem     |
| ReportGenerator           | ReportGenerator          |
| TaskCard                  | TaskCard                 |
| AnalysisReport            | AnalysisReport           |
| ProjectManagementDatabase | ProjectManagementDatabase |
| TaskDetails               | TaskDetails              |
# Ánh xạ các lớp thiết kế vào các gói

## Subsystem: PrintService

| **Design Element**    | **Owning Package**                     |
|------------------------|----------------------------------------|
| PayrollController      | Applications::Payroll                 |
| IPrintService          | Middleware::Services::Printing        |
| PrintService           | Middleware::Services::Printing        |
| Paycheck               | BusinessServices::PayrollArtifacts    |
| Printer                | Hardware::Devices::Printer            |

---

# Subsystem: ProjectManagementDatabase

| **Design Element**        | **Owning Package**                           |
|----------------------------|----------------------------------------------|
| Employee                  | Applications::EmployeeManagement             |
| TimeManagementSystem      | Applications::TaskManagement                 |
| ReportGenerator           | Applications::Reporting                      |
| TaskCard                  | BusinessServices::TaskArtifacts              |
| AnalysisReport            | BusinessServices::ReportingArtifacts         |
| ProjectManagementDatabase | Middleware::DataManagement                   |
| TaskDetails               | BusinessServices::TaskArtifacts              |

#biểu đồ mô tả các layers
![Diagram](https://www.planttext.com/api/plantuml/png/R9FFRjim3CRlUWh1bvw2tNiecYNh7w05kcPz05PX4ZMov97q2gFOa_MmHzehZBQJHlAQYv6F-lYZIEhl-vzB5Y1fws34Iq2xwbYmjdVG8R65kBQF641yYhpp3HjpPfUuyH5jE1nXsu3RmnRPldhPsMSKGUh3gHLpYDdgWP0nof1gJ5_rta9-CrP_BW2p_LOt8NM8cVG07QKG5YbA_qKolyq9C6-QuDqqVwxcwN_u6kyXghDM_7ZhBFo8JIAvneW4aahGrvRr_dheBcszorZ7mAY_bPMx7RfzNW3mVW6qpgHvXD2nvn5UC9SWOEVE3TWFOAyUn896wGMTdAxNdti6nWb-YG8-S06wZHi25cgTj8GPQn8eUJxgo3FbTf1MIB-ympx_nzPGlat5mh3MuEDss3dDGbuwKsp7R9rUu-oY6EcvhLOuBEdF5bcuCdbq5d0ZwYW7evu5X63BELQcF7MaPJrMunMAstrPwKhW4FdFfOv9fzJrnFgmncPCA_oKyhr5wWRDBZtfA4DNcKdQe_FG_DvsewtJ9pmeTf7gMlyhprngX_eN_Wy00F__0m00)



