# Báo cáo cá nhân — Ngày 11

Họ tên: **Nguyen Anh Tien**   Mã học viên: **2A202603120**  
Phiên bản CVAT (Help → About): **2.74.1**  
Guideline: **Road v1.0**   Lần nộp (`revision` trong manifest): **3**  
Thời điểm export trên CVAT: **22/11/2026, front 11:53 ICT; fisheye 11:56 ICT**   Số lần nộp lại sau Rework: **2**  
Manifest revision 3 được tạo lúc **11:59 ICT**. Bản revision 2 được lưu tại thư mục `r2/`.

**Trạng thái:** Đã áp dụng các sửa đổi theo phiếu QC của Vũ Tuyết Trinh và xuất revision 3. Đây chưa phải kết luận Đạt: còn 6 cảnh báo QC1-02 cần coach xác nhận, vùng `drivable` ở B06 chưa bổ sung kịp, và một số ca thuộc tính chưa đủ chắc để tự chốt. Chưa có vòng QC lại sau revision 3.

## 1. Kiểm project

| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Có | `lane` polyline; `road_curb` polyline; `crosswalk` polygon; `drivable` polygon; `traffic_light` rectangle; `traffic_sign` rectangle. |
| Thuộc tính và giá trị | Có | Đã chạy lint trên 2 ZIP CVAT export; không báo label hoặc giá trị thuộc tính lạ. Các ca cần coach xác nhận được nêu ở Mục 3. |
| 4 tag ảnh | Có | 20/20 ảnh core có đủ 4 tag `camera`, `timeofday`, `weather`, `source` trong XML. |

Polyline lane đi từ gần xe ra xa, bám tâm vạch, kết thúc ở điểm xa nhất còn quan sát được. Với fisheye, đường được thêm điểm theo cung nhìn thấy; không kéo qua vật che hoặc ra ngoài ảnh. Mỗi ảnh có một giá trị cho từng tag `camera`, `timeofday`, `weather`, `source`.

## 2. Số lượng đã gán

| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 28 | 9 | 7 | 21 | 20 | 18 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 4 | 7 | 8 | 6 | 4 | 5 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

**Tổng shape:** front **103**; fisheye **34**. Có 4 tag/ảnh nên tổng giá trị tag là front **48**, fisheye **32**.

## 3. Bảng ca khó

| Ảnh | Nhãn | Phân vân giữa | Trạng thái revision 3 / việc tiếp theo |
| --- | --- | --- | --- |
| A05 | `lane`, `drivable` | Không nhìn thấy L1/R1; vùng direct có lấn vào dải xe đỗ không? | Chưa thêm vạch để tránh suy đoán; đang chờ rà lại mép polygon direct và xin coach xác nhận ngoại lệ QC1-02. |
| A06 | `lane` | Các vệt trắng đứt mờ có phải L1/R1? | Tạm chưa thêm lane vì các vệt mờ khó phân biệt với vạch ngang; chờ đối chiếu kỹ hơn với coach để chốt ngoại lệ QC1-02. |
| A07 | `lane` | Vạch trắng mờ sát dải phân cách có phải L1? | Tạm chưa thêm L1 vì vạch quá mờ sát dải phân cách; chờ coach xác nhận ngoại lệ QC1-02. |
| A09 | `lane` | Có R1 riêng hay chỉ có curb; L2 single hay double? | Tạm giữ nguyên L2 và chưa thêm R1; chờ hỏi thêm coach về kiểu vạch L2 và ngoại lệ QC1-02 cho R1. |
| A08 | `traffic_light`, `traffic_sign` | Đèn hướng ngang và các biển cấm rẽ bị thiếu | Đã thêm box đèn vàng nhìn ngang và hai box biển cấm rẽ riêng. |
| A12 | `traffic_light` | Biểu tượng người đi bộ màu trắng không có giá trị màu tương ứng trong taxonomy | Đã sửa #1 thành `traffic_sign/mandatory`, #3 thành đèn người đi bộ, #4 thành `facing=side`, #5 thành `color=green`; màu biểu tượng trắng của #3 vẫn cần coach hướng dẫn cách mã hóa. |
| B02 | `traffic_light` | Box sát rìa nằm trong vignette; một đèn xanh nhỏ có thể là đèn người đi bộ | Đã xóa box nằm chủ yếu trong vignette. Hai box còn lại giữ nguyên thuộc tính hiện có; đèn xanh nhỏ nhìn nghiêng khá khó phân biệt `vehicle` hay `pedestrian`, tạm giữ nguyên để hỏi thêm coach. |
| B03 | `traffic_sign`, `drivable` | Nhóm hai biển và loại vùng lái thứ hai | Đã sửa nhóm biển #5 sang `information`, #6 sang `mandatory`; vùng lái thứ hai thành `alternative`; R1 giữ polyline 6 điểm theo cung. |
| B06 | `drivable`, `lane` | Thiếu vùng lái; lane ngắn chưa bám cung | Đã tăng lane lên 5 điểm. Ranh vùng mặt đường ở góc fisheye còn khá mờ nên chưa kịp vẽ `drivable`, cần rà kỹ để bổ sung sau. |
| B08 | `lane` | Polyline 3 điểm chưa theo cung | Đã cập nhật thành polyline 8 điểm theo cung quan sát được. |

