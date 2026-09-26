# Blind handoff

Bạn có 15 phút để đọc guideline và gắn nhãn các ảnh trong `images/`.

1. Tạo CVAT task từ `images/`, dùng raw labels trong `cvat_labels.json`, đặt guideline vào Guide.
2. Không hỏi owner về domain rule; hãy ghi mọi câu hỏi vào clarification log của owner.
3. Export `CVAT for images 1.1`; nếu task dùng track, export `CVAT for video 1.1`.
4. Gửi lại ZIP export cùng câu trả lời cho 5 câu hỏi:
   - Rule nào rõ nhất / giúp quyết định nhanh nhất : Ưu tiên ranh giới vật lý như bó vỉa, đảo và rào chắn; chỉ gán phần mặt đường nhìn thấy, không suy đoán phần bị che. Quy tắc này giúp xác định polygon và vùng cần loại trừ nhanh.
   - Rule nào mơ hồ hoặc phải tự suy diễn : area/alternative cần cùng mạng đường, cùng chiều và có kết nối chuyển làn nhìn thấy được. Khi vạch mờ hoặc không rõ biển áp dụng cho làn nào, khó kết luận đủ ba điều kiện.
   - Sample nào khiến guideline “vỡ” : GTS01.png — tại nút giao có hai biển gần nhau, nhưng khó xác định biển nào áp dụng cho làn/nhánh nào và polygon area/alternative bên trái có hợp lệ không.
   - Attribute/default nào trong CVAT dễ gây thao tác sai : Bộ nhãn không có thuộc tính hay giá trị mặc định (attributes: []). Rủi ro thao tác là vẽ polygon khi đang chọn nhầm nhãn; cần kiểm tra label đang active trước mỗi polygon.
   - Một thay đổi cụ thể giúp annotator mới ít hỏi hơn : Thêm một ví dụ nút giao có biển và mũi tên, chú thích rõ biển áp dụng cho làn nào, rồi minh họa vùng nào là area/drivable, area/alternative hoặc không gán nhãn.
