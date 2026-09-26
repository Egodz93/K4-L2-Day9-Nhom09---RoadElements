# Revision log

Chỉ tăng version sau khi có bằng chứng calibration hoặc blind handoff. Không ghi trước kết quả chưa xảy ra.

| Version | Đổi gì | Vì sao | Bằng chứng |
|---|---|---|---|
| v1 | Tạo hai nhãn polygon `area/drivable` và `area/alternative`; thêm rule cho vạch tạm, ray, che khuất và đường không vạch | Cần phân biệt đường mặc định với lựa chọn hợp pháp và chặn vùng nguy hiểm | `GTS04`, `GTS07`, `GTS17`, `GTS24`, `GTS26` |
| v2 | Làm rõ điều kiện tạo `area/alternative` quanh đảo/nút giao và chỗ nhập tách; cấm tạo vùng chính bên trái xe ngược chiều ở đường không vạch | Hai người gán nhãn khác số polygon ở các cảnh này | `06_calibration_report.csv`: `GTS02`, `GTS20`, `GTS25`, `GTS26` |
