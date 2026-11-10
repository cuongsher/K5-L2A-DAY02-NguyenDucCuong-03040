# Mini guideline — bài làm cá nhân

> Điền nội dung này trước khi bắt đầu gán nhãn. Giữ lại các quyết định sau khi self-QC.

## Định nghĩa lớp

| Lớp | Định nghĩa của bạn | Ví dụ/điểm phân biệt |
| --- | --- | --- |
| `car` | Phương tiện ô tô chở người, có kích thước nhỏ hoặc trung bình. | Sedan, SUV, hatchback. |
| `truck` | Phương tiện chuyên dùng để chở hàng hóa. | Xe tải thùng, xe tải ben. |
| `bus` | Phương tiện chở nhiều hành khách. | Xe buýt, xe khách. |
| `van` | Xe chở người hoặc hàng hóa, có khoang thân xe kín và kích thước nhỏ hơn xe tải thông thường. | Minivan, xe van chở hàng. |


## Quy tắc chung

- Box bám sát vật thể nghĩa là: Vẽ bounding box bao quanh toàn bộ phần phương tiện nhìn thấy được, không lấy quá nhiều phần nền xung quanh.
- Vật thể bị che khuất: Vẫn gán nhãn nếu có thể nhận diện được loại phương tiện, box bao quanh phần nhìn thấy được.
- Vật thể bị cắt bởi rìa ảnh: Vẫn gán nhãn nếu nhận diện được phương tiện, box giới hạn trong phạm vi ảnh.
- Vật thể rất nhỏ/mơ hồ: Không gán nhãn nếu không thể xác định chính xác loại phương tiện.

## Ghi lại quyết định cho ít nhất ba ca mơ hồ

| Ảnh | Tình huống | Quyết định cuối | Lý do theo schema |
| --- | --- | --- | --- |
| `drive_008` | Xe ô tô bị che khuất một phần bởi phương tiện khác. | Gán nhãn `car`. | Vẫn nhận diện được loại xe và phần nhìn thấy đủ để vẽ box. |
| `drive_019` | Xe bus bị cắt một phần ở rìa ảnh. | Gán nhãn `bus`. | Phương tiện vẫn nhận diện được, box chỉ bao quanh phần nằm trong ảnh. |
| `drive_019` | Xe ở xa, kích thước nhỏ và khó phân biệt giữa car và van. | Không gán nhãn. | Không đủ thông tin để xác định chính xác class theo schema. |
