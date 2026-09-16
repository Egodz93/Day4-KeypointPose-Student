# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Phạm Văn Thân   Nhóm: G05   Ngày: 16/09/2026

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán |20 |
| Số skeleton |29 |
| v=2 / v=1 / v=0 |345/119/29 |
| Thời gian trung bình mỗi ảnh |7p |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1.left_ear: 59% - 17/29<br>
2.right_ear: 45% - 13/29<br>
3.left_wrist: 34% - 10/29<br>

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->
 Hai khớp tai có tỷ lệ v=1 cao nhất vì nhiều người quay nghiêng hoặc đội mũ bảo hiểm, khiến vị trí tai phải được ước lượng dù vẫn nằm trong ảnh. Cổ tay và hông cùng đạt 34%, cổ tay thường bị tay lái hoặc cơ thể che, còn hông vốn là vị trí giải phẫu phải suy ra qua quần áo. Vì vậy “hay bị che” và “khó xác định vị trí giải phẫu” là hai nguyên nhân khác nhau.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình |0.9384 |0.9395 |
| OKS@0.50 |0.9655 |1.0 |
| OKS@0.75 |0.9655 |1.0 |
| Lỗi `dao_trai_phai` |0 |0 |
| Lỗi `nham_nguoi` |1 |0 |
| Lỗi `xoa_khop_bi_che` |2 |0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

-train_13, bổ sung skeleton của người còn thiếu.
-train_10, người số 1, left_hip và right_hip: đổi từ v=0 thành v=1, đồng thời đặt chấm ước lượng vì hông còn trong ảnh nhưng bị che.
-train_04, người số 1, left_wrist: kéo điểm từ cơ thể người bên cạnh về đúng cánh tay của người đang gán.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->
Lỗi đảo trái phải xuất hiện ở train2. Ảnh đó khá khó khi người quay đầu dẫn đến khó xác định chính xác eye,nose,ear. Việc quay đầu khiến model nhận diện sai đó là lỗi đảo trái phải.
## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 |0.8450 |0.8450 |0.0000 |
| pose_mAP50-95 |0.6853 |0.6853 |0.0000 |
| pose_precision |0.9734 |0.9746 |+0.0012 |
| pose_recall |0.8462 |0.8462 |0.0000 |
| box_mAP50-95 |0.8119 |0.8054 |-0.0065 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?
pose_mAP50-95 thay đổi 0.0000. Không có giảm hay tăng đo được. Checkpoint tốt nhất xuất hiện ngay epoch 1, cho thấy 20 ảnh chưa tạo được cải thiện pose có thể đo trên tập test nhỏ này.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?
Sau fine-tune, box_mAP50-95 - pose_mAP50-95 = 0.8054 - 0.6853 = 0.1201. Model tìm vùng người dễ hơn định vị chính xác 17 khớp. Nếu so tại mAP50, chênh lệch là 0.9819 - 0.8450 = 0.1369.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
train_13 có OKS thấp nhất giữa model: 0.640. Nhãn của tôi đáng tin hơn trong trường hợp này vì gold ghép đủ cả ba người, không có lỗi nghiêm trọng, và OKS với gold lần lượt là 0.8064, 0.8709, 0.9554.
5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?
Có. train_13 vừa là ảnh có người tôi gán kém nhất so với gold (0.8064), vừa là ảnh model bất đồng nhiều nhất (0.640). Ảnh có ba người, một người rất nhỏ và các cơ thể bị chồng lấn, nên khó cho cả người gán và model.
## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->
Trong train_10, người số 1, left_hip không nhìn thấy rõ vì phần thân dưới bị quần áo và xe che. Tuy nhiên vị trí hông vẫn nằm trong khung và có thể ước lượng dựa trên trục thân, vai và hướng của chân. Vì vậy tôi vẫn đặt chấm tại vị trí giải phẫu ước lượng và chọn v=1, không dùng v=0. Lần chấm trước đã xác nhận việc để khớp này là v=0 làm mất điểm trực tiếp.