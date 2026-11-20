# Báo cáo cá nhân — Ngày 11
Họ tên: Đỗ Hoàng Anh    Mã học viên: 2A202603187
Phiên bản CVAT (Help → About): 2.81.0
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1
Thời điểm export (ngày giờ trên CVAT): 20/11/2026, front 23:56 và fisheye 23:44 (giờ VN)    Số lần nộp lại sau Rework: 0

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane và road_curb là polyline, crosswalk và drivable là polygon, traffic_light và traffic_sign là rectangle |
| Thuộc tính và giá trị | Đúng | Dán JSON từ `road_lab.taxonomy` vào tab Raw, nên khớp từng giá trị |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source; mỗi tag có một thuộc tính select `value` |


## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 29 | 10 | 5 | 23 | 26 | 24 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 6 | 11 | 7 | 11 | 4 | 2 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |


## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane L1, R1 | Vẽ hay bỏ | Bỏ | Đường nhỏ, hai bên đỗ xe, mặt đường không có vạch sơn nào |
| A06 | lane R1 | Vẽ hay bỏ | Bỏ | Đường rộng dưới cầu vượt, bên phải xe không có vạch phân làn. Chỉ có một vạch trắng ở góc dưới phải, quá xa xe để gán R1 |
| A09 | lane R1 | Vẽ hay bỏ | Bỏ | Bên phải chỉ có lề đường, không có vạch |

Cả ba ảnh đều bị lint báo QC1-02 (thiếu L1/R1). Tôi để nguyên vì ảnh thật sự không có vạch, và cần coach xác nhận để được miễn.

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi:  Quyết định nhận được:  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| dohoanganh-front.zip | Được | A01: / 10 | A02: / 8 | Có |
| dohoanganh-fisheye.zip | Được | B01: / 4 | B02: / 5 | Có |



## 6. Ảnh chụp màn hình
1. Tab Labels của project: đủ 6 label vẽ và 4 label tag.

![Tab Labels của project](dohoanganh-report-images/1-labels.png)

2. Một ảnh camera trước đã gán: vùng lái, vạch làn, mép đường và biển.

![Ảnh camera trước đã gán](dohoanganh-report-images/2-front.webp)

3. Ảnh fisheye B03 (camera sau) đã gán: vùng lái dừng ở mép thân xe, polyline mép đường đi theo cung ở bên phải.

![Ảnh fisheye B03 đã gán](dohoanganh-report-images/3-fisheye-B03.webp)

Phóng to vùng lái của B03: các điểm đặt dày dọc cung dưới theo mép thân xe, bốn tag ảnh ở góc trên trái.

![Vùng lái B03 phóng to](dohoanganh-report-images/4-fisheye-B03-drivable.webp)

4. Một đoạn XML có `<polyline label="lane">` (ảnh A01, trong `dohoanganh-front.zip`):

```xml
<polyline label="lane" source="manual" occluded="0" points="111.85,720.00;273.16,578.75;311.77,547.57;334.56,527.88;345.35,519.37;353.44,513.18" z_order="0">
  <attribute name="position">L1</attribute>
  <attribute name="style">dashed</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```

## 7. Tự đánh giá
Lỗi tôi mắc nhiều nhất là QC1-02, thiếu L1 hoặc R1: lần lint đầu tiên có 12 ảnh dính lỗi này. Kế đến là QC1-01, quên đặt tag ở A06, A07, A14 và B06, và quên đổi `camera` từ front sang fisheye_front ở B01. Nguyên nhân là tôi vẽ nhãn trước rồi để tag cho sau, và CVAT tự điền giá trị mặc định nên nhìn tưởng đã xong. Ở Ngày 20 tôi sẽ đặt bốn tag ngay khi mở ảnh, và đọc lại từng tag trước khi sang ảnh khác. Với L1 và R1, tôi sẽ tự hỏi "bên trái và bên phải làn mình đã có vạch chưa" trước khi lưu.

Nhãn của tôi đi vào model huấn luyện nhận diện làn đường. Một lỗi tôi đã sửa là A09: vạch trắng đứt ở bên trái xe nhưng tôi gán R1. Nếu để nguyên, model sẽ học rằng vạch nằm bên trái ảnh có nhãn "bên phải". Model dùng để giữ làn sẽ hiểu sai xe đang nằm ở đâu trong làn, kéo xe về sai hướng, và lỗi này khó thấy vì hình vẽ vẫn đúng chỗ, chỉ có nhãn `position` sai.
