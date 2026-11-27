> 🌐 **Ngôn ngữ:** 🇻🇳 Tiếng Việt (hiện tại) · [🇬🇧 English](./error-reporting.md) · [🇯🇵 日本語](./error-reporting_ja.md)

# Nhận báo lỗi của site qua Slack, Google Chat…

## Giới thiệu
Khi site gặp lỗi, hệ thống luôn ghi vào file log trên máy chủ. Tài liệu này hướng dẫn **gửi thêm báo lỗi tới kênh chat của đội vận hành**
(Slack, Google Chat, hoặc dịch vụ khác như Mattermost, Discord) để biết sự cố ngay, không phải mở log. Tài liệu dành cho quản trị viên và người
vận hành site; đọc xong bạn tự cấu hình được trên trang quản trị và kiểm tra được là tin báo đã tới.

## Nhìn nhanh
Mỗi báo lỗi đều được ghi log; tin gửi ra kênh chat thì qua thêm một bước lọc để không làm ngập kênh:

```mermaid
flowchart LR
    A["Site gặp lỗi"] --> B["Ghi file log<br/>(luôn luôn)"]
    A --> C{"Đã gửi<br/>gần đây?"}
    C -->|"chưa"| D["Gửi tới các ô<br/>đã điền URL"]
    C -->|"rồi"| E["Bỏ qua lần gửi"]
```

- **Cấu hình ở màn Webhook** trong trang quản trị: ba ô Slack, Google Chat và webhook bên thứ ba.
- **URL là bí mật**: lưu mã hoá, màn chỉ hiện "Đã lưu / Chưa đặt", không hiện lại URL.
- **Không làm chậm site**: mỗi lần gửi tối đa 3 giây; dịch vụ chat lỗi hay chậm thì site vẫn chạy bình thường.
- **Không ngập kênh**: cùng một lỗi chỉ gửi một lần trong 60 giây, file log vẫn ghi đủ.

