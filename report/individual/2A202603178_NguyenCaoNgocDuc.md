# Báo cáo cá nhân — Nguyễn Cao Ngọc Đức — 2A202603178

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Nguyễn Cao Ngọc Đức
- MSSV: 2A202603178
- Email: không cung cấp
- Link repository: https://github.com/ducnguyen-ai/K5-L2-Day04-NguyenCaoNgocDuc-2A202603178-KeypointPose-Student
- Phiên bản CVAT (Help → About): 2.74.1
- Máy: Windows · RAM 16 GB · GPU NVIDIA GeForce RTX 4060 Laptop 8 GB · CVAT local qua Docker, cổng 8081
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Tổng thời gian thực hành: khoảng **120 phút** (học viên tự ước lượng).
- Giờ bắt đầu / kết thúc: không ghi lại chính xác; thực hành và rà soát qua hai ngày 12–13/11/2026.

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có | Có | 19 |
| `face` | Skeleton | 13 | Có | Có | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu): Có. Trái/phải được hiểu theo người trong ảnh.

Cách đổi cờ cho **một điểm**: chọn đúng điểm trong phần Parts của skeleton hoặc menu chuột phải của điểm, bật/tắt `occluded` hay `outside`, rồi Save; không dùng `hidden` thay cho cờ visibility.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | Chưa ghi nhận số đếm | Chưa ghi nhận số đếm | Chưa ghi nhận |
| `occluded` | 3 | 6 | Chưa ghi nhận số đếm | Chưa ghi nhận số đếm | Chưa ghi nhận |
| `back` | 2 | 4 | Chưa ghi nhận số đếm | Chưa ghi nhận số đếm | Chưa ghi nhận |
| `small` | 1 | 3 | Chưa ghi nhận số đếm | Chưa ghi nhận số đếm | Chưa ghi nhận |
| `crowd` | 1 | 3 | Chưa ghi nhận số đếm | Chưa ghi nhận số đếm | Chưa ghi nhận |
| `faces` | 8 | 8 | — | — | Chưa ghi nhận |

- Không ghi số ảnh hoàn thành riêng tại mốc phút 105.
- Tổng thời gian khoảng 120 phút; không bấm giờ riêng CP1, CP2, CP3 hoặc từng nhóm ảnh.
- Không có số đo để xác định ảnh tốn thời gian nhất. Ba ca tiêu biểu cần xem kỹ được phân tích ở mục 3.

## 3. Bảng ca khó (CP1, CP2)

Ba ca tiêu biểu dưới đây được tổng hợp từ ảnh, bản xuất và trao đổi thực tế; không xếp hạng theo thời gian vì không có số đo từng ảnh.

| Ảnh | Người / mặt | Điểm | Cờ / quyết định trong bản cuối | Vấn đề cần cân nhắc | Phân tích |
|---|---|---|---|---|---|
| `000000522889.jpg` | Người mặc áo cam ở hậu cảnh | `left_shoulder` | Giữ visible (`v=2`) | Sát mép ảnh có phải là ngoài ảnh? | Học viên phóng to vai và cung cấp ảnh minh chứng: điểm vẫn nằm trong khung trên phần vai. Cảnh báo khoảng cách tới mép không tự chứng minh điểm ở ngoài. Bản xuất mới không còn cảnh báo sát mép. |
| `face_380639.jpg` | Người cúi đầu, mắt nhắm | `left_eye_upper/lower`, `right_eye_upper/lower` | Học viên chọn giữ nguyên sau khi nhìn lại | Đặt đúng mép mí khi mắt nhắm; phân biệt vị trí và tên điểm | Khoảng cách hai mí nhỏ nên đường nối khó đọc. Bản xuất vẫn có hai cảnh báo y của mí trên lớn hơn mí dưới. Học viên cho biết chưa thấy sai trên ảnh; ảnh không bật tên điểm nên chưa đủ bằng chứng để khẳng định cảnh báo sai. |
| `000000030960.jpg` | Hai người trong ảnh cưới bị cắt phần chân | `left_ankle`, `right_ankle` | `outside` (`v=0`) trong bản xuất | Khớp ngoài khung hay khớp bị che nhưng còn ước lượng được? | Cổ chân nằm ngoài ảnh nên không kéo điểm về mép hoặc đặt lên cẳng chân. Tọa độ cũ vẫn có thể còn trong JSON, nhưng `v=0` mới quyết định điểm bị bỏ qua khi huấn luyện/chấm. |

## 4. Bảng tự review (CP3)

Học viên xác nhận đã rà lại cả hai job, cập nhật nhãn và Save. Riêng hai ảnh `000000522889.jpg` và `face_380639.jpg`, học viên cho biết đã xem cảnh báo và chọn giữ nguyên. Bảng dưới được tổng hợp **sau khi sửa**, kết hợp phản hồi đó với kết quả kiểm tra ZIP; không có nhật ký đầy đủ ghi lỗi trước mỗi lần sửa.