## 4. Phản hồi Phiếu QC 1 nhận được

Người kiểm: **Vũ Tuyết Trinh** (22/11/2026). Phiếu đánh giá 20 ảnh core / 213 mục (133 shape + 80 tag), quyết định **Rework** với **1 lỗi nặng + 29 lỗi chính (13,6%)** và 6 ca chờ lead. Bảng dưới phản hồi trực tiếp theo mã QC trong phiếu; trạng thái là tự kiểm sau sửa, chưa được Trinh QC lại.

| Mã lỗi | Số lỗi trong phiếu | Đồng ý? | Đã sửa sau phiếu? |
| --- | ---: | --- | --- |
| QC1-01 | 0 | Có | Không cần. |
| QC1-02 | 0 lỗi QC; 6 cảnh báo lint | Có về nguyên tắc không vẽ vạch giả; A06/A07 cần coach rà vạch mờ/đứt | Chưa chốt ngoại lệ: A05 L1/R1, A06 L1/R1, A07 L1, A09 R1 vẫn thiếu; cần coach xác nhận. |
| QC1-03 | 0 | Có | Không cần. |
| QC1-04 | 1 | Có | Đã kéo dài A03 R1, bổ sung điểm dọc đoạn vạch còn thấy. |
| QC1-05 | 0 | Có | Không cần. |
| QC1-06 | 5 | Có | Đã sửa A01 L2 thành double; A04 L1 thành vàng/double và R1 thành dashed; A11 L1 thành vàng và R1 thành dashed. |
| QC1-07 | 5 | Có | Đã sửa 4/5 mục (A07, A10, A11, B03); riêng B06 chưa kịp bổ sung polygon `drivable`. |
| QC1-08 | 4 (1 nặng, 3 chính) | Có | Đã đổi A12 đèn #5 sang green; đổi A12 #1 thành biển ONE WAY; thêm đèn vàng nhìn ngang ở A08; xóa box đèn B02 nằm chủ yếu trong vignette. |
| QC1-09 | 10 | Có | Đã sửa nhóm/hướng biển A03, loại/màu đèn A06, loại/hướng đèn và nhóm biển A12, nhóm hai biển B03 theo từng đối tượng trong phiếu. Còn 2 ca khó chờ coach chốt: màu biểu tượng người đi bộ trắng ở A12 và loại đèn xanh nhỏ ở B02. |
| QC1-10 | 3 | Có | Đã thêm biển ONE WAY A06, thêm hai biển cấm rẽ A08, tách cụm ba biển A10 thành ba box. |
| QC1-11 | 2 | Có | Đã tăng mật độ điểm lane fisheye B06 lên 5 điểm và B08 lên 8 điểm theo cung nhìn thấy. |
| QC1-12 | 0 | Có | Đã xuất lại hai ZIP CVAT for images 1.1 và tạo manifest revision 3; hai ZIP không chứa ảnh. |

Sau sửa, linter báo **6 cảnh báo nặng QC1-02, 0 cảnh báo chính, 0 cảnh báo nhẹ**. Đây chỉ là kiểm tra cấu trúc; không thay thế xác nhận ngoại lệ của coach hoặc QC lại của bạn cùng lớp. Chưa ghi nhận lô Đạt.

