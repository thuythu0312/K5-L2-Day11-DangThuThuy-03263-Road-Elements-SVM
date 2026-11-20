# Báo cáo cá nhân — Ngày 11
Họ tên: Đặng Thu Thủy               Mã học viên: 03263  
Phiên bản CVAT (Help → About): CVAT v2.82.0 (Server)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 20/11/2026    Số lần nộp lại sau Rework: 0  

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | Đủ 6 label: lane, road_curb, crosswalk, drivable, traffic_light, traffic_sign |
| Thuộc tính và giá trị | Có | Khớp hoàn toàn với configs/road_v1_labels.json |
| 4 tag ảnh | Có | Đủ 4 tag: camera, timeofday, weather, source (mỗi tag có thuộc tính value) |
Cách kết thúc polyline trên bản CVAT này: Bấm phím N trên bàn phím (hoặc click đúp chuột vào điểm nút cuối cùng)  
Cách đặt tag ảnh trên bản CVAT này: Chọn biểu tượng Tag ở thanh công cụ bên trái, chọn label tag, sau đó mở tab Details bên phải để chỉnh giá trị value  

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 25 | 5 | 4 | 5 | 19 | 16 |
| front-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 6 | 2 | 4 | 3 | 5 | 1 |
| fisheye-extra (đã làm __ / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane / road_curb | Vẽ lane hay road_curb | road_curb | Hai bên mép đường là vỉa hè gờ cao, mặt đường không có vệt sơn kẻ đường nên không gán lane L1/R1 |
| A06 | lane / road_curb | Vẽ vạch R1 bên phải | road_curb | Mép đường bên phải là lề đường không sơn, chỉ có vạch L1 bên trái |
| A07 | lane | Có vạch L1 hay không | Không vẽ L1 | Làn đường bên trái không có vạch phân làn rõ rệt, tuân thủ nguyên tắc không vẽ bịa vạch |
| A08 | lane | Có vạch L1 hay không | Không vẽ L1 | Vạch bên trái bị khuất và không có vệt sơn, chỉ gán vạch R1 và R2 bên phải |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Đoàn Anh Hậu  Quyết định nhận được: Release  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-02 | 5 | Đồng ý ghi nhận | Không cần sửa vì là ca miễn trừ không có vạch sơn theo guideline |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| dangthuthuy-front.zip | Có | 4 / 4 | 3 / 3 | Có (camera=front) |
| dangthuthuy-fisheye.zip | Có | 1 / 1 | 6 / 6 | Có (camera=fisheye_front) |

## 6. Ảnh chụp màn hình
1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển) (ví dụ: A12).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong (ví dụ: B03).
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: Cảnh báo QC1-02 do công cụ lint tự động bắt khi thiếu L1/R1 ở các ảnh không có vạch sơn. Cách tránh ở Ngày 20: Quan sát kỹ hiện trường ODD, nếu vạch sơn thực sự không có thì chủ động note ngay vào danh mục ngoại lệ để đối soát nhanh.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: Nhãn vạch làn đi vào bài toán Lane Detection / LKA (Lane Keeping Assist). Nếu gán sai chiều (từ xa về gần) hoặc gán vỉa hè thành lane, mô hình học sai vector hướng di chuyển và nhận diện sai tim đường, dẫn đến hệ thống lái tự động đánh lái lệch tâm đường gây mất an toàn.  

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | không có làn | không có làn | 604.6 | 544.8 | 488.2 |
| x của bạn kia | không có làn | không có làn | 602.1 | 546.0 | 489.5 |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"? Hàng y=640 sẽ đổi thành "không có làn" vì polyline dừng trước khi chạm tới cao độ y=640.  
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)? Ở hàng 640 hai bạn lệch nhau 2.5 px, ở hàng 560 lệch nhau 1.3 px. Lệch ở hàng gần xe (y=720 hoặc y=640) ảnh hưởng LKA nghiêm trọng hơn nhiều vì đây là vị trí điều khiển trực tiếp góc đánh lái tức thời của xe, sai lệch nhỏ ở gần xe sẽ khuếch đại thành sai lệch quỹ đạo lớn ở phía trước.  
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó? Về mặt toán học nội suy tọa độ giao điểm với hàng ngang y thì giá trị x không đổi. Tuy nhiên script nội suy và mô hình học chuỗi điểm (sequential model) sẽ gặp khó khăn trong việc xác định điểm gốc xe và vector chiều chuyển động của làn.  
