# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:** 2A202603794
- **Họ và tên:** Nguyễn Minh Quân
- **SEED** (in ở ô đầu notebook): 4406

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | ☑ |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | ☑ |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | ☑ |

## 2. Kết quả chính

| Mô hình | f1 | f1_SUB |
|---|---:|---:|
| 1. BoW + LogReg (tự code) | 0.859 | 0.919 |
| 2. BoW + MLP (deep learning) | 0.906 | 0.919 |
| 3a. Encoder (MiniLM) + kNN | 0.907 | 0.974 |
| 3b. Encoder (MiniLM) + LogReg | 0.957 | 0.974 |
| 3c. Encoder (MiniLM) + MLP head | 0.946 | 0.974 |

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

*Model nào tụt nhiều nhất, ở nhóm case nào? Nêu 2 case cụ thể và cơ chế khiến model sai.*

## 5. Thử thách cá nhân

*Đề theo SEED của bạn, cách làm, kết quả, giải thích.*

## 6. Phương án cho sản phẩm thật

(1) Đạt độ trễ: (p95 < 50 ms) BoW + LogReg, BoW + MLP, Encoder + LogReg, Encoder + MLP head. Đạt cả độ trễ lẫn chất lượng:(p95 \approx 36.60 ms, F1 \approx 0.957). Encoder (MiniLM) + LogReg. Chi phí LLM/tháng: Khoảng  30.000− 150.000 USD/tháng cho 300 triệu tin nhắn. 

## 7. AI log và điều đã học

| Phần | Bạn hỏi AI gì (prompt) | AI trả lời/viết gì | Bạn đã sửa / kiểm chứng gì |
|---|---|---|---|
| TODO 4.1| hướng dẫn viết hàm call_openai|Cung cấp cấu trúc hàm gọi API chuẩn|Kiểm tra lại tính tương thích của thư viện.|
| TODO 4.2| xây dựng hàm build_classification_prompt hỗ trợ cả zero-shot và few-shot|Đề xuất template prompt rõ ràng|Đọc hiểu logic truyền tham số đầu vào và tùy chỉnh lại câu lệnh hướng dẫn cho phù hợp với ngữ cảnh.|
| TODO 4.3|Viết hàm parse_label để bóc tách chuỗi phản hồi từ LLM thành nhãn số (0 hoặc 1)|Cung cấp hàm kiểm tra từ khóa "spam" và "ham" từ chuỗi kết quả.|Phát hiện lỗi thực tế: Khi test với chuỗi 'Not spam', hàm bị trả về None do xung đột logic nhận diện từ khóa. Đã sửa: Đưa điều kiện kiểm tra cụm từ phủ định ("not spam") lên ưu tiên kiểm tra trước tiên để khắc phục triệt để lỗi.|
| TODO 4.4|Hoàn thiện hàm xử lý hàng loạt llm_classify_batch|Cung cấp logic vòng lặp batch, cơ chế xử lý độ trễ, ước tính token và tính chi phí.|Rà soát lại các biến đếm, đảm bảo hàm gọi lồng ghép đúng cơ chế xử lý lỗi mạng/rate-limit có sẵn trong template của bài lab.|
