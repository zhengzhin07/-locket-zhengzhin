# Zhengzhin — Locket tùy chỉnh 2

## Kết quả theo yêu cầu

1. Bỏ cả nhóm chú thích quảng bá/cá nhân ở đầu danh sách, gồm bốn mục. Giữ 90 chú thích thường và nội dung đã đăng trước đó. LICENSE/NOTICE vẫn ghi nhận giấy phép mã nguồn.
2. Ngày Gold: đổi purchase_date/original_purchase_date liên quan và original_purchase_date ở subscriber sang 2007-03-16T00:00:00Z. Khi Gold đang hoạt động, giữ nguyên product, ngày hết hạn, store, quyền sở hữu, billing và dữ liệu khác. Đây là chỉnh dữ liệu phản hồi cục bộ; chưa xác nhận nhãn ngày trên iPhone đã hiển thị theo dữ liệu này. Không thay đổi hồ sơ mua hàng thật.
3. Chưa thêm giao diện chọn ảnh bìa/video, tích xanh tùy chỉnh hoặc ảnh anime vào chủ đề máy ảnh Locket. Không có schema đã xác minh cho các phần đó; không tạo các field giả để tuyên bố có tính năng.
4. Thêm 10 PNG khung đã gửi. Trang chọn đi kèm module mở bằng Safari, lưu lựa chọn trong Shadowrocket. Mặc định Conan. Chỉ một khung được gửi qua widget_frame_event cho cấu hình đang dùng; chưa tạo bộ chọn 10 khung trong giao diện Locket hoặc khung động.

## Cập nhật repo

Giải nén gói. Tải các tệp trực tiếp lên thư mục gốc repo:
https://github.com/zhengzhin07/-locket-zhengzhin/upload/main

Tất cả tệp trong gói nằm cùng cấp, không có thư mục con. Giữ nguyên tên các tệp. Tải cả 10 file frame-*.png. Giữ các ảnh nền chú thích đã có trong repo; bản này vẫn sử dụng chúng.

Module chính:
https://raw.githubusercontent.com/zhengzhin07/-locket-zhengzhin/main/Locket-Zhengzhin.sgmodule

Sau Commit changes, cập nhật module trong Shadowrocket. Script-path dùng locket.js?v=custom-2 để lấy bản mới. Chỉ bật một module Locket và dùng thiết lập MITM/chứng chỉ của module trước.

## Chọn khung

Bật Shadowrocket rồi mở Safari:
http://zhengzhin-status.invalid/frames

Chạm một mẫu. Khi trang báo đã lưu, mở lại Locket để ứng dụng lấy cấu hình; widget có thể cập nhật chậm theo iOS. Thay khung làm đổi UID, URL và ETag cấu hình. Trang không tự xóa cache hoặc ép iOS render ngay.

Trang xem trạng thái:
http://zhengzhin-status.invalid/status

Báo cáo:
http://zhengzhin-status.invalid/report.json

Báo cáo phải có build "zhengzhin-custom-2". Sau request Firebase mới, observed.firebase.sentCaptions là 90. observed.firebase.widget cho biết khung đã gửi trong response, không phải bằng chứng widget đã hiển thị. Nếu vẫn thấy nhóm chú thích cũ, kiểm tra ứng dụng đã fetch/activate cấu hình mới; ảnh chụp giao diện không thay thế việc kiểm tra báo cáo.

## Kiểm tra tiếp ảnh bìa/tích xanh/chủ đề máy ảnh

Module chính ghi cấu trúc của một danh sách trường Firebase đã biết: kiểu, số phần tử, tên trường trong allowlist. Không ghi giá trị chuỗi, ID, tên người dùng, URL ảnh, prompt, token hoặc ảnh. Trường lạ chỉ được đếm, không ghi tên. Mở mục chủ đề máy ảnh và trang cá nhân trong Locket rồi gửi phần báo cáo cấu trúc để kiểm tra tiếp.

Locket-Zhengzhin-Chan-Doan.sgmodule là BẢN THAY THẾ CHỈ DÙNG KHI CẦN CHẨN ĐOÁN PROFILE. Mặc định dùng module chính. Không bật đồng thời cả hai bản. Bản chẩn đoán thêm api.locketcamera.com vào MITM và chỉ quan sát response HTTPS /fetchUserV2; không sửa response, không gọi API ghi hoặc thay đổi thông tin tài khoản. Nó chỉ lưu sự hiện diện/kiểu của một danh sách trường profile cố định, không lưu giá trị hoặc dữ liệu cá nhân. Nếu dùng để kiểm tra, mở trang cá nhân Locket rồi xem observed.profile_schema trong báo cáo. Không thấy request chưa chứng minh app không có tính năng; app có thể dùng cache hoặc endpoint khác. Sau khi lấy báo cáo, chuyển về module chính.

## Giới hạn và kiểm thử

Mã được kiểm thử offline; 10 ảnh khung và trang chọn đã kiểm tra trên Chromium ở kích thước điện thoại. Chưa thử Shadowrocket/Locket trên iPhone. Cấu hình video kế thừa là 60 giây/100 MiB; không phải xác nhận máy chủ chấp nhận upload 60 giây hoặc profile hỗ trợ video.

16 nhóm kiểm tra tích hợp và 36 trường hợp observer profile đều đạt. Giữ nguyên giấy phép MIT trong LICENSE và ghi nhận nguồn trong NOTICE.txt. PNG khung được tách nền bằng AI từ ảnh tham chiếu của bạn nên có thể tái dựng nhẹ một số chi tiết.
