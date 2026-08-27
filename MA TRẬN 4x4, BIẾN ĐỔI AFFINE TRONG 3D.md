	## 1. Đại số tuyến tính căn bản & Các phép toán ma trận

### 1.1. Định nghĩa Ma trận & Vector
* **Ma trận (Matrix):** Bảng số thực hình chữ nhật gồm $m$ hàng và $n$ cột ($m \times n$):
$$A = \begin{bmatrix} a_{11} & a_{12} & \cdots & a_{1n} \\ a_{21} & a_{22} & \cdots & a_{2n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{m1} & a_{m2} & \cdots & a_{mn} \end{bmatrix} \in \mathbb{R}^{m \times n}$$

* **Vector cột (Column Vector):** Chuẩn định dạng trong đồ họa 3D hiện đại ($n \times 1$):
$$\mathbf{v} = \begin{bmatrix} x \\ y \\ z \end{bmatrix} \in \mathbb{R}^{3 \times 1}$$

---

### 1.2. Các phép toán cốt lõi giữa hai ma trận

#### 1. Phép cộng và trừ hai ma trận ($A \pm B$)
* **Điều kiện:** Hai ma trận phải có **cùng kích thước** ($m \times n$).
* **Công thức:** Cộng/trừ từng phần tử tương ứng:
$$(A \pm B)_{ij} = a_{ij} \pm b_{ij}$$
* **Tính chất:**
  * Giao hoán: $A + B = B + A$
  * Kết hợp: $(A + B) + C = A + (B + C)$

> [!NOTE] Ví dụ: Cộng & Trừ hai ma trận $2 \times 2$
> Cho $A = \begin{bmatrix} 1 & 3 \\ 5 & 2 \end{bmatrix}$ và $B = \begin{bmatrix} 4 & 1 \\ 0 & 6 \end{bmatrix}$:
> $$A + B = \begin{bmatrix} 1+4 & 3+1 \\ 5+0 & 2+6 \end{bmatrix} = \begin{bmatrix} 5 & 4 \\ 5 & 8 \end{bmatrix}$$
> $$A - B = \begin{bmatrix} 1-4 & 3-1 \\ 5-0 & 2-6 \end{bmatrix} = \begin{bmatrix} -3 & 2 \\ 5 & -4 \end{bmatrix}$$

---

#### 2. Phép nhân ma trận với một số vô hướng ($k \cdot A$)
* **Công thức:** Nhân mọi phần tử trong ma trận với số thực $k$:
$$(k \cdot A)_{ij} = k \cdot a_{ij}$$

> [!NOTE] Ví dụ: Nhân ma trận với số vô hướng $k = 3$
> Cho $k = 3$ và $A = \begin{bmatrix} 2 & -1 \\ 0 & 4 \end{bmatrix}$:
> $$3A = \begin{bmatrix} 3 \cdot 2 & 3 \cdot (-1) \\ 3 \cdot 0 & 3 \cdot 4 \end{bmatrix} = \begin{bmatrix} 6 & -3 \\ 0 & 12 \end{bmatrix}$$

---

#### 3. Phép nhân hai ma trận ($C = A \cdot B$)
* **Điều kiện:** Số **cột** của ma trận $A$ phải bằng số **hàng** của ma trận $B$.
  $$\text{Nếu } A \in \mathbb{R}^{m \times k} \text{ và } B \in \mathbb{R}^{k \times n} \implies C = AB \in \mathbb{R}^{m \times n}$$
* **Công thức:** Phần tử $c_{ij}$ ở hàng $i$, cột $j$ là tích vô hướng của **hàng $i$ của $A$** với **cột $j$ của $B$**:
$$c_{ij} = \sum_{r=1}^{k} a_{ir} b_{rj} = a_{i1}b_{1j} + a_{i2}b_{2j} + \cdots + a_{ik}b_{kj}$$

> [!WARNING] Tính chất then chốt của phép nhân ma trận
> 1. **KHÔNG có tính giao hoán:** $A \cdot B \neq B \cdot A$ (Đổi thứ tự nhân sẽ làm biến đổi sai lệch hoàn toàn).
> 2. **Có tính kết hợp:** $(A \cdot B) \cdot C = A \cdot (B \cdot C)$ (Cho phép gộp nhiều ma trận liên tiếp thành 1 ma trận duy nhất).
> 3. **Có tính phân phối:** $A(B + C) = AB + AC$.

> [!NOTE] Ví dụ: Nhân hai ma trận $2 \times 2$
> Cho $A = \begin{bmatrix} 1 & 2 \\ 3 & 4 \end{bmatrix}$ và $B = \begin{bmatrix} 5 & 6 \\ 7 & 8 \end{bmatrix}$:
> $$C = A \cdot B = \begin{bmatrix} 1 \cdot 5 + 2 \cdot 7 & 1 \cdot 6 + 2 \cdot 8 \\ 3 \cdot 5 + 4 \cdot 7 & 3 \cdot 6 + 4 \cdot 8 \end{bmatrix} = \begin{bmatrix} 5 + 14 & 6 + 16 \\ 15 + 28 & 18 + 32 \end{bmatrix} = \begin{bmatrix} 19 & 22 \\ 43 & 50 \end{bmatrix}$$
> *(Nếu tính $B \cdot A$ kết quả sẽ là $\begin{bmatrix} 23 & 34 \\ 31 & 46 \end{bmatrix} \neq A \cdot B$)*

---

#### 4. Phép chuyển vị ma trận (Transpose - $A^T$)
* **Định nghĩa:** Đổi các hàng thành các cột tương ứng:
$$(A^T)_{ij} = a_{ji}$$
* **Tính chất:**
  * $(A^T)^T = A$
  * $(A + B)^T = A^T + B^T$
  * $(A \cdot B)^T = B^T \cdot A^T$ *(chú ý đảo thứ tự nhân)*

> [!NOTE] Ví dụ: Chuyển vị ma trận $2 \times 3$ sang $3 \times 2$
> $$A = \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \end{bmatrix} \implies A^T = \begin{bmatrix} 1 & 4 \\ 2 & 5 \\ 3 & 6 \end{bmatrix}$$

---

#### 5. Định thức của ma trận (Determinant - $\det(A)$ hay $|A|$)

* **Định nghĩa:** Định thức là một **giá trị vô hướng (scalar)** duy nhất được tính từ một **ma trận vuông** ($n \times n$). Nó phản ánh tính chất biến đổi hình học và cho biết ma trận đó có khả năng nghịch đảo hay không.

##### A. Nguyên lý & Ý nghĩa hình học
* **Hệ số co giãn không gian:**
  * **Trong 2D ($2 \times 2$):** $|\det(A)|$ là **diện tích** của hình bình hành tạo bởi 2 vector cột $\hat{\mathbf{i}}', \hat{\mathbf{j}}'$.
  * **Trong 3D ($3 \times 3$):** $|\det(A)|$ là **thể tích** của khối hộp hình bình hành (Parallelepiped) tạo bởi 3 vector cột $\hat{\mathbf{i}}', \hat{\mathbf{j}}', \hat{\mathbf{k}}'$ (chính là tích hỗn tạp $(\hat{\mathbf{i}}' \times \hat{\mathbf{j}}') \cdot \hat{\mathbf{k}}'$).
