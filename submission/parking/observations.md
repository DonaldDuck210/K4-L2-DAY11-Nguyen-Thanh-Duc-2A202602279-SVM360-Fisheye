# Quan sát vạch ô đỗ

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): hai vạch sơn xiên ở dãy ô giữa tiền cảnh ảnh core: một chạy gần từ `(280, 519)` đến `(420, 553)`, vạch kế bên từ `(399, 518)` đến `(576, 544)` (tọa độ ảnh, pixel). Mỗi vạch phân cách hai ô đỗ liền nhau; chỉ theo phần sơn nhìn thấy, không kéo dài qua phần khuất.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: Không vẽ vạch dài chạy dọc lối xe lưu thông ở giữa bãi trong ảnh đối chiếu: nó hướng dẫn luồng xe, không tạo ranh giới cho một ô đỗ riêng. Mép curb/biên mặt đường cũng không phải vạch sơn chia ô.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: Polygon dừng tại mép vùng trống nhìn thấy và biên ảnh; không phủ lên xe, curb hay phần bị xe che, không nối qua vùng khuất.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): không có.