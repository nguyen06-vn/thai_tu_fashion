# Final Project Report: Web Design and Development

**Thai Tu Fashion** — website thời trang unisex phong cách Seoul · **Nhóm 5**

🌐 **Website:** https://thai-tu-fashion-v1.vercel.app &nbsp;·&nbsp; 🎬 **Video demo:** https://youtu.be/AcWo1JPZ79o

**Mục lục:** [Thông tin nhóm](#thông-tin-nhóm) · [Tổng quan](#tổng-quan-project-và-công-nghệ-sử-dụng) · [Cài đặt](#hướng-dẫn-cài-đặt-và-chạy-ứng-dụng) · [Task 1](#task-1-project-planning--teamwork) · [Task 2](#task-2-implement-user-interface) · [Task 3](#task-3-database-integration--dynamic-content) · [Task 4](#task-4-optimization) · [Task 5](#task-5-uiux-peer-review--evaluation) · [Deliverables](#deliverables-checklist) · [Đóng góp](#đánh-giá-mức-độ-đóng-góp) · [Self-Reports](#self-reports)

---

## Thông Tin Nhóm

| | |
|---|---|
| **Tên nhóm** | Nhóm 5 |
| **Tên dự án** | Thai Tu Fashion |
| **GitHub Repository** | https://github.com/huynhsy986-droid/thai_tu_fashion |
| **Website** | https://thai-tu-fashion-v1.vercel.app |
| **Video Demo** | https://youtu.be/AcWo1JPZ79o |
| **Ngày nộp** | 21/11/2026 |

### Thành viên nhóm

| Họ tên | MSSV | Vai trò |
|---|---|---|
| Lê Quang Khanh ([@lequangkhanh6002-pixel](https://github.com/lequangkhanh6002-pixel)) | 24090012 | PO/BA & Designer |
| Nguyễn Trần Minh Nguyên ([@nguyen06-vn](https://github.com/nguyen06-vn)) | 24090010 | Backend & Database |
| Huỳnh Tấn Sỹ ([@huynhsy986-droid](https://github.com/huynhsy986-droid)) | 24090017 | Frontend & QA |

---

## Tổng Quan Project và Công Nghệ Sử Dụng

**Mô tả ứng dụng:** Cửa hàng thời trang unisex trực tuyến lấy cảm hứng từ đường phố Seoul, dành cho khách hàng trẻ. Khách xem, lọc, chọn màu–size theo tồn kho thật, đặt hàng và theo dõi đơn; quản trị viên quản lý sản phẩm, tồn kho, đơn hàng, đánh giá và tin nhắn liên hệ.

**Tech stack:**

| Layer | Công nghệ |
|---|---|
| Frontend | HTML, CSS, **Tailwind CSS 3**, JavaScript (SPA) |
| Backend | Node.js 22, Express 5 (REST API) |
| Database | **PostgreSQL 17 trên Supabase** (Auth, Row Level Security) |
| Deploy | **Vercel** (CDN + Function, region Singapore) · Supabase (Singapore) |

**Tính năng chính:**
- **Mua sắm:** tìm kiếm không dấu, lọc theo danh mục/size/màu/giá, giỏ hàng, mã giảm giá, đặt hàng (không bán vượt tồn kho), thanh toán COD/online mô phỏng.
- **Tài khoản:** đăng ký/đăng nhập, quên mật khẩu qua email, theo dõi đơn hàng, yêu thích + báo giảm giá, báo có hàng.
- **Smart Studio:** gợi ý size từ số đo, phối outfit, stylist theo dịp, tìm bằng ảnh, thử đồ ảo (mô phỏng).
- **Giới thiệu & Liên hệ:** số liệu lấy từ database, form liên hệ có kiểm tra dữ liệu.
- **Quản trị:** dashboard doanh thu 8 tuần, sản phẩm, tồn kho, đơn hàng, khách hàng, đánh giá, tin nhắn liên hệ.

| Trang chủ | Chi tiết sản phẩm | Quản trị |
|---|---|---|
| ![Trang chủ](docs/screenshots/home-desktop.jpg) | ![Chi tiết sản phẩm](docs/screenshots/product.jpg) | ![Dashboard quản trị](docs/screenshots/admin-dashboard.jpg) |
| **Cửa hàng** | **Liên hệ (kiểm tra form)** | **Size Advisor** |
| ![Cửa hàng](docs/screenshots/shop.jpg) | ![Liên hệ](docs/screenshots/contact.jpg) | ![Size Advisor](docs/screenshots/size-advisor.jpg) |

---

## Hướng Dẫn Cài Đặt và Chạy Ứng Dụng

**Yêu cầu hệ thống:**

| Công cụ | Phiên bản |
|---|---|
| Node.js | >= 20 (khuyên dùng 22) |
| PostgreSQL | >= 15 (có `psql`) — hoặc dùng Supabase Cloud |

**Các bước cài đặt:**

```bash
# 1. Clone repository
git clone https://github.com/huynhsy986-droid/thai_tu_fashion.git
cd thai_tu_fashion

# 2. Cài đặt dependencies
cd backend && npm install && cd ..

# 3. Cấu hình môi trường (mặc định chạy được với Postgres local)
cp backend/.env.example backend/.env

# 4. Khởi tạo database: migrations + dữ liệu mẫu
DATABASE_URL=postgres://postgres:postgres@localhost:5432/thaitu bash scripts/db-reset.sh

# 5. Chạy ứng dụng → http://localhost:4000
cd backend && npm start
```

**Tài khoản dùng thử (chỉ khi chạy local):** khách `minhanh@demo.thaitu.vn` / `Demo@1234` · quản trị `admin@thaitu.vn` / `Admin@1234`.
Trên website thật, khách tự đăng ký; quyền quản trị do nhóm cấp (`npm run make-admin -- <email>`).

<details>
<summary>Chạy với Supabase Cloud · deploy · kiểm thử</summary>

`backend/.env`:

```
AUTH_PROVIDER=supabase
SUPABASE_URL=https://ceryulbobrlyxckrezts.supabase.co
SUPABASE_ANON_KEY=sb_publishable_JSzQ9dv_Ug9kPvi3qlxr_g_rfHCFc8F
DATABASE_URL=<Supabase → Connect → Session pooler, tự điền mật khẩu>
DATABASE_SSL=true
```

- Deploy Vercel/Render và biến môi trường: [`docs/08-deployment.md`](docs/08-deployment.md)
- Kiểm thử: `cd backend && npm test` (75 unit + 119 integration) · `cd frontend && npm ci && npm run test:e2e` (34 e2e)
- Khi API không chạy, giao diện tự chuyển chế độ dự phòng (dữ liệu lưu trong trình duyệt).

</details>

---

## Task 1: Project Planning & Teamwork

### (a) Phân công vai trò

Chia theo tầng, mỗi người chịu trách nhiệm trọn một mảng (chi tiết: [`docs/00-team-workflow.md`](docs/00-team-workflow.md)):

| Thành viên | Phụ trách |
|---|---|
| **Lê Quang Khanh** | Review prototype, PRD & tiêu chí nghiệm thu, wireframe, project plan, README, kịch bản video, điều phối peer review |
| **Nguyễn Trần Minh Nguyên** | Kiến trúc, thiết kế database & RLS trên Supabase, REST API, đăng nhập/quên mật khẩu, logging |
| **Huỳnh Tấn Sỹ** | Giao diện & kết nối API, Tailwind, trang Giới thiệu/Liên hệ, Lighthouse, GA/Sentry, kiểm thử e2e, CI, deploy |

### (b) Wireframe

- **Tool sử dụng:** wireframe low-fi dựng bằng HTML → xuất PNG (nguồn: [`docs/wireframes/src/`](docs/wireframes/src/)).
- **Các trang đã thiết kế** (10 trang, mỗi trang có bản desktop + mobile — xem tất cả: [`docs/wireframes/`](docs/wireframes/README.md)):
  ✅ Homepage · ✅ Cửa hàng · ✅ Chi tiết sản phẩm · ✅ Giỏ hàng · ✅ Thanh toán · ✅ Đăng nhập · ✅ Tài khoản · ✅ Quản trị · ✅ Giới thiệu · ✅ Liên hệ

| Trang chủ | Chi tiết sản phẩm | Liên hệ (mobile) |
|---|---|---|
| ![](docs/wireframes/01-home-desktop.png) | ![](docs/wireframes/03-product-desktop.png) | ![](docs/wireframes/10-contact-mobile.png) |

### (c) Project Plan

5 sprint ứng với 5 task của brief; mỗi sprint là một **Milestone**, mỗi việc là một **Issue** có nhãn task và người phụ trách. Chi tiết: [`docs/09-project-plan.md`](docs/09-project-plan.md).

**Milestones:**

| Milestone | Deadline | Trạng thái |
|---|---|---|
| Hoàn thành wireframe | 23/11/2026 | Đúng hạn |
| Setup GitHub & database schema | 23/11/2026 | Đúng hạn |
| Hoàn thành UI cơ bản | 25/11/2026 | Đúng hạn |
| Tích hợp database xong | 27/11/2026 | Đúng hạn |
| Optimization & peer review | 30/11 · 06/12/2026 | Optimization đúng hạn · Peer review đang thực hiện |
| Nộp bài | 07/12/2026 | Nộp ngày 21/11/2026 — đúng hạn |

### (d) GitHub Repository

- **Repository link:** https://github.com/huynhsy986-droid/thai_tu_fashion — [Issues](https://github.com/huynhsy986-droid/thai_tu_fashion/issues?q=is%3Aissue) · [Pull Requests](https://github.com/huynhsy986-droid/thai_tu_fashion/pulls?q=is%3Apr+is%3Amerged) · [Milestones](https://github.com/huynhsy986-droid/thai_tu_fashion/milestones)

### (e) Quy trình làm việc trên GitHub

**Issue → branch `feature/<số-issue>-…` → commit nhỏ `type(scope): mô tả (#issue)` → Pull Request có `Closes #issue` → CI xanh → merge.** Mỗi thành viên commit bằng tài khoản của mình.

**Ví dụ commit messages tiêu biểu:**

```
feat(api): POST /api/contact và quản trị /api/admin/contacts (#3)
chore(ui): cài Tailwind CSS v3, theme theo design system (#5)
perf(web): defer script, ảnh hero theo kích thước màn hình + preload LCP (#8)
fix(test): logger giả đủ hàm info/debug — CI xanh lại (#29)
```

| Pull Request #25 | Lịch sử commit |
|---|---|
| ![Pull Request #25](docs/screenshots/github-pull-request.png) | ![Danh sách commit](docs/screenshots/github-commits.png) |

*Vài commit có dấu ✗ đỏ là lỗi CI trong code test, đã ghi nhận ở issue [#29](https://github.com/huynhsy986-droid/thai_tu_fashion/issues/29) và sửa ở PR #30.*

---

## Task 2: Implement User Interface

### (a) Các trang đã xây dựng

| Trang | URL / Route | Mô tả | Người thực hiện |
|---|---|---|---|
| Homepage | `/#home` | Hero, danh mục, sản phẩm bán chạy, lookbook | Cả nhóm |
| Cửa hàng | `/#shop` | Lọc, sắp xếp, tìm kiếm | Cả nhóm · Huỳnh Tấn Sỹ |
| Chi tiết sản phẩm | `/#product-<id>` | Ảnh, màu/size theo tồn kho, đánh giá | Cả nhóm · Huỳnh Tấn Sỹ |
| Giỏ hàng · Thanh toán | `/#cart`, `/#checkout` | Mã giảm giá, đặt hàng | Huỳnh Tấn Sỹ |
| Đăng nhập · Tài khoản | `/#login`, `/#account` | Đăng ký, quên mật khẩu, đơn hàng, yêu thích | Huỳnh Tấn Sỹ |
| Quản trị | `/#admin` | 8 tab quản trị | Huỳnh Tấn Sỹ · Nguyễn Trần Minh Nguyên |
| Contact / About | `/#contact`, `/#about` | Form liên hệ, FAQ; giới thiệu thương hiệu | Huỳnh Tấn Sỹ |

### (b) Sử dụng Tailwind CSS

Cài **Tailwind CSS 3** bằng CLI (`npm run build:css`). Dùng `prefix: 'tw-'` và tắt `preflight` để không ảnh hưởng CSS sẵn có; màu, font, bo góc lấy từ design system nên giao diện đồng nhất. Áp dụng cho màn Đăng nhập, Giới thiệu, Liên hệ.

**Ví dụ utility classes đặc trưng nhóm đã dùng:** lưới responsive `tw-grid tw-grid-cols-1 lg:tw-grid-cols-[minmax(0,5fr)_minmax(0,7fr)]`, màu theo design system `tw-bg-grey tw-text-ink-soft`, ảnh `tw-aspect-[3/4] tw-object-cover`.

### (c) Các tính năng tương tác

| Tính năng | Mô tả | File / Component | Người thực hiện |
|---|---|---|---|
| Form validation | Đăng ký (thanh độ mạnh mật khẩu), thanh toán, liên hệ — lỗi tiếng Việt dưới từng ô | `js/auth.js`, `js/info.js` | Huỳnh Tấn Sỹ |
| Modal / menu | Tìm kiếm gợi ý, menu mobile, menu người dùng, xác nhận huỷ đơn | `js/app.js`, `js/auth.js` | Cả nhóm |
| Slider | Thanh thông báo chạy, thư viện ảnh sản phẩm | `js/components.js` | Cả nhóm |
| Bộ lọc động | Lọc, sắp xếp, tìm không dấu | `js/pages.js` | Cả nhóm |
| Smart Studio | Size Advisor, Outfit Builder, tìm bằng ảnh | `js/studio.js` | Cả nhóm |

Các tương tác được kiểm tra tự động bằng 34 kịch bản Playwright (`frontend/e2e/`).

### (d) Giao diện trên nhiều thiết bị

- [x] Mobile (< 768px)
- [x] Tablet (768px – 1024px)
- [x] Desktop (> 1024px)

| Mobile 390px | Tablet 820px | Desktop 1280px |
|---|---|---|
| ![](docs/screenshots/home-mobile.jpg) | ![](docs/screenshots/home-tablet.jpg) | ![](docs/screenshots/home-desktop.jpg) |

---

## Task 3: Database Integration & Dynamic Content

### (a) Thiết kế cơ sở dữ liệu

- **Database system:** PostgreSQL 17 (Supabase)
- **Số bảng:** 19 — tất cả bật Row Level Security

**Danh sách bảng:**

| Bảng | Mô tả | Các cột chính |
|---|---|---|
| `profiles` | Người dùng (khách / admin) | `id`, `full_name`, `email`, `role` |
| `categories`, `products`, `product_variants` | Danh mục, sản phẩm, biến thể màu × size | `name`, `price`, `sale_price`, `size`, `stock` |
| `cart_items`, `wishlist_items` | Giỏ hàng, yêu thích | `user_id`, `variant_id`, `quantity` |
| `orders`, `order_items`, `order_status_history` | Đơn hàng và lịch sử trạng thái | `id` (TTxxxx), `status`, `total` |
| `reviews` | Đánh giá | `product_id`, `rating`, `status` |
| `coupons` | Mã giảm giá | `code`, `type`, `value` |
| `contact_messages` | Tin nhắn liên hệ | `name`, `email`, `message`, `status` |
| *8 bảng khác* | Thông báo, số đo, outfit, nhận tin, bảng tra cứu… | xem ERD |

ER diagram và mô tả đầy đủ: [`docs/04-database-erd.md`](docs/04-database-erd.md)

### (b) Kết nối cơ sở dữ liệu

- **Công nghệ server-side:** Node.js + Express, thư viện `pg`
- **Cách kết nối:** RESTful API ([`docs/openapi.yaml`](docs/openapi.yaml)); mỗi truy vấn chạy dưới quyền người dùng nên RLS của Supabase là lớp phân quyền thật.
- **Các thao tác CRUD đã implement:**
  - [x] Create — đăng ký, đặt hàng, đánh giá, gửi liên hệ, admin thêm sản phẩm
  - [x] Read — sản phẩm, đơn hàng, dashboard, tin nhắn
  - [x] Update — hồ sơ, giỏ hàng, trạng thái đơn, giá/tồn kho
  - [x] Delete — xoá khỏi giỏ/yêu thích, danh mục, đánh giá, tin nhắn

```
Trình duyệt (SPA)  ──HTTPS/JSON──►  Express API (Vercel)  ──SQL + RLS──►  Supabase PostgreSQL
```

### (c) Các trang hiển thị dữ liệu động

| Trang | Dữ liệu hiển thị | Query / Endpoint | Người thực hiện |
|---|---|---|---|
| Trang chủ, Cửa hàng | 66 sản phẩm, tồn kho, điểm đánh giá | `GET /api/catalog` | Nguyễn Trần Minh Nguyên · Huỳnh Tấn Sỹ |
| Chi tiết sản phẩm | Sản phẩm, đánh giá | `GET /api/products/{id}` | Nguyễn Trần Minh Nguyên · Huỳnh Tấn Sỹ |
| Tài khoản → Đơn hàng | Đơn của tôi + trạng thái | `GET /api/orders` | Nguyễn Trần Minh Nguyên · Huỳnh Tấn Sỹ |
| Quản trị → Tổng quan | Doanh thu, đơn theo trạng thái, sắp hết hàng | `GET /api/admin/dashboard` | Nguyễn Trần Minh Nguyên · Huỳnh Tấn Sỹ |
| Quản trị → Liên hệ | Tin nhắn khách gửi | `GET /api/admin/contacts` | Nguyễn Trần Minh Nguyên · Huỳnh Tấn Sỹ |

| Quản trị → Đơn hàng | Giỏ hàng (mobile) |
|---|---|
| ![](docs/screenshots/admin-orders.jpg) | ![](docs/screenshots/cart-mobile.jpg) |

---

## Task 4: Optimization

### (a) Kiểm tra hiệu năng với Lighthouse

Đo trang chủ bằng Lighthouse (Chrome). **Trước:** bản trước tối ưu chạy ở máy nhóm · **Sau:** website thật trên Vercel. Chi tiết: [`docs/10-lighthouse.md`](docs/10-lighthouse.md).

**Kết quả trước khi tối ưu → sau khi tối ưu:**

| Metric | Mobile | Desktop |
|---|---|---|
| Performance | 74 → **86** | 95 → **99** |
| Accessibility | 95 → **100** | 95 → **100** |
| Best Practices | 100 → 100 | 100 → 100 |
| SEO | 100 → 100 | 100 → 100 |

| | Mobile | Desktop |
|---|---|---|
| **Trước** | ![Lighthouse mobile trước](docs/screenshots/lighthouse-before-home-mobile.jpg) | ![Lighthouse desktop trước](docs/screenshots/lighthouse-before-home-desktop.jpg) |
| **Sau** | ![Lighthouse mobile sau](docs/screenshots/lighthouse-after-vercel-mobile.png) | ![Lighthouse desktop sau](docs/screenshots/lighthouse-after-vercel-desktop.png) |

**Các vấn đề đã xác định và cách khắc phục:**

| Vấn đề | Hành động khắc phục |
|---|---|
| Chưa nén dữ liệu | Bật gzip trên server; CDN Vercel nén file tĩnh |
| Script chặn hiển thị | Thêm `defer` cho 13 file JavaScript |
| Ảnh lớn hơn màn hình | Ảnh nhiều kích thước (`srcset`), tải trước ảnh lớn nhất |
| Màu chữ chưa đủ tương phản | Chỉnh màu đạt chuẩn WCAG AA (4,5:1) |
| Thứ tự tiêu đề sai | Sửa tiêu đề cột chân trang `h4` → `h2` |
| Màn hình trắng khi tải | Khung tải skeleton cùng bố cục trang |

Thời gian hiện nội dung đầu tiên trên mobile giảm từ 3,0 s xuống **1,5 s**; TBT về **0 ms**. Mobile còn 86 vì ảnh hero tải qua mạng thật (LCP 4,2 s) — hướng cải thiện tiếp: đặt ảnh hero sẵn trong HTML.

### (b) Theo dõi lỗi và hành vi người dùng

**Google Analytics:**
- [x] Đã tích hợp trong code — **chưa bật trên website** (chưa tạo property GA4)
- **Tracking ID / Measurement ID:** `G-XXXXXXXXXX` (đặt vào biến `GA_MEASUREMENT_ID` trên Vercel để bật)
- Gửi lượt xem từng trang và sự kiện mua hàng: xem sản phẩm, thêm giỏ, thanh toán, đăng ký, liên hệ.

**Sentry (hoặc tương đương):**
- [x] Đã tích hợp trong code — **chưa bật trên website**; nhật ký lỗi JSON có mã request **đang chạy** (Vercel → Logs)
- **Tool sử dụng:** Sentry (trình duyệt + server)
- **Project DSN / Config:** biến `SENTRY_DSN`, `SENTRY_DSN_BROWSER` trên Vercel
- Theo dõi lỗi JavaScript trên trình duyệt và lỗi server (500); mỗi lỗi có mã `requestId` để tra cứu.

---

## Task 5: UI/UX Peer Review & Evaluation


### (a) Feedback cho các nhóm khác

*Đại diện Nhóm 5 đánh giá: **Lê Quang Khanh**. tiêu chí đánh giá dự án : [`docs/peer-review/`](docs/peer-review/).*

Review ngày 22/11/2026 trên Chrome, máy tính và điện thoại.
 
**Nhóm được review #1:**
- **Tên nhóm / Dự án:** Nhóm FocuSpace/Nhóm 2 - FocuSpace, phòng học ảo pixel có nhạc Lo-fi
- **Link dự án:** https://focuspace-iota.vercel.app

| Khía cạnh | Điểm mạnh | Gợi ý cải thiện | 
|---|---|---|
| Usability | Dùng ngay không cần tài khoản; menu gọn, mobile có nút ☰; Pomodoro 4 nhịp (Cổ điển, Sâu, Nhẹ, Tùy chỉnh); Thư viện lọc theo phòng và nhóm đồ vật. Có thể bắt đầu dùng ngay, không cần học trước. | Căn phòng trên điện thoại dọc bị xoay ngang 90°, không có hướng dẫn xoay máy; bấm cửa sổ chưa thấy bảng chỉnh thời tiết hiện ra dù trang Giới thiệu có hướng dẫn. |
| Aesthetics | Pixel art đồng nhất, bảng màu nâu–cam ấm hợp chủ đề Lo-fi; tranh phòng học rất có không khí; font dễ đọc tiếng Việt. | Thẻ Thư viện ghi kích thước pixel (26×26) không cần thiết với người dùng; nút Đăng nhập màu nhạt trông như bị vô hiệu. Có thể đổi sang màu nổi hơn để người dùng nhận ra ngay. |
| User-Friendliness | Lỗi form tiếng Việt dưới từng ô; nhãn trình đọc màn hình chi tiết; trang Giới thiệu có "Cách dùng nhanh" và nói rõ quyền riêng tư. | Trang Thống kê khi chưa đăng nhập nên có biểu đồ mẫu; thiếu "Quên mật khẩu"; Liên hệ nên có form ngay trên web. |

**Nhóm được review #2:**
- **Tên nhóm / Dự án:** Nhóm PawPass/Nhóm 4 - PawPass, sổ hộ chiếu thú cưng
- **Link dự án:** https://pawpass-hosothucung-web.vercel.app

| Khía cạnh | Điểm mạnh | Gợi ý cải thiện |
|---|---|---|
| Usability | Trang Giới thiệu dẫn dắt rõ: vấn đề → tính năng → "Bắt đầu trong 3 bước"; điện thoại không tràn ngang, nút đủ to. | Trang gốc mở thẳng màn đăng nhập, khách mới chưa biết sản phẩm làm gì → nên để trang Giới thiệu làm trang đầu; màn đăng nhập thiếu thanh menu như các trang khác. |
| Aesthetics | Chủ đề "hộ chiếu" sáng tạo, nhất quán: con dấu tiêm phòng, mèo/cún minh hoạ, màu cam–kem ấm áp; thẻ ví dụ bé "Mochi" cho thấy ngay sản phẩm. | Dòng báo lỗi đỏ nhỏ trên nền hồng hơi khó đọc; trên máy tính phần giới thiệu cạnh form đăng nhập khá nhỏ. |
| User-Friendliness | Lỗi form tiếng Việt, viền đỏ; form Liên hệ đếm ký tự và cảnh báo không ghi thông tin riêng tư; có FAQ. | Thiếu "Quên mật khẩu"; Liên hệ qua GitHub Issue cần tài khoản GitHub → thêm lựa chọn email; nên có tài khoản demo để dùng thử trước khi đăng ký. |

### (b) Xử lý feedback từ các nhóm khác

| Feedback | Nguồn (nhóm nào) | Quyết định | Lý do / Commit |
|---|---|---|---|
| | | | |

---

## Deliverables Checklist

- [x] **Source code trên GitHub**: https://github.com/huynhsy986-droid/thai_tu_fashion
- [x] **README.md**: hướng dẫn cài đặt, tổng quan, tính năng có screenshots, ERD
- [x] **Video demo trên YouTube**: https://youtu.be/AcWo1JPZ79o
- [ ] **Self-Report**: mỗi thành viên đã commit file vào `docs/self-reports/`

---

## Self-Reports

| Họ tên | MSSV | Link Self-Report |
|---|---|---|
| Lê Quang Khanh | 24090012 | [self-report-24090012.md](docs/self-reports/self-report-24090012.md) |
| Nguyễn Trần Minh Nguyên | 24090010 | [self-report-24090010.md](docs/self-reports/self-report-24090010.md) |
| Huỳnh Tấn Sỹ | 24090017 | [self-report-24090017.md](docs/self-reports/self-report-24090017.md) |

<details>
<summary>Tài liệu kỹ thuật</summary>

| Tài liệu | Nội dung |
|---|---|
| [`docs/02-PRD.md`](docs/02-PRD.md) | Yêu cầu sản phẩm, tiêu chí nghiệm thu |
| [`docs/03-solution-architecture.md`](docs/03-solution-architecture.md) | Kiến trúc hệ thống |
| [`docs/04-database-erd.md`](docs/04-database-erd.md) | ERD, phân quyền RLS |
| [`docs/05-api-docs.md`](docs/05-api-docs.md) · [`openapi.yaml`](docs/openapi.yaml) | Tài liệu API |
| [`docs/06-test-report.md`](docs/06-test-report.md) | Báo cáo kiểm thử |
| [`docs/08-deployment.md`](docs/08-deployment.md) | Deploy Vercel / Render |
| [`docs/10-lighthouse.md`](docs/10-lighthouse.md) | Báo cáo Lighthouse |

</details>
