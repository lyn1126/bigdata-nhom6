# Ứng dụng Big Data để phân tích phân khúc khách hàng và dự báo rủi ro giao hàng trễ trên sàn thương mại điện tử Olist (Brazil)

Đồ án cuối kỳ học phần Big Data – Nhóm 6.

- **Dữ liệu:** [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce) (Kaggle, giấy phép CC BY-NC-SA 4.0), khoảng 100.000 đơn hàng, giai đoạn 2016–2018.
- **Nội dung chính:** lưu trữ và truy vấn dữ liệu trên MongoDB, làm sạch và khám phá dữ liệu, phân khúc khách hàng bằng RFM + K-means, dự báo đơn giao trễ bằng học máy (CatBoost, XGBoost, LightGBM, Gradient Boosting...).
- **Báo cáo:** xem thư mục [`report/`](report/).

## Cấu trúc thư mục

```
├── README.md
├── data/
│   └── olist_clean.csv          # dữ liệu cấp đơn hàng sau khi làm sạch (do notebook 02 tạo ra)
├── notebooks/
│   ├── 01_kiem_tra_du_lieu.ipynb
│   ├── 02_eda.ipynb
│   ├── 03_rfm_k-means.ipynb
│   ├── 04_hoc_may.ipynb
│   ├── 05_import_mongodb.ipynb
│   └── 06_truy_van_mongodb.ipynb
├── results/                      # hình và bảng kết quả (02_eda, 03_rfm, 04_model)
└── report/                       # báo cáo Word/PDF
```


## Thứ tự chạy

Bấm vào nút để mở trực tiếp trên Google Colab.

| Bước | Notebook | Mục đích | Mở trên Colab |
|---|---|---|---|
| 1 | `01_kiem_tra_du_lieu` | Kiểm tra chất lượng ban đầu của 9 bảng dữ liệu | [![Open](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lyn1126/bigdata-nhom6/blob/main/notebooks/01_kiem_tra_du_lieu.ipynb) |
| 2 | `02_eda` | Làm sạch, tạo biến dẫn xuất, phân tích khám phá, xuất `olist_clean.csv` | [![Open](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lyn1126/bigdata-nhom6/blob/main/notebooks/02_eda.ipynb) |
| 3 | `03_rfm_k-means` | Phân khúc khách hàng RFM + K-means | [![Open](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lyn1126/bigdata-nhom6/blob/main/notebooks/03_rfm_k-means.ipynb) |
| 4 | `04_hoc_may` | Dự báo rủi ro giao hàng trễ, temporal backtesting, Future Test | [![Open](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lyn1126/bigdata-nhom6/blob/main/notebooks/04_hoc_may.ipynb) |
| 5 | `05_import_mongodb` | Nạp dữ liệu vào MongoDB Atlas (6 collection) | [![Open](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lyn1126/bigdata-nhom6/blob/main/notebooks/05_import_mongodb.ipynb) |
| 6 | `06_truy_van_mongodb` | CRUD và Aggregation Pipeline trên MongoDB | [![Open](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/lyn1126/bigdata-nhom6/blob/main/notebooks/06_truy_van_mongodb.ipynb) |

Các bước 3 và 4 độc lập với nhau, chỉ cần có `olist_clean.csv` (từ bước 2). Nhánh MongoDB (bước 5–6) chạy riêng, không ảnh hưởng đến bước 1–4.

## Cách chạy

1. Mở notebook bằng nút Colab ở trên → **Runtime → Run all**.
2. Bước 1, 2, 5 tự tải dữ liệu gốc từ Kaggle bằng `kagglehub` (không cần tài khoản Kaggle với bộ dữ liệu công khai).
3. Bước 3, 4 tự tải `olist_clean.csv` từ repo này (biến `CLEAN_URL` ở ô đầu). Nếu không tải được, Colab sẽ hiện hộp chọn tệp: hãy chọn file `data/olist_clean.csv` đã tải về máy.
4. Kết quả (hình, bảng) được ghi vào thư mục `./outputs/` của phiên Colab. Ô cuối mỗi notebook cho phép nén kết quả để tải về.

## Lưu ý về MongoDB (bước 5–6)

- Hai notebook này kết nối đến **cluster MongoDB Atlas của nhóm**; chuỗi kết nối (có mật khẩu) được nhập qua hộp mật khẩu khi chạy và **không được lưu trong notebook**.
- Người ngoài nhóm cần được cấp tài khoản chỉ đọc và địa chỉ IP phải được cho phép trong Atlas (Network Access). Nếu không thể kết nối, kết quả đã chạy sẵn vẫn xem được trong notebook và trong báo cáo (Chương 3).

## Ghi chú

- Ô "đẩy kết quả lên GitHub" ở cuối các notebook mặc định **tắt** (`PUSH_TO_GITHUB = False`); chỉ bật khi nhóm tự cập nhật repo.
- Thời gian chạy `04_hoc_may` khá lâu (tinh chỉnh tham số và temporal backtesting). Có thể đặt `QUICK_MODE = True` để chạy rút gọn khi chỉ kiểm tra code (kết quả không dùng cho báo cáo).
- Kết quả chỉ phản ánh dữ liệu thương mại điện tử Brazil giai đoạn 2016–2018.

## Thành viên nhóm

| Họ và tên | MSSV | Nhiệm vụ |
|Lê Yến Ngân|24126144|Import và truy vấn MongoDB, Khám phá và làm sạch dữ liệu (EDA), phân tích phân khúc khách hàng bằng RFM và K-means, Xây dựng và triển khai mô học máy, Chương 5, Tổng hợp word.|
|Hà Kiều Khanh|24126095|Chương 1, Import Mongodb, Dashboard Báo cáo hiệu suất giao hàng và phân tích rủi ro, Chương 6.|
|Nguyễn Đào Thanh Ngân|24126145|Chương 2, Truy vấn Mongodb, Dashboard Phân khúc khách hàng bằng RFM và K-means trên Power BI, Chương 6, Chương 7|
|Nguyễn Thị Kim Ngân|24126146|Chương 3 Mô tả dữ liệu, Phân tích phân khúc khách hàng bằng RFM và K-means,  Dashboard Báo cáo hiệu suất giao hàng và phân tích rủi ro, Chương 7.|
|Nguyễn Thị Thanh Giang|24126049|Chương 3, Phân tích và khám phá dữ liệu (EDA), Dashboard Kết quả machine learning và đánh giá khách hàng, Chương 6|
