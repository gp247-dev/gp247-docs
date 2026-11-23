> 🌐 **Ngôn ngữ:** 🇻🇳 Tiếng Việt (hiện tại) · [🇬🇧 English](./release.md) · [🇯🇵 日本語](./release_ja.md)

# Phát hành và bảo mật S-Cart

## Giới thiệu
Trang này dành cho **chủ site và người vận hành** S-Cart (dòng 3.x): cho biết mỗi bản phát hành có gì mới, nên dùng phiên
bản nào và cách cập nhật. Bản mới nhất: **S-Cart 3.11.0** (2026-11-23).

## Phiên bản nên dùng
Chạy `php artisan gp247:info` (hoặc `composer show "gp247/*"`) rồi so từng dòng với cột **Tối thiểu khuyến nghị**:

| Package | Tối thiểu khuyến nghị | Mới nhất |
| --- | --- | --- |
| gp247/core | **3.16.0** | 3.18.0 |
| gp247/front | **3.11.0** | 3.14.2 |
| gp247/shop | **3.12.0** | 3.14.1 |
| gp247/mcp | **2.0.1** | 2.1.1 |

- **Thấp hơn** cột "Tối thiểu khuyến nghị" → nên [cập nhật](#cập-nhật-thế-nào).
- **Đã đạt** → site đã có đủ các cải tiến quan trọng, kể cả khi bạn chưa cài lại S-Cart.
- **Thư viện bên thứ ba** → chạy thêm `composer audit` để kiểm, xem [Thư viện bên thứ ba](#thư-viện-bên-thứ-ba).

> ⚠️ **Lưu ý:** cập nhật **cả bộ package cùng lúc**: `gp247/shop` 3.12.0 cần `gp247/front` ≥ 3.11, `gp247/front` 3.10.0 trở lên cần `gp247/core` ≥ 3.14.2, `gp247/shop` 3.11.3 trở lên cần `gp247/core` ≥ 3.14.1, `gp247/front` 3.9.1 và `gp247/shop` 3.11.1 cần `gp247/core` ≥ 3.14, `gp247/front` 3.8.1 và `gp247/shop` 3.10.1 cần `gp247/core` ≥ 3.12.1, `gp247/front` 3.7.0 và `gp247/shop` 3.9.0 cần `gp247/core` ≥ 3.11, `gp247/shop` 3.8.1 cần `gp247/core` ≥ 3.10.3, `gp247/mcp` 2.0.1 cần `gp247/core` ≥ 3.9, `gp247/shop` 3.6.0 cần `gp247/core` ≥ 3.7,
> `gp247/front` 3.2.3 cần `gp247/core` ≥ 3.2.3. Dòng nào còn được hỗ trợ: xem [Vòng đời hỗ trợ](#vòng-đời-hỗ-trợ).

## Vòng đời hỗ trợ
| Dòng | Nền tảng | Trạng thái | Vá bảo mật đến |
| --- | --- | --- | --- |
| **3.x** | Laravel 13 · PHP 8.3+ | ✅ Đang hỗ trợ | 3/2028 |
| 2.x trở xuống | Laravel 12–13 | ⛔ Ngừng hỗ trợ | — |
| S-Cart 10.x trở xuống (`s-cart/s-cart`) | Laravel 12 trở xuống | ⛔ Ngừng phát triển | — |

- **Tính năng mới** chỉ vào dòng mới nhất.
- **Khi có dòng mới:** dòng trước được sửa lỗi nghiêm trọng thêm 6 tháng và vá bảo mật tới thời điểm ở bảng — không quá hạn
  hỗ trợ bảo mật của bản Laravel mà dòng đó dùng.
- **Site còn chạy 2.x trở xuống:** vẫn chạy được nhưng không còn nhận bản sửa nào. Site 2.1 / 2.2 nâng lên 3.x bằng
  `composer require … -W` và `php artisan gp247:update` — xem [Nâng cấp lên dòng 3.x](../install-upgrade/upgrade_vi.md).
- S-Cart 10.x (`s-cart/s-cart`) được tiếp nối bằng S-Cart (`gp247/s-cart`), đánh số lại từ 1.0 và hiện ở dòng 3.x.

## Điểm mới nổi bật
- **Nhân bản không chép SEO** — bản sao bắt đầu với tab SEO trống, không trùng tiêu đề bản gốc *(S-Cart 3.11)*
- **Cài mới mang tên và logo S-Cart** — cửa hàng, trang quản trị, lời chào đặt sẵn *(S-Cart 3.11)*
- **Nút Lưu cho Cấu hình tuỳ chỉnh** — sửa nhiều dòng rồi lưu một lần *(S-Cart 3.11)*
- **Nhóm Facebook ở chân trang** — biểu tượng nhóm Facebook trên giao diện mặc định *(S-Cart 3.11)*

## Cập nhật thế nào
**Bước 1 —** Sao lưu cơ sở dữ liệu và thư mục site.

**Bước 2 —** Cập nhật code:
```bash
composer update gp247/core gp247/front gp247/shop gp247/mcp
```
Site cài trước S-Cart 3.5.0 chưa có MCP server: chạy `composer require gp247/mcp -W` một lần thay cho lệnh trên.

**Bước 3 —** Áp dụng cập nhật dữ liệu, cấu hình, cache:
```bash
php artisan gp247:update
```

**Bước 4 —** Kiểm tra lại phiên bản bằng `php artisan gp247:info`.

Mỗi bản phát hành có thể có thêm việc riêng — xem mục **📋 Cần làm khi cập nhật** của bản đó bên dưới.
Chi tiết từng bước: [Cập nhật GP247 và S-Cart](../install-upgrade/update_vi.md).

## Các bản phát hành
Mới nhất ở trên. Bản *x.**Y*** có tính năng mới; bản *x.y.**Z*** chỉ sửa lỗi.

### S-Cart 3.11.0 — 2026-11-23
**Bản sao không mang SEO của bản gốc; cài mới có sẵn tên và logo S-Cart.**

**✨ Mới**
- **Nhân bản không chép SEO** — bản sao sản phẩm, trang bắt đầu với tab SEO trống, không lên Google với tiêu đề trùng bản gốc
  ([tài liệu](../s-cart/product/product-duplicate_vi.md))
- **Cài mới mang tên và logo S-Cart** — tên cửa hàng, trang quản trị, lời chào, menu đặt sẵn; site đang chạy không đổi
- **Nút Lưu cho Cấu hình tuỳ chỉnh** — sửa nhiều dòng rồi lưu một lần, như các tab cấu hình khác
- **Nhóm Facebook ở chân trang** — biểu tượng nhóm Facebook cạnh Facebook trên giao diện mặc định
- **Cho lập trình viên:** điểm cắm cho plugin SEO (nguồn nội dung cho màn Kiểm tra SEO, JSON-LD bổ sung, 301 của plugin); bộ
  test và CI công khai cho core, front, shop, mcp kèm helper test dùng chung; sản phẩm dựng trên GP247 tự khai tên, logo khi cài

**🔧 Cải thiện:** trang không có mô tả riêng thôi lặp mô tả cửa hàng; màn Kiểm tra SEO chạy được trên MariaDB; mục chuyển
hướng tới trang lỗi chỉ báo khi đích còn 404 trong 7 ngày qua

**📋 Cần làm khi cập nhật**
- Chạy `composer update` rồi `php artisan gp247:update` (đổi khoá link Facebook sang `group_url`, giữ link bạn đã nhập)
- *(Template tự viết)* link Facebook đang đọc `fanpage_url` thì đọc `group_url`, giữ `fanpage_url` làm dự phòng
- *(Site dùng plugin Tin tức)* cập nhật News ≥ 3.2.0 để nhân bản bài viết

<sub>Gồm core 3.18.0 · front 3.14.2 · shop 3.14.1 · mcp 2.1.1 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.11.0)</sub>

### S-Cart 3.10.0 — 2026-11-20
**Gắn GA4, Meta Pixel chỉ bằng dán ID, có banner cookie; nhân bản sản phẩm một nút.**

**✨ Mới**
- **Mã đo lường GA4, GTM, Meta Pixel** — chỉ dán ID, mã chạy theo nhóm cookie khách cho phép
  ([tài liệu](../seo/tracking-and-cookies_vi.md))
- **Banner cookie** — hỏi đồng ý trước, chỉ thông báo hoặc tắt; khách đổi ý bất cứ lúc nào qua "Cài đặt cookie"
- **Doanh thu quảng cáo trong GA4 và Meta** — tự gửi sự kiện xem sản phẩm, thêm giỏ, thanh toán, mua hàng
- **Header bảo mật** — bật/tắt từng header, bật HSTS an toàn từng bước ngay trong trang quản trị
  ([tài liệu](../security/security-production-config_vi.md#header-bảo-mật))
- **Nhân bản sản phẩm và trang** — một nút có bản sao đang tắt, chỉ sửa chỗ khác
  ([tài liệu](../s-cart/product/product-duplicate_vi.md))
- **Tìm sản phẩm theo tên** trong danh sách quản trị; bộ lọc danh mục có ô tìm
- **Cho lập trình viên:** template đổi màu banner bằng biến CSS; plugin nhập dữ liệu ghi 301 từ địa chỉ cũ của nền tảng khác;
  plugin tự chép dữ liệu riêng khi nhân bản sản phẩm ([tài liệu](../seo/seo-for-developers_vi.md))

**🔧 Cải thiện:** lưu sản phẩm, khách hàng, đơn hàng không còn báo trùng khoá trên site nhiều dữ liệu; chuyển hướng 301 chạy cả
với đường dẫn không còn trang nào (vd lấy từ Nhật ký 404); trang danh mục mở nhanh hơn trên cửa hàng lớn

**📋 Cần làm khi cập nhật**
- Chạy `composer update` rồi `php artisan gp247:update` (thêm chỉ mục cho bảng sản phẩm–danh mục; cửa hàng rất lớn nên chạy
  bằng dòng lệnh ngoài giờ cao điểm)
- Site gửi sẵn 4 header bảo mật sau khi cập nhật; site cần được nhúng (iframe) ở tên miền khác thì tắt X-Frame-Options trên
  màn **Header bảo mật**
- Mã đo lường và banner cookie **tắt sẵn** — muốn dùng, vào **SEO › Mã đo lường & cookie** (chỉ Administrator)
- *(Chạy bằng Docker)* lấy `docker/nginx/default.conf` mới của S-Cart để header không bị gửi hai lần; đã tự sửa file này thì
  gộp thay đổi
- *(Template tự viết)* giữ `<x-gp247-front::meta-head>` trong `<head>` để có mã đo lường và banner cookie

<sub>Gồm core 3.16.0 · front 3.12.0 · shop 3.13.0 · mcp 2.1.1 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.10.0)</sub>

### S-Cart 3.9.0 — 2026-11-18
**SEO có sẵn đầy đủ: tab SEO cho từng sản phẩm, tự 301 khi đổi đường dẫn, màn Kiểm tra SEO.**

**✨ Mới**
- **Tab SEO cho từng nội dung** — tiêu đề, mô tả trên Google, ảnh chia sẻ, noindex, canonical riêng cho sản phẩm, danh mục,
  thương hiệu, trang ([tài liệu](../seo/seo-content_vi.md))
- **Tự tạo redirect 301 khi đổi đường dẫn** — link cũ từ Google, Facebook, bookmark vẫn đưa khách tới trang mới
- **Màn Kiểm tra SEO và Nhật ký 404** — liệt kê việc Cần sửa / Nên xem kèm link sửa, nhắc trên Cảnh báo hệ thống; AI agent
  đọc được qua MCP ([tài liệu](../seo/seo-monitoring_vi.md))
- **Xác minh Google/Bing, mẫu tiêu đề, IndexNow** ngay trên màn Meta & JSON-LD, có hướng dẫn từng bước
  ([tài liệu](../seo/seo-settings_vi.md))
- **Trang riêng tư và trang lọc tự giấu khỏi Google** — kèm hreflang tự động, JSON-LD sản phẩm đầy đủ hơn
  ([tài liệu](../seo/seo-automatic_vi.md))
- **Một mục Tuỳ chỉnh giao diện cho mọi template** — chọn template rồi mở trang cài đặt của nó
- **Cho lập trình viên:** plugin/template cắm vào tab SEO, sitemap, JSON-LD, cảnh báo hệ thống; `gp247:doctor` in cả check của
  package ([tài liệu](../seo/seo-for-developers_vi.md))

**🔧 Cải thiện:** quản trị cửa hàng con chỉ lưu, xoá được trang, link, khối bố cục, thương hiệu, danh mục của cửa hàng mình
*(site đa cửa hàng)*; khuyến mãi đã tắt không còn đặt giá bán; cửa hàng hiện 5 sản phẩm một hàng trên màn rộng

**📋 Cần làm khi cập nhật**
- Chạy `composer update` rồi `php artisan gp247:update` (tạo bảng và menu SEO mới)
- Cấp quyền hai màn mới **Kiểm tra SEO**, **Nhật ký 404** cho người quản trị không phải quản trị gốc
- *(Template tự viết hoặc ghi đè `meta-head`)* đồng bộ theo [hợp đồng SEO của template](../seo/seo-for-developers_vi.md#hợp-đồng-seo-của-template) để in thẻ robots, hreflang, mã xác minh
- *(Site dùng plugin Tin tức)* cập nhật News ≥ 3.1.0 để có tab SEO cho tin

<sub>Gồm core 3.15.0 · front 3.11.0 · shop 3.12.0 · mcp 2.1.0 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.9.0)</sub>

### S-Cart 3.8.0 — 2026-11-15
**Khách sắp xếp sản phẩm theo ý mình; thư viện extension hiện đủ, ghi rõ bản cần core mới.**

**✨ Mới**
- **Sắp xếp sản phẩm cho khách** — Nổi bật, Mới nhất, Bán chạy, Giá thấp/cao, Tên A–Z; sắp theo giá dùng đúng giá khuyến mãi
  đang chạy
- **Thanh lọc sản phẩm gọn hơn** — tìm kiếm và sắp xếp chung một hàng, khoảng giá và thương hiệu một hàng, Enter là lọc giá
- **Thư viện extension trực tuyến hiện đủ** — extension cần core mới hơn ghi rõ "Cần core X.Y+" thay vì nút Cài; lọc nhóm tính
  trên cả thư viện
- **Cho lập trình viên:** dữ liệu mẫu `gp247:shop-sample` dùng bộ ảnh S-Cart thay ảnh ngẫu nhiên

**🔧 Cải thiện:** thẻ `og:image` chỉ dùng ảnh của trang hoặc ảnh chia sẻ của cửa hàng; origin bổ sung của MCP server hoạt động
trở lại; site cài mới không chạy lại migration cũ ở lần `gp247:update` đầu

**📋 Cần làm khi cập nhật**
- Chạy `composer update` rồi `php artisan gp247:update`
- Ảnh chia sẻ mẫu `org.jpg` đã bỏ: muốn có ảnh khi chia sẻ link, đặt ảnh của bạn ở **Thông tin website**
- *(Link cũ có `sort_asc` / `sort_desc`)* nay hiển thị theo thứ tự mặc định do quản trị đặt

<sub>Gồm core 3.14.0 · front 3.9.1 · shop 3.11.1 · mcp 2.0.3 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.8.0)</sub>

### S-Cart 3.7.0 — 2026-11-13
**Tên và nội dung hiển thị đúng như bạn gõ — hết `&amp;`.**

**✨ Mới**
- **Chữ lưu đúng như gõ** — tên sản phẩm, danh mục, trang có `&`, `<`, `"` hiện đúng ở quản trị, cửa hàng và API; dữ liệu cũ
  tự chuyển khi cập nhật
- **Mật khẩu và khoá bí mật giữ nguyên ký tự** — mật khẩu có `& < > "` đăng nhập được; mật khẩu SMTP, khoá thanh toán gửi
  đúng tới máy chủ
- **Cảnh báo chỗ in HTML thô** — Cảnh báo hệ thống và `gp247:doctor` chỉ ra file template, plugin của site in biến bằng
  `{!! !!}` ([tài liệu](../security/security-built-in_vi.md))
- **Cảnh báo proxy chưa khai báo** — báo khi trang quản trị đi qua proxy chưa có trong `TRUSTED_PROXIES`, kèm giá trị cần
  thêm ([tài liệu](../security/security-production-config_vi.md))
- **Thông tin server hiện phiên bản GP247 trước tiên** — so ngay với bảng "Phiên bản nên dùng", không cần dòng lệnh
- **Cho lập trình viên:** `gp247_text_plain()` thay `gp247_clean()` (deprecated, gỡ ở 4.0), escape khi in bằng `{{ }}`;
  REST API trả chữ gốc; dịch vụ ghi dùng chung cho sản phẩm, danh mục, thương hiệu, nhà cung cấp, khách hàng

**🔧 Cải thiện:** nội dung khách và quản trị nhập luôn hiện dạng chữ ở cửa hàng và màn đơn hàng; sắp xếp danh sách chỉ nhận
cột hợp lệ; `gp247:info` in phiên bản đúng như tag (3.12.1, không còn 3.12.1.0)

**📋 Cần làm khi cập nhật**
- **Sao lưu cơ sở dữ liệu trước** — `gp247:update` chuyển một lần chữ đã lưu dạng mã hoá (`&amp;` → `&`), không hoàn tác được
- Chạy `composer update` rồi `php artisan gp247:update`
- Mở **Cảnh báo hệ thống** (hoặc `php artisan gp247:doctor`): chỗ template, plugin tự viết in biến bằng `{!! !!}` → đổi sang
  `{{ }}`, trừ nội dung soạn bằng trình soạn thảo HTML
- Mật khẩu SMTP hoặc khoá bí mật có `& < > "` đã lưu trước bản này: nhập lại một lần
- *(Ứng dụng dùng REST API)* chuỗi nay trả đúng như gõ (`&`, không còn `&amp;`) — ứng dụng phải tự escape khi hiển thị

<sub>Gồm core 3.12.1 · front 3.8.1 · shop 3.10.1 · mcp 2.0.2 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.7.0)</sub>

### Các bản cũ hơn
| Bản | Ngày | Tóm tắt |
| --- | --- | --- |
| [S-Cart 3.6.1](https://github.com/gp247net/s-cart/releases/tag/3.6.1) | 2026-11-11 | Sao lưu và phục hồi chắc hơn cho site thật và shared host |
| [S-Cart 3.6.0](https://github.com/gp247net/s-cart/releases/tag/3.6.0) | 2026-11-09 | Sao lưu và phục hồi có sẵn trong S-Cart, chạy được cả trên shared host |
| [S-Cart 3.5.2](https://github.com/gp247net/s-cart/releases/tag/3.5.2) | 2026-11-07 | Cải tiến cho site chạy Docker hoặc đứng sau proxy / CDN |
| [S-Cart 3.5.1](https://github.com/gp247net/s-cart/releases/tag/3.5.1) | 2026-11-05 | Trang quản trị tự báo cấu hình chưa an toàn; cài đặt qua web gọn hơn |
| [S-Cart 3.5.0](https://github.com/gp247net/s-cart/releases/tag/3.5.0) | 2026-11-03 | MCP server có sẵn: hỏi và quản lý cửa hàng bằng AI agent |
| [S-Cart 3.4.0](https://github.com/gp247net/s-cart/releases/tag/3.4.0) | 2026-11-02 | Bán hàng qua ứng dụng riêng và đồng bộ ERP qua REST API |
| [S-Cart 3.3.1](https://github.com/gp247net/s-cart/releases/tag/3.3.1) | 2026-10-29 | Form liên hệ có hộp thư; bật/tắt REST API trong trang quản trị |
| [S-Cart 3.2](https://github.com/gp247net/s-cart/releases/tag/3.2) | 2026-10-23 | Thêm tiếng Nhật, vận chuyển chuẩn có vận đơn, giao diện tự cập nhật theo package |
| [S-Cart 3.1](https://github.com/gp247net/s-cart/releases/tag/3.1) | 2026-10-03 | Yêu cầu thanh toán ngoài giỏ hàng; mã hoá mật khẩu, khoá thanh toán đã lưu |
| [S-Cart 3.0.1](https://github.com/gp247net/s-cart/releases/tag/3.0.1) | 2026-09-04 | Gỡ lệnh `sc:*` cũ, dùng lệnh `gp247:*` — [danh sách lệnh](../cli/cli-introduction_vi.md) |
| [S-Cart 3.0](https://github.com/gp247net/s-cart/releases/tag/3.0) | 2026-08-30 | Mở đầu dòng 3.x: sổ thanh toán từng đơn, giảm giá trừ trước thuế — [ghi chú v3.0](../system/release-notes-3.0_vi.md) |

## Bảo mật

Giữ site an toàn không chỉ là cập nhật — cấu hình, khoá mã hoá, sao lưu, tài khoản và xử lý sự cố có ở bộ tài liệu [Bảo mật hệ thống GP247](../security/security-introduction_vi.md).

GP247 rà soát bảo mật thường xuyên, và các cải tiến được đưa vào từng bản phát hành. Cách đơn giản nhất để giữ site an
toàn là dùng ít nhất phiên bản ở bảng [Phiên bản nên dùng](#phiên-bản-nên-dùng) và cập nhật khi có bản mới.

## Phần mềm máy chủ (PHP, web server)
Lỗi của PHP và web server do chính nhà phát hành của chúng vá, không nằm trong bản phát hành GP247 — hãy cập nhật cả chúng.

| Sự cố | Mức độ | Đã vá ở PHP |
| --- | --- | --- |
| **PHP2Shell** — thực thi mã từ xa (CVE-2026-109618, CVE-2026-109619) · 2026-10-21 | Nghiêm trọng | 8.3.36 · 8.4.27 · 8.5.12 |

**Cần làm gì**
- **Xem phiên bản PHP:** `php -v`, hoặc **Admin → Thông tin server**.
- **PHP từ bản phát hành chính thức** (php.net, Docker image chính thức, đa số bảng điều khiển cho chọn phiên bản PHP): nâng
  lên bản đã vá của nhánh đang dùng, hoặc mới hơn.
- **PHP do Linux (Ubuntu, Debian, RHEL…) hoặc nhà cung cấp hosting quản lý:** các bên này thường vá trên phiên bản cũ, nên
  **chỉ nhìn số phiên bản không biết đã an toàn hay chưa** — cài bản cập nhật mới nhất của hệ điều hành, hoặc hỏi nhà cung
  cấp đã vá CVE-2026-109618 và CVE-2026-109619 chưa.
- **Chưa cập nhật được ngay:** đặt `session.upload_progress.enabled = Off` trong `php.ini` (GP247 không dùng tính năng này)
  rồi khởi động lại PHP. Cách này giảm rủi ro, không thay được việc cập nhật.
- **Chạy bằng Docker:** làm theo mục "Cập nhật bản vá bảo mật" trong
  [DOCKER_vi.md](https://github.com/gp247net/s-cart/blob/master/DOCKER_vi.md).

## Thư viện bên thứ ba
Lỗi của thư viện mà GP247 dùng (Livewire, Symfony…) do chính nhà phát hành thư viện vá; GP247 nâng mức tối thiểu khi cần.
Mã của GP247 không dùng tính năng bị ảnh hưởng của hai lỗi dưới đây, nhưng plugin bên thứ ba có thể dùng — vẫn nên cập nhật.

| Sự cố | Mức độ | Đã vá ở |
| --- | --- | --- |
| **Livewire** — vượt kiểm tra quyền (GHSA-mhf7-xp6r-6qrc) | Trung bình | livewire/livewire 4.4.8 (core 3.10.2 yêu cầu bản này) |
| **symfony/mime** — chèn header email (CVE-2026-45070) | Trung bình | symfony/mime 7.4.22 |

**Cần làm gì**
- **Cập nhật:** `composer update`, rồi kiểm bằng `composer show livewire/livewire symfony/mime`.
- **Kiểm mọi thư viện cùng lúc:** `composer audit` liệt kê các thư viện trong site đang có lỗi đã công bố.

## Báo lỗ hổng bảo mật
Phát hiện lỗ hổng, vui lòng gửi email tới **support@gp247.net** — **không** mở issue công khai trên GitHub để tránh lộ lỗi
trước khi có bản vá.

---

<sub>📅 **Cập nhật lần cuối:** 2026-11-23 · ✍️ **Tác giả (Author):** GP247</sub>
