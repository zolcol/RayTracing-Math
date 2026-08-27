

Tia sáng xuất phát từ điểm gốc $O(x_0, y_0, z_0)$ truyền theo vector hướng $\vec{d} = (d_x, d_y, d_z)$:

### 1. Dạng Vector
$$\vec{r}(t) = \mathbf{o} + t\vec{d} \quad (t \ge 0)$$

Trong đó:
- $\mathbf{o} = (x_0, y_0, z_0)$: Tọa độ điểm phát sáng (Ray Origin).
- $\vec{d} = (d_x, d_y, d_z)$: Vector chỉ hướng truyền sáng (Ray Direction).
- $t \in [0, +\infty)$: Tham số vô hướng đại diện cho bước truyền.

### 2. Dạng Hệ Tọa độ Tham số
$$\begin{cases} 
x(t) = x_0 + t \cdot d_x \\ 
y(t) = y_0 + t \cdot d_y \\ 
z(t) = z_0 + t \cdot d_z 
\end{cases} \quad (t \ge 0)$$

---

### 3. Các đặc tính quan trọng (Ứng dụng trong Ray Tracing / Quang học)
- **Ràng buộc chiều truyền:** Đường thẳng toán học có $t \in (-\infty, +\infty)$, nhưng tia sáng vật lý chỉ truyền theo một chiều từ nguồn nên điều kiện bắt buộc là **$t \ge 0$** (hoặc $t \in [t_{\min}, t_{\max}]$ với $t_{\min} > 0$ để tránh tự giao cắt).
- **Chuẩn hóa vector hướng:** Luôn ưu tiên chuẩn hóa $\vec{d}$ thành vector đơn vị ($|\vec{d}| = 1$):
  $$\hat{d} = \frac{\vec{d}}{|\vec{d}|} \implies \vec{r}(t) = \mathbf{o} + t\hat{d}$$
  Khi đó, **$t$ chính là khoảng cách hình học thực tế** từ điểm phát $\mathbf{o}$ tới điểm $\vec{r}(t)$.