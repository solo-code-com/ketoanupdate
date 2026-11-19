# Nhật ký phát hành (changelog)

Quy ước: GitHub chỉ giữ **file cài đặt của 3 bản gần nhất**. Các bản cũ hơn được
xoá file `.exe`/`.zip` để tiết kiệm dung lượng, nhưng **nội dung thay đổi vẫn được
ghi lại ở đây** để còn đối chiếu khi cần.

| Bản | Ngày (UTC) | File cài đặt | Ghi chú |
|---|---|---|---|
| 0.0.35 | 2026-11-19 | còn | Hướng dẫn sử dụng viết lại đầy đủ, trình bày HTML |
| 0.0.34 | 2026-11-19 | còn | Lưu kết quả tra cứu tờ khai vào DB; bỏ tooltip vô nghĩa |
| 0.0.33 | 2026-11-19 | còn | 401 ở nhánh máy tính tiền = mã captcha sai; tự đăng nhập lại giữa lượt |
| 0.0.32 | 2026-11-19 | đã xoá (chỉ giữ log) | PDF không báo thành công khi thiếu chữ; bỏ font Helvetica |
| 0.0.31 | 2026-11-19 | đã xoá (chỉ giữ log) | Schema v2: khoá chống trùng thêm người mua, tự nâng cấp có sao lưu |

## Chi tiết

### 0.0.35 — 19/11/2026
Viết lại toàn bộ tài liệu Hướng dẫn sử dụng:
- Màn hình Hướng dẫn hiển thị HTML: mục lục bấm được, bảng, khung ghi chú màu.
- 14 mục: bắt đầu 5 bước, khái niệm, hồ sơ công ty, hoá đơn mua/bán (8 mục nhỏ),
  báo cáo, gợi ý tờ khai, tờ khai & GNT, kiểm tra NNT, tự động tải, sao lưu,
  cài đặt & cập nhật, xử lý sự cố (8 tình huống), câu hỏi thường gặp, nơi lưu dữ liệu.
- Có tìm kiếm trong hướng dẫn, nút Về đầu / Tải lại; hộp thoại Trợ giúp dùng cùng tài liệu.

### 0.0.34 — 19/11/2026
- Tờ khai: kết quả tra cứu được lưu ngay vào cơ sở dữ liệu (trước đây chỉ hiện trên bảng,
  mở lại app phải tra cứu lại); cột "Mã hồ sơ" hiển thị đúng; bấm Tải lần hai bỏ qua
  tờ khai đã có tệp.
- Tooltip: chặn tooltip rỗng/trùng nội dung đang hiển thị trên bảng và thanh menu dọc;
  giữ tooltip có thông tin thật (lý do cổng từ chối, mã CQT, cảnh báo).

### 0.0.33 — 19/11/2026
- Nhánh máy tính tiền: cổng trả HTTP 401 khi mã xác nhận sai, trước đây bị hiểu là
  "phiên hết hạn" nên bỏ cả khúc → mỗi lần đồng bộ rơi vài khúc, số hoá đơn nhảy loạn.
  Nay 401 được coi là mã sai: hiện lại hộp captcha để nhập tay, không bỏ khúc.
- Phiên hết hạn giữa lượt: tự yêu cầu đăng nhập lại (nhập captcha) rồi tải tiếp một lần.
- Giới hạn 2 mã/trang ở nhánh máy tính tiền khi bị 429 để không đốt thêm mã.
- Khoá chung: đồng bộ tay và hẹn giờ không chạy chồng nhau.

### 0.0.32 — 19/11/2026 (file cài đặt đã xoá)
- PDF: nếu một dòng chữ không vẽ được thì trả thất bại thay vì báo "đã in xong"
  với bản PDF thiếu nội dung; bỏ font dự phòng Helvetica (thiếu dấu tiếng Việt);
  đóng file đúng cách khi lỗi; gộp PDF thiếu tệp có cảnh báo trong log.
- Nhập XML: hoá đơn bán ra thiếu MST người mua không còn bị gán người mua là chính công ty.
- Đóng app: quét worker theo tên thuộc tính, không dùng danh sách cố định.

### 0.0.31 — 19/11/2026 (file cài đặt đã xoá)
- Cơ sở dữ liệu schema v2: khoá chống trùng hoá đơn thêm `mst_mua`, nên hai hồ sơ công ty
  cùng mua của một người bán với cùng ký hiệu/số hoá đơn không còn ghi đè nhau.
- Tự nâng cấp khi mở app, có sao lưu `.bak-schema2` (kèm `-wal`/`-shm`) trước khi đổi
  cấu trúc; hỏng giữa chừng thì rollback và tự khôi phục lần mở sau.
- Đồng bộ: khoá gộp trùng nhận tên trường thay thế của API, đệm 0 số hoá đơn,
  tính cả người mua (trước đây có thể gộp nhầm nhiều hoá đơn thành một).
