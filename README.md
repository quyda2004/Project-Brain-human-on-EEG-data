# EEG Mental Attention State Classification

## 1. Tổng quan

**Chủ đề:** Phân loại trạng thái chú ý tinh thần bằng dữ liệu EEG.

**Nguồn dữ liệu:**  
[EEG Data for Mental Attention State Detection](https://www.kaggle.com/datasets/inancigdem/eeg-data-for-mental-attention-state-detection/data)

**Mô tả dữ liệu:**  
- Dữ liệu EEG được thu thập trong 25 giờ từ 5 người tham gia.
- Thí nghiệm: Mỗi người điều khiển tàu mô phỏng bằng "Microsoft Train Simulator" trong 35-55 phút.
- Ba trạng thái tinh thần:
  - **Tập trung (Focus):** Giám sát tàu một cách thụ động.
  - **Mất tập trung (Unfocus):** Tỉnh táo nhưng không chú ý.
  - **Buồn ngủ (Drowsy):** Dễ nhận thấy qua EEG (tăng dải alpha) hoặc dấu hiệu sinh lý.

**Quy trình thí nghiệm:**

| Giai đoạn      | Thời gian (phút) | Mô tả                    |
|----------------|------------------|---------------------------|
| Tập trung      | 10               | Theo dõi và điều khiển    |
| Mất tập trung  | 10               | Ngừng điều khiển, tỉnh táo|
| Buồn ngủ       | 10               | Thư giãn, dễ ngủ gật      |

- Thí nghiệm được thực hiện từ 7-9 giờ tối.
- Mỗi người tham gia: 7 thí nghiệm (2 làm quen, 5 chính thức).

**Thiết bị EEG:**
- Tai nghe Epoc EEG (chỉnh sửa).
- **12 kênh EEG** (vị trí F3, F4, Fz, C3, C4, Cz, Pz, F7, F8, FC5, FC6, AF3, AF4).
- Tốc độ lấy mẫu: $128 \text{ Hz}$
- Độ phân giải: $0.51 \, \mu V$
- Băng thông: $0.2 - 43 \, \text{Hz}$

**Cấu trúc dữ liệu:**
- Dữ liệu thô: Ma trận có kích thước $\{ \text{số mẫu} \} \times 25$.
- Dữ liệu EEG nằm ở các kênh từ $4$ đến $17$:
  $$
  \text{EEG channels} = o.data(:, 4:17)
  $$
- Một số kênh không sử dụng như: GYROX, GYROY, TIMESTAMP, MARKER...

---

## 2. Mục tiêu

- Tích lũy kiến thức chuyên sâu về tín hiệu EEG.
- Nắm quy trình xử lý tín hiệu não sóng phức tạp.
- Phân loại trạng thái tinh thần (Focus, Unfocus, Drowsy) bằng các mô hình máy học.

---



