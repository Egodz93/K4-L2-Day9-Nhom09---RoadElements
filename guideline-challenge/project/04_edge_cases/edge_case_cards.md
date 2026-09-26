# Edge-case library

---

CASE ID: EC01
Sample: GTS07
Scene: Công trường dưới cầu.
Observation: Vạch vàng tạm khác hướng vạch cũ; bên phải có rào và mặt đường thi công.
Decision: LABEL / IGNORE
Expected: Gán `area/drivable` trong hành lang do vạch vàng đang dẫn; bỏ vùng sau rào và không suy đoán đường vòng.
Rationale: Vạch tạm và ranh giới vật lý quyết định đường đi an toàn hiện tại.
Common mistake: Bám vạch cũ hoặc tô cả vùng thi công.
Diversity: conflict / critical

---

CASE ID: EC02
Sample: GTS24
Scene: Đường đô thị có ray tàu điện.
Observation: Ray nằm trong phần đường ô tô đang lưu thông.
Decision: LABEL
Expected: Giữ ray trong `area/drivable` nếu liên tục với làn xe chủ thể; không loại chỉ vì có ray.
Rationale: Downstream cần vùng ô tô đi được, không phân loại vật liệu mặt đường.
Common mistake: Cắt lỗ quanh từng đường ray.
Diversity: ambiguity

---

CASE ID: EC03
Sample: GTS26
Scene: Đường hẹp hai chiều không có vạch giữa.
Observation: Mặt đường bị chói; xe ngược chiều che mép trái.
Decision: LABEL / ESCALATE
Expected: Chỉ gán bảo thủ nửa phải nhìn thấy; không gán xe và nửa đường ngược chiều. Escalate nếu không ước lượng được tim đường.
Rationale: Tô cả mặt đường có thể tạo đường đi đối đầu xe ngược chiều.
Common mistake: Dùng toàn bộ bề rộng nhựa đường làm `area/drivable`.
Diversity: low_visibility / occlusion / critical / escalation

---

CASE ID: EC04
Sample: GTS02
Scene: Nút giao rộng có biển hướng bắt buộc.
Observation: Xe phía trước che phần nối; biển trái và phải phục vụ các nhánh khác nhau.
Decision: LABEL / ESCALATE
Expected: Chỉ gán phần tiếp tục chắc chắn của làn xe chủ thể; escalate nếu không xác định được biển áp dụng cho làn nào.
Rationale: Chọn sai nhánh làm thay đổi trực tiếp đường đi.
Common mistake: Tô toàn bộ lòng nút giao hoặc chọn nhánh theo cảm giác.
Diversity: ambiguity / occlusion / conflict / escalation

---

CASE ID: EC05
Sample: GTS05
Scene: Góc phố và vạch qua đường.
Observation: Tòa nhà cùng xe phía trước che phần lớn đường sau góc.
Decision: LABEL / IGNORE
Expected: Vạch qua đường thuộc cùng vùng mặt đường; dừng đa giác nơi phần nối bị che. Bỏ vỉa hè và người đi bộ.
Rationale: Không nội suy đường đi qua vùng không quan sát được.
Common mistake: Dừng tại vạch qua đường hoặc kéo polygon xuyên qua góc khuất.
Diversity: occlusion / truncation

---

CASE ID: EC06
Sample: GTS20
Scene: Nút giao có đảo dẫn hướng.
Observation: Xe che phần nối và nhiều nhánh xuất hiện quanh đảo.
Decision: LABEL / IGNORE / ESCALATE
Expected: Gán phần tiếp tục nhìn thấy của làn hiện tại; bỏ đảo. Nhánh khác chỉ là `area/alternative` khi thấy kết nối hợp lệ, nếu không thì escalate.
Rationale: Không được biến toàn bộ nút giao thành vùng đi được.
Common mistake: Nối polygon xuyên đảo hoặc qua xe.
Diversity: ambiguity / occlusion / escalation

---

CASE ID: EC07
Sample: GTS22
Scene: Ra khỏi gầm cầu với chênh sáng mạnh.
Observation: Vùng gần rõ nhưng vùng cửa cầu bị cháy sáng.
Decision: LABEL
Expected: Vẽ `area/drivable` ở phần có biên chắc chắn và dừng trước vùng mất biên; bỏ tường và vỉa hè.
Rationale: Biên bịa trong vùng cháy sáng làm sai hình học đường đi.
Common mistake: Kéo polygon tới vùng sáng chỉ theo hướng phối cảnh.
Diversity: low_visibility

---

CASE ID: EC08
Sample: GTS25
Scene: Đường nhiều nhánh tại chỗ nhập/tách làn.
Observation: Vạch đứt, vạch liền và vùng gạch chéo cùng xuất hiện.
Decision: LABEL / IGNORE
Expected: Nhánh chứa tâm mép dưới là `area/drivable`; nhánh còn kết nối qua vạch cho phép là `area/alternative`; bỏ vùng gạch chéo.
Rationale: Phân biệt đường mặc định và lựa chọn hợp pháp cho lập kế hoạch.
Common mistake: Gán mọi nhánh là `area/alternative` hoặc nối qua vùng gạch chéo.
Diversity: conflict / critical

---

CASE ID: EC09
Sample: GTS08
Scene: Cao tốc trong bóng cầu.
Observation: Vạch làn tối và xe phía trước che một phần mặt đường.
Decision: LABEL / IGNORE
Expected: Làn chứa tâm mép dưới là `area/drivable`; làn cùng chiều nối qua vạch đứt là `area/alternative`; không phủ xe hay dải phân cách.
Rationale: Bóng tối không làm mất chức năng của làn khi biên vẫn nhận ra được.
Common mistake: Bỏ toàn bộ vùng tối hoặc tô qua xe.
Diversity: low_visibility / occlusion

---

CASE ID: EC10
Sample: GTS11
Scene: Đường đô thị có đảo nhỏ và xe đỗ sát lề.
Observation: Biển trên đảo yêu cầu đi bên phải; nhiều xe che mặt đường.
Decision: LABEL / IGNORE
Expected: Gán làn hiện tại bên phải đảo; bỏ đảo, làn ngược chiều, xe và vỉa hè.
Rationale: Gán sai phía đảo tạo quỹ đạo đi ngược chiều.
Common mistake: Tô xuyên đảo hoặc dưới xe.
Diversity: occlusion / critical

---

CASE ID: EC11
Sample: GTS21
Scene: Đảo dẫn hướng trước vạch qua đường.
Observation: Biển yêu cầu đi bên trái đảo; vạch qua đường cắt ngang tuyến đi.
Decision: LABEL / IGNORE
Expected: `area/drivable` đi bên trái đảo và bao gồm phần vạch qua đường; bỏ đảo và vỉa hè.
Rationale: Đảo là ranh giới vật lý, còn vạch qua đường không chặn khả năng lưu thông.
Common mistake: Đi bên phải đảo hoặc dừng polygon tại vạch qua đường.
Diversity: conflict / critical

---

CASE ID: EC12
Sample: GTS28
Scene: Đường hẹp không có vạch giữa.
Observation: Xe ngược chiều ở mép trái và xe đỗ bên phải; tim đường chỉ có thể ước lượng.
Decision: LABEL / IGNORE
Expected: Gán bảo thủ nửa phải cho `area/drivable`; không tạo `area/alternative`; bỏ cả hai xe, vỉa hè và lối đỗ.
Rationale: Tô cả bề rộng dẫn tới đường đi đối đầu hoặc xuyên vật cản.
Common mistake: Dùng mép nhựa hai bên làm biên của một polygon duy nhất.
Diversity: ambiguity / occlusion / critical

---
