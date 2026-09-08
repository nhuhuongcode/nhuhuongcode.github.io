# Portfolio — hướng dẫn deploy & chỉnh sửa

Trang portfolio một file, không cần build, không cần cài gì. Chạy thẳng trên GitHub Pages.

```
site/
├── index.html          ← toàn bộ trang (HTML + CSS + JS)
├── .nojekyll           ← để GitHub Pages không xử lý qua Jekyll
├── README.md           ← file này
└── assets/img/         ← ảnh chụp màn hình dự án
```

---

## 1. Đưa lên GitHub Pages (`username.github.io`)

Thay `USERNAME` bằng tên tài khoản GitHub của bạn.

**Bước 1 — Tạo repo**

Vào https://github.com/new, đặt tên repo **chính xác** là `USERNAME.github.io`
(ví dụ tài khoản `uyennguyen` → repo `uyennguyen.github.io`), chọn **Public**, không tick thêm gì, bấm *Create repository*.

**Bước 2 — Đẩy code lên**

Mở Terminal, chạy từng dòng:

```bash
cd "/Users/nhuhuong/Desktop/project picture/site"

git init
git add .
git commit -m "Portfolio đầu tiên"
git branch -M main
git remote add origin https://github.com/USERNAME/USERNAME.github.io.git
git push -u origin main
```

> Nếu GitHub hỏi mật khẩu: dùng **Personal Access Token** thay cho mật khẩu
> (tạo tại *Settings → Developer settings → Personal access tokens → Tokens (classic)*, tick quyền `repo`).
> Hoặc cài [GitHub Desktop](https://desktop.github.com) rồi kéo thả thư mục `site` vào, khỏi cần dòng lệnh.

**Bước 3 — Bật Pages**

Vào repo trên GitHub → tab **Settings** → mục **Pages** (cột trái) →
*Source*: **Deploy from a branch** → *Branch*: `main` / `/ (root)` → **Save**.

Đợi 1–2 phút, trang sẽ chạy tại:

```
https://USERNAME.github.io
```

**Cập nhật về sau** — sửa `index.html` xong thì:

```bash
cd "/Users/nhuhuong/Desktop/project picture/site"
git add .
git commit -m "Cập nhật nội dung"
git push
```

---

## 2. Sửa nội dung ở đâu

Mở `index.html`, tìm dòng đánh dấu:

```
⬇⬇⬇  SỬA NỘI DUNG Ở ĐÂY  ⬇⬇⬇
```

Toàn bộ nội dung nằm trong hai khối JavaScript, không cần đụng tới HTML hay CSS:

### `PROFILE` — thông tin cá nhân

| Trường | Ý nghĩa |
|---|---|
| `name` | Tên hiển thị ở logo, footer, tiêu đề tab |
| `available` | Dòng chữ trong huy hiệu xanh ở đầu trang |
| `lede` | Câu giới thiệu dưới tiêu đề (cho phép thẻ `<strong>`) |
| `typed` | Các dòng chữ chạy hiệu ứng gõ máy — thêm/bớt tuỳ ý |
| `stats` | Ba con số đếm lên ở hero |
| `about` | Đoạn văn ở mục *Về tôi* |
| `skills` | Nhóm kỹ năng — thêm nhóm mới bằng cách copy một khối `{ group, items }` |
| `contacts` | Các dòng liên hệ. **Nhớ thay `USERNAME` trong link GitHub và điền link LinkedIn.** |

### `PROJECTS` — danh sách dự án

Mỗi dự án là một khối `{ ... }`. Thêm dự án mới bằng cách copy nguyên một khối rồi sửa.

| Trường | Ghi chú |
|---|---|
| `id` | Mã duy nhất, không dấu, không khoảng trắng |
| `kind` | `"web"` · `"app"` · `"dashboard"` — quyết định thẻ lọc và màu nhãn |
| `title` | Tên dự án |
| `status` | `{ type: "live" \| "test" \| "soon", text: "chữ hiển thị" }` |
| `tagline` | 1–2 câu hiện trên thẻ |
| `thumb` | Đường dẫn ảnh thu nhỏ, ví dụ `"assets/img/ten-anh.jpg"`. Để `null` nếu chưa có ảnh |
| `shot` | Ảnh lớn hiện trong popup. Để `null` nếu chưa có |
| `ph` | Chỉ dùng khi chưa có ảnh: `{ icon: "📊", from: "#màu1", to: "#màu2", bars: true }` — trang tự vẽ hình minh hoạ |
| `techs` | Mảng công nghệ. Thẻ chỉ hiện 4 cái đầu, còn lại gộp thành `+n` |
| `role` / `problem` / `features` / `result` | Nội dung trong popup. `features` cho phép thẻ `<strong>` |
| `note` | Khung ghi chú màu vàng trong popup — dùng cho dự án chưa công khai được |
| `links` | `[{ label: "Xem demo", href: "https://..." }]` — để `[]` nếu chưa có link |

### Thêm ảnh mới

Bỏ ảnh vào `assets/img/`, rồi trỏ đường dẫn trong `thumb` / `shot`.
Ảnh nên nén dưới ~300 KB. Tỷ lệ đẹp nhất cho `thumb` là **16:10** (ví dụ 1200×750).
Nếu ảnh là màn hình điện thoại (rất cao), cứ để nguyên — thẻ sẽ tự cắt phần trên.

---

## 3. Ba dự án đang chờ nội dung

| Dự án | Việc cần làm |
|---|---|
| **Ứng dụng di động** | Đang closed testing nên chưa để link Play Store (link closed testing người ngoài mở sẽ báo lỗi). Khi lên production: thêm ảnh, đổi `status` thành `{ type:"live", text:"Trên Google Play" }`, thêm `links` |
| **Dashboard Power BI** | Chờ bản demo dữ liệu giả. Khi có ảnh: điền `thumb` + `shot`, xoá `ph` và `note` |
| **Dashboard Looker Studio** | Như trên. Nếu bản demo public được thì thêm `links` trỏ tới report |

Ba thẻ này hiện đang dùng hình minh hoạ tự vẽ bằng CSS (không phải ảnh thật) nên vẫn trông chỉn chu khi trang đã online.

---

## 4. Xem thử ở máy trước khi push

Mở thẳng `index.html` bằng trình duyệt là được. Muốn giống môi trường thật hơn:

```bash
cd "/Users/nhuhuong/Desktop/project picture/site"
python3 -m http.server 8000
# mở http://localhost:8000
```
