# Reflection — Lab 19

**Tên:** Trịnh Quang Hưng
**Cohort:** Khóa 2
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 queries, kết quả cho thấy: **BM25 (keyword)** thắng trên
`exact` queries — khi user gõ đúng thuật ngữ kỹ thuật có trong corpus (ví dụ
"PostgreSQL replication slot"), BM25 score chính xác vì matchingverbatim.
**Vector (semantic)** thắng trên `paraphrase` queries — khi user diễn đạt ý
không dùng từ gốc trong doc (ví dụ "tự động mở rộng hạ tầng" thay vì
"cloud auto-scaling"), embedding nắm được ý nghĩa语义 dù không có keyword
trùng khớp. **Hybrid (RRF)** thắng rõ nhất trên `mixed` queries — kết hợp
cả hai tín hiệu, robust nhất vì user thực tế hiếm khi viết query 100% exact
hoặc 100% paraphrase. Hybrid cũng thắng trung bình tổng thể nhờ RRF k=60
cân bằng tốt giữa hai retriever.

Khi nào **không** dùng hybrid: (1) latency budget cực tight (< 5ms P99) vì
hybrid cần chạy cả hai retriever rồi fusion, gấp đôi compute; (2) corpus
nhỏ, domain hẹp với query luôn exact keyword (ví dụ log search) — BM25 đủ
mạnh, vector thêm overhead không đáng.

---

## Điều ngạc nhiên nhất khi làm lab này

_(Optional, 1–2 câu)_

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
