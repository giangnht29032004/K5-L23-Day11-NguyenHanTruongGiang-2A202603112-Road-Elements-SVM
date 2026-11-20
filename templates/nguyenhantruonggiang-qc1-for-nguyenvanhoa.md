# Phiếu QC 1 — Road v1.0

**Lô được kiểm** Nguyễn Văn Hòa  
**Người kiểm** Nguyễn Hán Trường Giang  
**Ngày** 20/11/2026  
**Phiên bản guideline** Road v1.0  
**File được kiểm** `nguyenvanhoa-front.zip` và `nguyenvanhoa-fisheye.zip`  
**Revision** Không thấy gửi 
**Số ảnh kiểm** 6 ảnh bắt buộc gồm A02, A05, A09, B02, B04 và B06. Không kiểm ảnh thêm.  
**Số nhãn đã kiểm** 56, gồm 32 shape và 24 tag

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | --- | ---: | --- |
| QC1-01 Tag camera | Sai thuộc tính / bỏ sót | 6 tag camera | 0 | Nặng |
| QC1-02 Đủ L1, R1 | Bỏ sót | 6 vị trí trên 3 ảnh front | 0 xác nhận, 3 cảnh báo chờ đối chiếu | Nặng |
| QC1-03 `position` | Sai thuộc tính / thừa | 10 lane | 0 xác nhận, vị trí làn ở A09 chờ làm rõ | Nặng |
| QC1-04 Tâm vạch, chiều, điểm dừng | Sai phạm vi / bỏ sót | 6 polyline front | 1 | Chính |
| QC1-05 Vạch đứt, che | Sai phạm vi / sai thuộc tính | 10 lane | 0 xác nhận, có cảnh báo trùng `position` ở A09 | Chính |
| QC1-06 `style`, `color`, `kind` | Sai thuộc tính | 10 lane | 0 xác nhận | Chính |
| QC1-07 Vùng lái | Sai phạm vi / bỏ sót / thừa | 11 vùng `drivable` và 4 vùng `crosswalk` | 1 | Chính |
| QC1-08 Đèn, màu | Bỏ sót / sai phạm vi / sai thuộc tính | 6 hộp đèn | 1 | Chính |
| QC1-09 `facing`, `type`, `group`, biển phụ | Sai thuộc tính | 6 hộp đèn và 1 hộp biển | 1 | Chính |
| QC1-10 Hình in, đủ biển | Bỏ sót / sai phạm vi | 1 hộp biển trong mẫu | 0 xác nhận | Chính |
| QC1-11 Fisheye | Sai phạm vi / sai thuộc tính | 4 polyline và 5 hộp | 3 | Chính |
| QC1-12 File | Lỗi file | 2 ZIP | 0 | Nhẹ / nặng |

## Danh sách lỗi

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A02 | `lane#5` | Chính | Vạch `L1` bắt đầu ở xa tại `(566, 399)` và kết thúc gần xe tại `(413, 716)`. Đảo thứ tự điểm để polyline đi từ gần ra xa. |
| 2 | QC1-07 | A09 | `drivable#3` | Chính | Polygon `direct` bao vùng bên trái vạch trắng đôi, nơi có xe chạy ngược chiều. Vẽ lại `direct` theo làn đang đi. |
| 3 | QC1-08 | B02 | `traffic_light#1` | Chính | Đèn phía trên bên phải hiện biểu tượng người đi bộ màu xanh. XML ghi `color=red`. Sửa thành `green`. |
| 4 | QC1-09 | B02 | `traffic_light#1` | Chính | Cùng cụm đèn đó có biểu tượng người đi bộ nhưng được gán `type=vehicle`. Sửa thành `pedestrian`. |
| 5 | QC1-11 | B02 | `traffic_light#1` | Chính | Tâm hộp nằm ở khoảng 92,2% bán kính theo phép tính của checker. XML ghi `edge_zone=false`. Bật `edge_zone`. |
| 6 | QC1-11 | B02 | `traffic_light#6` | Chính | Tâm hộp nằm ở khoảng 93,3% bán kính. XML ghi `edge_zone=false`. Bật `edge_zone`. |
| 7 | QC1-11 | B04 | `traffic_sign#1` | Chính | Tâm hộp biển cấm đi vào nằm ở khoảng 81,6% bán kính. XML ghi `edge_zone=false`. Bật `edge_zone`. |

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh có xe đỗ hai bên và không thấy rõ vạch sơn phân làn. Có thể xác nhận ngoại lệ `QC1-02` cho cả `L1` và `R1` không? | Chưa có |
| A09 | Vạch trắng đứt đã có polyline `lane#4`, nhưng cả ba polyline đều mang `L1`. Cần xác định làn xe camera đang đi trước khi kết luận thiếu `R1` hoặc sửa `position`. | Chưa có |

**Ghi chú ảnh đã rà** Ở B06, camera là `fisheye_left` và cả ba polyline `lane` đều có `position=other`, đúng quy tắc cho camera bên trái.

## Quyết định

**Lỗi nặng đã xác nhận** 0  
**Lỗi chính** 7 / 56 nhãn = **12,5%**  
**Lỗi nhẹ** 0  
**Ca chờ lead** 2  
**Quyết định** **Rework**  
**Lý do** Tỷ lệ lỗi chính đã xác nhận vượt 5%. Quyết định dựa trên 7 lỗi đã ghi trong mẫu kiểm.