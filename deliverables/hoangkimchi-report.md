# Báo cáo cá nhân Ngày 11

Họ tên: Hoàng Kim Chi  
Mã học viên: 2A202603172  
Phiên bản CVAT: 2.74.1, kiểm từ API của CVAT local.  
Guideline: Road v1.0. Bản xuất sau sửa: revision 2.  
Thời điểm xuất: 14:06:39 ngày 21/11/2026, giờ Việt Nam.  
Số lần nộp lại sau Rework: chưa có lần nộp chính thức.

Tôi đã chuẩn bị 28 ảnh, cấu hình project và lưu nhãn trong bốn task CVAT. Tôi dùng công cụ vẽ, công cụ hỗ trợ gán nhãn và Python để kiểm dữ liệu, xuất file, tạo manifest. Bản xuất có 177 hình và 112 tag. Tôi đã mở lại hai ZIP và đối chiếu số lượng với CVAT. Tôi đã sửa nhãn và kiểm lại cấu trúc dữ liệu. Bản này không còn hộp trùng tọa độ hoặc thiếu trường thuộc tính; còn bốn cảnh báo không thấy vạch cần ghi ngoại lệ và chưa có kết quả QC chéo.

## 1. Kiểm project

| Mục | Kết quả | Ghi chú |
| --- | --- | --- |
| Sáu nhãn, đúng kiểu | Đạt về cấu hình | lane/road_curb là polyline; crosswalk/drivable là polygon; traffic_light/traffic_sign là rectangle. |
| Thuộc tính và giá trị | Đủ cấu trúc | Tôi đối chiếu taxonomy; đủ trường chưa đồng nghĩa đúng giá trị cho từng đối tượng. |
| Bốn tag ảnh | 112 tag cho 28 ảnh | Mỗi ảnh có camera, timeofday, weather, source, mỗi tag có thuộc tính value. |

Tôi kết thúc polyline bằng phím N khi đang vẽ và lưu bằng Ctrl+S. Tôi đặt tag bằng công cụ Tag hoặc nhập nhãn CVAT, sau đó kiểm value. Tôi sửa thuộc tính trong Objects/Details, không coi giá trị mặc định là kết quả đã kiểm.

