# Reflection — Lab 19

**Tên:** Phan Tuấn Minh
**Cohort:** A20
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên golden set 50 queries, kết quả cho thấy:

- **`exact` queries**: BM25 (keyword) thắng hoặc ngang hybrid, vì query chứa từ khoá kỹ thuật xuất hiện verbatim trong corpus — BM25 match chính xác rất mạnh.
- **`paraphrase` queries**: Semantic (vector) có ưu thế hơn BM25, vì query dùng từ đồng nghĩa không có trong docs — chỉ embedding mới bắt được semantic similarity. Tuy nhiên với `bge-small-en` (English-trained), recall trên tiếng Việt còn hạn chế.
- **`mixed` queries**: Hybrid thắng rõ rệt (~100%), vì kết hợp signal từ cả BM25 (exact terms) và vector (semantic meaning) qua RRF fusion.

Khi nào **không** dùng hybrid:
- Khi query 100% exact keyword và corpus nhỏ → pure BM25 đủ tốt, nhanh hơn, tiết kiệm tài nguyên (không cần embedding model).
- Khi latency budget cực thấp (< 5ms) và không thể chạy embedding inference.
- Khi corpus đã được chuẩn hoá tốt về terminology → BM25 đủ chính xác.

---

## Điều ngạc nhiên nhất khi làm lab này

Hybrid search chỉ cần công thức RRF đơn giản (1/(k+rank)) mà đã cải thiện đáng kể so với từng mode riêng lẻ, đặc biệt trên mixed queries — pattern phổ biến nhất trong thực tế.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _N/A_
