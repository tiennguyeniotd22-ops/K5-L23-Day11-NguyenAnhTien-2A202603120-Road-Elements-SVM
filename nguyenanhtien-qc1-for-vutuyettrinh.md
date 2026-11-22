# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): **Vũ Tuyết Trinh (`vutuyettrinh`)**   Người kiểm (học viên): **Nguyen Anh Tien**  
Ngày: **22/11/2026**   Phiên bản guideline: **Road v1.0**  
File được kiểm: `vutuyettrinh-front.zip`, `vutuyettrinh-fisheye.zip`; **không có manifest nên chưa xác minh được revision**. SHA-256 của hai ZIP được ghi ở cuối phiếu để nhận diện đúng bản đã rà.  
Số ảnh kiểm: **8 ảnh core** (6 ảnh mẫu: A05, A06, A08, B03, B06, B08; thêm A09 và B04 để rà cảnh báo/lỗi thấy trong mẫu)   Số nhãn đã kiểm (shape + tag): **106**.

> Chỉ đánh giá ảnh core; các ảnh thêm A13–A16 và B09–B12 không tính vào kết luận QC1. Không có GT coach nên sai lệch hình học được đánh giá bằng guideline và quan sát ảnh, không phải phép đo đối chiếu GT.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 8 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 vị trí L/R | 1 xác nhận; 3 ngoại lệ chờ coach | nặng |
| QC1-03 position | sai thuộc tính / thừa | 13 lane | 0 xác nhận; 1 ca chờ coach | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 19 polylines lane/curb | 0 thấy rõ trong mẫu | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 13 lane | 0 thấy rõ trong mẫu | chính |
| QC1-06 style, color, kind | sai thuộc tính | 13 lane | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 31 drivable/crosswalk/curb | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 18 traffic_light | 0 thấy rõ trong mẫu | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 30 box đèn/biển | 0 thấy rõ trong mẫu | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 30 box đèn/biển | 0 thiếu rõ ràng trong mẫu | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 33 shape trong 4 ảnh fisheye | 0 xác nhận | chính |
| QC1-12 file | lỗi file | 2 ZIP | 0 lỗi định dạng; thiếu manifest để xác minh revision | nhẹ / nặng |

Số mục ở từng mã là số lần kiểm theo tiêu chí đó; cùng một shape có thể được kiểm theo nhiều mã, nên các hàng không cộng thành 106.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A06_b8c66e31-37045eec.jpg | lane R1 (bị thiếu) | nặng | Có vạch trắng dọc phần phải mặt đường nhưng chưa có polyline R1; các nét hiện có không theo vạch này. Bổ sung theo tâm vạch, kiểm tra hướng gần→xa và thuộc tính màu/style. Lint cũng báo thiếu R1. |
| 2 | QC1-06 | A09_c7e6d5d1-c8af9fe3.jpg | lane L2 (polyline gần (467,661)) | chính | Vạch tim đôi nhìn thấy màu vàng, nhưng thuộc tính đang `color=white`; sửa thành `yellow`. `kind=double` đang phù hợp. |
| 3 | QC1-07 | A09_c7e6d5d1-c8af9fe3.jpg | drivable `direct` (polygon có điểm (529.90,667.50), (1280,720)) | chính | Polygon kéo xuống qua mép ảnh và phủ lên phần nắp capo/xe ở đáy ảnh. Cắt vùng lái tại ranh đường–xe. |
| 4 | QC1-07 | A09_c7e6d5d1-c8af9fe3.jpg | drivable `direct` (polygon bắt đầu (479.26,662.46)) | chính | Có hai vùng `direct` tách bởi vạch làn/vạch vàng đôi. Vùng bên trái vạch vàng đôi không phải vùng đang đi (`direct`); gán `alternative` nếu xác nhận là làn cùng chiều liền kề, nếu là luồng ngược chiều thì bỏ vùng này. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05_b2576c8c-2de20b8a.jpg | Ảnh không thấy vạch sơn L1/R1 rõ; không tự vẽ thêm. Coach xác nhận ngoại lệ QC1-02 cho cả L1 và R1, rồi ghi mã ảnh/lý do vào phiếu QC. Điểm drivable gần đáy-trái (x≈0, y≈620) sát ranh kính/nắp capo; rà lại để chắc không ăn vào xe. | Chưa có |
| A08_c0deebc1-16cfa791.jpg | Lint báo thiếu L1. Có một polyline trắng dọc đang gán `position=other` (xấp xỉ (0,321)→(460,276)); xác định theo làn direct xem đây là L1/L2 hay thật sự ngoài các vị trí làn. Nếu là vạch sát làn đang đi, sửa position; không để `other` chỉ để né L1. | Chưa có |
| A09_c7e6d5d1-c8af9fe3.jpg | Lint báo thiếu R1, nhưng trong ảnh không thấy vạch sơn ở mép phải; đường kết thúc ở lề/curb. Coach xác nhận ngoại lệ QC1-02 cho R1 và ghi ảnh/lý do. | Chưa có |

