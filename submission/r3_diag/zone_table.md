# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 6 | 0 | 0 | 4 | 5 | — |
| mid | 7 | 4 | 0 | 3 | 10 | MISSING (4) |
| edge | 7 | 1 | 0 | 1 | 1 | MISSING (1) |

## Nhận xét

- **L:** thiếu nhiều nhất ở `mid`: 4/7 box tham chiếu (57%); `edge` thiếu 1/7 (14%), `center` 0/6, và không có box L spurious ở zone nào. Năm box thiếu theo đối chiếu cục bộ gồm 4 `Bike` và 1 `Pedestrian`.
- **M:** thiếu nhiều box tham chiếu nhất ở `center` (4/6), kế đến `mid` (3/7) và `edge` (1/7). Số box M không ghép được vào nhóm L/R cao nhất ở `mid` (10; so với 5 ở `center`, 1 ở `edge`). Đây là số đếm thô, không phải tỷ lệ false positive: `M_only` có thể cần kiểm tra thêm về vị trí, class hoặc ghép cặp.
- **Giả thuyết và giới hạn:** cảnh đông ở `mid` có thể khiến người gán nhãn bỏ sót xe nhỏ/bị che; độ méo fisheye ở rìa cũng là yếu tố cần kiểm tra, nhưng không giải thích được cụm thiếu `Bike` ở `mid` chỉ từ bảng này. Model có thể khó ở cảnh dày và ảnh fisheye, song các dự đoán không ghép được chưa đủ để kết luận model sai. Slice chỉ gồm 3 frame `B4-dense` (20 box tham chiếu), không đại diện toàn bộ ADASIND hay bốn camera SVM; teaching reference cũng là bản dạy học, không phải ground truth đã phê duyệt.
