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
- Dữ liệu EEG nằm ở các kênh từ $4$ đến $17$
- Một số kênh không sử dụng như: GYROX, GYROY, TIMESTAMP, MARKER...

---

## 2. Mục tiêu

- Tích lũy kiến thức chuyên sâu về tín hiệu EEG.
- Nắm quy trình xử lý tín hiệu não sóng phức tạp.
- Phân loại trạng thái tinh thần (Focus, Unfocus, Drowsy) bằng các mô hình máy học.

---

## 3) Quy trình

**Dữ liệu:**  
https://www.kaggle.com/datasets/inancigdem/eeg-data-for-mental-attention-state-detection

---
<img width="1833" height="575" alt="image" src="https://github.com/user-attachments/assets/ed6ea015-ccf9-4f3b-9b23-45ccc0fb69cb" />



### Bước 1: Tải dữ liệu
- Tải dữ liệu từ link trên.

### Bước 2: Tiền xử lý dữ liệu
- Chọn dữ liệu EEG từ các kênh 4 đến 17.
- Loại bỏ các kênh không cần thiết như GYROX, TIMESTAMP, MARKER, v.v.
- Loại bỏ các tần số nhiễu bằng Band pass và Notch.

### Bước 3: Biến đổi tín hiệu
- Áp dụng Short-Time Fourier Transform (STFT).
- Chuyển tín hiệu từ miền thời gian sang miền tần số:
### Bước 4: Tính năng lượng từng băng tần
- Tính tổng năng lượng trên từng băng tần (Delta, Theta, Alpha, Beta...)
### Bước 5: Làm mượt tín hiệu (trung bình trượt)
- Tính trung bình năng lượng theo thời gian
### Bước 6: Phân loại trạng thái tinh thần
- Đưa đặc trưng năng lượng vào mô hình phân loại (Random Forest, SVM, CNN).
- Phân loại 3 trạng thái: Focus, Unfocus, Drowsy.

## 4. Triển khai mô hình.
### 4.1 SVM:
<img width="614" height="554" alt="image" src="https://github.com/user-attachments/assets/fe0ab39e-6025-4bdf-9f69-f21a2faea3b9" />
### 4.2 Random Forest: 
<img width="595" height="560" alt="image" src="https://github.com/user-attachments/assets/dba42b17-062b-4a6e-b60d-b824b4875bca" />
### 4.3 CNN:
<img width="527" height="488" alt="image" src="https://github.com/user-attachments/assets/b8c43909-492c-40de-914a-489cc5df1389" />

## 5) Kết luận

### Nội dung nghiên cứu:
- Phát triển EEG BCI thụ động để theo dõi và phân loại ba trạng thái tinh thần: chú ý thụ động, thảnh thơi, và buồn ngủ.
- Sử dụng mô hình SVM đạt kết quả phân loại:
  - Tốt nhất: **98.93%**
  - Trung bình: **97.13%**

### Ứng dụng tiềm năng:
- **An toàn người lái xe:** Phát hiện trạng thái không tập trung hoặc buồn ngủ để cảnh báo.
- **Ứng dụng lâm sàng:** Theo dõi trạng thái tinh thần bệnh nhân, mở rộng theo dõi độ sâu gây mê dựa trên EEG.
- **Khái quát hóa:** Cơ sở phát triển hệ thống giám sát trạng thái tinh thần trong nhiều lĩnh vực (an ninh, y tế...).

### Ý nghĩa đặc biệt:
- Phương pháp phân tích tín hiệu EEG cung cấp cái nhìn mới về biểu diễn trạng thái tinh thần.
- Tiềm năng ứng dụng thực tiễn trong an toàn và giám sát sức khỏe.

---

## 6) Tài liệu tham khảo

- [Distinguishing mental attention states of humans via an EEG-based passive BCI using Machine Learning Methods](https://www.researchgate.net/publication/333499959_Distinguishing_mental_attention_states_of_humans_via_an_EEG-based_passive_BCI_using_Machine_Learning_Methods)


