# DVN Project Management

Ứng dụng web quản lý dự án của **DVN Tech**, được xây dựng bằng Next.js và React. Dự án cung cấp bộ khung Dashboard để tiếp tục phát triển các nghiệp vụ quản lý dự án, thành viên, công việc và tiến độ.

> **Trạng thái hiện tại:** dự án đang ở giai đoạn khởi tạo giao diện. Các chức năng đã có trong mã nguồn được mô tả ở phần [Chức năng hiện tại](#chức-năng-hiện-tại). Những chức năng quản lý nghiệp vụ như tạo dự án, CRUD task, đăng nhập và báo cáo chưa được triển khai.

## Mục lục

- [Tổng quan](#tổng-quan)
- [Chức năng hiện tại](#chức-năng-hiện-tại)
- [Công nghệ sử dụng](#công-nghệ-sử-dụng)
- [Yêu cầu môi trường](#yêu-cầu-môi-trường)
- [Cài đặt và chạy dự án](#cài-đặt-và-chạy-dự-án)
- [Biến môi trường](#biến-môi-trường)
- [Các lệnh thường dùng](#các-lệnh-thường-dùng)
- [Cấu trúc thư mục](#cấu-trúc-thư-mục)
- [Kiến trúc ứng dụng](#kiến-trúc-ứng-dụng)
- [Hướng dẫn sử dụng giao diện hiện tại](#hướng-dẫn-sử-dụng-giao-diện-hiện-tại)
- [Tích hợp Backend/API](#tích-hợp-backendapi)
- [Build và triển khai](#build-và-triển-khai)
- [Tình trạng phát triển](#tình-trạng-phát-triển)
- [Đóng góp](#đóng-góp)

## Tổng quan

DVN Project Management hướng tới một hệ thống tập trung giúp đội nhóm theo dõi và điều phối dự án. Giao diện hiện tại đã đặt nền móng cho:

- Khung Dashboard với Sidebar và Navbar dùng chung.
- Nhận diện đội nhóm **DVN TEAM** ở chế độ Private.
- Thanh tìm kiếm trên Navbar.
- Điều hướng tới khu vực Settings.
- Quản lý trạng thái giao diện bằng Redux Toolkit.
- Lưu trạng thái giao diện ở trình duyệt bằng Redux Persist.
- Kết nối API thông qua Redux Toolkit Query với URL cấu hình từ biến môi trường.
- Hỗ trợ giao diện sáng/tối ở cấp class Tailwind cho các thành phần đã khai báo.

## Chức năng hiện tại

### Đã triển khai

| Khu vực | Mô tả |
| --- | --- |
| Dashboard shell | Bố cục toàn màn hình gồm Sidebar cố định bên trái và nội dung chính bên phải. |
| Thương hiệu đội nhóm | Hiển thị tên DVN Tech, logo và thông tin DVN TEAM / Private. |
| Navbar | Hiển thị ô nhập tìm kiếm và biểu tượng Settings. |
| Điều hướng Settings | Có liên kết tới `/settings`; trang đích cần được triển khai nếu chưa tồn tại. |
| Global state | Có các state `isSidebarCollapsed` và `isDarkMode`, cùng các action tương ứng. |
| Persistence | State `global` được lưu vào `localStorage` thông qua Redux Persist ở phía trình duyệt. |
| API foundation | RTK Query đã được cấu hình với `NEXT_PUBLIC_API_URL` làm `baseUrl`; hiện chưa có endpoint cụ thể. |
| Responsive layout | Nội dung chính có khoảng đệm phù hợp khi Sidebar hiển thị trên màn hình kích thước trung bình trở lên. |

### Chưa triển khai

Các mục dưới đây chưa có route, component nghiệp vụ hoặc endpoint tương ứng trong mã nguồn hiện tại:

- Đăng ký, đăng nhập, đăng xuất và phân quyền người dùng.
- Quản lý thành viên và hồ sơ người dùng.
- Tạo, sửa, xóa và xem chi tiết dự án.
- Quản lý task, trạng thái, độ ưu tiên, người phụ trách và deadline.
- Kanban board, Gantt chart và kéo thả task.
- Dashboard thống kê, biểu đồ và báo cáo tiến độ.
- Thông báo, bình luận, tệp đính kèm và activity log.
- Tìm kiếm dữ liệu thực tế (ô tìm kiếm hiện mới là giao diện).
- Các API endpoint và cơ chế xác thực với backend.

## Công nghệ sử dụng

- **Next.js 16** với App Router.
- **React 19** và TypeScript.
- **Tailwind CSS 4** để xây dựng giao diện.
- **Material UI** và **MUI X Data Grid** cho các thành phần UI/bảng dữ liệu trong các bước phát triển tiếp theo.
- **Redux Toolkit**, **React Redux** và **Redux Persist** cho state management.
- **Redux Toolkit Query** và **Axios** cho lớp giao tiếp API.
- **Recharts** cho biểu đồ.
- **gantt-task-react** cho Gantt chart.
- **React DnD** cho các tương tác kéo thả.
- **date-fns** và **numeral** cho xử lý ngày tháng và định dạng số.
- **Lucide React** cho icon.
- **ESLint** và **Prettier** cho kiểm tra chất lượng và định dạng mã nguồn.

## Yêu cầu môi trường

- Node.js **20.9 trở lên** (khuyến nghị dùng phiên bản LTS).
- Một package manager: npm, pnpm, yarn hoặc bun.
- Backend chạy cục bộ tại `http://localhost:8000` nếu muốn tích hợp API.

Kiểm tra phiên bản:

```bash
node --version
npm --version
```

## Cài đặt và chạy dự án

### 1. Clone repository

```bash
git clone <repository-url>
cd project_management_dvn
```

### 2. Cài dependencies

Repository có cả `package-lock.json` và `pnpm-lock.yaml`. Chọn **một** package manager và sử dụng nhất quán:

```bash
# npm
npm install

# hoặc pnpm
pnpm install
```

### 3. Cấu hình biến môi trường

Tạo file `.env.local` ở thư mục gốc:

```env
NEXT_PUBLIC_API_URL=http://localhost:8000
```

Chi tiết xem tại [Biến môi trường](#biến-môi-trường).

### 4. Chạy môi trường phát triển

```bash
# npm
npm run dev

# hoặc pnpm
pnpm dev
```

Mở [http://localhost:3000](http://localhost:3000) trên trình duyệt.

## Biến môi trường

| Tên | Bắt buộc | Giá trị mẫu | Mô tả |
| --- | --- | --- | --- |
| `NEXT_PUBLIC_API_URL` | Có khi gọi API | `http://localhost:8000` | URL gốc được RTK Query sử dụng cho các request tới backend. |

Lưu ý:

- Prefix `NEXT_PUBLIC_` làm giá trị có thể xuất hiện ở phía client; không đặt secret, mật khẩu hoặc private key vào biến này.
- Sau khi thay đổi `.env.local`, cần khởi động lại dev server.
- File `.env.local` không nên commit lên Git.

## Các lệnh thường dùng

| Lệnh | Mục đích |
| --- | --- |
| `npm run dev` | Chạy server phát triển với hot reload. |
| `npm run build` | Build ứng dụng cho production. |
| `npm run start` | Chạy bản build production; cần chạy `npm run build` trước. |
| `npm run lint` | Chạy ESLint trên project. |

Với pnpm, thay `npm run <script>` bằng `pnpm <script>`, ví dụ `pnpm lint`.

## Cấu trúc thư mục

```text
.
├── app/
│   ├── (components)/
│   │   ├── Navbar/
│   │   │   └── index.tsx       # Thanh tìm kiếm và Settings
│   │   └── Sidebar/
│   │       └── index.tsx       # Sidebar và thông tin DVN TEAM
│   ├── state/
│   │   ├── api.ts              # Cấu hình RTK Query
│   │   └── index.tsx           # Global Redux slice
│   ├── dashboardWrapper.tsx    # Layout Dashboard và Redux Provider
│   ├── globals.css             # CSS toàn cục và Tailwind import
│   ├── layout.tsx              # Root layout, metadata và font Inter
│   ├── page.tsx                # Trang chủ hiện tại
│   └── redux.tsx               # Redux store, persistence và typed hooks
├── public/
│   └── logo.png                # Logo DVN TEAM
├── .env.local                  # Biến môi trường cục bộ, không commit
├── eslint.config.mjs           # Cấu hình ESLint
├── next.config.ts              # Cấu hình Next.js
├── package.json                # Scripts và dependencies
├── postcss.config.mjs          # Cấu hình PostCSS/Tailwind
├── tailwind.config.ts          # Theme Tailwind
└── tsconfig.json               # Cấu hình TypeScript
```

## Kiến trúc ứng dụng

### Root layout

`app/layout.tsx` khai báo metadata, font Inter và bọc toàn bộ ứng dụng bằng `DashboardWrapper`.

### Dashboard wrapper

`app/dashboardWrapper.tsx` cung cấp layout dùng chung:

1. Khởi tạo `StoreProvider`.
2. Hiển thị `Sidebar`.
3. Hiển thị `Navbar`.
4. Render nội dung route hiện tại trong vùng nội dung chính.

### Redux store

Store trong `app/redux.tsx` kết hợp:

- `global`: state giao diện.
- `api`: reducer và middleware của RTK Query.

Chỉ slice `global` được persist. State API cache không được lưu lâu dài trong `localStorage`.

### Thêm API endpoint

Khi backend sẵn sàng, thêm endpoint vào `app/state/api.ts` theo pattern RTK Query. Ví dụ:

```ts
export const api = createApi({
  baseQuery: fetchBaseQuery({
    baseUrl: process.env.NEXT_PUBLIC_API_URL,
  }),
  reducerPath: "api",
  tagTypes: ["Project"],
  endpoints: (build) => ({
    getProjects: build.query<Project[], void>({
      query: () => "/projects",
      providesTags: ["Project"],
    }),
  }),
});

export const { useGetProjectsQuery } = api;
```

Khi thêm endpoint thực tế, cần bổ sung type dữ liệu, xử lý trạng thái loading/error và cập nhật tag khi có mutation.

## Hướng dẫn sử dụng giao diện hiện tại

1. Khởi động ứng dụng bằng `npm run dev`.
2. Truy cập `http://localhost:3000`.
3. Quan sát Sidebar cố định bên trái với thương hiệu DVN Tech và thông tin DVN TEAM.
4. Sử dụng ô `Search...` trên Navbar để nhập nội dung tìm kiếm. Hiện ô này chưa kết nối với dữ liệu hoặc API.
5. Chọn biểu tượng Settings để điều hướng tới `/settings`. Route Settings cần được bổ sung nếu muốn sử dụng đầy đủ.

## Tích hợp Backend/API

Frontend mặc định trỏ tới:

```text
http://localhost:8000
```

Backend cần cung cấp API tương thích với các route mà frontend khai báo trong RTK Query. Khi tích hợp production:

- Đặt `NEXT_PUBLIC_API_URL` thành URL backend production.
- Cấu hình CORS cho origin của frontend.
- Thống nhất format response và error.
- Bổ sung cơ chế xác thực an toàn; không lưu secret ở frontend.
- Thêm endpoint vào `app/state/api.ts` thay vì gọi API rải rác trong component.

Hiện tại `api.ts` mới chỉ tạo API slice rỗng (`endpoints: () => ({})`), vì vậy ứng dụng chưa thực hiện request nghiệp vụ nào.

## Build và triển khai

### Kiểm tra trước khi build

```bash
npm run lint
npm run build
```

### Chạy production cục bộ

```bash
npm run start
```

Mặc định ứng dụng chạy tại [http://localhost:3000](http://localhost:3000).

### Triển khai lên Vercel

1. Import repository vào Vercel.
2. Chọn framework preset là Next.js.
3. Khai báo `NEXT_PUBLIC_API_URL` trong Environment Variables.
4. Deploy.

Nếu backend chạy ở domain khác, cần kiểm tra CORS và HTTPS trước khi kết nối từ frontend production.

## Tình trạng phát triển

### Đã có

- [x] Khởi tạo Next.js App Router.
- [x] TypeScript và Tailwind CSS.
- [x] Dashboard layout cơ bản.
- [x] Navbar, Sidebar và logo DVN.
- [x] Redux Toolkit và Redux Persist.
- [x] RTK Query foundation.
- [x] Cấu hình lint và build.

### Định hướng tiếp theo

- [ ] Bổ sung route Settings.
- [ ] Thiết kế model và API cho project, task, member.
- [ ] Thêm xác thực và phân quyền.
- [ ] Hoàn thiện trang danh sách/chi tiết dự án.
- [ ] Thêm Kanban, Gantt và quản lý deadline.
- [ ] Kết nối ô tìm kiếm với dữ liệu thực tế.
- [ ] Bổ sung test tự động và xử lý lỗi API thống nhất.

## Đóng góp

1. Tạo branch mới từ branch chính.
2. Thực hiện thay đổi theo cấu trúc và pattern hiện có.
3. Chạy `npm run lint` và `npm run build`.
4. Tạo pull request, mô tả rõ phạm vi thay đổi và cách kiểm thử.

## Bản quyền

Đây là mã nguồn nội bộ của DVN Tech. Quyền sử dụng và phân phối thực hiện theo chính sách của tổ chức.
