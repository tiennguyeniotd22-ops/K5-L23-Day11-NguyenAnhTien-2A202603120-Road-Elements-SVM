# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Anh Tiến        Người kiểm (học viên): Vũ Tuyết Trinh  
Ngày: 2026-11-22                                Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `nguyenanhtien-front.zip` (sha256 `195e3dcb…85ec6`), `nguyenanhtien-fisheye.zip` (sha256 `b2c8d035…03fe42`); lô gửi không kèm manifest nên không rõ `revision` (coi là lần nộp 1)  
Số ảnh kiểm: 20 (toàn bộ A01–A12, B01–B08) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 213 (133 shape + 80 tag)

Cách kiểm: chạy `road_check lint` trên hai file, rồi vẽ toàn bộ nhãn lên ảnh gốc và so từng nhãn với ảnh và guideline. `#` là thứ tự nhãn trong ảnh của file export (đếm từ 0).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 80 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 32 | 0 (6 cảnh báo lint chờ coach, xem Ca mơ hồ) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 32 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 28 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 28 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 32 | 5 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 28 | 5 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 25 | 4 | 1 nặng / 3 chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 42 | 10 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 17 | 3 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 35 | 2 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-08 | A12 | traffic_light #5 | nặng | Đèn xe quay về xe (facing front) đang sáng **xanh** nhưng gán color = red |
| 2 | QC1-06 | A01 | lane #6 (L2) | chính | Vạch mép trái là hai vạch trắng song song, gán kind = single (phải là double) |
| 3 | QC1-04 | A03 | lane #2 (R1) | chính | R1 chỉ 2 điểm, bắt đầu giữa ảnh (~700,465); bỏ đoạn vạch gần xe |
| 4 | QC1-09 | A03 | traffic_sign #1 | chính | Thấy mặt sau tấm biển (màu xám), gán facing = front, group = prohibitory |
| 5 | QC1-09 | A03 | traffic_sign #3 | chính | Biển thoi màu cam (công trường) là warning, gán prohibitory |
| 6 | QC1-09 | A03 | traffic_sign #4 | chính | Biển vàng chanh (trường học / người qua đường) là warning, gán information |
| 7 | QC1-06 | A04 | lane #2 (L1) | chính | L1 là vạch **vàng đôi**, gán white / single (CHECKPOINTS nêu A04 có vàng đôi) |
| 8 | QC1-06 | A04 | lane #0 (R1) | chính | R1 là vạch trắng đứt, gán style = solid |
| 9 | QC1-09 | A06 | traffic_light #9 | chính | Đèn người đi bộ (hình người đi trắng) gán type = vehicle |
| 10 | QC1-09 | A06 | traffic_light #12 | chính | Đèn người đi bộ (đang tắt) gán type = vehicle, color = red |
| 11 | QC1-10 | A06 | thiếu traffic_sign | chính | Biển "ONE WAY" trên cột giữa (~660–710, 215–240) chưa gán (mandatory) |
| 12 | QC1-07 | A07 | drivable #0 (direct) | chính | Vùng direct dừng ở đuôi xe phía trước (y≈408); guideline yêu cầu không khoét quanh xe khác, phải kéo tiếp lên đường |
| 13 | QC1-08 | A08 | thiếu traffic_light | chính | Cụm đèn vàng quay ngang trên cột phải (~870–895, 145–205) chưa gán (facing side) |
| 14 | QC1-10 | A08 | thiếu traffic_sign | chính | Các biển cấm rẽ trên cột phải (~990–1010, 185–245) chưa gán |
| 15 | QC1-07 | A10 | drivable #7 (direct) | chính | Direct tràn sang trái qua L1 vào làn giữa L2–L1, và dừng ở đuôi xe phía trước |
| 16 | QC1-10 | A10 | traffic_sign #4 | chính | Một box bao ba tấm biển xếp chồng (No Parking / No Standing / P cấm); mỗi tấm cần box riêng |
| 17 | QC1-06 | A11 | lane #4 (L1) | chính | L1 là vạch vàng (tim đường), gán color = white |
| 18 | QC1-06 | A11 | lane #0 (R1) | chính | R1 là vạch trắng đứt, gán style = solid |
| 19 | QC1-07 | A11 | drivable #5 (direct) | chính | Có polygon direct thứ hai ở phần đường bên phải R1, sát hàng xe đỗ; phần này không phải làn đang đi |
| 20 | QC1-08 | A12 | traffic_light #1 | chính | Gán biển "ONE WAY" thành traffic_light (red, vehicle); đúng phải là traffic_sign mandatory |
| 21 | QC1-09 | A12 | traffic_light #3 | chính | Đèn người đi bộ (hình người đi) gán type = vehicle |
| 22 | QC1-09 | A12 | traffic_light #4 | chính | Cụm đèn nhìn từ cạnh bên, không thấy mặt đèn; gán facing = front, color = red (đúng: side, unknown) |
| 23 | QC1-09 | A12 | traffic_sign #2 | chính | Biển tên đường "Greene" màu xanh lá là information, gán prohibitory |
| 24 | QC1-08 | B02 | traffic_light #3 | chính | Box (1178–1275, 49–203) phần lớn nằm trong vùng tối viền ảnh, không sát vỏ đèn nào |
| 25 | QC1-07 | B03 | drivable #4 (direct) | chính | Ảnh có hai polygon direct; làn bên kia R1 phải là alternative |
| 26 | QC1-09 | B03 | traffic_sign #5 | chính | Bảng chỉ dẫn nền xanh dương là information, gán prohibitory |
| 27 | QC1-09 | B03 | traffic_sign #6 | chính | Biển xanh dương có mũi tên bắt buộc đi theo hướng là mandatory, gán information |
| 28 | QC1-07 | B06 | thiếu drivable | chính | Trọng tâm của B06 là "drivable + lane position=other" nhưng ảnh không có polygon drivable nào |
| 29 | QC1-11 | B06 | lane #0 (other) | chính | Lane chỉ 3 điểm, ngắn, không đi theo cung (lint cũng báo) |
| 30 | QC1-11 | B08 | lane #1 (other) | chính | Lane chỉ 3 điểm, chưa đặt điểm theo cung (lint cũng báo) |

