# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 4 |
| center | B4 | SPURIOUS | 5 |
| edge | B4 | MISSING | 2 |
| edge | B4 | SPURIOUS | 1 |
| mid | B4 | MISSING | 6 |
| mid | B4 | SPURIOUS | 10 |

## Top defects
- SPURIOUS: 16 (ví dụ frame adasind_258420.jpg)
- MISSING: 12 (ví dụ frame adasind_258420.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`): `E5_unresolved`. Ở `adasind_258420.jpg`, model `M3` (`Bike`) được xếp `M_only`, còn reference có `R3` (`Bike`) gần như cùng vị trí. IoU giữa hai box là 0.472, dưới ngưỡng ghép 0.5; vì vậy chưa thể kết luận đây là false positive thật hay cùng một xe bị box lệch khiến phép ghép bỏ lỡ. 16 `SPURIOUS` là kết quả so sánh theo phép ghép, không mặc nhiên là 16 vật thể giả độc lập.
- Cách xử lý và owner: `P3` (ưu tiên xác minh thấp, chưa có bằng chứng tác động an toàn). `qa` kiểm tra ảnh gốc và overlay để phân xử `M3` với `R3`; nếu là cùng xe, ghi nhận ảnh hưởng của ngưỡng/geometry, nếu là hai vật khác nhau mới xác nhận false positive. Chỉ chuyển `ai_team` điều tra sau khi xác minh được lỗi thuộc dự đoán model.
- Bằng chứng: `submission/findings.csv` (dòng `r3_diag`, `adasind_258420.jpg`, `M3`, `M_only`, `SPURIOUS`); overlay tại `submission/r3_diag/model_compare.html`; box `R3 Bike` trong overlay có tọa độ `(124,800)-(149,863)`, `M3 Bike` `(126.1,825.8)-(152.4,867)`. Quy tắc ghép IoU ≥ 0.5 nằm trong `svm11/match.py`; luật vẽ trên ảnh gốc là R02 trong `docs/02-rules-vi.md`. Chưa có ảnh raster riêng trong `submission/screenshots/`.
