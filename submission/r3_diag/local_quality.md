# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `678fe67498bce14413754b860836014c4259f8ddca821145e2a5ee4c85b5fdb3`; slice `B4-dense`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_258420.jpg, adasind_270517.jpg, adasind_310008.jpg. Frame thiếu trong export: không.
TP=15; FP=0; FN=5; số lần đối chiếu=20; mean IoU của TP=0.848.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.750 | 0.938 | 0.800 |
| precision | 1.000 | 0.750 | 0.000 |
| recall | 0.750 | 0.714 | 0.000 |
| jaccard | 0.750 | 0.714 | 0.000 |
| dice | 0.857 | 0.731 | 0.000 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 0 | 0 | 4 | 0.800 | 0.000 | 0.000 | 0.000 | 0.000 |
| Car | 3 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Pedestrian | 6 | 0 | 1 | 0.950 | 1.000 | 0.857 | 0.857 | 0.923 |
| ThreeWheeler | 6 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_258420.jpg | 5 | 0 | 3 | 0.625 | 1.000 | 0.625 |
| adasind_270517.jpg | 5 | 0 | 2 | 0.714 | 1.000 | 0.714 |
| adasind_310008.jpg | 5 | 0 | 0 | 1.000 | 1.000 | 1.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | <missing> |
|---|---:|---:|---:|---:|---:|
| Bike | 0 | 0 | 0 | 0 | 4 |
| Car | 0 | 3 | 0 | 0 | 0 |
| Pedestrian | 0 | 0 | 6 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 6 | 0 |
| <extra> | 0 | 0 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
