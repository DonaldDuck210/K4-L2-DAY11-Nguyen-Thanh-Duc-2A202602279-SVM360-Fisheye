# Sensor context

- **Rig (quan sát, không phải thông số xác nhận):** Ảnh ADASIND là góc nhìn của một camera fisheye trên xe, hướng ra cảnh giao thông phía trước; vị trí lắp có vẻ ở phía trước xe. Bộ dữ liệu trong lab không xác nhận xe/mẫu camera, điểm lắp, độ cao, hướng lắp hay calibration. Đây không phải dữ liệu của hệ thống bốn camera SVM.
- **`ego_body`:** Phần thân xe gắn camera xuất hiện sát đáy khung hình ở các frame có thể thấy xe. Chỉ vẽ polygon trên phần thân xe thực sự hiện ra; không suy rộng sang mặt đường hay đối tượng giao thông. Theo guideline, không có `ego_body` ở frame `006840` và `271039`.
- **Vòng kính (lens circle):** Ảnh có kích thước 1080×1920 px. Theo các tâm/bán kính trong `assets/frames.csv`, tâm vòng kính thay đổi theo frame, xấp xỉ `(417–630, 891–1023)` px và bán kính `770–829` px. Đường kính khoảng 1540–1660 px, tức khoảng 80–86% chiều cao ảnh; vòng chiếm gần hết bề ngang và bị cắt bởi biên ảnh. Polygon `lens_border` đã có sẵn để soát, không tự vẽ thêm.
