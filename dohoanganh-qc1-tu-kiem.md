# Phiếu QC 1 — Road v1.0 (tự kiểm lô của mình, bản thực hành)

Lô được kiểm (học viên): Đõ Hoàng Anh      Người kiểm (học viên): Đỗ Hoàng Anh
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): dohoanganh-front.zip và dohoanganh-fisheye.zip, revision 1
Số ảnh kiểm: 20 (A01–A12, B01–B08)   Số nhãn đã kiểm (shape + tag): 238

Cách kiểm: chạy `road_check lint`, rồi mở ảnh gốc A03, A05, A06, A08, A09 và B03 để xem trực tiếp. Các lỗi còn lại dựa vào lint, chưa đối chiếu bằng mắt. Không có GT nên không đo được độ lệch 5 px.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 20 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 32 | 4 (chờ lead) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 35 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 35 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 35 | 3 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 35 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 34 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 30 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 56 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 56 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 41 | 1 (+2 chờ lead) | chính |
| QC1-12 file | lỗi file | 238 | 26 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A05 | lane | nặng | Thiếu L1. Đã xem ảnh: đường nhỏ, xe đỗ hai bên, không có vạch sơn. Chờ lead miễn |
| 2 | QC1-02 | A05 | lane | nặng | Thiếu R1, cùng lý do. Chờ lead miễn |
| 3 | QC1-02 | A06 | lane | nặng | Thiếu R1. Đã xem ảnh: bên phải không có vạch phân làn sát xe. Chờ lead miễn |
| 4 | QC1-02 | A09 | lane | nặng | Thiếu R1. Đã xem ảnh: bên phải chỉ có lề đường. Chờ lead miễn |
| 5 | QC1-05 | A04 | lane (hai polyline L1) | chính | Vạch vàng đôi vẽ thành hai polyline cùng position L1, nên gộp một polyline `kind=double` |
| 6 | QC1-05 | A09 | lane (hai polyline L2) | chính | Vạch trắng đôi vẽ thành hai polyline cùng position L2, cần gộp |
| 7 | QC1-05 | A11 | lane (hai polyline L1) | chính | Vạch trắng đôi vẽ thành hai polyline cùng position L1, cần gộp |
| 8 | QC1-11 | B08 | lane #4 | chính | Lane chỉ có 3 điểm, fisheye cần đặt điểm theo cung |
| 9 | QC1-12 | A14 | ảnh | nhẹ | Ảnh không có nhãn nào (đã chủ ý bỏ, thuộc ảnh thưởng) |
| 10 | QC1-12 | A02, A03, A04, A05, A06, A08, A09, A10, A11, A12 | drivable, lane, road_curb, crosswalk | nhẹ | 19 điểm lặp liền nhau do click hai lần, cần xoá điểm thừa |
| 11 | QC1-12 | B01, B02, B03, B05, B06, B08 | drivable, crosswalk, road_curb | nhẹ | 7 điểm lặp liền nhau, cần xoá điểm thừa |


## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh không có vạch sơn, có được miễn QC1-02 (L1, R1) không? | |
| A06 | Bên phải không thấy vạch phân làn sát xe, có được miễn thiếu R1 không? | |
| A09 | Bên phải chỉ có lề đường, có được miễn thiếu R1 không? | |
| A04, A09, A11 | Vạch đôi vẽ một polyline `kind=double` hay hai polyline? Guideline không nói rõ, tôi suy ra là một polyline từ code `bdd_to_cvat_road.py` | |
| B02 | Hai đèn (#2, #3) được gợi ý bật `edge_zone`, chưa kiểm bằng mắt có đúng ngoài 80 % bán kính không | |

## Quyết định
Lỗi nặng: 4 (đều chờ lead)   Lỗi chính: 4 / 238 nhãn = 1,7 %   Lỗi nhẹ: 26   Ca chờ lead: 5  
Quyết định (Release / Hold / Rework): Hold
Lý do (theo luật của phiếu): Có 4 lỗi nặng QC1-02 nhưng cả bốn đều ở ảnh không thấy vạch, nên phụ thuộc lead có miễn hay không. Lỗi chính 1,7 % dưới ngưỡng 5 %. Câu trả lời của lead ảnh hưởng tới kết luận, nên chọn Hold. Nếu lead không miễn thì quyết định là Rework.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng.