## 5. Kiểm file export

| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | ---: | ---: | --- |
| `nguyenanhtien-front.zip` — Task #7 / Job #6 | Có; CVAT for images 1.1 | A01: 12 / 12 | A02: 10 / 10 | Có (`front`) |
| `nguyenanhtien-fisheye.zip` — Task #9 / Job #8 | Có; CVAT for images 1.1 | B01: 10 / 10 | B02: 9 / 9 | Có (`fisheye_front`) |

CVAT hiển thị Job #6 **completed 12/12** và Job #8 **completed 8/8**. Hai ZIP chỉ chứa `annotations.xml`, không chứa ảnh; XML có lần lượt 12 và 8 ảnh, đủ tag trên mọi ảnh. `road_check lint` revision 3 kiểm tra được 20 ảnh và ghi 6 cảnh báo QC1-02. Manifest revision 3 ghi **103 shape front** và **34 shape fisheye**; đủ tag ở 12/12 và 8/8 ảnh (tương ứng 48 và 32 giá trị tag nếu tính 4 tag/ảnh). Xem [manifest](nguyenanhtien-manifest.json). Bản revision 2 được giữ trong `r2/`.

Bộ file hiện có để nộp gồm: `nguyenanhtien-front.zip`, `nguyenanhtien-fisheye.zip`, `nguyenanhtien-manifest.json`, [phiếu QC tôi lập cho Trinh](nguyenanhtien-qc1-for-vutuyettrinh.md), và báo cáo này. Phiếu QC nhận từ Trinh lưu riêng tại [vutuyettrinh-qc1-for-nguyenanhtien.md](vutuyettrinh-qc1-for-nguyenanhtien.md).

## 6. Ảnh chụp màn hình và trích XML

1. Tab Labels của project: [project-labels.jpg](review-evidence/project-labels.jpg).
2. Ảnh camera trước A12, minh họa lane L2 `double`: [A12-L2-double.jpg](review-evidence/A12-L2-double.jpg).
3. Ảnh fisheye B03 với lane R1 theo cung: [B03-R1-fixed.jpg](review-evidence/B03-R1-fixed.jpg).
4. XML lane B03 được trích từ ZIP fisheye **revision 3**: [B03-lane-snippet.xml](review-evidence/B03-lane-snippet.xml).

```xml
<polyline label="lane" source="file" occluded="0" points="926.37,589.97;867.42,488.77;825.17,413.12;783.91,359.08;717.10,308.97;677.80,283.43" z_order="0">
  <attribute name="position">R1</attribute>
  <attribute name="style">dashed</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```

Các ảnh minh họa là ảnh rà soát đã lưu trong thư mục `review-evidence`; ZIP và XML revision 3 là bản annotation hiện hành.

## 7. Tự đánh giá

Mã lỗi có nhiều mục nhất trong phiếu Trinh là **QC1-09 (10 mục)**, chủ yếu là phân loại/hướng nhìn của đèn và nhóm biển. Cách tránh lặp lại: kiểm từng đối tượng với hình dạng và chức năng nhìn thấy, rồi rà lại `type`, `color`, `facing`, `group` trước khi export. QC1-02 vẫn còn 6 cảnh báo; không tự suy đoán vạch và cần coach xác nhận ngoại lệ.

Lỗi QC1-08 A12 trước sửa gán đèn #5 màu đỏ trong khi ảnh thể hiện xanh. Nếu giữ lại, mô hình đèn giao thông học sai nhãn trạng thái đỏ/xanh, tăng false positive đèn đỏ và có thể làm sai quyết định dừng/đi trong hệ thống downstream. B06 thiếu `drivable` cũng làm mô hình học thiếu vùng mặt đường ở góc fisheye. Hai ZIP revision 3 đã cập nhật sửa A12; B06 vẫn cần bổ sung polygon `drivable` trước khi chốt hoàn tất lô.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor

**Không thực hiện** hoạt động row-anchor tùy chọn.

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | — | — | — | — | — |
| x của bạn kia | — | — | — | — | — |

Ba câu row-anchor không áp dụng vì không làm phần buffer.
