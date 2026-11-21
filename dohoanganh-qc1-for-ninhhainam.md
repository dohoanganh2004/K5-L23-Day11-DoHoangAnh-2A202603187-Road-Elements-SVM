# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): ninhhainam        Người kiểm (học viên): dohoanganh
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): ninhhainam-front.zip và ninhhainam-fisheye.zip; chưa nhận được manifest nên chưa biết `revision`
Số ảnh kiểm: 6 (A02, A07, A08, A10, B02, B05; không có ảnh thêm)   Số nhãn đã kiểm (shape + tag): 119

Cách kiểm: chạy `road_check lint` trên cả hai zip (44 cảnh báo toàn lô), rồi vẽ nhãn của bạn lên ảnh gốc của 6 ảnh trên để đối chiếu từng cảnh báo bằng mắt. Không có GT nên không đo được độ lệch 5 px (QC1-04 chỉ kiểm chiều vạch). Phần group, facing và type của đèn, biển mới xem lướt, chưa kiểm từng hộp.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 10 | 0 (+2 chờ lead) | nặng |
| QC1-03 position | sai thuộc tính / thừa | 16 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 16 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 16 | 3 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 16 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 11 | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 14 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 41 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 41 | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 29 | 9 | chính |
| QC1-12 file | lỗi file | 119 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-07 | A02 | drivable #6, #7 | chính | `direct` và `alternative` bị đảo. Làn đang đi (chứa tâm đáy ảnh, x≈640) là polygon #7 nhưng gán `alternative`; polygon #6 là làn bên trái nhưng gán `direct` |
| 2 | QC1-04 | A07 | lane #0 (R2) | chính | Polyline 2 điểm ở (1254,475)→(1280,484), điểm đầu cao hơn điểm cuối, vẽ từ xa về gần |
| 3 | QC1-05 | A07 | lane #0, #5 (R2) | chính | Một vạch R2 bị tách thành hai polyline: #0 nối tiếp đầu gần của #5 |
| 4 | QC1-07 | A07 | drivable #4 (direct) | chính | Polygon dừng ở y≈413, ngay đuôi xe phía trước, bỏ phần mặt đường phía sau xe. Guideline gán theo "đi được nếu đường trống" |
| 5 | QC1-04 | A08 | lane #14 (R1) | chính | Polyline 2 điểm đi từ (643,308) xuống (765,450), vẽ từ xa về gần |
| 6 | QC1-05 | A08 | lane #13, #14, #33 (R1) | chính | Một vạch R1 đứt bị vẽ thành ba polyline 2 điểm, trong đó #14 và #33 ghi `solid` |
| 7 | QC1-05 | A08 | lane #18, #29 (L1) | chính | Hai polyline cùng position L1, vạch đứt có thể bị tách |
| 8 | QC1-10 | A08 | traffic_sign | chính | Thiếu hộp biển phụ "PASSENGER CARS ONLY" nằm trên biển xanh chỉ hướng (group `supplementary`) |
| 9 | QC1-07 | A10 | drivable #4 (direct) | chính | Polygon bắt đầu từ y≈456, dưới đuôi xe phía trước, bỏ phần đường sau xe (polygon bên trái lên tới y≈333) |
| 10 | QC1-11 | B02 | traffic_light #3 | chính | Đèn ở sát rìa vòng ảnh, `edge_zone` đang là false, cần bật |
| 11 | QC1-11 | B02 | traffic_light #4 | chính | Như trên |
| 12 | QC1-11 | B02 | traffic_light #5 | chính | Như trên |
| 13 | QC1-11 | B05 | traffic_sign #4 | chính | Hộp nằm sát mép trên vòng ảnh (y≈4), `edge_zone` false, cần bật |
| 14 | QC1-11 | B05 | traffic_sign #5 | chính | Như trên |
| 15 | QC1-11 | B05 | traffic_sign #6 | chính | Như trên |
| 16 | QC1-11 | B05 | traffic_sign #14 | chính | Như trên |
| 17 | QC1-11 | B05 | traffic_sign #15 | chính | Như trên |
| 18 | QC1-11 | B05 | traffic_light #8 | chính | Hộp sát mép trên vòng ảnh, `edge_zone` false, cần bật |

Dòng 2 và 3 cùng một polyline (A07 #0) nhưng khác lỗi: ngược chiều (QC1-04) và vạch bị tách (QC1-05), nên ghi riêng. Dòng 6 và 7 tính mỗi dòng một lỗi, mặc dù lint đếm thành hai cảnh báo QC1-05 của A08.

Lint còn báo thêm các cảnh báo hộp dưới 8 px ở A10 (3) và A12 (1). Đó là gợi ý, không phải lỗi chấm, nên không tính.

Trong 6 ảnh này không có ảnh nào hoàn toàn không lỗi. A02 là ảnh lint không báo gì, nhưng mình đã mở ra và thấy lỗi `direct`/`alternative` bị đảo (dòng 1).

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A07 | Thiếu L1: bên trái làn đang đi là dải bê tông (đã có `road_curb`), không thấy vạch sơn. Có được miễn QC1-02 không? | |
| A10 | Thiếu R1: bên phải làn đang đi là làn buýt có chữ "ONLY", không thấy rõ vạch phân làn. Có được miễn QC1-02 không? | |
| B02 | `road_curb` #8 (3 điểm) và #9 (2 điểm) là đoạn ngắn gần thẳng, lint báo ít điểm. Có tính lỗi QC1-11 không? | |
| B05 | `road_curb` #0, #2, #12 chỉ 2–3 điểm; #12 và #13 chạy chồng nhau ở mép trên. Có tính lỗi QC1-11 hoặc nhãn thừa không? | |

## Quyết định
Lỗi nặng: 0 (2 ca QC1-02 chờ lead)   Lỗi chính: 18 / 119 nhãn = 15,1 %   Lỗi nhẹ: 0   Ca chờ lead: 4  
Quyết định (Release / Hold / Rework): Rework
Lý do (theo luật của phiếu): Không có lỗi nặng chắc chắn, nhưng lỗi chính chiếm 15,1 % số nhãn đã kiểm, vượt ngưỡng 5 %. Theo luật, vượt ngưỡng thì Rework, kể cả khi lead trả lời bốn ca chờ theo hướng nào. Phần lớn lỗi là `edge_zone` ở fisheye (9 lỗi) và vạch đứt vẽ ngược chiều hoặc bị tách ở A07, A08. Nếu lead không miễn hai ca QC1-02 thì còn thêm hai lỗi nặng.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
