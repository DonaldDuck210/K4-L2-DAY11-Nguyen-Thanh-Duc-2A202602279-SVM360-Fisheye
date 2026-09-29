# Guideline patch

- **Rule mới đề xuất (R12 — Diễn giải `M_only` sát ngưỡng):** Trong báo cáo L/R/M, `M_only`/`SPURIOUS` là kết quả ghép tự động, không tự nó chứng minh model phát hiện vật không tồn tại. Khi box M cùng class có thể là cùng vật với box L hoặc R nhưng IoU dưới 0.5, người soát phải kiểm tra ảnh gốc và overlay; ghi `E5_unresolved` nếu chưa đủ bằng chứng phân biệt box lệch với false positive thật. Không tự hạ ngưỡng ghép và không sửa hồi tố nhãn đã khóa chỉ để làm các nguồn khớp nhau.
- **Áp dụng cho:** Bước đối chiếu model L/R/M ở mọi class và zone; đặc biệt các cell `M_only` được báo `SPURIOUS`.
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R01–R11 quy định phạm vi và cách gán nhãn, còn taxonomy chỉ định nghĩa `M_only` là model-only. Chưa có hướng dẫn phân xử trường hợp một box cùng class nằm sát box L/R nhưng không đạt ngưỡng IoU 0.5 của phép ghép ba nguồn. Ví dụ `adasind_258420.jpg`: `M3 Bike` gần `R3 Bike`, IoU 0.472; báo cáo xếp `M3` thành `M_only` dù overlay gợi ý có thể là cùng xe.
- **`rules_version` mới:** Đề xuất `v1.1.0` (bổ sung hướng dẫn diễn giải/review, không đổi taxonomy hay ngưỡng ghép).
- **Hiệu lực từ:** Lần chạy `r3_diag` kế tiếp sau khi patch được duyệt; không áp dụng hồi tố cho export `r1_craft` đã khóa.