| Ảnh | Người / mặt | Điểm / phạm vi rà soát | Mã | Kết quả ghi nhận | Trạng thái |
|---|---|---|---|---|---|
| `000000564304.jpg` | Người trượt ván | Cấu trúc skeleton và số instance | `ok` | Bản xuất có 1 skeleton, đủ 17 điểm; script không cảnh báo ảnh này. | Đã xuất |
| `000000522889.jpg` (`crowd`) | Người hậu cảnh và vận động viên | Vai sát mép; cặp cổ chân | `position` | Học viên xem lại và giữ điểm vai trong khung; cảnh báo sát mép đã hết. Cảnh báo hướng cặp cổ chân vẫn còn, chưa có ghi chép xác định đó là tư thế thật hay đảo tên. | Vai đã kiểm; cổ chân cần đối chiếu tên |
| `000000521817.jpg` | Người trong cảnh chợ | Cặp mắt trái/phải | `lr_swap` | Script nghi ngờ cặp mắt khác hướng các khớp còn lại; đây là mã lỗi nghi ngờ, chưa khẳng định có đảo nhãn. | Còn cảnh báo |
| `000000480582.jpg` (`back`) | Hai người trong cảnh đàn cừu | Cấu trúc và visibility | `ok` | Bản xuất có 2 skeleton, đủ 17 điểm mỗi skeleton; script không cảnh báo ảnh này. Không dùng kết quả này để khẳng định mọi cờ đã đúng về ngữ nghĩa. | Đã xuất |
| `000000307757.jpg` (`back`) | Hai người quay lưng dưới ô | Cấu trúc, trái/phải và visibility | `ok` | Bản cuối có 2 skeleton; các cảnh báo thấy rõ mặt nhưng gán như quay lưng ở lần kiểm trước không còn. | Đã xuất |
| `face_380754.jpg` | Người đeo kính gọng | Cấu trúc và thứ tự 13 điểm | `ok` | Có 1 skeleton mặt, đủ 39 số; script không cảnh báo ảnh này. | Đã xuất |
| `face_380639.jpg` | Người cúi đầu, mắt nhắm | Hai cặp mí trên/mí dưới | `position` | Học viên xem ảnh phóng to và chọn giữ nguyên; script vẫn báo hai cặp mí. Cần bật tên điểm để kết luận về từng mí. | Giữ nguyên; còn cảnh báo |
| `face_296767.jpg` | Người đeo kính râm | 8 điểm mắt phía sau tròng | `ok` | JSON có 8 điểm `v=1`, 5 điểm `v=2`, `num_keypoints=13`; script không cảnh báo. | Đã xuất |

Tổng hợp **mã ghi nhận trong 8 dòng**: `ok=5`, `position=2`, `lr_swap=1`; các mã nghi ngờ không được tính thành lỗi đã xác nhận hoặc đã sửa. Không có đủ dữ liệu để thống kê tổng số thao tác sửa lỗi thực tế.

Quy tắc cần giữ khi phân biệt `v=1` và `v=0`: khớp bị che nhưng xác định khá chắc vị trí thì `v=1`; khớp ngoài ảnh hoặc không xác định đáng tin cậy thì `v=0`. Bản persons hiện không có điểm `v=1`, nên số liệu này cần được cân nhắc khi đánh giá các trường hợp che khuất; script không tự xác nhận quyết định visibility là đúng.

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Kiểm tra trực tiếp JSON xuất, không chỉnh sửa nội dung file ZIP:

| File | Người / mặt kiểm | Số phần tử `keypoints` | Số điểm theo cờ visibility | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `NguyenCaoNgocDuc_persons.zip` | `000000030960.jpg`, annotation ID 1 | 51 | v=0: 9, v=1: 0, v=2: 8 | Có (8) |
| `NguyenCaoNgocDuc_persons.zip` | `000000522889.jpg`, annotation ID 17 | 51 | v=0: 1, v=1: 0, v=2: 16 | Có (16) |
| `NguyenCaoNgocDuc_faces.zip` | `face_296767.jpg`, annotation ID 4 | 39 | v=0: 0, v=1: 8, v=2: 5 | Có (13) |

`outside` được xuất thành `v=0`; `occluded` được xuất thành `v=1`. Điểm `outside` vẫn mang tọa độ cũ trong bản xuất CVAT 2.74.1, không được tự sửa JSON thành `0,0`. Hai ZIP chỉ chứa annotation, không kèm ảnh gốc; tên và thứ tự keypoint đã đối chiếu với schema của lab.

Hai job đã chuyển sang `completed`: persons Task #18 / Job #17; faces Task #19 / Job #18.

Kết quả script tự kiểm:

