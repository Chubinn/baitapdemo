# HTQT Frontend

Frontend Vue 3 sử dụng Vite, Vue Router, Pinia và Axios. Màn hình `/demo` gọi API Spring Boot thông qua proxy của Vite.

## Yêu cầu

- Node.js theo phiên bản khai báo trong `package.json`
- Backend Spring Boot đang chạy tại `http://localhost:8080`

## Cài đặt và chạy

Mở terminal trong thư mục `htqt-frontend`:

```sh
npm install
npm run dev
```

Mở địa chỉ được Vite hiển thị, thường là <http://localhost:5173>.

## Kết nối Spring Boot

Vite chuyển tiếp yêu cầu bắt đầu bằng `/api` đến `http://localhost:8080`. Màn hình demo gọi:

```text
GET http://localhost:5173/api/demo
```

Backend cần cung cấp `GET /api/demo` và trả về danh sách JSON, ví dụ:

```json
["Spring Boot", "Vue.js", "MySQL"]
```

Nếu gọi trực tiếp từ trình duyệt sang backend, hãy cấu hình CORS ở backend. Khi dùng proxy Vite trong môi trường phát triển, frontend gọi cùng origin nên thường không cần cấu hình CORS chỉ để chạy màn hình này.

## Lệnh hữu ích

```sh
npm run dev      # Chạy môi trường phát triển
npm run build    # Tạo bản build production
npm run preview  # Xem thử bản build
```