* **Ý nghĩa dấu của $\det(A)$:**
  * $\det(A) > 0$: Giữ nguyên định hướng hệ trục tọa độ (hệ tay phải vẫn là hệ tay phải).
  * $\det(A) < 0$: Đảo ngược định hướng không gian (phản chiếu gương - reflection, làm đảo thứ tự winding của tam giác trong render).
  * $\det(A) = 0$: Không gian bị ép bẹp (3D bị ép dẹp thành mặt phẳng hoặc đường thẳng) $\implies$ Ma trận bị **suy biến (Singular)**, làm mất thông tin $\implies$ **KHÔNG thể tìm được ma trận nghịch đảo**.

---

##### B. Công thức tính toán & Giải thích

###### 1. Ma trận cấp $2 \times 2$
* **Công thức:**
$$\det(A) = \begin{vmatrix} a & b \\ c & d \end{vmatrix} = ad - bc$$
* **Giải thích:** Tích đường chéo chính ($ad$) trừ đi tích đường chéo phụ ($bc$).

> [!NOTE] Ví dụ: Định thức $2 \times 2$
> Cho $A = \begin{bmatrix} 3 & 8 \\ 4 & 6 \end{bmatrix}$:
> $$\det(A) = (3 \cdot 6) - (8 \cdot 4) = 18 - 32 = -14$$
> *(Ý nghĩa: Biến đổi làm phóng to diện tích lên 14 lần và đảo ngược hướng không gian).*

---

###### 2. Ma trận cấp $3 \times 3$
Có 2 cách tính phổ biến:

* **Cách 1: Quy tắc Sarrus (Quy tắc đan chéo):**
$$\det(A) = \begin{vmatrix} a & b & c \\ d & e & f \\ g & h & i \end{vmatrix} = (aei + bfg + cdh) - (ceg + bdi + afh)$$

* **Cách 2: Khai triển Laplace (Cofactor Expansion theo hàng 1):**
$$\det(A) = a \begin{vmatrix} e & f \\ h & i \end{vmatrix} - b \begin{vmatrix} d & f \\ g & i \end{vmatrix} + c \begin{vmatrix} d & e \\ g & h \end{vmatrix} = a(ei - fh) - b(di - fg) + c(dh - eg)$$
*(Quy tắc dấu: đan xen $+ - +$).*

> [!NOTE] Ví dụ: Định thức $3 \times 3$
> Cho $A = \begin{bmatrix} 1 & 2 & 3 \\ 0 & 1 & 4 \\ 5 & 6 & 0 \end{bmatrix}$:
> Khai triển theo hàng 1:
> $$\det(A) = 1 \begin{vmatrix} 1 & 4 \\ 6 & 0 \end{vmatrix} - 2 \begin{vmatrix} 0 & 4 \\ 5 & 0 \end{vmatrix} + 3 \begin{vmatrix} 0 & 1 \\ 5 & 6 \end{vmatrix}$$
> $$\det(A) = 1(0 - 24) - 2(0 - 20) + 3(0 - 5) = -24 + 40 - 15 = 1$$
> *(Vì $\det(A) = 1 \neq 0 \implies$ Ma trận bảo toàn thể tích và có thể nghịch đảo).*

---

###### 3. Ma trận cấp tổng quát $n \times n$ (Khai triển Laplace)
$$\det(A) = \sum_{j=1}^{n} (-1)^{i+j} a_{ij} M_{ij}$$
* $M_{ij}$ (Minor): Định thức của ma trận con cấp $(n-1) \times (n-1)$ thu được khi xóa bỏ hàng $i$ và cột $j$.
* $C_{ij} = (-1)^{i+j} M_{ij}$ (Cofactor / Phần bù đại số).

