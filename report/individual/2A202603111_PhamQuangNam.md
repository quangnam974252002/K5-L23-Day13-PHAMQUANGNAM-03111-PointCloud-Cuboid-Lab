# Báo cáo Day 13 — <Phạm Quang Nam>, <03111>

> **Cách dùng mẫu này:** đổi tên file thành `<MSSV>_<HoTen>.md` (họ tên không dấu, viết liền), ví dụ `2A202600123_NguyenVanAn.md`. Đổi tên, đừng chép thành file thứ hai.
>
> Xoá mọi dấu TODO và dòng gợi ý (dòng bắt đầu bằng `>`). Mỗi con số lấy từ **bảng A** hoặc **phiếu tự kiểm** trong `submission/`, kèm đơn vị (m, °). Ảnh để trong `report/individual/images/` (nộp LMS trong file zip, không commit); trong báo cáo chỉ ghi **tên file ảnh**. Báo cáo này nằm trên repo public: không chép biển số, chữ trên biển hiệu hay biển chỉ đường, tên đường, địa danh; nhắc tới bạn khác thì ghi MSSV, không ghi họ tên. Cả báo cáo ~2 trang.

## 1. Kết luận trước
(học viên): mã số, task `D13-…`, 10 frame của bạn; hệ điều hành, trình duyệt, phiên bản CVAT (tên tài khoản → About); MSSV bạn ngồi cạnh. Rồi 2–3 câu: tổng bao nhiêu cuboid, frame nào ít nhất và vì sao; `selfcheck` cờ bao nhiêu cuboid trên tổng số; bạn tin phần nào nhất và phần nào còn yếu nhất (hướng, đáy, kích thước, class, vật xa).

> 03111
> D13-03111
> s01f25, s01f40, s02f12, s02f37, s03f03, s03f18, s04f15, s04f55, s05f04, s05f48
> Window 10 Home
> Firefox
> 2.83.0
> 
> 84
> s05f48 ít nhất vì có ít vật có thể định dạng rõ.
> 
>

(học viên): cách dùng CVAT, 3 dòng: đổi góc nhìn (nhìn từ trên xuống, xoay, dời); vẽ và chỉnh một cuboid (Shape, nháy đúp, Top/Side/Front); bật mũi tên hướng (Cuboid orientation) và xem cuboid trên ảnh camera (`preview`).
> Đọc hướng dẫn xử dụng trước khi dùng
> Nháy đúp sau khi ấn vào icon cuboid vào 1 điểm muốn vẽ/gán nhãn
> 
> 

## 2. Đọc frame (Bước 2)
Hai frame đọc kỹ. Ảnh: `t1-<frame>-3d`, `t1-<frame>-top` (ảnh nhìn từ trên xuống, có đánh dấu phía trước, +x, +y).

| Frame | Phía trước xe ở cạnh nào của ảnh nhìn từ trên xuống; +x, +y chỉ về đâu | Mặt đường (phẳng/dốc; thấp hơn LiDAR ~ m) | Vật xa nhất đọc được (~ m) | Loại vật thấy | Vật phía sau / hai bên | Cụm chưa đọc được |
|---|---|---|---|---|---|---|
| s03f18 | không | phẳng | 56.6 | car | car | |
| s05f48 | không | phẳng | 30.3 | car | car | |

(học viên): 3 điều **chỉ camera** cho biết và 3 điều **chỉ LiDAR** cho biết, lấy từ chính hai frame trên.
> Camera cho biết mầu của vật, chi tiết vật trong ảnh và vật ở xa hoặc ở nền
> lidar cho biết vật ở đâu trong 3d, vị trí của vật và độ sâu của vật xung quanh 
Tám frame lướt:

| Frame | Phía trước ở cạnh nào của ảnh nhìn từ trên xuống | Điều lạ (nếu có) |
|---|---|---|
|  | | |

## 3. Ba cuboid có hướng dẫn (Bước 3)
Ảnh: `t2-a-car`, `t2-b-bus-truck`, `t2-c-ped-cyclist`.

