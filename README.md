# AI Tutor XSTK — MVP

Website gia sư AI tiếng Việt cho môn Xác suất & Thống kê. MVP hiện có:
- Giao diện chat responsive.
- Chọn chủ đề và chế độ: gợi ý, giảng lý thuyết, kiểm tra bài, lời giải đầy đủ, tạo bài luyện tập.
- API server-side gọi mô hình OpenAI qua biến môi trường.
- Công cụ tính toán hạn chế, hỗ trợ số học, tổ hợp, CDF chuẩn, PMF nhị thức và Poisson.
- Không đưa API key xuống trình duyệt.

## Yêu cầu
- Node.js 20 trở lên
- API key của nhà cung cấp mô hình được cấu hình ở máy chủ

## Chạy trên máy tính

```bash
npm install
cp .env.example .env.local
```

Mở `.env.local`, điền `OPENAI_API_KEY` và tùy chọn `OPENAI_MODEL`. Sau đó:

```bash
npm run dev
```

Mở http://localhost:3000

## Triển khai online chi phí thấp (Vercel)

1. Tạo repository GitHub và tải mã nguồn dự án lên.
2. Đăng nhập Vercel, import repository.
3. Trong Project Settings → Environment Variables, thêm:
   - `OPENAI_API_KEY` = API key của bạn
   - `OPENAI_MODEL` = `gpt-4o-mini` (hoặc model khả dụng bạn chọn)
4. Deploy. Sau khi deploy, Vercel cấp một URL công khai.
5. Không bao giờ đặt API key trong biến `NEXT_PUBLIC_*`, mã frontend, GitHub hoặc tin nhắn chat.

Lưu ý: API model thường tính phí riêng theo mức sử dụng; hosting có thể có giới hạn theo gói. Kiểm tra giá và điều khoản hiện hành trước khi công khai.

## Kiến trúc

- Frontend: Next.js 14 + React + TypeScript.
- Backend: Next.js Route Handler tại `app/api/tutor/route.ts`.
- AI: OpenAI API, model cấu hình bằng biến môi trường.
- Tính toán: `mathjs` cho biểu thức và `jstat` cho một số phân phối.
- Triển khai: Vercel.

## Các giới hạn hiện tại

Đây là MVP khởi đầu, chưa phải nền tảng sản xuất hoàn chỉnh:
- Chưa có đăng nhập, phân quyền sinh viên/giảng viên, cơ sở dữ liệu hoặc lưu hồ sơ dài hạn.
- Chưa có tải ảnh/PDF, OCR chữ viết tay, bảng viết iPad hoặc voice chat.
- Barem chấm điểm, diễn đàn, bản đồ tư duy và thống kê lỗi cá nhân chưa được triển khai.
- Công cụ tính toán chỉ hỗ trợ những hàm được nêu trong API, chưa phải bộ giải đại số tổng quát.
- Nên bổ sung giới hạn tốc độ, kiểm soát chi phí, kiểm thử bảo mật, logging có bảo vệ dữ liệu và bộ test toán học trước khi dùng rộng rãi.

## Lộ trình tiếp theo

1. Đăng nhập + PostgreSQL/Supabase, hồ sơ người học và vai trò giảng viên.
2. Upload PDF/ảnh + OCR/vision và giao diện chấm theo rubric.
3. Bảng viết số hóa dùng stylus/iPad.
4. Ngân hàng câu hỏi, trắc nghiệm chấm tự động, tạo 5 bài tương tự.
5. Hồ sơ lỗi sai, phân tích lỗ hổng, bản đồ tư duy và diễn đàn.
6. Giọng nói qua speech-to-text/text-to-speech hoặc realtime API.
7. Bộ kiểm thử chuyên môn cho xác suất, biến ngẫu nhiên, phân phối và suy luận thống kê.

## Lưu ý học thuật

AI có thể sai. Hãy xác minh các kết quả quan trọng bằng công cụ tính toán, tài liệu môn học và giảng viên. Không tải dữ liệu cá nhân nhạy cảm của sinh viên lên khi chưa có cơ chế bảo vệ phù hợp.
