# Thực hành Oracle: quản lý nhân viên

Bộ script tạo bảng nhân viên và thực hành thêm, xem, cập nhật, xóa dữ liệu bằng Oracle SQL.

## Yêu cầu

- Đã cài đặt và khởi động Oracle Database (ví dụ Oracle Database XE).
- Có tài khoản kết nối vào schema đích và tài khoản đó có quyền `CREATE TABLE`, `INSERT`, `SELECT`, `UPDATE` và `DELETE`.
- Bảng dùng cột identity, yêu cầu Oracle Database 12c trở lên.

Oracle Database phải tồn tại trước. Trong Oracle, bảng được tạo trong schema của tài khoản đang kết nối; script này không tạo hoặc cấu hình máy chủ database hay tài khoản Oracle.

## Chạy trong SQL Developer

1. Tạo hoặc chọn một kết nối tới Oracle Database, rồi kết nối bằng tài khoản schema muốn dùng.
2. Mở `01_create_employees.sql` và chạy bằng **Run Script (F5)**. Script tạo bảng `NHAN_VIEN`, thêm ba nhân viên mẫu, commit dữ liệu và hiển thị danh sách.
3. Mở `02_crud_practice.sql` và chạy bằng **Run Script (F5)** để thực hiện lần lượt:
   - `INSERT`: thêm nhân viên `NV004`.
   - `SELECT`: xem danh sách.
   - `UPDATE`: cập nhật phòng ban, chức vụ và lương của `NV004`.
   - `DELETE`: xóa `NV004`.
   - `SELECT`: xác nhận nhân viên đã bị xóa.

Script thực hành commit sau mỗi thao tác ghi. Khi chạy xong toàn bộ, `NV004` đã bị xóa; ba nhân viên mẫu vẫn còn. Để quan sát kết quả ở từng bước, chạy từng câu lệnh hoặc từng phần trong SQL Developer thay vì chạy toàn bộ script một lần.

## Cấu trúc bảng

| Cột | Ý nghĩa |
| --- | --- |
| `MA_NV` | Khóa chính tự tăng |
| `MA_NHAN_VIEN` | Mã nhân viên, không được trùng |
| `HO_TEN` | Họ tên |
| `GIOI_TINH`, `NGAY_SINH` | Giới tính, ngày sinh |
| `PHONG_BAN`, `CHUC_VU` | Phòng ban, chức vụ |
| `LUONG` | Lương, không được âm |
| `EMAIL`, `SO_DIEN_THOAI` | Thông tin liên hệ |
| `NGAY_TAO`, `NGAY_CAP_NHAT` | Thời điểm tạo và cập nhật bản ghi |

`NGAY_CAP_NHAT` được cập nhật tường minh trong câu lệnh `UPDATE`; nếu viết câu cập nhật khác, hãy đặt cột này thành `SYSTIMESTAMP` tương tự.

## Thực hành riêng từng câu lệnh

```sql
-- Them
INSERT INTO NHAN_VIEN (MA_NHAN_VIEN, HO_TEN, PHONG_BAN, CHUC_VU, LUONG)
VALUES ('NV005', 'Đỗ Minh Tâm', 'Kế toán', 'Nhân viên', 11000000);
COMMIT;

-- Xem
SELECT * FROM NHAN_VIEN ORDER BY MA_NV;

-- Sua
UPDATE NHAN_VIEN
SET LUONG = 12500000, NGAY_CAP_NHAT = SYSTIMESTAMP
WHERE MA_NHAN_VIEN = 'NV005';
COMMIT;

-- Xoa: kiểm tra điều kiện WHERE trước khi chạy
DELETE FROM NHAN_VIEN
WHERE MA_NHAN_VIEN = 'NV005';
COMMIT;
```

Chỉ chạy `01_create_employees.sql` một lần trên schema mới. Script không tự xóa bảng cũ; nếu bảng `NHAN_VIEN` đã tồn tại, hãy chọn schema khác hoặc xử lý bảng hiện có sau khi sao lưu dữ liệu cần giữ.
