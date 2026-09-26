# Team

Điền trước phút 15. Thay mọi placeholder; còn sót thì `make status` báo ở gate G1.

- **Team:** Nhom09 (ví dụ `team07`)
- **Nhóm peer test bài của mình:** Thunderbolt 
- **Nhóm mình test bài của:** Thunderbolt
- **Problem family:** Drivable area (xem README mục "1 · Chọn bài toán")
- **Nguồn ảnh:** `gtsdb` (`bdd100k`, `gtsdb`, `lisa` — chỉ dùng ảnh trong `data/`)

| Thành viên       | GitHub          | Vai trò chính | File phụ trách                                                                                                          |
| ---------------- | --------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Nguyễn Tiến Dũng | @DungTien04     | Xây guideline | `01_problem_statement.md`, `02_guideline.md`, `08_revision_log.md`                                                          |
| Vũ Tuấn Hiệp     | @vth2004        | Viết báo cáo  | `00_team.md`, `05_qa_plan.md`, `07_blind_handoff/peer_feedback.md`, `07_blind_handoff/clarification_log.csv`              |
| Vũ Minh Duy      | @AGeneration    | Annotator     | `04_edge_cases/edge_case_cards.md`, `04_edge_cases/gold_decisions.csv`, `sample_pack.csv`                                  |
| Phạm Văn Thân    | @Egodz93        | Xây guideline | `03_cvat_labels.json`, `03_ontology_and_cvat_setup.md`, `09_cvat_export_or_task_reference.txt`                            |
| Nguyễn Xuân Sơn  | XuanSonVinuniAI | Annotator     | `06_calibration_report.csv`, `06_calibration_exports/`, `07_blind_handoff/peer_output/`                                    |

Gợi ý chia vai (nhóm 2–3 người thì gộp): **spec owner** (`01`, `02`), **CVAT owner** (`03_*`, `sample_pack.csv`,  
`09`), **gold owner** (`04_edge_cases/`), **QA owner** (`05`, `06`, `07_blind_handoff/`). Mỗi file một người sửa  
chính để tránh xung đột git. Calibration thì mọi người cùng label.
