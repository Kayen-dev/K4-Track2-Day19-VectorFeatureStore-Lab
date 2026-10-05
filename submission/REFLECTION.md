# Reflection — Lab 19

**Tên:** _Bổ sung họ tên trước khi nộp_
**Cohort:** A20-K4
**Path đã chạy:** Lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 câu hỏi, hybrid RRF đạt Precision@10 trung bình cao nhất
(78,6%), nhỉnh hơn BM25 (77,8%) và semantic search (73,2%). Với câu `exact`,
BM25 mạnh nhất vì thuật ngữ xuất hiện nguyên văn; hybrid giữ mức tương đương.
Với `mixed`, hybrid đạt 100% vì kết hợp được tín hiệu từ khóa chính xác và độ
tương đồng ngữ nghĩa. Riêng `paraphrase`, vector chưa thắng trên cấu hình Lite:
model `bge-small-en-v1.5` thiên về tiếng Anh nên hiểu diễn đạt lại bằng tiếng
Việt còn yếu; đây là dấu hiệu nên thử `bge-m3` rồi index lại.

Tôi không dùng hybrid khi truy vấn là mã, ID hoặc thuật ngữ bắt buộc khớp chính
xác — BM25 đơn giản, nhanh và dễ giải thích hơn. Tôi chọn pure vector khi người
dùng chủ yếu diễn đạt tự nhiên, đa ngôn ngữ, corpus đã được đánh giá bằng một
embedding model phù hợp và lexical match không mang thêm giá trị. Hybrid cũng
không đáng dùng nếu phần tăng chất lượng quá nhỏ so với chi phí latency và vận
hành hai index.

---

## Điều ngạc nhiên nhất khi làm lab này

Điều ngạc nhiên nhất là lựa chọn embedding model có thể đảo ngược kỳ vọng
“vector thắng paraphrase”; phải đo theo từng slice thay vì tin vào nhãn mode.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