> [!TIP] Ứng dụng trong Đồ họa & Ray Tracing với ma trận $4 \times 4$
> Ma trận Affine $4 \times 4$ luôn có hàng cuối cùng là $\begin{bmatrix} 0 & 0 & 0 & 1 \end{bmatrix}$. Khi khai triển Laplace theo hàng 4:
> $$\det(M_{4 \times 4}) = 0 \cdot C_{41} + 0 \cdot C_{42} + 0 \cdot C_{43} + 1 \cdot \det(M_{3 \times 3}) = \det(M_{3 \times 3})$$
> *(Định thức của ma trận Affine $4 \times 4$ chính bằng định thức của khối xoay & co giãn $3 \times 3$ bên trong nó).*

---

##### C. Bản chất toán học & Nguồn gốc công thức Laplace

###### 1. Tại sao lại là $a_{ij}$ nhân với định thức con $M_{ij}$? (Phân rã Thể tích)
Trong đồ họa 3D, định thức của ma trận $3 \times 3$ gồm 3 vector hàng $\mathbf{u}, \mathbf{v}, \mathbf{w}$ chính là **thể tích khối hộp** tạo bởi 3 vector đó:
$$\text{Thể tích} = \mathbf{u} \cdot (\mathbf{v} \times \mathbf{w}) = (\text{Chiều cao } \mathbf{u}) \times (\text{Diện tích mặt đáy tạo bởi } \mathbf{v}, \mathbf{w})$$

Nếu đặt $\mathbf{u} = (a, b, c)$, ta khai triển tích vô hướng:
$$\mathbf{u} \cdot (\mathbf{v} \times \mathbf{w}) = a(\mathbf{v} \times \mathbf{w})_x + b(\mathbf{v} \times \mathbf{w})_y + c(\mathbf{v} \times \mathbf{w})_z$$

Quan sát từng thành phần của tích có hướng (Cross product):
* $(\mathbf{v} \times \mathbf{w})_x = v_y w_z - v_z w_y = \begin{vmatrix} v_y & v_z \\ w_y & w_z \end{vmatrix} = M_{11}$ *(Diện tích hình chiếu đáy lên mặt phẳng YZ, chính là định thức con khi xóa hàng 1 cột 1 chứa $a$)*.
* $(\mathbf{v} \times \mathbf{w})_y = -(v_x w_z - v_z w_x) = -\begin{vmatrix} v_x & v_z \\ w_x & w_z \end{vmatrix} = -M_{12}$ *(Diện tích hình chiếu đáy lên mặt phẳng XZ, kèm dấu trừ quy tắc bàn tay phải)*.
* $(\mathbf{v} \times \mathbf{w})_z = v_x w_y - v_y w_x = \begin{vmatrix} v_x & v_y \\ w_x & w_y \end{vmatrix} = M_{13}$ *(Diện tích hình chiếu đáy lên mặt phẳng XY)*.

$$\implies \det(A) = a \cdot M_{11} - b \cdot M_{12} + c \cdot M_{13}$$
> **Bản chất:** Khai triển Laplace thực chất là phép chiếu không gian $n$ chiều xuống các mặt phẳng $(n-1)$ chiều: Lấy từng tọa độ thành phần nhân với diện tích đáy chiếu tương ứng.

###### 2. Nguồn gốc của dấu đan xen $(-1)^{i+j}$ (Tính phản xứng)
* Trong đại số tuyến tính, **mỗi khi hoán vị (đổi chỗ) 2 hàng hoặc 2 cột bất kỳ, hướng của không gian bị lật ngược (từ hệ tay phải sang hệ tay trái), làm định thức nhân với $-1$**.
* Để tính đóng góp của phần tử $a_{ij}$ ở hàng $i$, cột $j$:
  * Cần tráo đổi $i - 1$ lần để dời hàng $i$ lên hàng 1.
  * Cần tráo đổi $j - 1$ lần để dời cột $j$ sang cột 1.
  * Tổng số lần tráo đổi là $(i - 1) + (j - 1) = i + j - 2$.
* Vì mỗi lần tráo đổi tạo ra thừa số $-1$, dấu tổng quát là:
  $$(-1)^{i + j - 2} = (-1)^{i+j} \cdot (-1)^{-2} = (-1)^{i+j}$$
  Tạo nên quy tắc dấu bàn cờ vua:
  $$\begin{bmatrix} + & - & + & \cdots \\ - & + & - & \cdots \\ + & - & + & \cdots \\ \vdots & \vdots & \vdots & \ddots \end{bmatrix}$$

###### 3. Ý nghĩa thực chiến trong CUDA Ray Tracing
* Trên GPU (CUDA), phân nhánh rẽ nhánh (branching/recursion) rất chậm, nên **không ai viết hàm đệ quy Laplace tổng quát**.
* Nhờ hiểu bản chất Laplace là tích hỗn tạp, với ma trận $3 \times 3$ ta có thể viết code dạng đóng (closed-form) cực nhanh bằng lệnh vector của CUDA: `dot(u, cross(v, w))` chỉ tốn vài chu kỳ xung nhịp.

---

