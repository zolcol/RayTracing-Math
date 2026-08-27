
> [!abstract] Định nghĩa
> Công thức Cramer là phương pháp đại số tuyến tính dùng định thức (determinant) để tìm nghiệm giải tích tường minh của hệ phương trình đại số tuyến tính có số phương trình bằng số ẩn ($n \times n$).

---

## 1. Dạng Tổng Quát & Điều Kiện Áp Dụng

Cho hệ $n$ phương trình tuyến tính $n$ ẩn dưới dạng ma trận:

$$A\mathbf{x} = \mathbf{b} \iff \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n1} & a_{n2} & \cdots & a_{nn} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} = \begin{bmatrix} b_1 \\ b_2 \\ \vdots \\ b_n \end{bmatrix}$$

- **Điều kiện cần và đủ để có nghiệm duy nhất:** Ma trận hệ số $A$ là ma trận vuông và khả nghịch:
  $$D = \det(A) \neq 0$$

- **Công thức nghiệm:**
  $$x_i = \frac{D_i}{D} = \frac{\det(A_i)}{\det(A)} \quad (\forall i = 1, 2, \dots, n)$$
  *Trong đó:* $A_i$ (hoặc $D_i$) là ma trận thu được khi thay thế cột thứ $i$ của ma trận $A$ bằng vector cột vế phải $\mathbf{b}$.

---

## 2. Chứng Minh Súc Tích

1. Khi $\det(A) \neq 0$, ma trận nghịch đảo $A^{-1}$ tồn tại và được biểu diễn qua ma trận phụ hợp $\operatorname{adj}(A)$:
   $$A^{-1} = \frac{1}{\det(A)} \operatorname{adj}(A)$$

2. Nhân hai vế phương trình $A\mathbf{x} = \mathbf{b}$ với $A^{-1}$:
   $$\mathbf{x} = A^{-1}\mathbf{b} = \frac{1}{\det(A)} \operatorname{adj}(A)\mathbf{b}$$

3. Khai triển phần tử thứ $i$ của vector nghiệm $\mathbf{x}$:
   $$x_i = \frac{1}{\det(A)} \sum_{j=1}^n (\operatorname{adj}(A))_{ij} b_j = \frac{1}{\det(A)} \sum_{j=1}^n C_{ji} b_j$$
   *(với $C_{ji}$ là phần bù đại số của phần tử $a_{ji}$ trong ma trận $A$)*.

4. Theo **định lý khai triển Laplace**, tổng $\sum_{j=1}^n b_j C_{ji}$ chính là định thức của ma trận $A$ khi thay thế cột thứ $i$ bằng vector $\mathbf{b}$ (tức $\det(A_i)$).

$$\Rightarrow x_i = \frac{\det(A_i)}{\det(A)} = \frac{D_i}{D} \quad \blacksquare$$

---

## 3. Ví Dụ Minh Họa Chi Tiết

Giải hệ phương trình:
$$\begin{cases} x + 2y + z = 4 \\ 3x - y + 2z = 7 \\ 2x + 3y - z = 1 \end{cases}$$

### Bước 1: Tính định thức ma trận hệ số $D$
$$D = \begin{vmatrix} 1 & 2 & 1 \\ 3 & -1 & 2 \\ 2 & 3 & -1 \end{vmatrix} = 1(1 - 6) - 2(-3 - 4) + 1(9 + 2) = -5 + 14 + 11 = 20 \neq 0$$
*(Vì $D = 20 \neq 0$, hệ có nghiệm duy nhất)*.

### Bước 2: Tính các định thức thành phần $D_x, D_y, D_z$
- **Thay cột 1 bằng vế phải $\begin{bmatrix} 4 & 7 & 1 \end{bmatrix}^T$:**
  $$D_x = \begin{vmatrix} \mathbf{4} & 2 & 1 \\ \mathbf{7} & -1 & 2 \\ \mathbf{1} & 3 & -1 \end{vmatrix} = 4(1 - 6) - 2(-7 - 2) + 1(21 + 1) = -20 + 18 + 22 = 20$$

- **Thay cột 2 bằng vế phải $\begin{bmatrix} 4 & 7 & 1 \end{bmatrix}^T$:**
  $$D_y = \begin{vmatrix} 1 & \mathbf{4} & 1 \\ 3 & \mathbf{7} & 2 \\ 2 & \mathbf{1} & -1 \end{vmatrix} = 1(-7 - 2) - 4(-3 - 4) + 1(3 - 14) = -9 + 28 - 11 = 8$$

- **Thay cột 3 bằng vế phải $\begin{bmatrix} 4 & 7 & 1 \end{bmatrix}^T$:**
  $$D_z = \begin{vmatrix} 1 & 2 & \mathbf{4} \\ 3 & -1 & \mathbf{7} \\ 2 & 3 & \mathbf{1} \end{vmatrix} = 1(-1 - 21) - 2(3 - 14) + 4(9 + 2) = -22 + 22 + 44 = 44$$

### Bước 3: Kết luận nghiệm
$$x = \frac{D_x}{D} = \frac{20}{20} = 1$$
$$y = \frac{D_y}{D} = \frac{8}{20} = \frac{2}{5} = 0.4$$
$$z = \frac{D_z}{D} = \frac{44}{20} = \frac{11}{5} = 2.2$$

---

## 4. Biện Luận & Đánh Giá

| Trường hợp | Trạng thái nghiệm | Hướng xử lý |
| :--- | :--- | :--- |
| **$D \neq 0$** | Hệ có **nghiệm duy nhất**: $x_i = \frac{D_i}{D}$ | Áp dụng công thức Cramer. |
| **$D = 0$ và $\exists D_i \neq 0$** | Hệ **vô nghiệm** | Dừng tính toán. |
| **$D = 0$ và $\forall D_i = 0$** | Hệ **vô số nghiệm** hoặc **vô nghiệm** | Chuyển sang **phương pháp khử Gauss** để xác định hạng ma trận. |

> [!tip] Đánh giá thực tế
> - **Ưu điểm:** Cho phép giải độc lập từng ẩn riêng lẻ mà không cần giải toàn bộ hệ.
> - **Nhược điểm:** Độ phức tạp tính toán tăng theo cấp số giai thừa ($O((n+1)!)$), chỉ tối ưu cho hệ cấp nhỏ ($n \le 3$). Với hệ lớn hơn, phương pháp khử Gauss ($O(n^3)$) được ưu tiên tuyệt đối.