Project: [d11-road-hoangkimchi](http://localhost:8080/projects/5). Các job: [front](http://localhost:8080/tasks/24/jobs/19), [front-extra](http://localhost:8080/tasks/25/jobs/20), [fisheye](http://localhost:8080/tasks/26/jobs/21), [fisheye-extra](http://localhost:8080/tasks/27/jobs/22).

Cả bốn job còn in progress, giai đoạn annotation. Tôi chưa đánh completed; còn bước xác nhận ngoại lệ và QC chéo trước khi chốt bài. Các kiểm thử mã không phải điểm chất lượng nhãn của tôi.

## 2. Số lượng đã gán

| Task | Ảnh trong file | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 29 | 0 | 7 | 26 | 25 | 15 |
| front-extra | 4 | 9 | 0 | 7 | 10 | 8 | 12 |
| fisheye | 8 | 5 | 0 | 10 | 5 | 1 | 2 |
| fisheye-extra | 4 | 0 | 0 | 4 | 1 | 0 | 1 |
| Tổng | 28 | 43 | 0 | 28 | 42 | 34 | 30 |

Tôi ghi số hình từ bản xuất r2. Số lượng không thay thế kiểm hình học hoặc điểm chấm của coach. Tôi chưa có bảng phân công nhóm nhãn từng ảnh trong repo để xác nhận đầy đủ phạm vi.

## 3. Bảng ca khó và xử lý cảnh báo

| Ảnh | Nhãn | Trường hợp | Cách tôi xử lý | Xác nhận |
| --- | --- | --- | --- | --- |
| A05 | lane L1 | Đường không có vạch sơn phân làn nhìn thấy | Tôi không vẽ vạch giả; đề nghị áp dụng ngoại lệ không thấy vạch. | Cần coach xác nhận ngoại lệ. |
| A05 | lane R1 | Đường không có vạch sơn phân làn nhìn thấy | Tôi không vẽ vạch giả; đề nghị áp dụng ngoại lệ không thấy vạch. | Cần coach xác nhận ngoại lệ. |
| A06 | lane R1 | Mép phải là vỉa hè, vạch phân làn không rõ | Tôi không lấy mép vỉa hè làm lane để bù R1. | Cần coach xác nhận ngoại lệ. |
| A14 | lane R1 | Phía phải bị che và không thấy vạch đủ rõ | Tôi không suy đoán tọa độ ngoài căn cứ ảnh. | Cần coach xác nhận ngoại lệ. |
| B07/B08 | lane fisheye | Polyline ít điểm | Tôi đã chỉnh điểm; lint bản r2 không còn hai cảnh báo ít điểm. | Kết quả lint chưa chứng minh sai số tâm ≤5 px. |
| B11 | Vạch ô đỗ | Ngoài phạm vi lane của bài | Tôi không gán lane cho các đường ô đỗ. | Theo guideline. |

Tôi ghi lý do không có vạch trong bảng ca khó. Tôi chưa có xác nhận trực tiếp của coach nên chưa coi các cảnh báo là đã được miễn chính thức. Manifest giữ nguyên bốn cảnh báo QC1-02, không xóa hoặc sửa kết quả công cụ để tạo trạng thái không lỗi.

## 4. Tự kiểm sau sửa và phiếu QC nhận được

| Hạng mục | Kết quả kiểm bản r2 |
| --- | --- |
| Bốn tag mỗi ảnh | Đủ 112 tag, camera theo đúng tên ảnh. |
| Thuộc tính hình | 177 hình có đủ trường, giá trị thuộc danh sách hợp lệ. |
| Hộp trùng tọa độ | Không phát hiện nhóm trùng chính xác ở lần đọc lại. |
| Position lane camera bên | Không còn cảnh báo position tại B07/B08. |
| Polyline ít điểm | Không còn cảnh báo ba điểm tại B07/B08. |
| Cảnh báo chính/nhẹ | Lint: 0 chính, 0 nhẹ. |
| Ca không thấy vạch | 4 cảnh báo nặng QC1-02 tại A05/A06/A14, ghi riêng để xin xác nhận. |

Tôi đã sửa nhãn sau lần tự kiểm trước và xuất lại bản r2. Những kết quả trên xác nhận cấu trúc dữ liệu và các điều kiện lint kiểm được; không có nghĩa tất cả hình học và ý nghĩa đối tượng đã được kiểm chéo độc lập.

Tôi đã đối chiếu hai ZIP Khải vừa gửi ngày 21/11/2026 và hoàn thành [phiếu tôi kiểm bài Khải](hoangkimchi-qc1-for-lequangkhai.md). Tôi kiểm trực quan A01, A08, A10, B01, B03, B06, gồm 50 hình và 24 tag, tổng 74 nhãn. Tôi ghi bốn lỗi chính khác nhau, tỷ lệ 4/74 = 5.41%, quyết định Rework cho bản file này. Các số đo cũ đã được kiểm lại: ba điểm lane đã dưới 5 px tại điểm kiểm và điểm dải phân cách B06 đã nằm ngoài polygon, nên tôi không lặp lại bốn lỗi cũ.

Tôi chuẩn bị hai ZIP và manifest r2 để Khải kiểm lô tôi. Tôi chưa nhận phiếu nhận xét độc lập được Khải xác nhận, nên chưa ghi quyết định chính thức của Khải vào báo cáo này. Các bản tự rà và tài liệu trao đổi được giữ riêng ở local.

Tôi tiếp tục sửa theo bản ZIP cụ thể được nhận xét và sẽ cập nhật kết quả QC nhận được khi Khải xác nhận. Không coi lint hết cảnh báo hình học là đã được người kiểm độc lập chấp nhận.

Tôi giữ bản trước sửa trong `out/bao-cao-cu/truoc-r2/` và `out/ban-giao-r1/`. Manifest hiện tại là revision 2 để phân biệt rõ với bản r1, chưa có lần nộp lại chính thức sau phiếu Rework của người kiểm.

## 5. Kiểm file export

Tôi xuất từng task bằng CVAT for images 1.1, tắt Save images, rồi gộp front với front-extra và fisheye với fisheye-extra. Bản xuất từng task được giữ local để đối chiếu. Hai ZIP bàn giao chỉ chứa annotations.xml.

| File | Mở lại được? | Số hình ảnh 1, CVAT/file | Số hình ảnh 2, CVAT/file | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| hoangkimchi-front.zip | Có | A01: 8/8 | A02: 5/5 | Có, đủ 16 ảnh |
| hoangkimchi-fisheye.zip | Có | B01: 2/2 | B02: 2/2 | Có, đủ 12 ảnh |

Tôi đã tạo [manifest revision 2](hoangkimchi-manifest.json). Hai file có contains_images=false, đủ 20 ảnh bắt buộc và 8 ảnh thêm. Lint ghi **4 cảnh báo nặng, 0 cảnh báo chính, 0 cảnh báo nhẹ**. Cả bốn thuộc các ca không thấy vạch ở mục 3; cần coach xác nhận để áp dụng ngoại lệ.

Hai ZIP lưu local trong deliverables, không đưa lên Git. Tôi chưa nộp bản này như bản đạt yêu cầu và chưa đổi job sang completed.

## 6. Minh chứng

Tôi lưu bản xuất từng task, bảng kiểm export và dữ liệu đối chiếu trong `out/bao-cao-cap-nhat-cuoi/`. Tôi đã đọc lại XML thật của ZIP front. Dưới đây là polyline R1 trên A01 trong bản r2:

```xml
<polyline label="lane" source="manual" occluded="0" points="655.10,675.40;524.20,588.10;448.10,533.00;411.60,508.50" z_order="0">
  <attribute name="position">R1</attribute>
  <attribute name="style">dashed</attribute>
  <attribute name="color">white</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```

Tôi dùng đoạn XML này để kiểm tên label, thuộc tính và tọa độ. Nó không thay thế ảnh chụp màn hình theo yêu cầu mẫu báo cáo.

| Minh chứng yêu cầu | Trạng thái |
| --- | --- |
| Tab Labels của project | Cần bổ sung ảnh chụp giao diện. |
| Ảnh front đã hoàn thiện theo nhóm được giao | Cần bổ sung ảnh chụp giao diện sau khi chốt QC. |
| Ảnh fisheye phóng to polyline cong | Cần bổ sung ảnh chụp giao diện sau khi chốt QC. |
| Đoạn XML có polyline label=lane | Đã trích XML thật ở trên; cần ảnh chụp đoạn XML nếu coach yêu cầu đúng hình thức ảnh. |

Tôi lưu ảnh minh chứng trong `deliverables/minh-chung/` ở local, không đưa ảnh BDD100K/WoodScape vào Git. Ảnh chồng nhãn phục vụ tự kiểm không được dùng thay ảnh chụp CVAT.

## 7. Tự đánh giá

Tôi cần ưu tiên QC1-03 về position, QC1-07 về vùng đi được và QC1-08/09 về đèn, biển. Tôi chưa có số đếm kiểm chéo để kết luận mã nào nhiều nhất. Tôi cần kiểm từng đối tượng ngay sau khi vẽ và tránh chạy công cụ nhiều lần gây nhãn trùng.

Nhãn lane cung cấp tọa độ mục tiêu cho mô hình học vị trí vạch; polygon cung cấp vùng phân đoạn; hộp và thuộc tính cung cấp đối tượng/trạng thái. Ví dụ, ghi đèn xanh thành red tạo mẫu huấn luyện mâu thuẫn với ảnh. Tôi đã sửa các trường hợp đèn xanh ghi đỏ ở A08/A14 trước khi xuất bản cập nhật. Việc sửa màu giúp nhãn phản ánh trạng thái trong ảnh; các hộp nhỏ vẫn cần kiểm trực quan khi QC.

Tôi đã kiểm nhãn trùng và thuộc tính trên bản r2; tôi tiếp tục đối chiếu hình học ở mức phóng lớn trong vòng QC. Tôi chỉ nộp bản hoàn chỉnh sau khi xử lý lỗi và nhận kiểm chéo.

## 8. Từ polyline đến đích row-anchor

Tôi dùng R1 của A01, nội suy tuyến tính từ tọa độ thật trong file export. Tôi chưa có polyline của bạn được ghép để so sánh.

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của tôi | Không có làn | Không có làn | 602.0 | 542.0 | 485.4 |
| x của bạn được kiểm | Chưa nhận | Chưa nhận | Chưa nhận | Chưa nhận | Chưa nhận |

Điểm gần xe nhất của R1 hiện dừng tại y≈675.4, nên hàng 720/680 không có giao điểm. Nếu cắt thêm 40 px ở đầu gần xe, hàng 640 cũng mất giao điểm; hàng 600/560 vẫn nằm trong miền y. Nếu cắt đầu xa xe thì kết quả khác, nên tôi cần nêu rõ đầu bị cắt.

Tôi chưa tính được độ lệch hai người tại 720/560 do chưa có dữ liệu bạn. Sai số gần xe có ý nghĩa trực tiếp với vị trí làn ngay trước xe. Đảo thứ tự đỉnh không đổi giao điểm hình học x tại y, nhưng vi phạm chiều gần ra xa và bị lint phát hiện; xử lý phụ thuộc thứ tự đỉnh cần quy ước thống nhất.
