
# THIẾT KẾ CANTEEN API

## 1. Mô tả hệ thống

Hệ thống Canteen API quản lý thực đơn căng tin trường học.

Sinh viên có thể xem, lọc và tìm kiếm món ăn.
Nhân viên có thể thêm, sửa và xóa món ăn.

## 2. Đặc tả tài nguyên MenuItem

| Trường | Kiểu dữ liệu | Ràng buộc |
|---|---|---|
| id | int | Tự động tăng |
| name | str | 2-100 ký tự, không trùng tên |
| category | enum | com, bun_pho, do_uong, an_vat |
| price | int | > 0, <= 200000, chia hết cho 1000 |
| available | bool | Mặc định true |
| updated_at | datetime | Tự động cập nhật |

## 3. Danh sách Endpoint

| Method | URI | Thành công | Lỗi |
|---|---|---|---|
| GET | /menu-items | 200 | 422 |
| GET | /menu-items/{id} | 200 | 404, 422 |
| POST | /menu-items | 201 | 409, 422 |
| PUT | /menu-items/{id} | 200 | 404, 409, 422 |
| PATCH | /menu-items/{id} | 200 | 404, 409, 422 |
| DELETE | /menu-items/{id} | 204 | 404 |

## 4. Query Parameters

GET /menu-items hỗ trợ:

- category: lọc loại món
- available: lọc món còn bán/hết
- max_price: lọc mức giá tối đa
- sort: id, price, name
- order: asc, desc

## 5. Quy tắc nghiệp vụ

BR1: Tên món duy nhất, không phân biệt chữ hoa và chữ thường.

BR2: Giá lớn hơn 0, không quá 200000 và là bội số 1000.

BR3: Loại món thuộc com, bun_pho, do_uong, an_vat.

BR4: Món tạm hết chỉ chuyển available thành false, không xóa.

## 6. Cấu trúc hệ thống

- schemas.py: kiểm tra và định dạng dữ liệu.
- repository.py: lưu trữ và thao tác món ăn.
- routers/menu.py: xử lý 6 API CRUD.
- main.py: khởi tạo FastAPI.
