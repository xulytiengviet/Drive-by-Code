# Drive-by-Code (DBC-AVP)

**Active Visual Probing for Camera-Based Autonomous Driving**

Mô phỏng nghiên cứu AVF chạy trực tiếp trên trình duyệt, không cần API trả phí. **Thiết kế: Long Ngo. Giấy phép: MIT (2026).**

## Demo

- [Trang Drive-by-Code](https://xulytiengviet.github.io/Drive-by-Code/)
- Chọn bài toán bám làn, dừng trước vạch hoặc dừng tránh vật cản.
- Xem mô phỏng trạng thái BEV và hình chiếu phía trước **tổng hợp** (không phải sensor RGB thật).
- Bật **Active View** để tạo báo cáo quan sát và **Active Probe** để chạy 3 thử nghiệm giả định trên bản sao trạng thái trong 5 giây.
- Thử chỉnh vận tốc, gain điều khiển và nhiễu; xuất dữ liệu JSON.

## Kiến trúc

Task Spec → Policy → 2D Dynamics → Passive Logs → Active View/Probe → Evaluator → Refinement (future).

### Thành phần đã triển khai

- HTML/CSS/JavaScript không phụ thuộc máy chủ.
- Kinematics đơn giản tại bước thời gian 0,05 giây; controller phản hồi Kp và yaw, giới hạn lái; phanh trước vật cản/vạch dừng; cảnh báo TTC.
- Thu thập số lượt chạy, tỉ lệ đạt nhiệm vụ, sự cố và kết quả chẩn đoán.
- Hệ thống View và Probe có thể lặp lại; không cho phép truyền lệnh tới xe thật.

### Chưa triển khai (roadmap nghiên cứu)

- CARLA và ROS 2 bridge; camera RGB/depth/segmentation thực.
- Code Agent (Codex / Claude) tự tạo và kiểm thử policy hoặc diagnostic program.
- Đánh giá nghiêm ngặt đa seed, đối chứng, khoảng tin cậy và sim-to-real.

## Phương pháp khoa học

So sánh (A) log only, (B) log + passive camera và (C) Active View + Probe. Sử dụng cùng seed, cùng giới hạn số lần sửa, kiểm tra success rate, false completion, iterations, information gain và safety interventions. Các kết quả giả định trong tài liệu đề xuất không phải số liệu đã đo cho Drive-by-Code.

## Nguồn cảm hứng

[Fly-by-Code](https://fly-by-code.github.io/) — *Embodied Coding Agents for Aerial Manipulation with Active Visual and Physical Feedback*. Nguồn gốc công trình được ghi nhận, dữ liệu kết quả Fly-by-Code không được coi là benchmark DBC.

## An toàn

**Simulation-only.** Không sử dụng controller này trên phương tiện thật, không probe nguy hiểm ngoài thực địa. Mô hình đồ họa 2D không thay thế CARLA, camera vật lý, phân tích an toàn ISO 26262 hoặc bằng chứng an toàn độc lập.

MIT © 2026 Long Ngo.