```text
----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: NguyenCaoNgocDuc_persons.zip
  Số ảnh: 12 · số skeleton `person`: 21 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000030960=2, 000000056651=2, 000000194027=1, 000000211458=1, 000000269462=3, 000000307757=2, 000000336477=1, 000000480582=2, 000000521817=2, 000000522889=3, 000000525227=1, 000000564304=1
  Cờ v: v=2 235 (66%) · v=1 0 (0%) · v=0 122 (34%)
  num_keypoints trung bình: 11.2
- File face: NguyenCaoNgocDuc_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_137371=1, face_204787=1, face_223746=1, face_296767=1, face_380639=1, face_380754=1, face_490361=1, face_559185=1
  Cờ v: v=2 95 (91%) · v=1 8 (8%) · v=0 1 (1%)
  num_keypoints trung bình: 12.9
- Ghi chú: 123 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 4
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các cảnh báo còn lại:

- `000000521817.jpg`: hướng cặp mắt khác với các cặp khớp còn lại; cần đối chiếu hướng đầu với hướng thân.
- `000000522889.jpg`: hướng cặp mắt cá khác với các cặp khớp còn lại; cần đối chiếu tư thế chân thực tế.
- `face_380639.jpg`: hai cảnh báo mí trên nằm dưới mí dưới theo tọa độ y. Học viên đã xem ảnh phóng to và cho biết chưa thấy sai; cần kiểm tra bằng tên điểm trước khi kết luận là cảnh báo hình học không phù hợp tư thế.

Cảnh báo `left_shoulder` sát mép của `000000522889.jpg` đã hết ở lần xuất mới nhất. Ảnh học viên cung cấp cho thấy điểm vai nằm trong khung; sát mép không đồng nghĩa với `outside`.

Kết quả ĐẠT của script xác nhận cấu trúc dữ liệu, không thay thế kiểm tra nhãn bằng mắt.



## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor (đủ 17 điểm có tên):

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO val2017 / Wikimedia Commons.

## 7. Tự đánh giá

Phần rút kinh nghiệm được đề xuất từ các ca và bản xuất đã quan sát; không có thống kê để kết luận lỗi nào học viên mắc nhiều nhất.

1. **Điều cần ưu tiên ở lần sau:** kiểm tra tên từng điểm và cờ visibility trước khi Save. Một đường nối nhìn hợp lý vẫn có thể mang nhầm tên mí trên/mí dưới hoặc trái/phải. Khi có cảnh báo, phóng to ảnh, bật tên điểm rồi kiểm tra tư thế thực tế, thay vì chỉ nhìn màu và hình skeleton.

2. **Quy tắc đề xuất bổ sung:** với điểm sát mép ảnh, kiểm tra điểm có nằm trên đúng khớp còn nhìn thấy trong ảnh hay không; không đổi sang `outside` chỉ vì cảnh báo khoảng cách tới mép. Ghi lại ảnh và lý do nếu quyết định giữ nguyên cảnh báo. Ví dụ: vai ở `000000522889.jpg`.

3. **Ảnh hưởng tới model:** keypoint visible/occluded cung cấp vị trí mục tiêu cho heatmap hoặc nhánh dự đoán tọa độ. Đặt điểm lên cẳng chân thay cho cổ chân sẽ dạy model sai tâm khớp. Điểm `v=0` thường bị loại khỏi phần loss/evaluation của keypoint; lạm dụng cờ này làm mất tín hiệu học cho khớp bị che nhưng vẫn ước lượng được. Đảo tên trái/phải còn làm sai phép hoán đổi cặp điểm khi tăng cường dữ liệu bằng lật ảnh. Vì vậy cần rà tên, vị trí và visibility như ba kiểm tra riêng.

## 8. Khó khăn và lỗi kỹ thuật

- Sau khi hai task ban đầu không còn tồn tại, chạy lại quy trình setup để liên kết assignment với Task #18 và #19, giữ nguyên MSSV và bộ ảnh được chia.
- Khi phát sinh thắc mắc điểm hiện lại, đã đối chiếu cờ `outside` trên server với bản lưu trước khi xuất. ZIP được xuất trực tiếp từ CVAT và không chỉnh JSON bằng tay.
- Công cụ chụp minh chứng qua trình duyệt tự dừng vì không xác minh chắc chắn URL Chrome. Học viên đã tự chụp và cung cấp đủ bốn ảnh minh chứng bắt buộc.

## Bonus

B1 và B2 chưa thực hiện; không có file xuất bonus. Không ghi nhận điểm bonus hoặc kết quả so sánh B3 khi chưa hoàn thành các bước tương ứng.

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Hướng dẫn, schema và script `lab.py`, `src/check_submission.py` trong repo lớp.
- CVAT 2.74.1 local: chỉnh sửa, lưu và xuất COCO Keypoints 1.0.
- Torchvision Keypoint R-CNN ResNet50-FPN pretrained: tạo gợi ý 17 điểm người trên GPU local; MediaPipe Face Landmarker: tạo gợi ý điểm khuôn mặt, ánh xạ sang bộ 13 điểm của lab. Học viên chỉnh sửa và kiểm tra các gợi ý trong CVAT. Nguồn annotation được giữ theo thực tế, không đổi toàn bộ thành `manual`.
- Trợ lý AI hỗ trợ thiết lập môi trường, chạy model, xuất/kiểm tra file và tổng hợp báo cáo từ dữ liệu cùng phản hồi của học viên. Những phần phân tích được đề xuất đã được phân biệt với trải nghiệm học viên xác nhận.
- Quy trình có bước sinh điểm tự động, vì vậy không mô tả đây là bài được tạo hoàn toàn bằng tay.
