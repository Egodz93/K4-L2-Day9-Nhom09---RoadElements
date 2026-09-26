# Problem statement + downstream contract

## Bài toán

Gán đa giác cho phần mặt đường nhìn thấy mà xe chủ thể có thể đi hợp lệ, đồng thời phân biệt làn hiện tại với vùng có
thể chuyển sang; khó nhất ở nút giao, đường không có vạch, vùng che khuất và vạch tạm.

## Downstream contract

1. **Người dùng:** mô hình nhận biết vùng chạy xe và hệ thống lập kế hoạch đường đi.
2. **Đầu ra:** đa giác `area/drivable` và `area/alternative`; không có thuộc tính.
3. **Lỗi nghiêm trọng nhất:** gán làn ngược chiều, vỉa hè, đảo, vật cản hoặc đường cấm thành vùng đi được.
4. **Escalation:** tạo issue trong CVAT và chuyển cho người phụ trách guideline; không tự thêm nhãn.

## Scope

- **Trong scope:** làn hiện tại, phần nối hợp lệ và làn cùng chiều/làn rẽ có thể tiếp cận hợp pháp.
- **Ngoài scope:** làn ngược chiều, vỉa hè, lề dừng, bãi đỗ, đảo, dải phân cách, vùng cấm, vật cản và phần bị che.
- **Geometry tolerance:** tại biên rõ, sai lệch tối đa 5 px; không được vượt qua ranh giới vật lý. Biên mờ phải vẽ
  bảo thủ hoặc chuyển xử lý.

## Output chấm được

`LABEL` được thể hiện bằng đa giác và tên nhãn trong export. `IGNORE` được thể hiện bằng việc không có đa giác tại
vùng loại trừ và được đối chiếu với gold. `ESCALATE` được ghi bằng issue trong CVAT và phải được giải quyết trước
export cuối; không tạo class thứ ba.

## Dữ liệu và giới hạn

Nguồn `gtsdb` có 28 ảnh PNG tĩnh, kích thước 1360×800. Sample pack dùng 4 ảnh example, 6 ảnh calibration và 5 ảnh
blind. Dữ liệu chủ yếu ban ngày tại Đức, không có chuỗi thời gian hay bản đồ, nên chỉ dùng bằng chứng trong từng ảnh.
