# ☕ BrewLite

Ứng dụng đặt cà phê không dùng tiền mặt.

---

## 📖 Giới thiệu dự án

**BrewLite** là ứng dụng đặt và thanh toán đồ uống không dùng tiền mặt, giúp khách hàng giảm thời gian xếp hàng và nhận đơn nhanh tại quầy.

Dự án được xây dựng theo mô hình Frontend - Backend tách biệt, sử dụng **Next.js** cho Frontend và **NestJS** cho Backend.

Quy trình phát triển phần mềm được thực hiện theo phương pháp **Agile Scrum**.

---

## 🛠️ Công nghệ sử dụng

### Frontend

- Next.js
- React
- TypeScript
- Tailwind CSS
- Zustand
- React Query

### Backend

- NestJS
- TypeScript
- REST API
- Passport JWT
- class-validator

### Database

- PostgreSQL
- Prisma ORM

### Package Manager

- **pnpm** - khuyến nghị
- **npm** - có thể sử dụng

> Project sử dụng **pnpm** làm package manager chính. Các thành viên trong nhóm nên ưu tiên sử dụng pnpm để thống nhất môi trường phát triển.

---

## 📁 Cấu trúc dự án

```text
BrewLite/
│
├── frontend/                  # Frontend - Next.js
│   ├── src/
│   ├── public/
│   ├── package.json
│   └── ...
│
├── backend/                   # Backend - NestJS
│   ├── src/
│   ├── prisma/
│   ├── package.json
│   └── ...
│
├── package.json               # Cấu hình project root
├── pnpm-workspace.yaml        # Cấu hình pnpm workspace
├── .gitignore
├── README.md
└── ...
```

---

# 🚀 Hướng dẫn cài đặt và chạy dự án

## 1. Yêu cầu hệ thống

Trước khi chạy project, cần cài đặt:

- **Node.js** - khuyến nghị phiên bản LTS
- **PostgreSQL**
- **Git**
- **pnpm** - khuyến nghị

Kiểm tra phiên bản Node.js:

```bash
node -v
```

Kiểm tra npm:

```bash
npm -v
```

Kiểm tra pnpm:

```bash
pnpm -v
```

Kiểm tra Git:

```bash
git --version
```

---

## 2. Clone project

Clone repository:

```bash
git clone <repository-url>
```

Di chuyển vào thư mục project:

```bash
cd BrewLite
```

---

## 3. Cài đặt Dependencies

### Cách 1 - Sử dụng pnpm (khuyến nghị)

Tại thư mục gốc của project:

```bash
pnpm install
```

Nếu project sử dụng pnpm workspace, lệnh trên sẽ cài đặt dependencies cho các package trong workspace.

Sau khi cài đặt xong, có thể chạy toàn bộ project bằng:

```bash
pnpm dev
```

---

### Cách 2 - Sử dụng npm

Nếu không sử dụng pnpm, có thể cài dependencies riêng cho từng phần.

#### Frontend

```bash
cd frontend
npm install
```

#### Backend

```bash
cd ../backend
npm install
```

Sau đó quay lại thư mục gốc:

```bash
cd ..
```

> **Lưu ý:** Không nên sử dụng npm và pnpm lẫn lộn trong cùng một môi trường phát triển. Nhóm khuyến nghị thống nhất sử dụng **pnpm**.

> Nếu project đã sử dụng `pnpm-lock.yaml`, không nên commit thêm `package-lock.json`.

---

# 🔐 4. Cấu hình biến môi trường

Các thông tin nhạy cảm như mật khẩu database, JWT secret và API key không được commit lên Git.

Mỗi thành viên cần tự tạo file `.env` trên máy của mình.

---

## Backend

Tại thư mục:

```text
backend/
```

Tạo file:

```text
.env
```

Dựa trên file:

```text
.env.example
```

Ví dụ:

```env
PORT=4000

DATABASE_URL="postgresql://username:password@localhost:5432/brewlite"

JWT_SECRET="your-secret-key"
JWT_EXPIRES_IN="1d"
```

Thay các giá trị mẫu bằng thông tin PostgreSQL trên máy của bạn.

---

## Frontend

Tại thư mục:

```text
frontend/
```

Tạo file:

```text
.env.local
```

Ví dụ:

```env
NEXT_PUBLIC_API_URL=http://localhost:4000
```

Biến `NEXT_PUBLIC_API_URL` dùng để cấu hình địa chỉ Backend API.

---

# 🗄️ 5. Cấu hình PostgreSQL

Đảm bảo PostgreSQL đã được:

1. Cài đặt trên máy.
2. Khởi động service PostgreSQL.
3. Tạo database cho project.

Ví dụ database:

```text
Database name: brewlite
Host: localhost
Port: 5432
```

Chuỗi kết nối được cấu hình trong:

```env
DATABASE_URL="postgresql://username:password@localhost:5432/brewlite"
```

Backend sử dụng **Prisma ORM** để giao tiếp với PostgreSQL.

Các lệnh Prisma cần thiết sẽ được cập nhật trong quá trình phát triển project.

