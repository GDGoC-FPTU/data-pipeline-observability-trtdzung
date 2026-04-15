[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23574089&assignment_repo_type=AssignmentRepo)

# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** tiendungtran2005@gmail.com
**Name:** Trần Tiến Dũng

---

## Mô tả

Trong bài lab này, tôi xây dựng một pipeline ETL đơn giản để xử lý dữ liệu từ file JSON và xuất kết quả ra CSV. Pipeline gồm 4 bước chính:

- `Extract`: đọc dữ liệu từ `raw_data.json`
- `Validate`: loại bỏ các bản ghi không hợp lệ như giá nhỏ hơn hoặc bằng `0`, hoặc `category` rỗng
- `Transform`: chuẩn hóa `category` về dạng Title Case, tính thêm `discounted_price` giảm 10%, và thêm thời gian xử lý `processed_at`
- `Load`: lưu dữ liệu đã xử lý vào file `processed_data.csv`

Ngoài ra, tôi cũng chạy thử nghiệm stress test với `agent_simulation.py` để so sánh phản hồi của agent khi dùng dữ liệu sạch và dữ liệu rác.

---

## Cách chạy

### Yêu cầu

```bash
pip install pandas
```

### Chạy ETL Pipeline

```bash
python solution.py
```

Kết quả sau khi chạy:

- Đọc dữ liệu từ `raw_data.json`
- Giữ lại `3` bản ghi hợp lệ
- Loại bỏ `2` bản ghi lỗi
- Tạo file `processed_data.csv`

### Chạy Stress Test cho Agent

Trước tiên tạo dữ liệu rác:

```bash
python generate_garbage.py
```

Sau đó chạy mô phỏng agent:

```bash
python agent_simulation.py
```

Kết quả thực tế:

- Với `processed_data.csv`, agent trả lời: `Laptop at $1200`
- Với `garbage_data.csv`, agent trả lời: `Nuclear Reactor at $999999`

Điều này cho thấy chất lượng dữ liệu ảnh hưởng trực tiếp đến chất lượng câu trả lời của agent.

---

## Cấu trúc thư mục

```text
├── solution.py            # Script ETL chính
├── raw_data.json          # Dữ liệu đầu vào
├── processed_data.csv     # Dữ liệu sau khi xử lý
├── generate_garbage.py    # Tạo dữ liệu rác để stress test
├── garbage_data.csv       # Dữ liệu rác phục vụ mô phỏng agent
├── agent_simulation.py    # Script mô phỏng phản hồi của agent
├── experiment_report.md   # Báo cáo kết quả thử nghiệm
├── STUDENT_GUIDE.md       # Hướng dẫn làm và nộp bài
└── README.md              # Mô tả dự án
```

---

## Kết quả

- Pipeline chạy thành công, không lỗi
- Dữ liệu đầu vào có `5` bản ghi
- Sau bước validation, còn `3` bản ghi hợp lệ
- `2` bản ghi bị loại do giá không hợp lệ hoặc `category` rỗng
- Dữ liệu đầu ra có thêm các cột `discounted_price` và `processed_at`
- Báo cáo thử nghiệm đã được điền trong `experiment_report.md`

---

## Nhận xét

Bài lab giúp làm rõ vai trò của ETL và Data Observability trong hệ thống AI. Khi dữ liệu được làm sạch trước khi đưa vào sử dụng, agent có thể phản hồi hợp lý hơn. Ngược lại, nếu dữ liệu chứa outlier, kiểu dữ liệu sai hoặc giá trị thiếu, agent rất dễ đưa ra kết quả sai lệch dù câu hỏi không thay đổi.
