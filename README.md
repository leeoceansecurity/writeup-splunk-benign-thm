

## Mô tả
Đây là bản tổng hợp chi tiết về cách tôi đã thực hiện và trả lời các câu hỏi trong lab Splunk trên nền tảng TryHackMe. Bài viết cung cấp hướng dẫn chi tiết từng bước để truy vấn logs, phát hiện tài khoản đáng ngờ, phân tích hành vi tải xuống mã độc, và xử lý các sự kiện bảo mật khác trong hệ thống Windows.

## Nội dung chính
- Cách đếm số lượng logs ingest trong một khoảng thời gian cụ thể.
- Phân tích tài khoản giả mạo thông qua logs.
- Phát hiện các scheduled tasks được thực thi bởi người dùng trong logs.
- Tìm kiếm các hành vi nghi ngờ liên quan đến tải xuống mã độc sử dụng LOLBINs (Living Off The Land Binaries).
- Điều tra các sự kiện hậu khai thác và phát hiện kết nối đến máy chủ điều khiển (C2).

## Mục tiêu
Hy vọng bài viết  tổng hợp này  giúp mọi người  nắm vững kỹ năng điều tra logs và phát hiện các dấu hiệu tấn công trong hệ thống sử dụng Splunk và các công cụ bảo mật liên quan.

## Cách sử dụng
Đọc qua các truy vấn và phân tích trong file splunk-writeup.md trên để hiểu cách giải quyết từng vấn đề trong lab Splunk trên TryHackMe.
