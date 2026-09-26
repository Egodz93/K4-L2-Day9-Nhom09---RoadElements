# QA plan + quality gates

## Flow

Guideline → Calibration → Production → Self-QC → Review → Rework → Quality Gate.

- **Người review:** `[TỰ ĐIỀN]`; review 100% ảnh calibration và ảnh gắn tag `critical`, cộng 20% ảnh còn lại
  (tối thiểu 5 ảnh nếu đủ dữ liệu).
- **Chọn mẫu:** lấy toàn bộ `critical`, `ambiguity`, `occlusion`; phần còn lại chọn ngẫu nhiên và có mẫu của mỗi
  annotator.
- **Theo dõi issue:** ghi issue trong CVAT với `mã ảnh | vị trí | lỗi | rule`; chỉ đóng sau khi sửa và reviewer xác nhận.
- **Guideline gap:** ghi bằng chứng vào revision log, sửa rule, tăng version ở đúng mốc calibration hoặc handoff và
  rà lại các ảnh chịu ảnh hưởng.

## Defect severity

| Severity | Định nghĩa | Ví dụ | Action |
|---|---|---|---|
| Critical | Tạo đường đi nguy hiểm hoặc sai luật | Gán làn ngược chiều, đảo, vỉa hè hay đường cấm là vùng đi được | Dừng gate, sửa lỗi và review 100% ảnh cùng loại |
| Major | Sai class, thiếu vùng hợp lệ hoặc sai biên làm đổi cấu trúc đường đi | Đổi `drivable` thành `alternative`, nối qua xe, bỏ một nhánh hợp lệ | Rework ảnh và tăng gấp đôi mẫu review |
| Minor | Sai hình học nhỏ nhưng không đổi ý nghĩa | Lệch biên rõ không quá 5 px, thừa điểm trên đoạn thẳng | Sửa trước khi đóng batch |
| Question | Chưa đủ bằng chứng để quyết định | Không rõ lề hay làn, biển và vạch mâu thuẫn | Tạo issue và chuyển người phụ trách guideline |

## Metrics

| Metric | Cách tính | Lý do |
|---|---|---|
| Decision accuracy | Số decision đúng / tổng decision được review | Đo trực tiếp class, inclusion và exclusion |
| Critical defect rate | Số ảnh có lỗi critical / số ảnh được review | Bám hậu quả an toàn downstream |
| Geometry pass rate | Số polygon đạt biên 5 px, không tự cắt và không phủ vùng loại trừ / tổng polygon kiểm | Đo chất lượng đa giác thay vì cảm giác |

Metric high-risk: `critical defect rate` phải bằng 0.

## Quality gate

```text
PASS if:
  critical defect rate = 0
  decision accuracy >= 95%
  geometry pass rate >= 90%
  mọi issue đã đóng
REWORK if: không có lỗi critical nhưng một metric dưới ngưỡng
REJECT / ESCALATE if: có lỗi critical hoặc cùng guideline gap lặp lại từ 2 ảnh
```

Trade-off: review toàn bộ ảnh rủi ro để bảo vệ an toàn, nhưng chỉ lấy 20% ảnh thường để giữ chi phí phù hợp bộ dữ
liệu nhỏ. Ngưỡng geometry thấp hơn decision accuracy vì biên xa có thể mờ mà không làm đổi đường đi.
