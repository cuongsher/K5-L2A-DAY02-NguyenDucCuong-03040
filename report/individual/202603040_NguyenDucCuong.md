# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên: Nguyen Duc Cuong
- MSSV:2A202603040
- Email: cuongsher@gmail.com
- Lớp:2A
- Link repo bài làm: https://github.com/cuongsher/K5-L2A-DAY02-NguyenDucCuong-03040.git
- Link Colab đã chạy: https://colab.research.google.com/drive/1SAn2W3NwjtNC9KxDrbJlak_s3iwglZhB?usp=sharing

## 2. Schema và mini guideline

Dẫn tới [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt ba ca mơ hồ đã quyết định, cách áp dụng schema và phần cần giảng viên làm rõ.

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý:
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: 
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: 
- Commit khóa nhãn ban đầu:

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 459 | |
| FP | 611 | |
| FN | 194 | |
| Precision | 0.429 | |
| Recall | 0.7029 | |
| F1 | 0.5328 | |
| mean_iou_of_matches | 0.8426 | |
| passed | false | |

khong rework (lab coach bao f1 >0.5 , mean_iou >0.8 la dat )

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch:
  Runtime: Linux-6.6.159+-x86_64-with-glibc2.39
  GPU/CPU: Tesla T4
  Ultralytics: 8.4.208
  Torch: 2.14.1+cu130

- Các tham số thay đổi so với notebook nếu có và lý do:
  Không thay đổi các tham số huấn luyện so với notebook gốc. Giữ nguyên cấu hình:
  Model: yolo26n.pt
  Epochs: 50
  Image size: 640
  Batch size: -1 (tự động điều chỉnh)
  Device: GPU nếu có, nếu không sử dụng CPU.
  Seed: 20260909.

- Đường dẫn best checkpoint trong phiên chạy:

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision |0.4105453698519763 |
| Recall |0.23026854853628678 |
| mAP50 | 0.27225886498171903|
| mAP50–95 | 0.20168300309748077|

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
   
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
   Cần kiểm tra độ chính xác của bounding box. Có thể box chưa ôm sát vật thể, bị lệch, quá rộng hoặc quá hẹp.

   mAP50 chỉ yêu cầu IoU đạt ngưỡng 0.5, trong khi mAP50–95 đánh giá ở nhiều ngưỡng IoU khắt khe hơn. Vì vậy, cần cải thiện vị trí và kích thước bounding box.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
   
   Các lỗi nhầm lẫn giữa car và van, hoặc giữa truck và van, có thể liên quan đến quy tắc phân biệt các lớp trong guideline.

   Nguyên nhân có thể do đặc điểm hình dáng của phương tiện tương đối giống nhau, dẫn đến việc gán nhãn chưa thống nhất.

   Dữ kiện cần kiểm tra: Confusion Matrix và các ảnh dự đoán có trường hợp mô hình nhận diện nhầm class.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
   
   Không sử dụng 10 ảnh Eval để train vì mục đích là đánh giá khách quan khả năng nhận diện của mô hình trên dữ liệu chưa được dùng để huấn luyện.

  Các ảnh này được sử dụng để kiểm tra khả năng tổng quát hóa của mô hình, đánh giá kết quả dự đoán và phát hiện các lỗi như bỏ sót vật thể, nhầm class hoặc bounding box chưa chính xác.

   Thông qua kết quả Eval, có thể xác định những điểm cần cải thiện cho mô hình trong các lần huấn luyện tiếp theo.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| | | | |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md): phần nào đã có kết quả, phần nào còn thiếu hoặc chưa kiểm được. Không tự nhận hoàn thành bước chưa chạy.

phan 3 Annotation và self-QC chua hoan thanh
## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.

su dung chatgpt de soat loi upgit + tim cach up git
chat gpt de kiem tra thong so o phan 5