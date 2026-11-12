# Báo cáo cá nhân — PhamPhuNguyenHung-2A202604062

Đổi tên file theo quy tắc `MSSV_HoTen.md`. Ví dụ: `20241234_NguyenVanAn.md`.

Dữ liệu: 12 ảnh người COCO val2017 (Lin et al., 2014) và 8 ảnh chân dung Wikimedia Commons, chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Phạm Phú Nguyên Hùng
- MSSV: 2A202604062
- Email: hungphamphunguyen@gmail.com
- Link repository: https://github.com/phamphunguyenhung/K5-L2B-DAY04-PhamPhuNguyenHung-2A202604062-KeypointPose
- Phiên bản CVAT (Help → About): 2.74.1 (đọc từ API /api/server/about)
- Máy: Windows 11 Pro · RAM 16 GB (Docker Desktop được cấp 7.7 GB) · chạy CVAT chế độ đầy đủ
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu:16:36
- Giờ kết thúc:17:22

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có (kiểm bằng tool) | Có (kiểm bằng tool) | 19 |
| `face` | Skeleton | 13 | Có (kiểm bằng tool) | Có (kiểm bằng tool) | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu): outside O occluded Q

...

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 0 | ___ | ___ |
| `occluded` | 3 | 6 | 0 | ___ | ___ |
| `back` | 2 | 4 | 0 | ___ | ___ |
| `small` | 1 | 1 | 2 | ___ | ___ |
| `crowd` | 1 | 3 | 0 | ___ | ___ |
| `faces` | 8 | 8 | — | — | |

- Số ảnh người đã xong ở mốc phút 105: 10 / 10
- Thời gian thực tế (phút): CP1 39 · CP2 45 · CP3 30 (phần này cần bạn ghi theo đồng hồ của mình, công cụ không đo được thời gian gán tay)
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?

...

## 3. Bảng ca khó (CP1, CP2)

Mỗi điểm bạn phân vân một dòng, nhất là phân vân giữa `v = 1` và `v = 0`, hoặc không chắc hướng người.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| face_324513.jpg | Mặt (kính râm) | `left_eye_upper`, `left_eye_lower`, `right_eye_upper`, `right_eye_lower` | `occluded` (v = 1) | v = 1 / v = 0 | Tròng kính râm tối che mắt, không thấy con người. Đặt điểm mí theo vị trí ước lượng từ gọng kính và đường mắt, dùng phím Q để đặt điểm dự đoán. Chọn v = 1 vì vị trí ước lượng được tương đối chắc. |

## 4. Bảng tự review (CP3)

Đi từ ảnh cuối về ảnh đầu. 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Ít nhất 8 dòng, kể cả dòng `ok`. Ghi lỗi trước, sửa sau.

Mã lỗi dùng đúng một trong: `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, `ok`.
không có

Tổng hợp số lỗi theo mã: 0

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn):
kính râm ở job 13 lí do chọn v=1 là vì thầy bảo trong buổi học online và thực tế mình vẫn phải dự đoán chứ nó k phải nằm ngoài, 1 số cam hồng ngoại vẫn view đc
...

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Tự kiểm tay trong file JSON:

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `HoVaTen_persons.zip` | | | | |
| `HoVaTen_persons.zip` | | | | |
| `HoVaTen_faces.zip` | | | | |

Sau khi xuất, CVAT ghi `occluded` thành `v = ___` và `outside` thành `v = ___`. Tọa độ của điểm `outside` trong file là `0, 0` hay tọa độ cũ? ___

Hai job đã chuyển sang completed trên CVAT? Có (stage `acceptance`, state `completed`, kiểm lại qua API). Đã export lại sau khi finish: số liệu không đổi.

Dán phần **TÓM TẮT** in ra từ `src/check_submission.py`:

```text
(dán ở đây)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

...

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

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   làm tay quá thủ công mà không dùng tools, và mình có thể copy trước các mẫu skeleton gần giống nhau để tăng tgian làm nếu làm tay

2. Một quy tắc bạn đề xuất thêm vào guideline (kèm ảnh ví dụ nếu có):

   làm quen được thao tác rồi thì làm 1 cách thông minh chứ không phải cố chấp tốn thời gian làm tay nếu thực sự mình không làm được thì hỏi AI và các giải pháp khác trên mạng để tăng quy trình không tự mày mò tốn tgian

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào (heatmap, trọng số trong loss, hay bước lật ảnh):
Ở Job 13, ảnh số 3, tôi kiểm tra lại và sửa nhãn visibility của các điểm mắt từ v=2 (nhìn thấy rõ) sang v=1 (bị che khuất) bằng phím Q, vì mắt bị kính râm che. Nếu giữ v=2, model sẽ học sai trọng số trong loss, coi các điểm mắt ước lượng là điểm nhìn thấy rõ, làm giảm độ chính xác khi dự đoán landmark.
   ...

## 8. Khó khăn và lỗi kỹ thuật

- Docker Desktop chưa chạy khi bắt đầu `lab.py check`: đã mở Docker Desktop, sau đó check OK.
- `lab.py setup` cần đăng nhập tương tác: đã đưa tài khoản vào file `.env` (không commit) và nạp biến môi trường trước khi chạy.
- Tải model `yolo11l-pose` bị ngắt ở 99%: đã chạy tải lại thành công.

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| | | | |
| | | | |
| | | | |

Kết quả `src/check_submission.py` cho `HoVaTen_bonus_persons.zip`:

```text
(dán ở đây)
```

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Ảnh không màu khó hơn ở điểm nào? Kính râm trên ảnh hồng ngoại có còn là `v = 1` không?

...

### B3 — Model so với nhãn của tôi (không tính điểm)

- Demo đã dùng:
- Ảnh đã thử:

1. Model có trả điểm cho khớp bị che, hay khớp ngoài ảnh không? Confidence ở các điểm đó thế nào?

   ...

2. Với người quay lưng, model có đổi trái/phải không?

   ...

3. Bộ điểm của model có giống 17 điểm COCO không?

   ...

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Model pose local `yolo11l-pose` (Ultralytics YOLO11, pretrained COCO) để sinh nháp skeleton người. Chạy trên CPU.
- OpenCV Haar cascade (dự phòng khi không có điểm mắt-mũi để neo nháp mặt).
- Công cụ tự viết `tools/skeleton-pose-manager` để sinh nháp, ghi lên CVAT có backup, và kiểm tra cấu trúc. Dữ liệu không rời máy.
- AI (Claude Code) dùng để viết code của công cụ trên. Mọi quyết định gán nhãn, cờ visibility, và nội dung mục 3, 4, 7 do người làm bài thực hiện.
- Số liệu nháp: người 323 điểm (job 12), mặt 104 điểm (job 13). Số điểm đã chỉnh tay (so với nháp, đo bằng `spm diff`): người 25/221 điểm lệch hơn 3 px, 33 điểm đổi cờ; mặt 84/104 điểm lệch hơn 3 px, 10 điểm đổi cờ.
