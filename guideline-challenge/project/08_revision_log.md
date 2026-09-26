# Revision log

Chỉ tăng version sau khi có bằng chứng calibration hoặc blind handoff. Không ghi trước kết quả chưa xảy ra.

| Version | Đổi gì | Vì sao | Bằng chứng |
|---|---|---|---|
| v1 | Tạo hai nhãn polygon `area/drivable` và `area/alternative`; thêm rule cho vạch tạm, ray, che khuất và đường không vạch | Cần phân biệt đường mặc định với lựa chọn hợp pháp và chặn vùng nguy hiểm | `GTS04`, `GTS07`, `GTS17`, `GTS24`, `GTS26` |
| v2 | Làm rõ điều kiện tạo `area/alternative` quanh đảo/nút giao và chỗ nhập tách; cấm tạo vùng chính bên trái xe ngược chiều ở đường không vạch | Hai người gán nhãn khác số polygon ở các cảnh này | `06_calibration_report.csv`: `GTS02`, `GTS20`, `GTS25`, `GTS26` |
| v3 | (1) Thêm rule bắt buộc tách đa giác tại đảo giao thông — khép polygon tại mép bó vỉa, không bao qua đảo; (2) Định lượng "bảo thủ" cho đường hai chiều không vạch: biên trái không vượt trung điểm hai mép nhựa, sai số ±5%; (3) Bổ sung rule cắt polygon tại mép xe che khuất; (4) Thêm example GTS11 và GTS28 vào mục 9; (5) Thêm lỗi thường gặp #11 và #12 | Blind handoff: GTS11-d2 (critical, 0) — polygon bao qua đảo; GTS11-d3 (major, 0) — không cắt tại mép xe; GTS28-d1 (critical, 0) — polygon bao full width; GTS28-d2 (critical, 0) — bao cả xe ngược chiều; GTS11-d1 gold sai (báo cáo riêng) | `07_blind_handoff/transfer_score.csv`, `07_blind_handoff/peer_feedback.md` |
