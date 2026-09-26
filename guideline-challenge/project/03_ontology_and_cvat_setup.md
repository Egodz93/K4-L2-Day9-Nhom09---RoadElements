# Hệ nhãn và thiết lập CVAT

Bảng dưới đây là nguồn chuẩn cho cấu hình CVAT. Tên nhãn, loại hình học, màu và thuộc tính phải khớp với
`03_cvat_labels.json`.

## Bảng hệ nhãn

| Tên | Hình học | Loại | Giá trị cho phép | Giá trị mặc định | Có thể thay đổi? | Lý do |
|---|---|---|---|---|---|---|
| `area/alternative` | Đa giác (`polygon`) | Nhãn (`class`) | Không áp dụng. Nhãn không có thuộc tính | Không có | Không áp dụng. Đây là ảnh tĩnh | Vùng xe có thể đi tới hợp pháp bằng cách chuyển sang làn cùng chiều hoặc nhánh rẽ có kết nối nhìn thấy được, nhưng không phải làn hiện tại của xe chủ thể |
| `area/drivable` | Đa giác (`polygon`) | Nhãn (`class`) | Không áp dụng. Nhãn không có thuộc tính | Không có | Không áp dụng. Đây là ảnh tĩnh | Làn hiện tại của xe chủ thể và phần nối hợp lệ của làn đó theo hướng di chuyển |

Màu hiển thị trong CVAT:

- `area/alternative`: `#62c4b2`.
- `area/drivable`: `#4a3d3c`.

## Nhãn hay thuộc tính

`area/drivable` và `area/alternative` là hai nhãn riêng vì chúng biểu diễn hai loại vùng có ý nghĩa khác nhau đối
với đường đi của xe. Mỗi vùng có một đa giác độc lập và được kiểm tra trực tiếp theo tên nhãn.

Không dùng thuộc tính vì `03_cvat_labels.json` quy định `attributes: []` cho cả hai nhãn. Không có giá trị mặc định
nên không phát sinh sai lệch do quên đổi thuộc tính. Tuy nhiên, CVAT có thể giữ lại nhãn vừa dùng. Người gán nhãn phải
kiểm tra tên nhãn trước khi hoàn thành mỗi đa giác để tránh nhầm vùng đi chính với vùng đi thay thế.

Không tạo thêm nhãn cho vùng không thể đi hoặc trường hợp chưa chắc chắn. Vùng không thể đi được để trống. Trường hợp
chưa chắc chắn được ghi bằng chức năng tạo vấn đề trong CVAT và phải được giải quyết trước khi xuất kết quả cuối.

## CVAT

- **Phiên bản CVAT** (`make cvat-status`): `2.75.1`.
- **Tên task calibration:** `nhom09-drivable-calib-v1` (chưa tạo trên CVAT).
- **Guide của task đã dán `02_guideline.md`?** Chưa, vì task calibration chưa được tạo.
- **Nhóm dùng Track hay Shape, vì sao:** dùng **Shape** vì dữ liệu gồm ảnh tĩnh và hai nhãn đều có hình học đa giác.
  Không dùng Track vì không có chuỗi khung hình để theo dõi.

### Các bước thiết lập cần khớp

1. Tạo task `nhom09-drivable-calib-v1`.
2. Nhập nguyên nội dung `03_cvat_labels.json` vào phần cấu hình nhãn dạng Raw.
3. Kiểm tra CVAT chỉ hiển thị `area/alternative` và `area/drivable`, cả hai dùng đa giác và không có thuộc tính.
4. Dán nguyên nội dung `02_guideline.md` vào phần Guide.
5. Tải các ảnh thuộc nhóm `calibration` lên task.
6. Mở một ảnh, vẽ thử mỗi nhãn một đa giác và kiểm tra tệp xuất giữ đúng tên nhãn.

## Kiểm thử thiết lập

Khi CVAT hoạt động, một thành viên không tham gia thiết lập phải mở task và trả lời được:

- Có hai nhãn là `area/drivable` và `area/alternative`.
- Dùng công cụ đa giác ở chế độ Shape.
- Không có thuộc tính cần gán.
- Khi chưa chắc chắn, không tạo nhãn mới. Người gán nhãn tạo vấn đề trong CVAT và chuyển cho người phụ trách xử lý.

Người kiểm thử cần ghi lại tên, thời điểm kiểm thử và chỗ bị vấp. Nếu không nhìn thấy đủ hai nhãn, thấy thuộc tính
không có trong JSON, không mở được Guide hoặc không xuất đúng tên nhãn, task chưa đạt điều kiện để hiệu chỉnh.
