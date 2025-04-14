<p align="center">
  <a href="https://www.uit.edu.vn/">
    <img src="https://i.imgur.com/WmMnSRt.png" alt="Trường Đại học CNTT" width="400">
  </a>
</p>

<h1 align="center"><b>CS317.P21 - PHÁT TRIỂN VÀ VẬN HÀNH HỆ THỐNG MÁY HỌC</b></h1>
<h2 align="center"><b>Lab 1 - Pipeline huấn luyện với experiment tracking</b></h2>

---

## Thông tin sinh viên
- **Họ tên**: Mai Văn Tân
- **MSSV**: 22521301

---

## Tổng quan dự án
**Bài toán**: Pipeline MLflow dự đoán giá nhà

### 🛠 Công nghệ sử dụng
| Thành phần         | Công dụng                               |
|--------------------|-----------------------------------------|
| Metaflow           | Quản lý workflow pipeline               |
| MLflow             | Tracking thí nghiệm và model management |
| Hyperopt           | Tối ưu siêu tham số                     |
| Scikit-learn       | Xây dựng và đánh giá model              |
| Vega-Lite          | Trực quan hóa dữ liệu trên Metaflow Card|

### Kiến trúc hệ thống
```plaintext
[Data Source] -> [Metaflow Pipeline] -> [MLflow Tracking] -> [Model Registry]
     │               │  │  │                    │
     └──[Preprocessing] │  └──[Hyperopt Tuning] │
                        └──[Training]───────────┘
```
### Workflow Pipeline
1. Start: Khởi tạo MLflow và thiết lập các model

2. Load Data: Đọc dữ liệu từ file CSV và log dataset lên MLflow

3. EDA: Phân tích dữ liệu với các biểu đồ:
- Phân phối giá nhà
- Tương quan giữa các features
- Biểu đồ phân bố các features
4. Preprocess: Tiền xử lý dữ liệu và chuẩn hóa
5. Hyperparameter Tuning: Tối ưu hyperparameter cho các model:
- Random Forest
- Gradient Boosting
- K-Nearest Neighbors
6. Train Final Models: Huấn luyện model cuối cùng với tham số tốt nhất
7. Evaluation: So sánh hiệu năng các model

### Demo
Xem tại: https://drive.google.com/file/d/1Xe3V-efY4fQkHRfx1XfsQAEGEkii9kUT/view?usp=drive_link

## Cài đặt
### Clone repository
```
git clone https://github.com/yourusername/housing-pipeline.git
cd housing-pipeline
```
### Thiết lập môi trường ảo
```
python -m venv .venv
source .venv/bin/activate  # Linux/MacOS
# hoặc
.\.venv\Scripts\activate  # Windows
```
### Cài đặt dependencies
```
pip install -r requirements.txt
```
### Khởi động MLflow Server (terminal mới)
```
mlflow server \
  --backend-store-uri sqlite:///mlflow.db \
  --default-artifact-root ./artifacts \
  --host 0.0.0.0 \
  --port 5000
```
### Thực thi pipeline
```
# Chạy toàn bộ pipeline
python src/housing_flow.py run
```
```
# Xem kết quả trên MLflow UI
http://localhost:5000
```
```
# Xem Metaflow Cards
python src/housing_flow.py card server
```

