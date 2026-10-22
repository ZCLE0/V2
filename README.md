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
5. Kiểm tra: mở link web + `#admin`, đăng nhập. Ngay dưới trạng thái có dòng **Máy chủ bản 9 · Sheet chạy bằng … · Mail báo đơn mới gửi tới …**. Nếu hiện khung đỏ **"Code.gs trên Sheet đang là bản cũ"** thì làm lại bước 1–3.

### Đang dùng Sheet của Gmail mới

- Web đã trỏ sẵn tới link `/exec` của Gmail mới: `https://script.google.com/macros/s/AKfycbyIS6XvGytETK_AEAa4bm4Rl7LliW-XqRo-oQO8IUEehYzdIjsiKUd9K6A1qs7w3u1r/exec` (trong `config.js`, và dự phòng trong cả 3 trang).
- Mail xác nhận, mail báo đơn và file 3D trên Drive đều đi bằng tài khoản đã **Triển khai** Apps Script. Khi triển khai, chọn **Thực thi với tư cách: Tôi (Gmail mới)** và **Ai có quyền truy cập: Bất kỳ ai**.
- Chạy `setup()` bằng Gmail mới: Gmail đó tự được thêm vào đầu ô **Email nhận thông báo đơn mới** ở tab Cài đặt. Nếu Sheet được chép từ tài khoản cũ và ô đó còn Gmail cũ, xóa Gmail cũ khỏi ô nếu không muốn nhận nữa.
- Sau này nếu tạo **triển khai mới** (không phải phiên bản mới) thì link `/exec` đổi. Khi đó sửa `sheetApi` trong `config.js`.

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
| Mã giảm giá (ai nhập trước được dùng) | tab Mã giảm giá | Mã giảm giá → Tạo mã / Thêm mã giảm giá |

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

## 5. Mã giảm giá (ai nhập trước được dùng)

- Tạo ở trang quản trị (phần **Mã giảm giá**, nút **Tạo mã** tự nghĩ mã) hoặc tab **Mã giảm giá**. Mỗi mã ghi:
  - **Giảm**: số tiền (`10000`, `10k`) hoặc phần trăm (`10%`);
  - **Áp dụng cho**: cả 2 loại, chỉ móc khóa thường, hoặc chỉ móc khóa tên;
  - **Số lượt dùng**: mã dùng được cho bao nhiêu người (để trống = 1). Ghi `5` thì **5 người khác nhau** nhập sớm nhất được giảm, mỗi người 1 lần;
  - **Combo áp dụng**: đơn đặt bao nhiêu cái thì được giảm, để tránh giảm chồng lên giá combo. Chọn trong danh sách (Chỉ lẻ 1 cái, Chỉ combo 2, Chỉ combo 3, Lẻ 1 cái hoặc combo 2, Từ 2 cái trở lên) hoặc tự ghi: `1, 2` · `3` · `2+`. Để trống = mọi số lượng. Với móc khóa tên, số này là số cái đặt;
  - ghi chú (không bắt buộc, vd. "đăng story").
- Mã **không gán cho ai**. Bạn đăng mã lên story/nhóm; **ai nhập và áp dụng trước thì người đó được dùng**. Nút **Chép** ở trang quản trị chép sẵn câu để đăng (có ghi số lượt và combo).
- Khách điền họ tên, lớp, SĐT, Gmail rồi bấm **Áp dụng**. Mỗi khách bấm Áp dụng được **giữ 1 lượt trong 45 phút** để chuyển khoản. Hết lượt trống thì người sau thấy "Các lượt còn lại đang được bạn khác giữ" (mã 1 lượt: "Mã này vừa được một bạn khác áp dụng"). Đặt đơn xong thì cột **Đã dùng** tăng 1. Quá 45 phút không đặt thì lượt đó mở lại.
- Khách đổi số lượng sau khi áp mã mà không đúng combo áp dụng thì trang báo ngay, không trừ tiền, và không cho đi tiếp cho tới khi khách đổi lại số lượng hoặc bỏ mã.
- **Chống 1 người dùng nhiều mã hoặc 1 mã nhiều lần:** mỗi người chỉ dùng được **1 mã, 1 lần**, kể cả mã còn lượt. Máy chủ coi là cùng một người nếu trùng **bất kỳ** điều nào sau (không phân biệt hoa thường, có dấu hay không dấu):
  - cùng SĐT, hoặc
  - cùng Gmail, hoặc
  - cùng link Facebook, hoặc
  - cùng **họ tên + lớp** (trùng tên nhưng khác lớp là người khác, vẫn được dùng).
- Mỗi người cũng chỉ giữ 1 mã một lúc: áp mã khác thì lượt đang giữ được nhả ra.
- 3 cột tự động ở tab Mã giảm giá: **Đã dùng** (số lượt đã dùng), **Trạng thái** (còn trống bao nhiêu lượt, ai đang giữ, lần dùng gần nhất), **Đang giữ** (máy ghi, đừng sửa). Muốn thêm lượt thì tăng Số lượt dùng. Mã đã có lượt dùng hoặc đang có người giữ thì không xóa được.
- Mã QR tự trừ tiền giảm. Tab Đơn hàng ghi cột **Mã giảm giá** và **Tiền giảm**. Mail xác nhận và mail báo đơn đều có dòng giảm giá.
- Máy chủ kiểm tra lại mã ngay lúc nhận đơn (kể cả khi ai đó gửi đơn thẳng, bỏ qua trang): sai combo, hết lượt hay người đã dùng mã thì đơn tính đủ tiền và có ghi chú ở cột Ghi chú để bạn liên hệ khách.

## 5b. Mã đặc biệt (bỏ qua chuyển khoản)

- Tạo ở tab **Mã đặc biệt** hoặc trang quản trị: tên người nhận + mã + số lượng. Người nhận gõ **tên + mã** (vd. `Nguyễn Văn A QUA7K2`) vào ô họ tên thì form chỉ còn **SĐT + địa chỉ nhận hàng**.
- Dùng được ở **cả 2 trang**:
  - móc khóa thường: gõ vào ô **Họ và tên**;
  - móc khóa tên: thiết kế xong bấm **Sở hữu thiết kế này**, rồi gõ vào ô **Họ và tên người đặt**. Đơn ghi đủ tên in, kiểu chữ và file 3D như đơn thường, mail báo đơn có đính kèm file STL + hướng dẫn in.
- Số lượng của mã = số móc khóa được nhận (móc khóa tên: số cái cùng tên). Mỗi mã dùng 1 lần.

## 6. Chưa nối Google Sheet thì sao?

- Trang vẫn chạy với giá, nơi nhận và mã QR dự phòng trong `config.js`.
- Móc khóa thường gửi đơn qua FormSubmit (email `orderEmail`).
- Móc khóa tên ở chế độ xem thử: không gửi đơn, nhưng tải được file STL.

Chi tiết về dựng hình, font và file in của móc khóa tên nằm trong `README_moc-khoa-ten.md`.
