# MERCHANDISE V2.0 · Bản gộp: I'M A CVLER + CUSTOM

Một trang web, một Google Sheet và một Apps Script cho cả hai loại móc khóa:

- **I'M A CVLER** (`cvler.html`): móc khóa NFC của trường.
- **CUSTOM** (`custom.html`): móc khóa in tên riêng, dựng 3D ngay trên trình duyệt.

## Các file

```
index.html            trang mở đầu: 2 móc khóa lơ lửng, bấm để chọn loại
cvler.html            đặt móc khóa của trường + trang quản trị (#admin)
custom.html           thiết kế + đặt móc khóa tên
config.js             cấu hình dự phòng dùng chung cho cả 3 trang (đã điền sẵn link Apps Script)
huong-dan.html        hướng dẫn tự ghi link vào móc khóa (gửi kèm mail xác nhận)
qr/vib.jpg            ảnh mã QR VIB (chỉ phần mã, không có số tài khoản), dùng khi máy khách không tạo được mã có sẵn số tiền
og.jpg                ảnh khi chia sẻ link
apps-script/Code.gs   mã cho Google Sheet
```

Đưa tất cả file (trừ thư mục `apps-script`) lên repo GitHub Pages. Có thể xóa `qr/hhd.webp` và `qr/ltd.webp` nếu repo đang có, bản này không dùng tới.

## 1. Cập nhật (làm 1 lần)

1. **Apps Script:** mở Sheet đang dùng → **Tiện ích mở rộng → Apps Script** → xóa mã cũ, dán toàn bộ `apps-script/Code.gs` → **Lưu**.
2. Chạy hàm **setup**, hoặc dùng menu **MERCH → Sắp xếp lại các tab** trong Sheet.
   - Hàm này tự sắp xếp lại Sheet, dù Sheet đang theo bản trước, theo bản 5, hay đã bị cả hai bản chạy chồng lên. Không mất đơn nào.
   - Mọi giá trị đang có ở tab Cài đặt được giữ nguyên; dòng nào còn thiếu thì được thêm vào.
3. **Triển khai → Quản lý triển khai → bút chì → Phiên bản mới → Triển khai.** Link `/exec` giữ nguyên, không phải sửa web.
4. Đưa các file lên GitHub → **Commit changes**.

## 2. Điều khiển ở đâu

| Việc | Tab Cài đặt | Trang quản trị (`…/#admin`) |
|---|---|---|
| Đóng / mở đặt hàng (cả 2 loại) | Mở đặt hàng | Đóng đặt hàng ngay / Mở lại |
| Giá 1 cái, combo 2, combo 3 | Giá … (móc khóa thường) | Giá bán → Lưu giá |
| Giá móc khóa tên, **giá cộng thêm khi có ký hiệu** | Giá móc khóa tên · Giá thêm ký hiệu cuối tên | Giá bán → Lưu giá |
| Số lượng tối đa mỗi đơn | Số lượng tối đa mỗi đơn | Giá bán → Lưu giá |
| Giới hạn móc khóa thường / móc khóa tên | 2 dòng Giới hạn | 2 ô Giới hạn |
| Mã QR chuyển khoản | Mã QR chuyển khoản (dữ liệu) · Ngân hàng · Chủ tài khoản | — |
| Tạm ẩn mã QR | Hiện mã QR chuyển khoản | Tạm ẩn mã QR / Hiện lại |
| Thông báo khi đóng / hết suất / ẩn QR | 3 dòng Thông báo | Lưu thông báo |
| Mã đặc biệt (bỏ qua chuyển khoản) | tab Mã đặc biệt | Mã đặc biệt → Thêm mã |
| Mã giảm giá riêng từng người | tab Mã giảm giá | Mã giảm giá → Thêm mã giảm giá |

Trang web và máy chủ cùng tính tiền theo giá ở Sheet. Dù ai sửa giá trên trình duyệt thì Sheet vẫn ghi đúng, và đơn bị tính lại có ghi chú ở cột Ghi chú.

