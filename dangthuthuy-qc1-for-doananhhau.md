# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đoàn Anh Hậu        Người kiểm (học viên): Đặng Thu Thủy  
Ngày: 20/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): doananhhau-front.zip, doananhhau-fisheye.zip (revision 1)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 48  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 6 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 11 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 11 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 4 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 11 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 4 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 4 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 7 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 5 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 5 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | lane#1@(110,718) | chính | Vạch L1 dừng sớm khoảng 30 px so với điểm xa nhất còn thấy rõ vạch (sai phạm vi) |
| 2 | QC1-06 | A04 | lane#2@(540,715) | chính | Vạch vàng đôi tim đường chọn kind=single thay vì kind=double (sai thuộc tính) |
| 3 | QC1-01 | A03 | tag#weather | nhẹ | Thiếu nhãn tag weather trên ảnh A03 (bỏ sót) |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A07 | Vạch L1 bên trái bị hàng xe đỗ che khuất hoàn toàn thì có cần vẽ nối occluded không? | Coach xác nhận: xe đỗ sát lề che mất vạch thì không vẽ bịa thêm, miễn trừ lỗi QC1-02 |

## Quyết định
Lỗi nặng: 0   Lỗi chính: 2 / 48 nhãn = 4.17 %   Lỗi nhẹ: 1   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): Release  
Lý do (theo luật của phiếu): Không có lỗi nặng (0 lỗi), tỷ lệ lỗi chính là 4.17% (nhỏ hơn ngưỡng 5.0% số nhãn đã kiểm), ca mơ hồ đã được Coach giải đáp thỏa đáng, đủ điều kiện nghiệm thu Release.  

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
