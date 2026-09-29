# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `B4-dense` / `adasind_258420.jpg` | L/R: 3 box reference chưa có ở L (`R2 Bike`, `R3 Bike`, `R7 Pedestrian`). L/R/M: 7 `MISSING`, 8 `SPURIOUS`; các số này gộp thiếu của L và model, không phải 15 lỗi annotator. | Nhiều khác biệt nhất trong ba frame; ưu tiên kiểm tra các vật nhỏ ở `mid` và ca `M3 Bike` (`M_only`) gần `R3 Bike` (IoU 0.472), chưa đủ căn cứ gọi là false positive. | Ảnh gốc và `submission/r1_craft/compare.html`; `submission/r3_diag/model_compare.html`; các dòng frame này trong `findings.csv`, giữ `object_ref`, `cell`, IoU, quyết định QA và ảnh crop/overlay. |
| `B4-dense` / `adasind_270517.jpg` | L/R: 2 box Bike trong reference chưa có ở L (`R3`, `R7`). L/R/M: 4 `MISSING`, 6 `SPURIOUS`, gồm hai `RM_noL`, hai `LR_noM` và sáu `M_only`. | Đối chiếu frame thứ hai có nhiều khác biệt; review riêng lỗi thiếu Bike của L và các model-only để không gộp lỗi của ba nguồn. So sánh với frame 258420 để xem pattern có lặp lại hay chỉ là ca đơn. | Ảnh gốc và overlay L/R/M; các dòng tương ứng trong `findings.csv` và `model_compare.md`; ghi kết luận cho từng object, rule áp dụng, người review và điểm còn chưa phân xử. |

Giới hạn của kết luận từ ba frame ADASIND: đây chỉ là ba frame của slice `B4-dense`, với teaching reference chưa được xác nhận là gold. Chúng giúp ưu tiên ca cần xem, không đại diện cho toàn ADASIND hay bốn camera SVM, và không cho phép ước lượng tỷ lệ lỗi. `M_only`/`SPURIOUS` là kết quả ghép tự động; cần kiểm tra ảnh trước khi gọi là false positive. Không coi các frame liền nhau trong cùng cảnh là các quan sát độc lập nếu chưa kiểm tra timestamp và scene.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập): xác nhận đủ 8 strata `front/rear/left/right × normal/hard`, mỗi stratum có số frame dương và tổng phân bổ bằng 200; sau khi chọn, đối chiếu số dự kiến với số thực tế theo camera, loại lát cắt, scene/timestamp và điều kiện rủi ro. Gắn các frame liên tiếp cùng một cảnh vào cùng scene cluster, giới hạn số frame mỗi cluster hoặc báo riêng số frame lẫn số cluster; kiểm tra không strata/camera nào bị bỏ trống và lưu lý do thay thế frame trùng cảnh. Kế hoạch phân tầng này giúp tìm ca khó và soát độ phủ, nhưng chưa đo tỷ lệ lỗi: cần mẫu xác suất đại diện, denominator rõ, quy trình gán nhãn độc lập và adjudication nhất quán mới có thể ước lượng tỷ lệ cùng độ bất định.
