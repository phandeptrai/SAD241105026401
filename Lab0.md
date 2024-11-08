# LAB 0: Tài Liệu Thiết Kế Phần Mềm với GitHub và PlantText

## Mục đích
Trong lab này, chúng ta sẽ học cách sử dụng kết hợp **GitHub** và **PlantText** để tạo ra tài liệu thiết kế phần mềm chuyên nghiệp. Qua các sơ đồ Use Case và Class Diagram, tài liệu này sẽ cung cấp một cái nhìn tổng quan về hệ thống, giúp dễ dàng hiểu cách hệ thống vận hành và tổ chức các lớp (class) chính.

---

## 1. Biểu đồ Use Case



![Biểu đồ Use Case](https://www.planttext.com/api/plantuml/svg/T58nJiCm5DrzYg_iN06roi804aXjnLPPiML79D-LxS1GCJ4m0WT0Ac822OcLHeZ15VVm2RW2JaiJfu0dw_tttl_lsr_rny1OgcrL5eHcLcaO6wv_haDMvaY8vfcbA0eEoO6lhy5ANz-XI61E89pAy8oQK5pThgvG04g_V9abG0sCq-cX4i6Znplb9HY_V4IO1UfJkQLESdvnh1MhCclwYf5qptqDdBk50f7x-WQaMpJJR4o6Z8rK6XBjEb2KO9Lxm2qpbJmxKzKEyQHQTodSEw3uVFNrVGxClNKDZYXImPijcN-LVwNRwDfybuGq7h2ttsqf0dgxYF0kNWIsISZwnNgUCHAF_XjlsmquikO_V0C00F__0m00)

### Chi tiết
- **Actors**: Người dùng và hệ thống
- **Use Cases**: 
  - Đăng nhập
  - Xem sản phẩm
  - Thêm vào giỏ hàng
  - Quản lý sản phẩm
  - Thanh toán
- **Liên kết**: Đường kết nối giữa từng tác nhân với các use case cho thấy vai trò của mỗi người dùng đối với các chức năng hệ thống.

---

## 2. Biểu đồ Class Diagram


### Các thành phần chính:
- **Classes**: Bao gồm các lớp chính trong hệ thống và các thuộc tính, phương thức (methods) của chúng.
- **Mối quan hệ**: Các quan hệ như **kế thừa** (inheritance) và **kết hợp** (association) giữa các lớp.

![Biểu đồ Class Diagram](https://www.planttext.com/api/plantuml/svg/UhzxlqDnIM9HIMbk3XTNSavYSR52S5WrbuA2ScQAWfL2Pbu9Y9sNc9jgfL1SKfIPbmxY9wQdmYM12AX58pD51wHA1oYbQSt5LOimpJC4P9wklt-0bK9QJduYI9Dki2ionz550S456UWIugIX2HS3cSOL7APWKwEh2pQGoo4rBmNeP000003__mC0)

---

## 3. Biểu đồ Tương Tác (Sequence Diagram)

### Các bước trong Sequence Diagram:
1. Người dùng gửi yêu cầu.
2. Hệ thống xử lý yêu cầu qua các bước.
3. Kết quả được trả về cho người dùng.

![Sequence Diagram](https://www.planttext.com/api/plantuml/svg/N51DIiD05DxFAJwwB-wpa2O450mII0Mtqsb81kqaJbv4rrswyW22HKGG2WfkJ1PTfFGUSmAlu4nQi7Ntvds_RtxQrQWYhgcUNJCkgD2ug5BDIhkIGfPS4GPHaKc5c6Vf0Bn251_2VarvgkoRaomKabJVIh6b-iaXDUJ49xpQWc70c0l3yDXwUZZFJRCiGNdtfJAGZLm_hkTsL3t0ejWn_SJ3YMcN4lVTUmrXchSQTzr2MA5fFmNp4qSB0mzdqhJp6KZpVLELRJvC-oGnxRvLni80mvtjM9lc1LUcMH5kQZV_zzqrlVnRE-TdbKCu_wEnRVfAc9Xc8Vk-Lk1Ez73gkgXUzB0VmKQfchhF_mK00F__0m00)