| Vật | Frame, idx | Class | Mũi tên yaw đúng hướng? | Đáy chạm đường? | Đã kiểm Top/Side/Front + ảnh? | Kích thước trong bảng 4.3? |
|---|---|---|---|---|---|---|
| (a) xe con gần | (học viên) | | | | | |
| (b) xe buýt hoặc xe tải | (học viên) | | | | | |
| (c) người đi bộ hoặc xe hai bánh | (học viên) | | | | | |

(học viên): vòng hiệu chuẩn: cuboid của bạn lệch so với các bạn ở điểm nào, cả lớp chốt cách hiểu guideline nào? Và các vật bạn **bỏ qua vì không đủ cơ sở** (frame, vị trí, mô tả, loại nghi vấn như UNCERTAIN_CLASS / LOW_VISIBILITY), hoặc ghi "không có".

## 4. Bốn hiện tượng chất lượng (Bước 4)
Nguyên nhân ghi là **giả thuyết**. Frame mượn thì ghi rõ nguồn: task chung, hoặc MSSV của bạn cho mượn.

| Hiện tượng | Frame / tên ảnh / nguồn | Nguyên nhân (giả thuyết) | Thấy gì trên point cloud | Hệ quả khi gán (theo guideline) |
|---|---|---|---|---|
| 1. Bóng che | (học viên) | | | |
| 2. Thưa ở xa | (học viên) | | | |
| 3. Phản xạ thấp / ít điểm bất thường | (học viên) | | | |
| 4. Điểm lạ | (học viên) | | | |

## 5. Số từ cuboid của tôi (Bước 5)
Lấy từ `submission/D13-<MÃ SỐ>-bangA.csv`; số điểm lấy từ cột `points_in` của `-tukiem.csv`. Mặt đường khoảng −1,7 m: z đáy lệch hơn 0,3 m là lơ lửng hoặc chìm.

| Cuboid (frame, idx, class) | z | h | z đáy = z − h/2 | dist_m | r = √(x²+y²+z²) | yaw_deg | Nhận xét (lơ lửng / chìm / chạm đường) |
|---|---|---|---|---|---|---|---|
| (học viên) | | | | | | | |
| (học viên) | | | | | | | |
| (học viên) | | | | | | | |

(học viên): (a) cuboid **gần nhất** và **xa nhất**: `dist_m` và r của từng cái. (b) Kích thước l, w, h của một người đi bộ (hoặc xe hai bánh) và một xe con so với bảng 4.3: chiều nào ngoài khoảng, vì sao. (c) `yaw_deg` của một xe cùng chiều phía trước và một xe ngược chiều (nếu có): có gần 270° và 90° không.

Mật độ theo khoảng cách (4 cuboid ở các `dist_m` khác nhau):

| Cuboid (frame, idx, class) | dist_m | Số điểm (`points_in`) |
|---|---|---|
| (học viên) | | |

(học viên): một câu quy luật ("xa gấp … lần thì số điểm còn khoảng …") và so với đường cong ở slide bài giảng (xe con: khoảng 1968 điểm ở 0–10 m, 718 ở 10–20 m, 214 ở 20–30 m, 72 ở 30–40 m, 19 ở 60–80 m). Rồi phần tự kiểm: hai cuboid bạn **đã sửa** sau `preview` / `selfcheck` (frame, idx, sửa gì), và những cảnh báo bạn **giữ nguyên** kèm lý do.

(học viên): đổi kiểm: MSSV người đã kiểm chéo với bạn, hai con số nào được đối chiếu với bảng A, khớp hay lệch (lệch thì đã sửa gì).

## 6. Ý nghĩa của nhãn, cách dùng AI và điều còn chưa chắc
(học viên): (a) hai câu, nói từ phía model sẽ học trên nhãn này: vì sao nhãn 3D đo bằng mét chứ không phải pixel; vì sao vật thưa điểm cần quy tắc riêng. (b) Dùng AI? Ghi 3 dòng: công cụ, câu hỏi chính, bạn dùng kết quả thế nào. Không dùng: ghi "không dùng". (c) Điều còn chưa chắc, lỗi phát hiện sau hạn (không chấm; viết bằng lời, không chép số từ phiếu hồ sơ lỗi).