##### D. Các tính chất quan trọng của Định thức
1. $\det(A \cdot B) = \det(A) \cdot \det(B)$
2. $\det(A^T) = \det(A)$
3. $\det(A^{-1}) = \dfrac{1}{\det(A)}$
4. $\det(k \cdot A_{n \times n}) = k^n \cdot \det(A)$ *(với $n$ là cấp ma trận)*

---

#### 6. Ma trận đơn vị ($I$) & Ma trận nghịch đảo ($A^{-1}$)

##### A. Định nghĩa & Điều kiện tồn tại
* **Ma trận đơn vị ($I$):** Đóng vai trò như số $1$ trong phép nhân số học ($A \cdot I = I \cdot A = A$):
$$I_4 = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
* **Ma trận nghịch đảo ($A^{-1}$):** Là ma trận thỏa mãn:
$$A \cdot A^{-1} = A^{-1} \cdot A = I$$
* **Điều kiện khả nghịch:** $A$ phải là ma trận vuông và **định thức khác không** ($\det(A) \neq 0$). Nếu $\det(A) = 0$, ma trận bị suy biến (Singular) và không thể nghịch đảo.

---

##### B. Cách 1: Phương pháp Đại số Tổng quát (Ma trận phụ hợp - Adjugate Matrix)
Phương pháp chuẩn xác dùng cho mọi ma trận vuông bất kỳ:
$$A^{-1} = \frac{1}{\det(A)} \text{adj}(A) = \frac{1}{\det(A)} C^T$$

###### Quy trình 4 bước tính toán:
1. **Bước 1:** Tính định thức $\det(A)$. Nếu $\det(A) = 0 \implies$ Dừng lại (không khả nghịch).
2. **Bước 2:** Lập **Ma trận phần bù đại số (Cofactor Matrix $C$)**:
   $$C_{ij} = (-1)^{i+j} M_{ij}$$
   *(với $M_{ij}$ là định thức của ma trận con khi bỏ hàng $i$, cột $j$).*
3. **Bước 3:** Chuyển vị ma trận $C$ để thu được **Ma trận phụ hợp (Adjugate Matrix $\text{adj}(A)$)**:
   $$\text{adj}(A) = C^T$$
4. **Bước 4:** Nhân vô hướng từng phần tử của $\text{adj}(A)$ với $\dfrac{1}{\det(A)}$.

---