Ảnh không ghi lỗi: B01, B04, B05, B07 (đủ tag; crosswalk, road_curb và drivable khớp ảnh).

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Lint báo QC1-02 thiếu L1 và R1. Ảnh là phố hẹp, không thấy vạch sơn. Coach xác nhận miễn chứ? Bạn chưa ghi lý do miễn. Polygon direct có lấn sang dải xe đỗ bên trái không? | |
| A06 | Lint báo thiếu L1/R1. Dưới cầu cạn có các vệt sơn trắng đứt (~480–590, 435 và ~700–850, 460–480). Đó có phải vạch làn cần gán không? | |
| A07 | Lint báo thiếu L1. Bên trái là dải phân cách bê tông, thấy mờ một vạch trắng sát chân dải phân cách. Có cần gán L1 không? | |
| A09 | Lint báo thiếu R1. Bên phải là lề, đã có road_curb. Mình nghĩ ca này được miễn; cần coach xác nhận. Vạch trắng cong bên trái (#1, L2) trông như vạch đôi nhưng gán single. | |
| A12 | Đèn đi bộ #3 sáng hình người đi màu trắng. Road v1.0 không có màu trắng, vậy chọn color nào? | |
| B02 | Box #2 có vẻ chứa một đèn đi bộ hình người xanh, nhìn nghiêng. Có phải sửa type = pedestrian, color = green không? | |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 29 / 213 nhãn = 13,6 %   Lỗi nhẹ: 0   Ca chờ lead: 6  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô còn 1 lỗi nặng (A12 #5: đèn quay về xe sáng xanh nhưng gán đỏ), nên phải Rework. Tỉ lệ lỗi chính 13,6 % cũng vượt ngưỡng 5 %. Sáu ca chờ lead không đổi quyết định này. Khi nộp lại, bạn cần tạo manifest với `--revision 2` và ghi vào phiếu mã các ảnh được coach miễn QC1-02.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
