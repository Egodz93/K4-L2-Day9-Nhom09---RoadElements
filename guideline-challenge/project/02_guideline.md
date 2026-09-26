# Annotation guideline — TODO tên bài toán

**Version:** v0

<!--
v0 = chưa có bản nháp. Đổi dòng Version ở trên thành v1 khi xong bản nháp đầu, v2 sau calibration, v3 sau blind
handoff; mỗi lần tăng version ghi một dòng vào 08_revision_log.md. `make freeze` đòi v2 trở lên.

File này là thứ nhóm peer nhận nguyên văn trong blind pack và là Guide dán vào CVAT. Peer KHÔNG nhận
edge_case_cards.md, gold_decisions.csv hay sample_pack.csv. Rule nào peer cần biết phải nằm ở đây.
No hidden rules: rule chỉ giải thích bằng miệng thì coi như không tồn tại.
Ví dụ trong guideline chỉ dùng ảnh split example hoặc calibration, không dùng ảnh blind.
-->

## 1. Objective + scope

**Mục tiêu:** Label vùng đường mà xe có thể di chuyển được (**drivable area**) trong ảnh giao thông đường bộ,
phục vụ huấn luyện model nhận diện không gian lái xe tự động.

**Trong scope — bắt buộc label:**
- Làn đường chính xe đang đi (ego lane)
- Các làn đường khác cùng chiều hoặc ngược chiều còn nhìn thấy rõ mặt đường
- Vùng giao lộ (intersection) mà xe có thể đi vào
- Đường phụ, ngõ, lề đường trải nhựa / bê-tông mà ô tô có thể đi qua

**Ngoài scope — không label (ignore):**
- Vỉa hè, lề đất, dải phân cách cứng, bồn hoa, vỉa hè bê-tông dành cho người đi bộ
- Vùng mặt đường bị che khuất hoàn toàn bởi xe khác, công trình, hay vật cản
- Bầu trời, toà nhà, cây cối, biển báo, đèn tín hiệu
- Vùng đường quá xa / quá nhỏ không xác định được biên rõ ràng

## 2. Annotation unit

- **Loại task:** Ảnh tĩnh (image-level) — không track, không frame sequence
- **Đơn vị:** Region (vùng) — mỗi vùng đường liền thông, không bị cắt đứt bởi vật cản cứng, là **một instance riêng**
- **Geometry:** Polygon (vẽ kín vùng drivable area)

**Khi nào tạo instance mới:**

| Tình huống | Xử lý |
|---|---|
| Các làn đường liền nhau, không có dải phân cách cứng | **Một** polygon bao toàn bộ |
| Hai làn bị tách bởi dải phân cách cứng / bồn hoa | **Hai** polygon riêng biệt |
| Đường chính + giao lộ liền thông nhau | **Một** polygon gộp chung |
| Đường rẽ phụ tách ra, không liền vùng chính | **Một** polygon riêng cho đường rẽ |


## 3. Geometry rule

TODO — rectangle / polyline / polygon; tight, visible hay amodal; đặt điểm thế nào; endpoint ở đâu; tolerance.

## 4. Taxonomy

TODO — class hierarchy; cái gì là class, cái gì là attribute; allowed values; default và khi nào dùng `unknown`.
Bảng đầy đủ ở `03_ontology_and_cvat_setup.md` — hai nơi phải khớp nhau.

## 5. Inclusion / exclusion

TODO — trường hợp bắt buộc label; trường hợp ignore.

## 6. Visibility / occlusion

TODO — bị che một phần, bị cắt mép ảnh, nhỏ/xa, phản chiếu, loá, độ tin cậy thấp.

## 7. Ambiguity / escalation

TODO — khi nào LABEL / IGNORE / UNKNOWN / ESCALATE khi bằng chứng không đủ. Ghi rõ **thể hiện mỗi quyết định trong
CVAT bằng cách nào** (attribute, giá trị, tag…), để quyết định đó nhìn thấy được trong file export.

## 8. Temporal rule

TODO — nếu là video/track: track bắt đầu/kết thúc khi nào, attribute nào mutable, xử lý chuyển trạng thái và bị che
ngắn. Task ảnh tĩnh ghi "Không áp dụng — task ảnh tĩnh".

## 9. Examples

TODO — positive, negative và edge case, mỗi ví dụ có sample_id (split example/calibration) và expected output.

| sample_id | Thấy gì | Expected output | Rule áp dụng |
|---|---|---|---|
| TODO | TODO | TODO | TODO |

## 10. Common mistakes

TODO — những lỗi reviewer có khả năng gặp nhiều nhất và cách tránh.
