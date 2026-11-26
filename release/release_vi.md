> 🌐 **Ngôn ngữ:** 🇻🇳 Tiếng Việt (hiện tại) · [🇬🇧 English](./release.md) · [🇯🇵 日本語](./release_ja.md)

# Phát hành và bảo mật S-Cart

## Giới thiệu
Trang này dành cho **chủ site và người vận hành** S-Cart (dòng 3.x): cho biết mỗi bản phát hành có gì mới, nên dùng phiên
bản nào và cách cập nhật. Bản mới nhất: **S-Cart 3.12.0** (2026-11-26).

## Phiên bản nên dùng
Chạy `php artisan gp247:info` (hoặc `composer show "gp247/*"`) rồi so từng dòng với cột **Tối thiểu khuyến nghị**:

| Package | Tối thiểu khuyến nghị | Mới nhất |
| --- | --- | --- |
| gp247/core | **3.16.0** | 3.19.0 |
| gp247/front | **3.11.0** | 3.15.0 |
| gp247/shop | **3.12.0** | 3.16.0 |
| gp247/mcp | **2.0.1** | 2.1.1 |

- **Thấp hơn** cột "Tối thiểu khuyến nghị" → nên [cập nhật](#cập-nhật-thế-nào).
- **Đã đạt** → site đã có đủ các cải tiến quan trọng, kể cả khi bạn chưa cài lại S-Cart.
- **Thư viện bên thứ ba** → chạy thêm `composer audit` để kiểm, xem [Thư viện bên thứ ba](#thư-viện-bên-thứ-ba).

> ⚠️ **Lưu ý:** luôn cập nhật **cả bộ package cùng lúc** bằng lệnh ở [Cập nhật thế nào](#cập-nhật-thế-nào) — Composer tự chọn
> các bản khớp nhau (vd `gp247/shop` 3.16.0 cần `gp247/core` ≥ 3.19). Dòng nào còn được hỗ trợ: xem [Vòng đời hỗ trợ](#vòng-đời-hỗ-trợ).

## Vòng đời hỗ trợ
| Dòng | Nền tảng | Trạng thái | Vá bảo mật đến |
| --- | --- | --- | --- |
| **3.x** | Laravel 13 · PHP 8.3+ | ✅ Đang hỗ trợ | 3/2028 |
| 2.x trở xuống | Laravel 12–13 | ⛔ Ngừng hỗ trợ | — |

- **Tính năng mới** chỉ vào dòng mới nhất.
- **Khi có dòng mới:** dòng trước được sửa lỗi nghiêm trọng thêm 6 tháng và vá bảo mật tới thời điểm ở bảng — không quá hạn
  hỗ trợ bảo mật của bản Laravel mà dòng đó dùng.
- **Site còn chạy 2.x trở xuống:** vẫn chạy được nhưng không còn nhận bản sửa nào. Site 2.1 / 2.2 nâng lên 3.x bằng
  `composer require … -W` và `php artisan gp247:update` — xem [Nâng cấp lên dòng 3.x](../install-upgrade/upgrade_vi.md).

## Điểm mới nổi bật
- **Dữ liệu của tôi** — khách tự tải bản sao dữ liệu và tự xoá tài khoản, có thời gian chờ để đổi ý *(S-Cart 3.12)*
- **Yêu cầu dữ liệu cá nhân** — xử lý mọi yêu cầu xem, xoá dữ liệu của khách trên một màn, có hạn xử lý *(S-Cart 3.12)*
- **Hạn lưu giữ dữ liệu** — tự dọn dữ liệu cũ theo số ngày bạn đặt, không cần cron *(S-Cart 3.12)*
- **Chọn tỉnh, phường từ danh sách** — gõ để tìm, tra theo mã bưu chính khi có plugin địa chỉ *(S-Cart 3.12)*

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

### S-Cart 3.12.0 — 2026-11-26
**Khách tự tải, tự xoá dữ liệu của mình; địa chỉ chọn từ danh sách.**

**✨ Mới**
- **Dữ liệu của tôi** — khách tự tải bản sao dữ liệu (tệp ZIP) và tự xoá tài khoản, có thời gian chờ để đổi ý
  ([tài liệu](../s-cart/personal-data/personal-data_vi.md))
- **Yêu cầu dữ liệu cá nhân** — một màn xử lý mọi yêu cầu xem, xoá của khách, kể cả khách không có tài khoản qua trang
  `/privacy-request`; quá hạn có cảnh báo
- **Xoá khách là xoá sạch** — dữ liệu cá nhân bị xoá ở mọi nơi, đơn hàng giữ cho sổ sách và bỏ tên, liên hệ; khôi phục bản sao lưu
  cũ không đưa khách đã xoá trở lại
- **Hạn lưu giữ dữ liệu** — tự dọn giỏ hàng bỏ dở, tin nhắn liên hệ, nhật ký cũ theo số ngày bạn đặt, không cần cron
- **Chọn tỉnh, phường từ danh sách** — khách gõ để tìm, tra theo mã bưu chính khi cài plugin địa chỉ của quốc gia
  ([tài liệu](../s-cart/customer-address/customer-address_vi.md))
- **Cho lập trình viên:** plugin khai báo bảng có dữ liệu khách để được tải, xoá, dọn theo hạn
  ([tài liệu](../extension/declare-personal-data_vi.md)); plugin địa chỉ theo quốc gia
  ([tài liệu](../extension/create-address-plugin_vi.md)); lệnh `gp247:personal-data-retention`

**🔧 Cải thiện:** bản sao lưu không còn gói kèm bản sao bảng do lần phục hồi trước tạo ra; plugin, template mất thư mục gỡ đăng ký
được bằng nút **Gỡ đăng ký** rồi cài lại như mới; Composer thôi cảnh báo gói `laravel/legacy-factories` bị bỏ

**📋 Cần làm khi cập nhật**
- Chạy `composer update` rồi `php artisan gp247:update` (tạo bảng yêu cầu dữ liệu, hạn lưu giữ; thêm cột lần đăng nhập cuối của khách)
- Xem màn **Bảo mật › Hạn lưu giữ dữ liệu**: các mục bật sẵn (nhật ký thao tác quản trị giữ 365 ngày, giỏ hàng 180 ngày…) bắt đầu dọn
  sau 30 ngày — muốn giữ lâu hơn thì đổi số ngày hoặc tắt trước đó
- Nút **Xoá** khách trong quản trị nay tạo yêu cầu xoá, chờ 3 ngày rồi mới xoá (huỷ được; đổi số ngày ở **Cấu hình website › Dữ liệu cá nhân**)
- Đặt liên kết tới trang `/privacy-request` ở chân trang hoặc trang chính sách bảo mật (trang chỉ có khi cửa hàng đã bật gửi email)
- *(Template tự viết)* thêm mục **Dữ liệu của tôi** vào khu tài khoản — giao diện mặc định và GP247-EC ≥ 1.0.7 có sẵn
- *(Code của site còn gọi `factory()` kiểu Laravel 7)* chạy `composer require laravel/legacy-factories`

<sub>Gồm core 3.19.0 · front 3.15.0 · shop 3.16.0 · mcp 2.1.1 · [GitHub Release](https://github.com/gp247net/s-cart/releases/tag/3.12.0)</sub>

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

### Các bản cũ hơn
| Bản | Ngày | Tóm tắt |
| --- | --- | --- |
| [S-Cart 3.7.0](https://github.com/gp247net/s-cart/releases/tag/3.7.0) | 2026-11-13 | Tên và nội dung hiển thị đúng như bạn gõ — hết `&amp;` |
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
| [S-Cart 3.0](https://github.com/gp247net/s-cart/releases/tag/3.0) | 2026-08-30 | Mở đầu dòng 3.x: sổ thanh toán từng đơn, giảm giá trừ trước thuế |

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

<sub>📅 **Cập nhật lần cuối:** 2026-11-26 · ✍️ **Tác giả (Author):** GP247</sub>
