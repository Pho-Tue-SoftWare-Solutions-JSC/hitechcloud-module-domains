# Deployment Checklist

Checklist triển khai module `hitechcloud_domains` vào môi trường test hoặc production.

## 1. Chuẩn bị mã nguồn

- [ ] Đảm bảo thư mục module là `hitechcloud_domains`
- [ ] Đảm bảo file chính tồn tại: `class.hitechcloud_domains.php`
- [ ] Đảm bảo các file tài liệu đi kèm đã có:
  - [ ] `README.md`
  - [ ] `README.en.md`
  - [ ] `ADMIN-GUIDE.md`
  - [ ] `CHANGELOG.md`
- [ ] Kiểm tra lại version trong `class.hitechcloud_domains.php`

## 2. Chuẩn bị môi trường HostBill

- [ ] Xác định đúng thư mục domain modules của HostBill
- [ ] Backup module cũ nếu đang thay thế bản cũ
- [ ] Backup database trước khi test các flow thật
- [ ] Xác nhận môi trường là test hay production

## 3. Cấu hình API

- [ ] Nhập `API URL`
- [ ] Cấu hình một trong các cách xác thực:
  - [ ] `Access Token`
  - [ ] hoặc `Refresh Token`
  - [ ] hoặc `Username` + `Password`
- [ ] Bật/tắt `Use Bearer Token` đúng với cơ chế auth của API
- [ ] Bật `Verify SSL` cho production
- [ ] Cấu hình `Timeout` phù hợp
- [ ] Nhập `Default Payment Method` nếu dùng register/transfer/renew theo order flow

## 4. Kích hoạt module

- [ ] Chép module vào đúng thư mục của HostBill
- [ ] Kích hoạt module trong admin HostBill
- [ ] Lưu cấu hình module
- [ ] Kiểm tra module hiển thị đúng tên và mô tả

## 5. Test chức năng cơ bản

- [ ] Test kết nối API
- [ ] Lookup domain
- [ ] WHOIS domain
- [ ] Lấy danh sách domain
- [ ] Lấy nameservers
- [ ] Update nameservers
- [ ] Lấy EPP code
- [ ] Bật/tắt registrar lock
- [ ] Bật/tắt ID protection
- [ ] Lấy/cập nhật contact info
- [ ] Bật/tắt auto renew
- [ ] Lấy/cập nhật email forwarding
- [ ] DNS create/update/delete
- [ ] DNSSEC list/add/delete

## 6. Test nghiệp vụ quan trọng

- [ ] Test register domain trên môi trường an toàn
- [ ] Test transfer với EPP code hợp lệ
- [ ] Test renew domain
- [ ] Xác nhận order thực sự tạo provisioning mong muốn
- [ ] Kiểm tra log action trong HostBill

## 7. Kiểm tra dữ liệu sau deploy

- [ ] Domain ID remote được resolve đúng
- [ ] Nameservers được lưu đúng
- [ ] Contact data map đúng field
- [ ] DNS records đồng bộ đúng với phía API
- [ ] DNSSEC key hiển thị đúng dữ liệu
- [ ] Không phát sinh lỗi cURL / SSL / timeout

## 8. Rủi ro cần xác nhận trước production

- [ ] Xác nhận lại API hiện dùng có thực sự là registrar backend API hay chỉ là user API
- [ ] Xác nhận register/transfer/renew không chỉ tạo order mà còn thực sự xử lý provisioning
- [ ] Xác nhận `Default Payment Method` hợp lệ ở môi trường production
- [ ] Xác nhận retry / rollback nếu API lỗi giữa chừng

## 9. Sau triển khai

- [ ] Theo dõi log 24-48 giờ đầu
- [ ] Theo dõi lỗi xác thực token
- [ ] Theo dõi lỗi timeout / SSL
- [ ] Theo dõi sai lệch dữ liệu domain giữa HostBill và API
- [ ] Ghi nhận endpoint nào cần mở rộng thêm
