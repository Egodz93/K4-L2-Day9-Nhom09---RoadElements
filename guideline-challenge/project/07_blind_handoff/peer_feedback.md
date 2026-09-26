# Peer feedback + owner response

Phần 1 do **nhóm peer** trả lời (gửi kèm file export). Phần 2 do **nhóm owner** điền. Thay mọi placeholder mới
là xong (gate G5).

- **Nhóm peer:** Thunderbolt 
- **Người label blind:** 26ai.thinhnv (thinhnv@vinuni.edu.vn)

## 1. Peer trả lời

1. **Rule nào rõ nhất / giúp quyết định nhanh nhất?** Rule phân biệt `area/drivable` (làn chứa tâm mép dưới ảnh) và `area/alternative` (làn cùng chiều kề bên nối qua vạch đứt) rất rõ — áp dụng đúng hoàn toàn cho GTS01 và GTS08. Rule IGNORE dải phân cách cứng và vỉa hè cũng không gây do dự.

2. **Rule nào mơ hồ hoặc phải tự suy diễn?** Hai điểm mơ hồ: (a) Khi có đảo giao thông, guideline chưa nói rõ cần vẽ bao nhiêu polygon và giới hạn polygon đến đâu so với đảo; (b) "Bảo thủ" trong "label area/drivable bảo thủ cho nửa phải" (GTS28) không được định nghĩa — không rõ biên giữa đường là tim đường hay vạch kẻ.

3. **Sample nào khiến guideline "vỡ"?** GTS11 (đảo giao thông) và GTS28 (đường hai chiều không có vạch giữa rõ ràng). GTS11 không có rule nào chỉ rõ cách tách polygon tại đảo. GTS28 thiếu định nghĩa "bảo thủ" và cách xác định biên giữa đường không có vạch.

4. **Attribute / default nào trong CVAT dễ gây thao tác sai?** Không có attribute trong schema (cvat_labels.json để trống `attributes: []`). Rủi ro chính là chọn nhầm label `area/alternative` thành `area/drivable` hoặc ngược lại do hai màu khá giống nhau (#62c4b2 xanh ngọc vs #4a3d3c nâu tối).

5. **Một thay đổi cụ thể giúp annotator mới ít hỏi hơn?** Bổ sung vào guideline mục "Xử lý đảo giao thông": quy định rõ (a) vẽ tách polygon tại mép đảo, (b) chỉ bao làn xe đang đi, không bao vùng đảo hay làn ngược chiều. Kèm ví dụ ảnh GTS11 với expected output đúng.

## 2. Owner phân loại

Owner không tranh luận để bảo vệ guideline. Mỗi feedback và mỗi decision peer làm sai được xếp vào một hướng xử lý.

| Feedback / decision sai | Nguyên nhân | Xử lý | Bằng chứng |
|---|---|---|---|
| GTS11-d1: `gold sai` — polygon bao cả hai bên đảo (x≈54→1144) nhưng gold chấm correct=1 | **guideline gap** — không có rule về cách vẽ polygon khi có đảo giao thông; annotator không có căn cứ để tách | accept + revise: bổ sung rule "Khi có đảo, vẽ riêng polygon cho từng làn, không bao qua đảo"; cập nhật gold d1 = 0 trong lần review tiếp | annotations.xml GTS11 points x min≈54, max≈1144; ảnh rộng 1360px → polygon chiếm ~80% chiều ngang |
| GTS11-d2: correct=0 — polygon bao rộng qua khu vực đảo, không IGNORE | **guideline gap** (cùng nguyên nhân d1) — thiếu rule đảo giao thông | accept + revise: rule đảo bổ sung vào mục 5 (Inclusion/exclusion); thêm edge case card GTS11 | annotations.xml GTS11: 1 polygon duy nhất bao từ y≈520 đến y=800 toàn chiều ngang |
| GTS11-d3: correct=0 — polygon không tách/khép tại mép xe | **guideline gap** — mục 3 (Geometry rule) chưa có hướng dẫn cụ thể xử lý occlusion bởi xe | accept + revise: bổ sung vào mục 3 "Khi xe che khuất một phần, khép polygon tại mép ngoài xe, không vẽ dưới xe"; kèm ví dụ minh họa | annotations.xml GTS11: polygon không có điểm nào thể hiện cắt tại mép xe |
| GTS28-d1: correct=0 — polygon bao full width thay vì nửa phải bảo thủ | **guideline gap** — từ "bảo thủ" và "nửa phải" không có định nghĩa định lượng; annotator không biết biên giữa đường ở đâu khi không có vạch kẻ | accept + revise: định nghĩa "bảo thủ = không vượt quá tim đường ước tính; khi không có vạch, lấy điểm giữa chiều ngang làn đường nhìn thấy làm biên" | annotations.xml GTS28: x min≈154, max≈1358 → bao gần full width 1360px |
| GTS28-d2: correct=0 — polygon bao cả vùng xe ngược chiều | **execution error** do hệ quả của d1 — khi polygon đã bao full width thì tự động bao cả xe ngược chiều | reject with evidence: lỗi thực thi do không đọc kỹ expected "bảo thủ nửa phải"; sau khi revise guideline d1, d2 tự được giải quyết | annotations.xml GTS28 points x bắt đầu 154 (gần mép trái) và kết thúc 1358 (gần mép phải) |
| Feedback mơ hồ về đảo giao thông (Q3) | **guideline gap** — thiếu example và rule cho cảnh đảo | accept + revise: thêm sample GTS11 vào mục 9 (Examples) và mục 10 (Common mistakes) với expected output rõ ràng | Peer xác nhận GTS11 khiến guideline "vỡ" |
| Feedback thiếu định nghĩa "bảo thủ" (Q2, Q3) | **guideline gap** — thuật ngữ chủ quan không được lượng hóa | accept + revise: bổ sung định nghĩa vào mục 3 Geometry rule và mục 5 Inclusion/exclusion | Peer xác nhận GTS28 là sample gây vỡ guideline |