###### 1. Công thức nhanh cho ma trận $2 \times 2$:
$$\begin{bmatrix} a & b \\ c & d \end{bmatrix}^{-1} = \frac{1}{ad - bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$$
*(Quy tắc nhớ: Đổi chỗ đường chéo chính $a \leftrightarrow d$, đổi dấu đường chéo phụ $-b, -c$, rồi chia cho $\det$).*

> [!NOTE] Ví dụ: Nghịch đảo ma trận $2 \times 2$
> Cho $A = \begin{bmatrix} 4 & 7 \\ 2 & 6 \end{bmatrix}$:
> 1. Tính $\det(A) = 4(6) - 7(2) = 24 - 14 = 10 \neq 0$.
> 2. Đổi chỗ đường chéo chính và đổi dấu đường chéo phụ:
>    $$\text{adj}(A) = \begin{bmatrix} 6 & -7 \\ -2 & 4 \end{bmatrix}$$
> 3. Nhân với $\frac{1}{\det(A)} = \frac{1}{10} = 0.1$:
>    $$A^{-1} = \frac{1}{10} \begin{bmatrix} 6 & -7 \\ -2 & 4 \end{bmatrix} = \begin{bmatrix} 0.6 & -0.7 \\ -0.2 & 0.4 \end{bmatrix}$$
> 4. Kiểm tra lại:
>    $$A \cdot A^{-1} = \begin{bmatrix} 4(0.6) + 7(-0.2) & 4(-0.7) + 7(0.4) \\ 2(0.6) + 6(-0.2) & 2(-0.7) + 6(0.4) \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = I$$

---

###### 2. Ví dụ chi tiết cho ma trận $3 \times 3$:
Cho $A = \begin{bmatrix} 1 & 0 & 2 \\ 2 & -1 & 3 \\ 4 & 1 & 8 \end{bmatrix}$:

* **Bước 1 (Tính $\det(A)$ theo hàng 1):**
  $$\det(A) = 1((-1)(8) - 3(1)) - 0 + 2(2(1) - (-1)(4)) = 1(-11) + 2(6) = 1 \neq 0$$

* **Bước 2 (Tính 9 phần bù đại số $C_{ij} = (-1)^{i+j} M_{ij}$):**
  * $C_{11} = +((-1)(8) - 3(1)) = -11, \quad C_{12} = -(2(8) - 3(4)) = -4, \quad C_{13} = +(2(1) - (-1)(4)) = 6$
  * $C_{21} = -(0(8) - 2(1)) = 2, \quad\quad C_{22} = +(1(8) - 2(4)) = 0, \quad\quad C_{23} = -(1(1) - 0(4)) = -1$
  * $C_{31} = +(0(3) - 2(-1)) = 2, \quad\quad C_{32} = -(1(3) - 2(2)) = 1, \quad\quad C_{33} = +(1(-1) - 0(2)) = -1$
  
  $$\implies C = \begin{bmatrix} -11 & -4 & 6 \\ 2 & 0 & -1 \\ 2 & 1 & -1 \end{bmatrix}$$

* **Bước 3 & 4 (Chuyển vị $C^T$ và chia cho $\det(A) = 1$):**
  $$A^{-1} = \frac{1}{1} C^T = \begin{bmatrix} -11 & 2 & 2 \\ -4 & 0 & 1 \\ 6 & -1 & -1 \end{bmatrix}$$

---

##### C. Cách 2: Phương pháp Nghịch đảo Hình học Nhanh (Fast Geometric Inverse) – Tối ưu cho Ray Tracing / CUDA

Trong Engine Ray Tracing, việc tính nghịch đảo đại số $4 \times 4$ trên GPU rất tốn tài nguyên. Do ma trận biến đổi thế giới được tạo từ chuỗi $M = T \cdot R \cdot S$, ta tận dụng tính chất hình học để tính nghịch đảo tức thì trong $O(1)$:

###### 1. Nghịch đảo từng phép biến đổi cơ bản:
* **Tịnh tiến ($T$):** Chỉ cần đổi dấu vector tịnh tiến:
  $$T(t_x, t_y, t_z)^{-1} = T(-t_x, -t_y, -t_z) = \begin{bmatrix} 1 & 0 & 0 & -t_x \\ 0 & 1 & 0 & -t_y \\ 0 & 0 & 1 & -t_z \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
* **Co giãn ($S$):** Nghịch đảo từng hệ số co giãn:
  $$S(s_x, s_y, s_z)^{-1} = S\left(\frac{1}{s_x}, \frac{1}{s_y}, \frac{1}{s_z}\right) = \begin{bmatrix} \frac{1}{s_x} & 0 & 0 & 0 \\ 0 & \frac{1}{s_y} & 0 & 0 \\ 0 & 0 & \frac{1}{s_z} & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
* **Xoay ($R$):** Vì $R$ là ma trận trực giao ($R \cdot R^T = I$), nên **nghịch đảo chính là chuyển vị**:
  $$R^{-1} = R^T \quad (\text{Chỉ cần đổi hàng thành cột, 0 phép tính chia!})$$

###### 2. Nghịch đảo chuỗi biến đổi tổng hợp $M = T \cdot R \cdot S$:
Áp dụng tính chất $(A \cdot B \cdot C)^{-1} = C^{-1} \cdot B^{-1} \cdot A^{-1}$:
$$M^{-1} = (T \cdot R \cdot S)^{-1} = S^{-1} \cdot R^T \cdot T^{-1}$$

> [!TIP] Ứng dụng trong Ray Tracing (Instancing Transformation)
> Khi bắn tia sáng từ World Space vào mô hình Object Space:
> Thay vì tính nghịch đảo ma trận $4 \times 4$ tốn kém, ta lấy $S^{-1} \cdot R^T \cdot T^{-1}$ biến đổi trực tiếp tia sáng ($\text{Ray}_{\text{origin}}$ và $\text{Ray}_{\text{direction}}$) với độ chính xác số thực tối đa và tốc độ xử lý GPU cực cao.

---

##### D. Các tính chất quan trọng của Ma trận nghịch đảo
1. $(A^{-1})^{-1} = A$
2. $(A \cdot B)^{-1} = B^{-1} \cdot A^{-1}$ *(chú ý đảo thứ tự)*
3. $(A^T)^{-1} = (A^{-1})^T$
4. $\det(A^{-1}) = \dfrac{1}{\det(A)}$

---

#### 7. Phép nhân Ma trận với Vector ($A\mathbf{v}$)
* Vector $\mathbf{v}$ kích thước $n \times 1$ được xem như ma trận $n \times 1$:
$$\mathbf{v}' = A\mathbf{v} \implies v'_i = \sum_{j=1}^{n} a_{ij} v_j$$

> [!NOTE] Ví dụ: Nhân ma trận $3 \times 3$ với vector $3 \times 1$
> $$\begin{bmatrix} 2 & 0 & 1 \\ 1 & 3 & 0 \\ 0 & -1 & 4 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \\ 3 \end{bmatrix} = \begin{bmatrix} 2(1) + 0(2) + 1(3) \\ 1(1) + 3(2) + 0(3) \\ 0(1) + (-1)(2) + 4(3) \end{bmatrix} = \begin{bmatrix} 5 \\ 7 \\ 10 \end{bmatrix}$$

---

## 2. Tọa độ đồng nhất (Homogeneous Coordinates)

### 2.1. Giới hạn của ma trận $3 \times 3$
Ma trận $3 \times 3$ luôn giữ cố định gốc tọa độ:
$$M_{3 \times 3} \cdot \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ 0 \end{bmatrix}$$
Không thể biểu diễn phép tịnh tiến ($\mathbf{v}' = \mathbf{v} + \mathbf{t}$) bằng một phép nhân ma trận $3 \times 3$.

### 2.2. Thành phần $w$ trong không gian 4D
* **Điểm (Point) ($w = 1$):** Có vị trí xác định, chịu tác động của phép tịnh tiến.
$$\mathbf{p} = \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix}$$
* **Vector hướng / Vận tốc / Pháp tuyến (Direction Vector) ($w = 0$):** Chỉ phương hướng và độ lớn, **không bị ảnh hưởng** bởi phép tịnh tiến.
$$\mathbf{d} = \begin{bmatrix} x \\ y \\ z \\ 0 \end{bmatrix}$$

> [!NOTE] Ví dụ minh họa phân biệt Điểm và Vector hướng
> * Điểm $P$ tại vị trí $(2, 5, -1)$ biểu diễn trong tọa độ đồng nhất là $\mathbf{p} = \begin{bmatrix} 2 & 5 & -1 & 1 \end{bmatrix}^T$.
> * Vector vận tốc gió $\vec{v}$ hướng $(0, 10, 0)$ biểu diễn là $\mathbf{d} = \begin{bmatrix} 0 & 10 & 0 & 0 \end{bmatrix}^T$.

### 2.3. Cấu trúc tổng quát ma trận $4 \times 4$
$$M = \begin{bmatrix} R_{11} & R_{12} & R_{13} & T_x \\ R_{21} & R_{22} & R_{23} & T_y \\ R_{31} & R_{32} & R_{33} & T_z \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

---

## 3. Bản chất hình học: Ma trận là bản đồ Vector cơ sở

Mọi vector $\mathbf{v} = (x, y, z, 1)^T$ là tổ hợp tuyến tính của các vector cơ sở:
$$\mathbf{v} = x\hat{\mathbf{i}} + y\hat{\mathbf{j}} + z\hat{\mathbf{k}} + 1\vec{\mathbf{O}}$$

Từng cột của ma trận $4 \times 4$ đại diện cho tọa độ mới của các trục sau biến đổi:
$$M = \begin{bmatrix} | & | & | & | \\ \hat{\mathbf{i}}' & \hat{\mathbf{j}}' & \hat{\mathbf{k}}' & \vec{\mathbf{O}}' \\ | & | & | & | \end{bmatrix}$$

* **Cột 1 ($\hat{\mathbf{i}}'$):** Tọa độ mới của trục $X$ sau biến đổi.
* **Cột 2 ($\hat{\mathbf{j}}'$):** Tọa độ mới của trục $Y$ sau biến đổi.
* **Cột 3 ($\hat{\mathbf{k}}'$):** Tọa độ mới của trục $Z$ sau biến đổi.
* **Cột 4 ($\vec{\mathbf{O}}'$):** Vị trí mới của gốc tọa độ $(0, 0, 0)$.

$$M\mathbf{v} = x\hat{\mathbf{i}}' + y\hat{\mathbf{j}}' + z\hat{\mathbf{k}}' + w\vec{\mathbf{O}}'$$

---

## 4. Chi tiết các phép biến đổi Affine

### 4.1. Phép co giãn (Scale Matrix)
Thay đổi độ dài các trục cơ sở theo tỷ lệ $(s_x, s_y, s_z)$:
$$S(s_x, s_y, s_z) = \begin{bmatrix} s_x & 0 & 0 & 0 \\ 0 & s_y & 0 & 0 \\ 0 & 0 & s_z & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

Tác động lên vector:
$$S \cdot \mathbf{v} = \begin{bmatrix} s_x & 0 & 0 & 0 \\ 0 & s_y & 0 & 0 \\ 0 & 0 & s_z & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} = \begin{bmatrix} s_x \cdot x \\ s_y \cdot y \\ s_z \cdot z \\ 1 \end{bmatrix}$$

> [!NOTE] Ví dụ: Co giãn một điểm trong không gian
> Thu phóng điểm $P(2, 3, 4, 1)$ với hệ số co giãn $s_x = 2, s_y = 0.5, s_z = 3$:
> $$S(2, 0.5, 3) \cdot \begin{bmatrix} 2 \\ 3 \\ 4 \\ 1 \end{bmatrix} = \begin{bmatrix} 2 & 0 & 0 & 0 \\ 0 & 0.5 & 0 & 0 \\ 0 & 0 & 3 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 2 \\ 3 \\ 4 \\ 1 \end{bmatrix} = \begin{bmatrix} 2 \cdot 2 \\ 0.5 \cdot 3 \\ 3 \cdot 4 \\ 1 \end{bmatrix} = \begin{bmatrix} 4 \\ 1.5 \\ 12 \\ 1 \end{bmatrix}$$

---

### 4.2. Phép tịnh tiến (Translation Matrix)
Dời gốc tọa độ $\vec{\mathbf{O}}$ đến vị trí mới $(t_x, t_y, t_z)$:
$$T(t_x, t_y, t_z) = \begin{bmatrix} 1 & 0 & 0 & t_x \\ 0 & 1 & 0 & t_y \\ 0 & 0 & 1 & t_z \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

* **Tác động lên Điểm ($w = 1$):**
$$T \cdot \begin{bmatrix} x \\ y \\ z \\ 1 \end{bmatrix} = \begin{bmatrix} x + t_x \cdot 1 \\ y + t_y \cdot 1 \\ z + t_z \cdot 1 \\ 1 \end{bmatrix} = \begin{bmatrix} x + t_x \\ y + t_y \\ z + t_z \\ 1 \end{bmatrix} \quad \text{(Dịch chuyển vị trí)}$$

* **Tác động lên Vector hướng ($w = 0$):**
$$T \cdot \begin{bmatrix} x \\ y \\ z \\ 0 \end{bmatrix} = \begin{bmatrix} x + t_x \cdot 0 \\ y + t_y \cdot 0 \\ z + t_z \cdot 0 \\ 0 \end{bmatrix} = \begin{bmatrix} x \\ y \\ z \\ 0 \end{bmatrix} \quad \text{(Không bị thay đổi)}$$

> [!NOTE] Ví dụ: Tịnh tiến vector $(5, -2, 4)$
> Cho vector tịnh tiến $(t_x, t_y, t_z) = (5, -2, 4)$:
> 1. Điểm $P(1, 2, 3, 1)$:
> $$T \cdot \begin{bmatrix} 1 \\ 2 \\ 3 \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 & 5 \\ 0 & 1 & 0 & -2 \\ 0 & 0 & 1 & 4 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \\ 3 \\ 1 \end{bmatrix} = \begin{bmatrix} 1 + 5 \\ 2 - 2 \\ 3 + 4 \\ 1 \end{bmatrix} = \begin{bmatrix} 6 \\ 0 \\ 7 \\ 1 \end{bmatrix}$$
> 2. Vector hướng $\vec{d}(1, 2, 3, 0)$:
> $$T \cdot \begin{bmatrix} 1 \\ 2 \\ 3 \\ 0 \end{bmatrix} = \begin{bmatrix} 1 & 0 & 0 & 5 \\ 0 & 1 & 0 & -2 \\ 0 & 0 & 1 & 4 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 1 \\ 2 \\ 3 \\ 0 \end{bmatrix} = \begin{bmatrix} 1 \\ 2 \\ 3 \\ 0 \end{bmatrix} \quad \text{(Không đổi)}$$

---

### 4.3. Phép xoay (Rotation Matrix) & Nguồn gốc lượng giác

#### Chứng minh hình học (Mặt phẳng 2D):
Xoay hệ trục tọa độ một góc $\theta$ ngược chiều kim đồng hồ:
1. **Trục $X$ ban đầu $\hat{\mathbf{i}} = (1, 0)^T$:** Khi xoay góc $\theta$, mút vector chạm đường tròn đơn vị tại $(\cos\theta, \sin\theta)^T$.
$$\hat{\mathbf{i}}' = \begin{bmatrix} \cos\theta \\ \sin\theta \end{bmatrix}$$
2. **Trục $Y$ ban đầu $\hat{\mathbf{j}} = (0, 1)^T$:** Vuông góc với $\hat{\mathbf{i}}$, góc quay là $\theta + 90^\circ$:
$$\hat{\mathbf{j}}' = \begin{bmatrix} \cos(\theta + 90^\circ) \\ \sin(\theta + 90^\circ) \end{bmatrix} = \begin{bmatrix} -\sin\theta \\ \cos\theta \end{bmatrix}$$

Ghép lại thành ma trận xoay 2D:
$$R(\theta) = \begin{bmatrix} \hat{\mathbf{i}}' & \hat{\mathbf{j}}' \end{bmatrix} = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$$

#### Chứng minh bằng đại số (Công thức cộng góc):
Điểm ban đầu $P(x, y)$ với $x = r\cos\alpha, y = r\sin\alpha$. Khi xoay thêm góc $\theta$:
$$x' = r\cos(\alpha + \theta) = r\cos\alpha\cos\theta - r\sin\alpha\sin\theta = x\cos\theta - y\sin\theta$$
$$y' = r\sin(\alpha + \theta) = r\cos\alpha\sin\theta + r\sin\alpha\cos\theta = x\sin\theta + y\cos\theta$$

Dạng ma trận:
$$\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}$$

#### 3 Ma trận xoay trong không gian 3D ($4 \times 4$):

* **Quanh trục Z ($R_z$):** Giữ nguyên tọa độ $z$ ($z' = z$):
$$R_z(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 & 0 \\ \sin\theta & \cos\theta & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

* **Quanh trục X ($R_x$):** Giữ nguyên tọa độ $x$ ($x' = x$):
$$R_x(\theta) = \begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta & 0 \\ 0 & \sin\theta & \cos\theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

* **Quanh trục Y ($R_y$):** Giữ nguyên tọa độ $y$ ($y' = y$):
$$R_y(\theta) = \begin{bmatrix} \cos\theta & 0 & \sin\theta & 0 \\ 0 & 1 & 0 & 0 \\ -\sin\theta & 0 & \cos\theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$

> [!NOTE] Ví dụ: Xoay điểm quanh trục Z một góc $\theta = 90^\circ$
> Với $\theta = 90^\circ \implies \cos 90^\circ = 0, \sin 90^\circ = 1$. Ma trận xoay:
> $$R_z(90^\circ) = \begin{bmatrix} 0 & -1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
> Tác động lên điểm $P(1, 0, 0, 1)$ trên trục $X$:
> $$P' = R_z(90^\circ) \cdot \begin{bmatrix} 1 \\ 0 \\ 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 0(1) - 1(0) \\ 1(1) + 0(0) \\ 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 0 \\ 1 \\ 0 \\ 1 \end{bmatrix} \implies \text{Điểm chuyển sang trục } Y.$$

---

## 5. Ghép các phép biến đổi (Matrix Concatenation)

### 5.1. Thứ tự nhân chuẩn (TRS)
Phép nhân thực hiện từ **phải sang trái**:
$$\mathbf{v}_{\text{world}} = (T \cdot R \cdot S) \cdot \mathbf{v}_{\text{local}}$$

1. **Scale ($S$):** Co giãn quanh tâm cục bộ của vật.
2. **Rotate ($R$):** Xoay quanh tâm cục bộ.
3. **Translate ($T$):** Dịch chuyển vật thể đến vị trí đích trong thế giới.

> [!CAUTION] Lỗi đảo thứ tự (SRT)
> Nếu Translate trước khi Rotate/Scale, vật thể sẽ xoay quanh gốc tọa độ thế giới (tạo quỹ đạo quay lớn) thay vì tự quay quanh chính nó.

> [!NOTE] Ví dụ: Tính toán chuỗi biến đổi TRS tổng hợp
> Giả sử cần biến đổi một mô hình 3D:
> 1. Phóng to 2 lần theo mọi trục: $S(2, 2, 2)$
> 2. Xoay $90^\circ$ quanh trục Z: $R_z(90^\circ)$
> 3. Tịnh tiến đến vị trí $(3, 4, 0)$: $T(3, 4, 0)$
>
> Biến đổi điểm $P_{\text{local}}(1, 0, 0, 1)$:
> * **Bước 1 (Scale):** $P_1 = S \cdot P = (2 \cdot 1, 2 \cdot 0, 2 \cdot 0, 1)^T = (2, 0, 0, 1)^T$
> * **Bước 2 (Rotate):** $P_2 = R_z(90^\circ) \cdot P_1 = (0, 2, 0, 1)^T$
> * **Bước 3 (Translate):** $P_3 = T \cdot P_2 = (0 + 3, 2 + 4, 0 + 0, 1)^T = (3, 6, 0, 1)^T$
>
> Hoặc gộp thành ma trận $M = T \cdot R_z \cdot S$:
> $$M = \begin{bmatrix} 1 & 0 & 0 & 3 \\ 0 & 1 & 0 & 4 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 0 & -1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} 2 & 0 & 0 & 0 \\ 0 & 2 & 0 & 0 \\ 0 & 0 & 2 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix} = \begin{bmatrix} 0 & -2 & 0 & 3 \\ 2 & 0 & 0 & 4 \\ 0 & 0 & 2 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$$
> Khi đó: $M \cdot \begin{bmatrix} 1 \\ 0 \\ 0 \\ 1 \end{bmatrix} = \begin{bmatrix} 0(1) - 2(0) + 0(0) + 3(1) \\ 2(1) + 0(0) + 0(0) + 4(1) \\ 0(1) + 0(0) + 2(0) + 0(1) \\ 1 \end{bmatrix} = \begin{bmatrix} 3 \\ 6 \\ 0 \\ 1 \end{bmatrix}$.

---

### 5.2. Xoay quanh điểm bất kỳ (Pivot Point $\mathbf{P}$)
Để xoay vật thể quanh một điểm $\mathbf{P}(p_x, p_y, p_z)$ thay vì gốc tọa độ $(0, 0, 0)$:
$$M_{\text{pivot}} = T(\mathbf{P}) \cdot R(\theta) \cdot T(-\mathbf{P})$$

1. $T(-\mathbf{P})$: Dời tâm $\mathbf{P}$ về gốc tọa độ $(0, 0, 0)$.
2. $R(\theta)$: Thực hiện xoay quanh gốc tọa độ.
3. $T(\mathbf{P})$: Trả tâm $\mathbf{P}$ về lại vị trí ban đầu trong không gian.

> [!NOTE] Ví dụ: Xoay điểm $A(3, 2, 0)$ quanh điểm Pivot $P(1, 2, 0)$ một góc $90^\circ$ quanh trục Z
> 1. Dời $P$ về gốc tọa độ: $A_1 = A - P = (3 - 1, 2 - 2, 0 - 0) = (2, 0, 0)$
> 2. Xoay $90^\circ$ quanh trục Z: $A_2 = R_z(90^\circ) \cdot (2, 0, 0)^T = (0, 2, 0)$
> 3. Dời ngược lại vị trí $P$: $A' = A_2 + P = (0 + 1, 2 + 2, 0 + 0) = (1, 4, 0)$

---

## 6. Bảng tổng kết ma trận biến đổi

| Phép biến đổi                    | Ma trận $4 \times 4$                                                                                                                  | Ý nghĩa hình học                                            |
| :------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ | :---------------------------------------------------------- |
| **Tịnh tiến** $T(t_x, t_y, t_z)$ | $\begin{bmatrix} 1 & 0 & 0 & t_x \\ 0 & 1 & 0 & t_y \\ 0 & 0 & 1 & t_z \\ 0 & 0 & 0 & 1 \end{bmatrix}$                                | Dời gốc tọa độ đến vị trí $(t_x, t_y, t_z)$                 |
| **Co giãn** $S(s_x, s_y, s_z)$   | $\begin{bmatrix} s_x & 0 & 0 & 0 \\ 0 & s_y & 0 & 0 \\ 0 & 0 & s_z & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$                                | Thay đổi độ dài các trục cơ sở theo tỉ lệ $(s_x, s_y, s_z)$ |
| **Xoay trục X** $R_x(\theta)$    | $\begin{bmatrix} 1 & 0 & 0 & 0 \\ 0 & \cos\theta & -\sin\theta & 0 \\ 0 & \sin\theta & \cos\theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$ | Giữ nguyên trục X, quay mặt phẳng YZ góc $\theta$           |
| **Xoay trục Y** $R_y(\theta)$    | $\begin{bmatrix} \cos\theta & 0 & \sin\theta & 0 \\ 0 & 1 & 0 & 0 \\ -\sin\theta & 0 & \cos\theta & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$ | Giữ nguyên trục Y, quay mặt phẳng ZX góc $\theta$           |
| **Xoay trục Z** $R_z(\theta)$    | $\begin{bmatrix} \cos\theta & -\sin\theta & 0 & 0 \\ \sin\theta & \cos\theta & 0 & 0 \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{bmatrix}$ | Giữ nguyên trục Z, quay mặt phẳng XY góc $\theta$           |