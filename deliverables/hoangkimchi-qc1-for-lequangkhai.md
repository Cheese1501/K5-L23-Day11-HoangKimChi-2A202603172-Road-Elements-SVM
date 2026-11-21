# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Lê Quang Khải — 2A202603237.  
Người kiểm (học viên): Hoàng Kim Chi — 2A202603172.  
Ngày đối chiếu bản file: 21/11/2026. Phiên bản guideline: Road v1.0.  
File được kiểm: hai ZIP task 40 và task 42, tên đầy đủ và SHA256 ở cuối phiếu. Không có manifest của Khải đi kèm hai file, nên tôi chưa xác nhận revision của lô.  
Số ảnh kiểm trực quan: **6**, không kiểm ảnh thêm. Số nhãn trong mẫu: **50 shape + 24 tag = 74 nhãn**.

Tôi kiểm A01, A08, A10, B01, B03, B06 trên cùng bộ ảnh gốc. Tôi kiểm định dạng hai ZIP trên toàn bộ ảnh chứa trong file; phần nhận xét trực quan và mẫu số tỷ lệ lỗi chỉ dùng sáu ảnh trên. Tôi không dùng bài của người khác làm GT.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi xác định | Mức |
| --- | --- | ---: | --- | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1/R1 | bỏ sót | 6 | 0; 2 trường hợp chờ xác nhận phạm vi/ngoại lệ | nặng |
| QC1-03 position | sai thuộc tính / thừa | 9 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 13 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 5 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 9 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 7 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 11 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 27 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 16 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 13 | 0 | chính |
| QC1-12 file | lỗi file | 74 | 0 | nhẹ / nặng |

Số mục kiểm là đơn vị theo từng tiêu chí: camera tính theo ảnh; L1/R1 tính theo vị trí; các mục hình học/thuộc tính tính theo đối tượng. Một nhãn có thể được kiểm ở nhiều mã nhưng chỉ được tính một lần trong mẫu số 74 nhãn. Mã QC1-12 gồm kiểm mở file, schema và nhãn trong mẫu, ngoài ra hai ZIP được kiểm không kèm ảnh. Số 0 chỉ có nghĩa chưa phát hiện lỗi xác định trong phạm vi kiểm, không chứng nhận toàn lô hoàn hảo hoặc sai số ≤5 px.

## Danh sách lỗi

| # | Mã | Ảnh | Nhãn (label, tham chiếu) | Mức | Mô tả và hướng sửa |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-06 | A01 | lane #1, L2, đầu (0,600.5) | chính | Vạch ngoài trái là hai nét trắng liền song song nhưng kind=single. Sửa kind=double; tâm polyline cần theo quy ước vạch đôi của lớp. |
| 2 | QC1-04 | B03 | lane #4, R1, (431,322) → (583,297) | chính | Đường chỉ bám một đoạn ngang ở phía xa, không theo chuỗi vệt trắng dọc làn nhìn thấy ở nửa trái ảnh và bỏ đoạn gần. Rà lại đối tượng, hướng gần ra xa và vẽ theo tâm vệt sơn thật; không dùng đoạn biên ngang để thay vạch làn. |
| 3 | QC1-07 | A08 | drivable #2, direct, đầu (0,509) | chính | Biên trái mở tới mép trái ảnh, bao cả vùng nhiều làn/vạch hướng rẽ bên trái thành direct. Giới hạn direct theo làn xe đang đi; vùng cùng chiều bên cạnh tách alternative, tránh gộp toàn mặt đường. |
| 4 | QC1-09 | A10 | traffic_sign #11, hộp (46,48)–(96,171) | chính | Một hộp bao nhiều tấm biển cấm đỗ/dừng xếp dọc trên cột. Tách hộp theo từng tấm biển thực tế, sát mép; không gộp cả cột biển thành một đối tượng. |

Tham chiếu `#n` là thứ tự shape trong annotations.xml do trình đọc repo đánh từ 0; không phải ID server CVAT. Tôi kèm tọa độ đầu/hộp để người sửa tìm đúng đối tượng. Các lỗi ở các hàng là những đối tượng khác nhau, không đếm lặp một lỗi dưới hai mã.

## Ca mơ hồ

| Ảnh | Câu hỏi cho lead | Lời đáp hiện có |
| --- | --- | --- |
| A08:L1, A10:R1 | Có yêu cầu lane và có đủ vạch để gán ở vị trí này không? | Tôi chưa có xác nhận coach trong hai file được kiểm; không tự tính thành lỗi nặng xác định hoặc tự miễn. |
| Ngoại lệ ngoài mẫu: A05, A06, A07, A12 | Lint toàn bộ 20 ảnh còn báo thiếu L1/R1 ở các vị trí tương ứng. | Khải đã có giải trình trong phiếu cũ; tôi cần bản xác nhận coach nếu dùng để miễn, không cộng các mục ngoài mẫu vào tỷ lệ sáu ảnh. |
| Hình học | Sai số tối đa so GT và trạng thái che khuất có đúng hoàn toàn không? | Chưa có GT; kiểm trực quan không thay phép chấm GT. |

## Quyết định

Lỗi nặng xác định trong mẫu: **0**. Lỗi chính xác định: **4 / 74 nhãn = 5.41%**. Lỗi nhẹ xác định: **0**. Ca chưa chốt phạm vi/ngoại lệ: 2.  
Quyết định cho bản file được đối chiếu: **Rework**.  
Lý do: tỷ lệ lỗi chính xác định trong mẫu lớn hơn 5%, đã đủ điều kiện trả sửa theo luật lớp. Các ca chờ lead ghi riêng; không dùng Hold thay cho Rework khi đã vượt ngưỡng. Tôi chưa cho điểm số vì không có GT/rubric chấm đầy đủ.

## File và dấu vân tay

- `task_40_annotations_2026_11_21_04_00_08_cvat for images 1.1.zip` — 42696 byte; SHA256 `50bc7fa186573c15b59428910bddcbe2ab6f41ae5aa57254d03783cfe03bc861`.
- `task_42_annotations_2026_11_21_04_01_54_cvat for images 1.1.zip` — 21842 byte; SHA256 `20ad189dc71e756018bc6de2183b80013e70f8211c62574f3d360ae9a5f6a980`.

Tôi đề nghị sửa các lỗi đã ghi rồi gửi lại đúng bản export mới để kiểm lại. Tôi giữ bản file này và phiếu này để phân biệt trước/sau sửa.

## Đối chiếu bốn góp ý của bản nhận xét trước

Tôi không giữ nguyên bốn lỗi cũ khi file đã thay đổi:

| Vị trí cũ | Kết quả trên hai ZIP vừa nhận |
| --- | --- |
| A01 L2 tại (100,571) | Điểm này nằm trên polyline, khoảng cách 0 px. Không lặp lại nhận xét lệch 10.5 px tại điểm này. |
| A10 L2 tại (260,522) | Khoảng cách 0 px. Không lặp lại nhận xét lệch 9.5 px tại điểm này. |
| B03 L1 tại (770,345) | Khoảng cách khoảng 2.97 px, dưới 5 px tại điểm kiểm cục bộ. Không kết luận cả đường đã đạt từ một điểm. |
| B06 tại (1000,470) trên dải phân cách | Điểm này đã nằm ngoài polygon crosswalk. Không lặp lại lỗi bao dải phân cách ở chính điểm này. |

Khoảng cách tính trên tọa độ ảnh gốc và polyline trong XML; đây là phép kiểm điểm cục bộ, không phải so với GT toàn ảnh.
