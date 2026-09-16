# Mini guideline - nhóm: G05 |  người gán: Phạm Văn Thân  |  ngày: 16/09/2026

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Ước lượng từ trục thân, hai vai và hướng chân; nếu hông còn trong khung thì vẫn đặt chấm và chọn `v=1`, không xóa khớp. | ![Ví dụ hông bị che](assets/screenshots/Screenshot%202026-09-16%20144222.png) |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Nếu còn nhìn rõ tâm tai thì chọn `v=2`. Nếu không thấy rõ nhưng tai vẫn ở trong khung, ước lượng theo mắt và đường viền đầu rồi chọn `v=1`. | ![Ví dụ tai bị mũ che](assets/screenshots/Screenshot%202026-09-16%20104021.png) |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Vẫn tạo đủ 17 điểm. Điểm nhìn rõ dùng `v=2`, điểm bị che nhưng còn trong khung dùng `v=1`, chỉ các điểm thực sự nằm ngoài mép ảnh mới dùng `v=0`. | ![Ví dụ người bị cắt ở mép ảnh](assets/screenshots/Screenshot%202026-09-16%20144230.png) |
| Cổ tay nằm sau tay lái / sau thân mình | Lần theo vai → khuỷu tay → cẳng tay của đúng người, ước lượng vị trí cổ tay và chọn `v=1`; nếu nhìn rõ thì dùng `v=2`. | ![Ví dụ cổ tay sau tay lái](assets/screenshots/Screenshot%202026-09-16%20144222.png) |
| Hai người chồng lên nhau | Hoàn thành trọn vẹn từng người rồi mới sang người kế tiếp. Mỗi khớp phải lần theo chi của chính người đó; khớp bị người kia che nhưng còn trong khung dùng `v=1`. | ![Ví dụ hai người chồng lên nhau](assets/screenshots/Screenshot%202026-09-16%20144240.png) |
| Người nhỏ đến mức nào thì không gán nữa | Trong bộ 20 ảnh core không bỏ qua người chỉ vì họ nhỏ. Còn nhận ra được là người thì vẫn tạo đủ 17 điểm; điểm không rõ nhưng còn trong ảnh dùng `v=1`. | ![Ví dụ người nhỏ vẫn phải gán](assets/screenshots/Screenshot%202026-09-16%20140345.png) |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_4`, người thứ `1`, khớp `left_wrist`

- Mơ hồ ở chỗ nào: cổ tay ở gần người bên cạnh và xe.
- Bạn quyết thế nào: lần theo vai và khuỷu tay của chính người đó.
- Vì sao:  lần chấm đầu phát hiện điểm gần cổ tay của người khác.
- Nếu người khác quyết ngược lại thì model học sai cái gì: model học nối cánh tay sang cơ thể khác.

![Ca 1 - cổ tay ở gần người bên cạnh và xe](assets/screenshots/Screenshot%202026-09-16%20144230.png)

### Ca 2 - ảnh `train_10`, người thứ `1`, khớp `left_hip`

- Mơ hồ ở chỗ nào: hông bị che, không nhìn thấy bề mặt khớp.
- Bạn quyết thế nào: đặt điểm ước lượng và dùng v=1.
- Vì sao: hông vẫn nằm trong khung; gold xác nhận v=0 là xoá khớp bị che.
- Nếu người khác quyết ngược lại thì model học sai cái gì: model không được học vị trí hông trong các ca bị che.

![Ca 2 - hông bị che nhưng vẫn nằm trong khung](assets/screenshots/Screenshot%202026-09-16%20144222.png)

### Ca 3 - ảnh `train_13`, người thứ `3`, khớp ``

- Mơ hồ ở chỗ nào: người nhỏ, nhiều chi tiết khớp khó nhìn và gần các skeleton khác.
- Bạn quyết thế nào:  vẫn tạo đủ 17 điểm, hoàn thành riêng người đó rồi mới chuyển sang người kế tiếp.
- Vì sao: người vẫn có trong vật thể, chỉ là quá mờ
- Nếu người khác quyết ngược lại thì model học sai cái gì: model học bỏ sót người nhỏ hoặc gắn khớp sang người kế bên.

![Ca 3 - người nhỏ gần các skeleton khác](assets/screenshots/Screenshot%202026-09-16%20140345.png)

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `______` (bạn `___%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**:
- Luật mới bổ sung vào mục 2 sau khi thống nhất:
