## 1. Thiết lập bài toán
- **Phương trình tia sáng (Ray):** 
  $$\vec{r}(t) = \mathbf{o} + t\vec{d} \quad (t \ge 0)$$
  - $\mathbf{o} = (o_x, o_y, o_z)$: Gốc của tia (Ray Origin)
  - $\vec{d} = (d_x, d_y, d_z)$: Vector hướng (Ray Direction, giả định đã chuẩn hóa $|\vec{d}| = 1$)

- **Phương trình mặt cầu (Sphere):** 
  $$|\mathbf{p} - \mathbf{c}|^2 = R^2 \iff (\mathbf{p} - \mathbf{c}) \cdot (\mathbf{p} - \mathbf{c}) = R^2$$
  - $\mathbf{c} = (c_x, c_y, c_z)$: Tâm mặt cầu (Center)
  - $R$: Bán kính mặt cầu (Radius)

---

## 2. Thiết lập phương trình bậc hai
Thay $\mathbf{p} = \vec{r}(t) = \mathbf{o} + t\vec{d}$ vào phương trình mặt cầu:

$$(\mathbf{o} + t\vec{d} - \mathbf{c}) \cdot (\mathbf{o} + t\vec{d} - \mathbf{c}) = R^2$$

Đặt $\vec{oc} = \mathbf{o} - \mathbf{c}$ (vector từ tâm đến gốc tia), phương trình trở thành:

$$(t\vec{d} + \vec{oc}) \cdot (t\vec{d} + \vec{oc}) = R^2$$
$$t^2(\vec{d} \cdot \vec{d}) + 2t(\vec{d} \cdot \vec{oc}) + (\vec{oc} \cdot \vec{oc}) - R^2 = 0$$

Phương trình có dạng chuẩn: 
$$A t^2 + 2B' t + C = 0$$

Trong đó:
- $A = \vec{d} \cdot \vec{d} = |\vec{d}|^2$ *(nếu $\vec{d}$ đã chuẩn hóa thì $A = 1$)*
- $B' = \vec{d} \cdot \vec{oc} = \vec{d} \cdot (\mathbf{o} - \mathbf{c})$
- $C = \vec{oc} \cdot \vec{oc} - R^2 = |\mathbf{o} - \mathbf{c}|^2 - R^2$

---

## 3. Biện luận nghiệm qua biệt thức $\Delta'$

Biệt thức thu gọn:
$$\Delta' = (B')^2 - A \cdot C$$

- **Trường hợp 1: $\Delta' < 0$**
  - Tia sáng không cắt mặt cầu (No Hit).
- **Trường hợp 2: $\Delta' = 0$**
  - Tia sáng tiếp xúc mặt cầu tại 1 điểm duy nhất: $t = -\frac{B'}{A}$.
- **Trường hợp 3: $\Delta' > 0$**
  - Phương trình cho hai nghiệm $t_1, t_2$ trên đường thẳng:
    $$t_1 = \frac{-B' - \sqrt{\Delta'}}{A}, \quad t_2 = \frac{-B' + \sqrt{\Delta'}}{A} \quad (t_1 < t_2)$$

---

## 4. Thuật toán xác định $t_{\min}$ (Điểm va chạm đầu tiên)

Vì tia sáng chỉ truyền theo chiều $t \ge 0$ (hoặc xét ngưỡng tránh lỗi tự giao cắt $t \in [t_{\min\_bound}, t_{\max\_bound}]$ với $t_{\min\_bound} = 10^{-4}$):

1. **Nếu $t_1 > 0$:**
   - Điểm phát sáng nằm **bên ngoài** mặt cầu và hướng vào mặt cầu.
   - $$t_{\min} = t_1$$
2. **Nếu $t_1 \le 0$ và $t_2 > 0$:**
   - Điểm phát sáng nằm **bên trong** mặt cầu (hoặc $t_1$ nằm phía sau nguồn).
   - $$t_{\min} = t_2$$
3. **Nếu $t_2 \le 0$:**
   - Toàn bộ mặt cầu nằm **phía sau** gốc tia sáng $\implies$ Không có giao điểm hợp lệ.

---

## 5. Xác định tọa độ va chạm và Pháp tuyến bề mặt

Khi tìm được $t_{\min}$:

- **Tọa độ điểm giao cắt (Hit Point):**
  $$\mathbf{P}_{\text{hit}} = \mathbf{o} + t_{\min}\vec{d}$$

- **Vector pháp tuyến đơn vị hướng ra ngoài (Outward Normal Vector):**
  $$\hat{N} = \frac{\mathbf{P}_{\text{hit}} - \mathbf{c}}{R}$$