## 3. Mã QR chuyển khoản

- Mọi đơn của cả 2 loại đều chuyển vào **mã QR chung ở tab Cài đặt**, mặc định là VIB · LE ANH QUAN.
- Trang tự thêm số tiền và nội dung chuyển khoản vào mã cho từng đơn.
- Trang chỉ hiện mã QR, tên chủ tài khoản và ngân hàng, **không hiện số tài khoản**.
- Có nút **Lưu ảnh mã QR** để khách mở ảnh đó trong app ngân hàng.
- Muốn đổi tài khoản: quét mã QR mới, dán chuỗi đọc được (bắt đầu bằng `000201`) vào ô *Mã QR chuyển khoản (dữ liệu)*, rồi sửa tên ngân hàng và chủ tài khoản.
- Tab Người bán có cột **QR riêng**, đang để trống. Chỉ điền khi muốn đơn qua link của người đó chuyển vào tài khoản riêng của họ.

## 4. Người bán và link riêng

- Link riêng là link web + `?ref=MÃ`, ví dụ `https://zcle0.github.io/V2/?ref=HHD`. Cột **Link riêng** trong tab Người bán tạo sẵn link này. Link cũ dạng `?nb=hhd` vẫn chạy.
- Mã người bán được giữ suốt hành trình của khách: trang chọn → móc khóa thường hoặc móc khóa tên → chuyển khoản → mail xác nhận.
- Khách vào link của ai thì **nhận hàng ở Nơi giao hàng của người đó**, liên hệ bằng Họ tên + SĐT của người đó, không phải chọn. Người chưa điền Nơi giao hàng thì dùng tab Giao nhận (dự phòng).
- Mỗi đơn có một mail báo đơn duy nhất, gửi cùng lúc cho bạn và người bán.
- Cột **Kiểm tra** báo thiếu gì cho từng người bán (✓ / ⚠). Các cột tự tính: số đơn, số cái, doanh thu, đã nhận tiền, hoa hồng.

## 5. Mã giảm giá (riêng từng người)

- Tạo ở trang quản trị (phần **Mã giảm giá**) hoặc tab **Mã giảm giá**. Mỗi mã ghi:
  - mức giảm: số tiền (`10000`, `10k`) hoặc phần trăm (`10%`);
  - **Gmail và/hoặc SĐT của đúng người được dùng**;
  - áp dụng cho cả 2 loại, chỉ móc khóa thường, hoặc chỉ móc khóa tên.
- Khách nhập mã ở ô **Mã giảm giá** khi đặt, cả trang móc khóa thường lẫn móc khóa tên. Mã chỉ nhận khi khách nhập đúng Gmail/SĐT đã ghi; ghi cả 2 thì phải đúng cả 2.
- **Mỗi mã dùng 1 lần.** **Mỗi người (cùng Gmail hoặc cùng SĐT) chỉ dùng được 1 mã giảm giá**, dù được cho nhiều mã.
- Mã QR tự trừ tiền giảm. Tab Đơn hàng ghi cột **Mã giảm giá** và **Tiền giảm**. Mail xác nhận và mail báo đơn đều có dòng giảm giá.
- Máy chủ kiểm tra lại mã ngay lúc nhận đơn. Nếu mã không còn hợp lệ (vd. vừa bị dùng), đơn được tính đủ tiền và có ghi chú ở cột Ghi chú để bạn liên hệ khách.

## 6. Chưa nối Google Sheet thì sao?

- Trang vẫn chạy với giá, nơi nhận và mã QR dự phòng trong `config.js`.
- Móc khóa thường gửi đơn qua FormSubmit (email `orderEmail`).
- Móc khóa tên ở chế độ xem thử: không gửi đơn, nhưng tải được file STL.

Chi tiết về dựng hình, font và file in của móc khóa tên nằm trong `README_moc-khoa-ten.md`.