---

# ▶️ 6. Chạy toàn bộ project

Sau khi:

- Cài đặt dependencies.
- Cấu hình biến môi trường.
- Khởi động PostgreSQL.
- Hoàn tất cấu hình database.

Tại thư mục gốc:

```bash
pnpm dev
```

Lệnh này sẽ khởi động đồng thời Frontend và Backend.

### Frontend

```text
Next.js
http://localhost:3000
```

### Backend

```text
NestJS
http://localhost:4000
```

Kiến trúc khi chạy:

```text
                    ┌───────────────┐
                    │    Browser    │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────┐
                    │    Next.js    │
                    │   Frontend    │
                    │    :3000      │
                    └───────┬───────┘
                            │
                         REST API
                            │
                            ▼
                    ┌───────────────┐
                    │    NestJS     │
                    │    Backend    │
                    │    :4000      │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────┐
                    │  PostgreSQL   │
                    └───────────────┘
```

---

# ▶️ 7. Chạy riêng Frontend và Backend

## Frontend

### Sử dụng pnpm

Từ thư mục gốc:

```bash
pnpm --dir frontend dev
```

Hoặc:

```bash
cd frontend
pnpm dev
```

Frontend chạy tại:

```text
http://localhost:3000
```

### Sử dụng npm

```bash
cd frontend
npm run dev
```

---

## Backend

### Sử dụng pnpm

Từ thư mục gốc:

```bash
pnpm --dir backend start:dev
```

Hoặc:

```bash
cd backend
pnpm start:dev
```

Backend chạy tại:

```text
http://localhost:4000
```

### Sử dụng npm

```bash
cd backend
npm run start:dev
```

---


# 📝 8. Quy tắc Commit

Project sử dụng **Conventional Commits**.

| Type | Mục đích |
|---|---|
| `feat` | Thêm tính năng |
| `fix` | Sửa lỗi |
| `refactor` | Tái cấu trúc code |
| `docs` | Cập nhật tài liệu |
| `style` | Thay đổi format/code style |
| `test` | Thêm hoặc sửa test |
| `chore` | Cấu hình hoặc bảo trì |

Ví dụ:

```bash
git commit -m "feat: add user authentication"

git commit -m "feat: add product management"

git commit -m "fix: fix login validation"

git commit -m "refactor: refactor authentication service"

git commit -m "docs: update README"
```

Commit message nên:

- Ngắn gọn.
- Mô tả đúng thay đổi.
- Không viết nội dung quá chung chung như `update`, `fix`, `change`.

---

# 🔒 9. Bảo mật

Không commit các thông tin nhạy cảm lên Git.

Các thông tin cần bảo mật bao gồm:

- Database username/password.
- Database connection string.
- JWT secret.
- API key.
- Access token.
- Private key.
- Các thông tin xác thực khác.

Các file môi trường thực tế:

```text
.env
.env.local
```

đã được cấu hình trong `.gitignore`.

Thay vào đó, sử dụng:

```text
.env.example
```

để cung cấp danh sách các biến môi trường cần thiết cho project.

Ví dụ:

```env
PORT=
DATABASE_URL=
JWT_SECRET=
JWT_EXPIRES_IN=
```

---

# 🚫 10. Các file không được commit

Không commit các file hoặc thư mục:

```text
node_modules/
.env
.env.local
.next/
dist/
*.log
```

Các file này đã được cấu hình trong `.gitignore`.

Đặc biệt:

```text
package-lock.json
```

không nên được commit nếu nhóm đã thống nhất sử dụng:

```text
pnpm
```

và repository đang sử dụng:

```text
pnpm-lock.yaml
```

---

# 👥 11. Setup project cho thành viên mới

Thành viên mới có thể setup project theo thứ tự:

```text
Clone repository
       ↓
Cài Node.js
       ↓
Cài pnpm
       ↓
pnpm install
       ↓
Tạo file .env
       ↓
Tạo file frontend/.env.local
       ↓
Cấu hình PostgreSQL
       ↓
Cấu hình DATABASE_URL
       ↓
pnpm dev
       ↓
Bắt đầu phát triển
```

Nếu `package.json` hoặc `pnpm-lock.yaml` có thay đổi sau khi pull code:

```bash
git pull
pnpm install
```

sau đó chạy:

```bash
pnpm dev
```

---

# 🧹 12. Một số lưu ý khi phát triển

- Không code trực tiếp trên `main`.
- Commit thường xuyên và rõ ràng.
- Không commit `node_modules`.
- Không commit `.env` hoặc thông tin nhạy cảm.
- Không commit `package-lock.json` nếu project sử dụng pnpm.
- Không tự ý thay đổi cấu trúc project nếu chưa thống nhất với nhóm.
- Trước khi tạo Pull Request cần kiểm tra project chạy bình thường.
- Ưu tiên sử dụng **pnpm** để đảm bảo môi trường phát triển thống nhất.

---

# 📌 Project Status

**Status:** In Development

BrewLite hiện đang trong quá trình phát triển.