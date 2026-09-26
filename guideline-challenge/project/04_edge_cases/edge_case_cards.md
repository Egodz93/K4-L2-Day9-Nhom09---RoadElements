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

CASE ID: EC13
Sample: GTS11
Scene: Đường đô thị có đảo nhỏ, biển yêu cầu đi bên phải đảo.
Observation: Nhiều xe đỗ che mặt đường bên phải đảo; làn trái đảo nhìn thấy nhưng xe không được phép đi.
Decision: LABEL / IGNORE
Expected: Vẽ một `area/drivable` chỉ cho làn bên phải đảo. Khép polygon tại mép bó vỉa đảo — không nối sang phần đường bên trái đảo. Khép thêm tại mép ngoài xe đỗ, không vẽ dưới xe. Bỏ toàn bộ đảo, làn ngược chiều, vỉa hè và xe.
Rationale: Đảo là ranh giới vật lý cứng. Vẽ polygon xuyên đảo tạo quỹ đạo đi ngược chiều hoặc lên đảo — lỗi critical trong downstream.
Common mistake: Vẽ một polygon duy nhất bao cả hai bên đảo. Vẽ phủ lên xe đỗ hoặc nối mặt đường dưới xe.
Diversity: occlusion / conflict / critical / escalation

---

CASE ID: EC14
Sample: GTS11
Scene: Xe đang chạy che một phần mặt đường, còn mặt đường phía sau xe vẫn nhìn thấy một phần.
Observation: Polygon bao xuyên qua thân xe thay vì khép tại mép xe.
Decision: LABEL
Expected: Khép polygon `area/drivable` tại mép ngoài cùng của xe. Nếu mặt đường phía sau xe còn xác định được biên rõ ràng, tạo đa giác thứ hai riêng cho phần đó. Hai polygon không được nối qua thân xe.
Rationale: Vẽ dưới xe suy diễn mặt đường không quan sát được — vi phạm nguyên tắc chỉ label phần nhìn thấy; downstream nhận được đường đi không thực tế.
Common mistake: Bỏ qua xe hoàn toàn và kéo polygon liên tục dưới/qua xe.
Diversity: occlusion / geometry / critical

---

CASE ID: EC15
Sample: GTS28
Scene: Đường hẹp hai chiều không có vạch giữa, xe ngược chiều ở mép trái, xe đỗ bên phải, tim đường chỉ ước lượng được.
Observation: Annotator dùng mép nhựa hai bên làm biên của một polygon duy nhất — bao cả xe ngược chiều.
Decision: LABEL / ESCALATE
Expected: Xác định tim đường = trung điểm chiều ngang giữa hai mép nhựa ở phần gần xe chủ thể. Biên trái của `area/drivable` không vượt tim đường (sai số ±5% chiều rộng tổng). Không tạo `area/alternative`. Bỏ cả hai xe, vỉa hè và lối đỗ. Nếu không xác định được tim đường trong sai số, escalate và tạo issue trong CVAT.
Rationale: Bao cả xe ngược chiều trong drivable area tạo đường đi đối đầu — lỗi critical; "bảo thủ" phải có định nghĩa định lượng để annotator không tự diễn giải.
Common mistake: Dùng toàn bộ bề rộng nhựa đường làm `area/drivable`. Không escalate khi tim đường không xác định được.
Diversity: ambiguity / occlusion / critical / escalation

---

CASE ID: EC16
Sample: GTS11 (gold dispute)
Scene: Gold decision d1 chấm correct=1 nhưng polygon thực tế bao cả hai bên đảo.
Observation: Đây là trường hợp gold sai — decision đã khóa nhưng annotation thực tế không khớp với expected "làn bên phải đảo".
Decision: ESCALATE — báo cáo riêng
Expected: Giữ nguyên correct=1 theo bản khóa. Ghi chú "gold sai:" kèm bằng chứng (tọa độ polygon x≈54→1144 trong ảnh rộng 1360px). Tạo báo cáo riêng cho reviewer để cập nhật gold trong lần review tiếp.
Rationale: Không tự sửa gold đã khóa — mọi thay đổi gold phải qua reviewer. Ghi bằng chứng rõ để không mất thông tin khi bàn giao.
Common mistake: Tự đổi correct=0 khi phát hiện gold sai mà không ghi báo cáo. Bỏ qua trường hợp gold sai và không báo cáo.
Diversity: conflict / escalation / gold_dispute