## Trong trang này
- [Chọn dịch vụ nhận báo lỗi](#chọn-dịch-vụ-nhận-báo-lỗi) — dịch vụ nào dùng được, điền vào ô nào
- [Lấy địa chỉ webhook](#lấy-địa-chỉ-webhook) — tạo URL nhận tin trên từng dịch vụ
- [Cấu hình trên màn Webhook](#cấu-hình-trên-màn-webhook) — các bước điền URL và gửi thử
- [Dự phòng trong .env](#dự-phòng-trong-env) — để vẫn nhận báo lỗi khi cơ sở dữ liệu gặp sự cố
- [Điều kiện & ràng buộc](#điều-kiện--ràng-buộc-hiểu-trước-khi-thao-tác) — địa chỉ hợp lệ, giới hạn thời gian và tần suất

## Chọn dịch vụ nhận báo lỗi
Mục này giúp bạn biết dịch vụ chat của đội có dùng được không và điền URL vào ô nào.

| Dịch vụ | Dùng được | Điền vào ô | URL mẫu (định dạng) |
| --- | --- | --- | --- |
| Slack | ✅ | Slack | `https://hooks.slack.com/services/T.../B.../...` |
| Google Chat | ✅ | Google Chat | `https://chat.googleapis.com/v1/spaces/AAAAbCdEfGh/messages?key=xxxx&token=xxxx` |
| Mattermost | ✅ | Webhook bên thứ ba | `https://chat.example.com/hooks/xxxxxxxxxxxxxxxx` |
| Discord | ✅ | Webhook bên thứ ba | `https://discord.com/api/webhooks/123456789012345678/xxxx/slack` (thêm `/slack` vào **cuối**) |
| Microsoft Teams, Chatwork, Telegram, LINE | ❌ | — | Không nhận tin vào một URL (cần token hoặc định dạng riêng) |

> ℹ️ **Thông tin:** các URL trên chỉ minh hoạ **hình dạng** của một URL webhook — phần `xxxx` là mã bí mật mà dịch vụ cấp cho bạn. Trên màn Webhook, mỗi ô hiện sẵn URL mẫu mờ trong ô trống và một dòng ghi chú bên dưới (lấy URL ở đâu, ví dụ).

- **Google Chat** cần tài khoản Google Workspace bản Business hoặc Enterprise.
- **Điền bao nhiêu ô cũng được.** Mỗi báo lỗi được gửi tới mọi ô có URL.
- **Ô "Webhook bên thứ ba" nhận dịch vụ bất kỳ** miễn là dịch vụ đó nhận một yêu cầu POST với nội dung JSON `{"text": "..."}` (gợi ý cạnh tên ô).

## Lấy địa chỉ webhook
Mục này giúp bạn tạo URL nhận tin. Tên menu có thể khác đôi chút tuỳ phiên bản của từng dịch vụ.

> ⚠️ **Lưu ý:** URL webhook là **bí mật** — ai có URL đều gửi được tin vào kênh của bạn. Không dán URL vào ticket, ảnh chụp hay kho mã nguồn.

**Slack**
1. Mở <https://api.slack.com/apps>, bấm **Create New App** → **From scratch**, đặt tên (ví dụ `Báo lỗi site`) và chọn workspace.
2. Trong app, mở **Incoming Webhooks**, bật **Activate Incoming Webhooks**.
3. Bấm **Add New Webhook to Workspace**, chọn kênh nhận tin, bấm **Allow**.
4. Sao chép URL dạng `https://hooks.slack.com/services/...`.

**Google Chat**
1. Mở space sẽ nhận tin, bấm tên space ở đầu trang → **Apps & integrations**.
2. Bấm **Add webhooks**, đặt tên, bấm **Save**.
3. Sao chép URL dạng `https://chat.googleapis.com/v1/spaces/...`.

**Mattermost**
1. Vào **Integrations** → **Incoming Webhooks** → **Add Incoming Webhook**.
2. Chọn kênh, bấm **Save**, sao chép URL.

**Discord**
1. Vào **Server Settings** → **Integrations** → **Webhooks** → **New Webhook**, chọn kênh.
2. Bấm **Copy Webhook URL**.
3. Thêm `/slack` vào cuối URL: `https://discord.com/api/webhooks/<id>/<token>/slack`. Thiếu `/slack` thì Discord từ chối tin.

## Cấu hình trên màn Webhook
Mục này hướng dẫn điền URL vào site và gửi thử một tin.

1. Đăng nhập trang quản trị, mở menu **Webhook** (đường dẫn `<địa chỉ site>/<tiền tố admin>/config/webhook`). Màn hiện khối mô tả và ba ô:

   ![Màn Webhook: khối mô tả "Kênh nhận báo lỗi của site" và ba ô — ô Gửi tới Slack webhook đã lưu (nhãn Đã lưu, nút Xoá giá trị đã lưu), hai ô Gửi tới Google webhook và Gửi tới webhook bên thứ ba còn trống với URL mẫu mờ, nhãn Chưa đặt; dưới mỗi ô có dòng ghi chú](./images/webhook-screen_vi.png)

2. Dán URL vào ô tương ứng: **Gửi tới Slack webhook**, **Gửi tới Google webhook** hoặc **Gửi tới webhook bên thứ ba**.
3. Đọc dòng ghi chú dưới mỗi ô nếu chưa chắc URL đúng dạng — ghi chú nêu nơi lấy URL và một ví dụ. Bấm **Lưu**. Nếu thành công, dưới ô hiện nhãn **Đã lưu** và ô trở về trống — URL không bao giờ hiện lại.
   Nếu ô báo "URL phải dùng https và trỏ tới địa chỉ công khai…", kiểm tra lại URL (xem [Điều kiện & ràng buộc](#điều-kiện--ràng-buộc-hiểu-trước-khi-thao-tác)); khi có ô bị báo lỗi thì không ô nào được lưu.
4. Muốn đổi URL: dán URL mới vào ô và bấm **Lưu**. Để trống ô khi bấm **Lưu** thì URL đã lưu được **giữ nguyên**.
   Muốn ngừng gửi tới một kênh: bấm **Xoá giá trị đã lưu** cạnh nhãn **Đã lưu** của ô đó và xác nhận — URL bị xoá ngay, không hoàn tác được.
5. Gửi thử một báo lỗi — mở terminal tại thư mục gốc của site (cùng chỗ với file `artisan`) và chạy:

   ```
   php artisan tinker --execute="gp247_report('Thử báo lỗi từ site');"
   ```

   Nếu thành công, kênh chat nhận một tin có dòng thời gian, dòng `[site] <địa chỉ site> · env=...` và nội dung `Thử báo lỗi từ site`.

6. Không thấy tin? Mở file `storage/logs/gp247-<ngày>.log`, tìm dòng `gp247 report webhook failed (<tên máy chủ>): <lý do>`.
   Lý do `http_403`, `http_404` nghĩa là URL sai hoặc webhook đã bị xoá ở phía dịch vụ chat.

> ℹ️ **Thông tin:** ô **Chatwork** của các bản trước đã được gỡ — Chatwork không nhận tin qua một URL webhook. URL Chatwork đã nhập (chưa bao giờ hoạt động) bị xoá khi cập nhật.

## Dự phòng trong .env
Mục này dành cho người muốn **vẫn nhận báo lỗi khi cơ sở dữ liệu gặp sự cố** — lúc đó site không đọc được cấu hình lưu trên màn Webhook.

Thêm URL vào file `.env` ở thư mục gốc của site, rồi chạy `php artisan config:clear` (site dùng `config:cache` thì chạy lại `php artisan config:cache`):

```
LOG_SLACK_WEBHOOK_URL=https://hooks.slack.com/services/XXX/YYY/ZZZ
GP247_REPORT_WEBHOOK_URL=https://mattermost.example.com/hooks/XXX
```

| Biến | Dự phòng cho ô | Dùng khi |
| --- | --- | --- |
| `LOG_SLACK_WEBHOOK_URL` | Slack | ô Slack trên màn trống, hoặc không đọc được cơ sở dữ liệu |
| `GP247_REPORT_WEBHOOK_URL` | Webhook bên thứ ba | ô bên thứ ba trên màn trống, hoặc không đọc được cơ sở dữ liệu |

- **Màn hình được ưu tiên**: ô trên màn có URL thì giá trị trong `.env` không được dùng.
- **Hai giới hạn chỉnh được trong `.env`** (không bắt buộc): `GP247_REPORT_TIMEOUT` (mặc định `3` giây mỗi lần gửi) và `GP247_REPORT_THROTTLE` (mặc định `60` giây không gửi lại cùng một lỗi).

## Điều kiện & ràng buộc (hiểu trước khi thao tác)
Các giới hạn dưới đây bảo vệ site và kênh chat; biết trước để không bất ngờ khi màn từ chối URL hay một tin không tới.

**Khi lưu URL trên màn**
- **Bắt buộc `https`** — tin báo lỗi chứa địa chỉ trang và thông tin lỗi, không gửi qua kết nối không mã hoá.
- **Phải là địa chỉ công khai trên Internet** — URL trỏ tới `localhost`, mạng nội bộ (`10.x`, `192.168.x`…) bị từ chối, để không ai lợi dụng site gọi vào hệ thống nội bộ.
- **Không chứa tên đăng nhập / mật khẩu trong URL** (`https://user:pass@...`) — dạng này bị từ chối.
- **Một ô sai thì không ô nào được lưu** — tránh lưu dở một nửa cấu hình.

**Khi gửi**
- **Không đi theo chuyển hướng** — URL trả về chuyển hướng (301/302) bị coi là lỗi gửi; dùng đúng URL cuối mà dịch vụ cấp.
- **Mỗi kênh tối đa 3 giây mỗi lần** — dịch vụ chat chậm không làm trang của khách bị treo.
- **Cùng một lỗi chỉ gửi một lần trong 60 giây**, và **tối đa 30 tin mỗi phút** cho mọi lỗi — lỗi lặp trên trang đông khách không làm ngập kênh hay bị dịch vụ chat chặn. File log vẫn ghi đủ từng lần.
- **Tin dài quá 4000 ký tự bị cắt** — giới hạn độ dài tin của dịch vụ chat; nội dung đầy đủ nằm trong file log.
- **Gửi lỗi không được thử lại** — lần gửi thất bại chỉ ghi vào file log, không lặp lại để tránh dồn tải lúc site đang có sự cố.

## Hỏi & Đáp (Q&A)
**Câu 1: Sau khi lưu, ô lại trống. URL của tôi có bị mất không?**

→ Không. URL được lưu mã hoá và không hiện lại để tránh lộ; nhãn **Đã lưu** dưới ô cho biết đã có URL.

**Câu 2: Tôi muốn xoá URL đã lưu thì làm sao?**

→ Bấm **Xoá giá trị đã lưu** cạnh nhãn **Đã lưu** của ô đó rồi xác nhận. Để trống ô rồi bấm Lưu thì **không** xoá — URL cũ được giữ để tránh xoá nhầm.

**Câu 3: Có cần cron hay hàng đợi (queue) không?**

→ Không. Tin được gửi ngay trong lúc xử lý yêu cầu gặp lỗi — chạy được cả trên shared hosting.

**Câu 4: Tôi dùng Microsoft Teams hoặc Chatwork thì sao?**

→ Hai dịch vụ này không nhận tin dạng `{"text"}` vào một URL nên chưa dùng được trực tiếp. Bạn vẫn có báo lỗi trong file log.

**Câu 5: Vì sao màn báo URL của tôi không hợp lệ dù mở được trên trình duyệt?**

→ URL phải dùng `https` và trỏ tới địa chỉ công khai. URL `http://…`, URL của máy trong mạng nội bộ hay có tên đăng nhập trong URL đều bị từ chối.

**Câu 6: Nhiều site cùng gửi về một kênh, làm sao biết tin của site nào?**

→ Mỗi tin có dòng `[site] <APP_URL> · env=<APP_ENV> · ...`. Đặt `APP_URL` của mỗi site đúng tên miền thật.

**Câu 7: Tin báo lỗi có chứa mật khẩu hay mã bí mật không?**

→ Không có chuỗi truy vấn của URL hay tham số lệnh. Dù vậy tin có địa chỉ trang và nội dung lỗi, nên chỉ gửi vào kênh riêng của đội vận hành.

**Câu 8: Một lỗi xảy ra liên tục nhưng tôi chỉ nhận một tin?**

→ Đúng thiết kế: cùng một lỗi chỉ gửi một lần trong 60 giây. Xem file log để biết số lần thực tế.

**Câu 9: Cơ sở dữ liệu sập thì có nhận được báo lỗi không?**

→ Chỉ khi bạn đặt URL trong `.env` (xem [Dự phòng trong .env](#dự-phòng-trong-env)). URL chỉ lưu trên màn nằm trong cơ sở dữ liệu nên không đọc được lúc đó.

**Câu 10: Tôi muốn tắt hẳn việc gửi ra kênh chat?**

→ Bấm **Xoá giá trị đã lưu** ở mọi ô có URL và để trống các biến dự phòng trong `.env`. Báo lỗi vẫn được ghi vào file log.

---

<sub>📅 **Cập nhật lần cuối:** 2026-11-25 · ✍️ **Tác giả (Author):** GP247</sub>