## Quyết định
Lỗi nặng: **1 xác nhận** (thêm 1 ca position A08 chờ lead; 3 vị trí thiếu L1/R1 ở A05/A09 chờ coach miễn trừ)   Lỗi chính: **3 / 106 nhãn = 2,83 %**   Lỗi nhẹ: **0 xác nhận**   Ca chờ lead: **3 ảnh / quyết định miễn trừ-position**  
Quyết định (**Release / Hold / Rework**): **Rework**  
Lý do: Có một lỗi nặng QC1-02 đã xác nhận ở A06; theo luật Phiếu QC 1, chỉ cần một lỗi nặng là Rework. Ngoài ra, A09 có 3 lỗi chính được ghi ở trên. Tỉ lệ lỗi chính trong mẫu dưới 5%, nhưng không làm thay đổi quyết định vì còn lỗi nặng. Cần sửa và export lại, rồi QC lại revision mới. A05/A09 không được vẽ làn giả; chỉ chốt miễn trừ sau khi coach xác nhận.

## Kiểm tra file và lint
- Hai ZIP đều mở được, mỗi ZIP chỉ chứa `annotations.xml` theo CVAT for images 1.1; không có ảnh nhúng.
- Có 16 ảnh front và 12 ảnh fisheye; các ảnh core A01–A12 và B01–B08 đều có trong gói. XML có đủ bốn tag trên mọi ảnh; lint không báo sai tag camera.
- `road_check lint` trên cả hai ZIP: **5 cảnh báo nặng core** (A05 L1/R1, A06 R1, A08 L1, A09 R1) và **6 cảnh báo nặng nếu tính cả ảnh thưởng** (thêm A14 R1). Lint chỉ gợi ý; A05/A09 cần coach xác nhận ngoại lệ, A06 được ghi lỗi ở trên, A08 cần coach phân xử line `other`.
- Các cảnh báo box thấp hơn 8 px là gợi ý, không tính lỗi vì guideline không bắt buộc gán đèn/biển thấp hơn 8 px. Lint còn báo một điểm drivable lặp ở A04; ảnh A04 không nằm trong mẫu 8 ảnh nên cần người gán tự rà.
- Không nhận được `<tên>-manifest.json`; do đó chưa xác định revision hoặc thời điểm export. Hash SHA-256 của bản đã QC:
  - `vutuyettrinh-front.zip` — `cb242b21da248251a3111492c4224cf90ca263edd0a15f5f363a327103355ca1`
  - `vutuyettrinh-fisheye.zip` — `acd35aeb9092e238b903b1f4f1b37a44744f2a15eefd314d9c2b764c56ddb8c0`
- Trạng thái job `completed` không thể xác minh từ file export.

## Ảnh đối chiếu
- [A05 — vùng drivable sát mép capo](review-evidence/vutuyettrinh/A05_overlay.jpg)
- [A06 — overlay mép phải](review-evidence/vutuyettrinh/A06_edge_zoom.jpg), [ảnh gốc phóng to](review-evidence/vutuyettrinh/A06_raw_edge_zoom.jpg)
- [A08 — lane `other`, cần chốt position](review-evidence/vutuyettrinh/A08_overlay.jpg)
- [A09 — lane màu và vùng drivable](review-evidence/vutuyettrinh/A09_lane_area_zoom.jpg)
- [B03](review-evidence/vutuyettrinh/B03_overlay.jpg), [B04](review-evidence/vutuyettrinh/B04_overlay.jpg), [B06](review-evidence/vutuyettrinh/B06_overlay.jpg), [B08](review-evidence/vutuyettrinh/B08_overlay.jpg) — kiểm tra mẫu fisheye.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
