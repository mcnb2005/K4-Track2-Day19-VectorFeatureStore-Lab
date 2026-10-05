# Reflection — Lab 19

**Tên:** Phạm Minh Cương
**MSSV:** 2A202602825
**Cohort:** A20-K4
**Path đã chạy:** lite

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Hybrid thắng trung bình với Precision@10 = 78,6%, cao hơn BM25 (77,8%) và
vector (73,2%). Với `exact`, BM25 và hybrid cùng đạt 96,7% vì thuật ngữ xuất
hiện nguyên văn. Với `mixed`, hybrid đạt 100% nhờ RRF kết hợp tín hiệu từ khóa
và ngữ nghĩa. Ở `paraphrase`, kết quả thực tế lại là BM25 33,3%, hybrid 32,0%
và vector 24,0%; nguyên nhân là `bge-small-en-v1.5` thiên về tiếng Anh nên biểu
diễn câu diễn đạt lại bằng tiếng Việt chưa tốt. Trong production tiếng Việt,
tôi sẽ thử `bge-m3` rồi đánh giá lại trước khi chọn.

Tôi không dùng hybrid khi truy vấn là mã, tên riêng hoặc thuật ngữ cần khớp
chính xác (BM25 đơn giản, nhanh hơn), hoặc khi hệ thống đã dùng embedding đa
ngữ tốt và truy vấn hoàn toàn ngữ nghĩa (pure vector giảm chi phí hợp nhất và
độ trễ). Hybrid chỉ nên là mặc định sau khi đo trên golden set thật.

---

## Điều ngạc nhiên nhất khi làm lab này

Ngưỡng semantic cache 0,75 vẫn trả lời sai 36%; phải tăng lên ít nhất 0,85 và
luôn namespace theo tenant. Một cache “hit nhiều” chưa chắc là cache tốt.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
