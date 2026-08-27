## 1. Bản chất hiện tượng Ray Acne (Shadow / Surface Acne)
- **Nguyên nhân:** Do giới hạn biểu diễn số thực dấu phẩy động theo chuẩn **IEEE-754** (`float32` hoặc `float64`), tọa độ điểm giao cắt $\mathbf{P}_{\text{hit}}$ tính được từ phương trình $\mathbf{P}_{\text{hit}} = \mathbf{o} + t\vec{d}$ không nằm chính xác tuyệt đối trên bề mặt lý thuyết mà bị lệch nhẹ (có thể nằm thụt vào bên trong bề mặt).
- **Hệ quả:** Khi bắn tiếp tia thứ cấp (Shadow Ray, Reflection Ray), tia này xuất phát từ $\mathbf{P}_{\text{hit}}$ và va chạm ngay với chính bề mặt đó tại $t \approx 0^+$, sinh ra các đốm đen/nhiễu hạt trên bề mặt vật thể (Ray Acne).

---

## 2. Kỹ thuật 1: Dịch chuyển gốc tia theo Pháp tuyến (Normal Offset)
Dịch chuyển điểm xuất phát của tia mới ra ngoài bề mặt một khoảng vô cùng nhỏ $\epsilon$ dọc theo vector pháp tuyến đơn vị $\hat{n}$.

### Công thức tổng quát:
$$\mathbf{P}_{\text{new}} = \mathbf{P}_{\text{hit}} \pm \epsilon \hat{n}$$

- **Tia phản xạ / Tia chiếu sáng (Shadow & Reflection Ray):**
  Tia đi ra khỏi bề mặt ($\vec{d}_{\text{new}} \cdot \hat{n} > 0$):
  $$\mathbf{P}_{\text{origin}} = \mathbf{P}_{\text{hit}} + \epsilon \hat{n}$$

- **Tia khúc xạ (Transmission / Refraction Ray):**
  Tia đi xuyên vào trong vật thể ($\vec{d}_{\text{new}} \cdot \hat{n} < 0$):
  $$\mathbf{P}_{\text{origin}} = \mathbf{P}_{\text{hit}} - \epsilon \hat{n}$$

- **Dạng gộp tổng quát theo hướng tia mới $\vec{d}_{\text{new}}$:**
  $$\mathbf{P}_{\text{origin}} = \mathbf{P}_{\text{hit}} + \text{sign}(\vec{d}_{\text{new}} \cdot \hat{n}) \cdot \epsilon \hat{n}$$

---

## 3. Kỹ thuật 2: Kẹp ngưỡng tham số $t$ ($t_{\min}$ Clamping)
Thay vì dịch chuyển điểm $\mathbf{P}_{\text{hit}}$, giữ nguyên gốc tia nhưng chỉ chấp nhận các nghiệm giao điểm $t$ nằm ngoài vùng nhiễu cận 0:

$$t \in [t_{\min}, t_{\max}] \quad \text{với } t_{\min} = \epsilon \quad (\text{thường chọn } \epsilon = 10^{-4} \text{ đến } 10^{-3})$$

- Bỏ qua mọi giao điểm có $t < t_{\min}$.

---

## 4. Kỹ thuật nâng cao: Adaptive Epsilon (Chống trôi sai số theo tỷ lệ)
Hằng số $\epsilon$ cố định sẽ thất bại nếu vật thể quá lớn (tọa độ $|\mathbf{P}| \gg 10^4$) hoặc quá nhỏ ($|\mathbf{P}| \ll 10^{-4}$). Cần co giãn $\epsilon$ theo độ lớn tọa độ điểm va chạm.

### Công thức Adaptive Epsilon:
$$\epsilon_{\text{adaptive}} = \epsilon_{\text{base}} \cdot \max(1.0, \|\mathbf{P}_{\text{hit}}\|_{\infty})$$

Trong đó:
- $\|\mathbf{P}_{\text{hit}}\|_{\infty} = \max(|P_x|, |P_y|, |P_z|)$: Chuẩn cực đại của tọa độ điểm va chạm.
- $\epsilon_{\text{base}}$: Sai số cơ sở của kiểu dữ liệu (với `float32` lấy $\approx 10^{-4} \sim 10^{-5}$, với `float64` lấy $\approx 10^{-7}$).