# Escalation ticket

## Ticket 1

- **Frame:** `adasind_258420.jpg` — model `M3 Bike` được ghép thành `M_only`, trong khi reference có `R3 Bike` gần cùng vị trí; IoU = 0.472, dưới ngưỡng ghép 0.5.
- **Ảnh chụp:** `submission/screenshots/escalation-m3-r3.png` (overlay L/R/M; xem thêm `submission/r3_diag/model_compare.html`).
- **Expected impact:** Nếu mọi ứng viên cùng class dưới ngưỡng đều bị đọc là false positive thật, số `SPURIOUS` và kết luận về model có thể bị diễn giải quá mức. Hiện chưa có căn cứ xác nhận `M3` là vật giả; không ảnh hưởng nhãn `r1_craft` đã khóa.
- **Owner:** `guideline` — cần quy định cách diễn giải ứng viên cùng class sát ngưỡng và khi nào chuyển QA phân xử.
- **Recommendation:** Duyệt hoặc bác đề xuất R12 trong `submission/20_guideline_patch.md`: giữ nguyên ngưỡng 0.5, nhưng yêu cầu QA xem ảnh/overlay và ghi `E5_unresolved` khi chưa phân biệt được box lệch với false positive. Không sửa nhãn hoặc số liệu hồi tố trước khi chốt quy tắc.
