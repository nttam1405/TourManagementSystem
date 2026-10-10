# Hệ thống Điều hành Tour Du lịch & Đại lý Lữ hành Quốc tế (ĐT15)

Bài tập lớn môn Lập trình hướng đối tượng với C++.

## Mục tiêu
Quản lý tour trong nước, quốc tế và MICE; đặt tour có kiểm soát số chỗ (tránh overbooking); tính phụ thu và phí hoàn hủy theo ngày; xuất hợp đồng du lịch; lưu dữ liệu ra file CSV / nhị phân.

## Kiến trúc
| Thư mục | Vai trò |
|---|---|
| `include/core`, `src/core` | Thực thể nghiệp vụ: `TourDuLich` (abstract) -> `TourTrongNuoc`, `TourQuocTe`, `TourMICE`; `KhachHang`, `HuongDanVien`, `DichVuLienKet` -> `KhachSan`, `PhuongTien`, `Visa`; `HopDongTour`, `BookingTour` |
| `patterns/factory` | Factory Method: tạo booking theo loại tour |
| `patterns/prototype` | Prototype: nhân bản tour mẫu |
| `patterns/strategy` | Strategy: chính sách phụ thu và hoàn hủy theo ngày |
| `services` | Logic điều hành: `TourManager`, `BookingManager`, `CustomerManager` (Smart Pointers) |
| `storage` | Đọc/ghi CSV và nhị phân |
| `ui` | Menu console, kiểm tra dữ liệu nhập |
| `utils` | Tiện ích ngày tháng, ngoại lệ tự định nghĩa |
| `tests` | Kiểm thử overbooking, hoàn hủy, file I/O, factory, prototype, bộ nhớ |
| `docs` | UML, báo cáo LaTeX, slide, minh chứng Jira, biên bản họp |

## Build & chạy
```bash
mkdir build && cd build
cmake ..
cmake --build .
./tms            # Windows: tms.exe
```
Build kèm test: `cmake -DBUILD_TESTS=ON ..` rồi `ctest`.

## Quy ước làm việc nhóm
- Mỗi thành viên commit bằng tài khoản cá nhân, message theo dạng `feat: ...`, `fix: ...`, `refactor: ...`.
- Chia nhánh theo tính năng: `feature/<tên-chức-năng>`, gộp vào `main` qua Pull Request.
- Mỗi lớp gồm một cặp file `.h` (khai báo) và `.cpp` (cài đặt).
- Không commit file nhị phân, `build/`, file rác LaTeX.

## Thành viên
| Họ tên | MSSV | Phụ trách |
|---|---|---|
|  |  |  |
