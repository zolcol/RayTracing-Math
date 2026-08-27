> [!NOTE] Định nghĩa
> **Tọa độ tỉ cự (Barycentric Coordinates)** là hệ tọa độ biểu diễn vị trí của một điểm $P$ dưới dạng tổ hợp tuyến tính trọng số của các đỉnh trong một đa giác (phổ biến nhất là tam giác $ABC$).

---

## 1. Định nghĩa toán học & Ý nghĩa hình học

Mọi điểm $P$ nằm trên mặt phẳng chứa tam giác $ABC$ đều được xác định bởi bộ ba số $(\alpha, \beta, \gamma)$ (hoặc $(w_A, w_B, w_C)$):

> [!NOTE] Biểu diễn cơ bản & Ràng buộc tọa độ tỉ cự
> $$P = \alpha A + \beta B + \gamma C \quad \text{với} \quad \alpha + \beta + \gamma = 1$$
> Biểu diễn qua hai ẩn độc lập $(u, v)$ với $\alpha = 1 - u - v$:
> $$P = (1 - u - v)A + uB + vC \iff P - A = u(B - A) + v(C - A)$$

- **$\alpha, u, v \ge 0$ và $u + v \le 1$:** Điểm $P$ nằm bên trong hoặc trên cạnh tam giác.
- **Có ít nhất một hệ số $< 0$:** Điểm $P$ nằm ngoài tam giác.

---

## 2. Các phương pháp tính toán tọa độ tỉ cự

Việc chia diện tích tam giác là cách tiếp cận hình học trực quan nhưng không hiệu quả trong tính toán thực tế. Dưới đây là các phương pháp đại số và giải tích vector chuẩn xác, tối ưu được sử dụng trong đồ họa máy tính.

---

### Phương pháp 1: Hệ phương trình tích vô hướng (Dot Products & Cramer's Rule)

#### 1. Khái niệm & Định nghĩa
- **Khái niệm:** Phương pháp này biểu diễn vector vị trí của điểm $P$ dưới dạng tổ hợp tuyến tính của hai vector cạnh tam giác, sau đó sử dụng phép **nhân vô hướng (Dot Product)** để chuyển phương trình vector thành một hệ hai phương trình đại số tuyến tính $2 \times 2$.
- **Định nghĩa toán học:** Cho tam giác $ABC$ và điểm $P$ trong không gian 2D hoặc 3D. Đặt các vector cạnh xuất phát từ đỉnh $A$:
  $$\vec{v_0} = C - A, \quad \vec{v_1} = B - A, \quad \vec{v_2} = P - A$$
  Tọa độ tỉ cự $(u, v)$ là nghiệm của phương trình vector:
  $$\vec{v_2} = u \vec{v_1} + v \vec{v_0}$$

#### 2. Thiết lập hệ phương trình
Để giải tìm 2 ẩn vô hướng $(u, v)$ từ phương trình vector (vốn có 3 thành phần $x, y, z$), ta nhân vô hướng cả hai vế lần lượt với $\vec{v_0}$ và $\vec{v_1}$:

$$\begin{cases}
(\vec{v_2} \cdot \vec{v_0}) = u (\vec{v_1} \cdot \vec{v_0}) + v (\vec{v_0} \cdot \vec{v_0}) \\
(\vec{v_2} \cdot \vec{v_1}) = u (\vec{v_1} \cdot \vec{v_1}) + v (\vec{v_0} \cdot \vec{v_1})
\end{cases}$$

Đặt các giá trị tích vô hướng:
- $d_{00} = \vec{v_0} \cdot \vec{v_0}$
- $d_{01} = \vec{v_0} \cdot \vec{v_1}$
- $d_{11} = \vec{v_1} \cdot \vec{v_1}$
- $d_{20} = \vec{v_2} \cdot \vec{v_0}$
- $d_{21} = \vec{v_2} \cdot \vec{v_1}$

Hệ phương trình trở thành dạng ma trận $2 \times 2$:
$$\begin{pmatrix} d_{11} & d_{01} \\ d_{01} & d_{00} \end{pmatrix} \begin{pmatrix} u \\ v \end{pmatrix} = \begin{pmatrix} d_{21} \\ d_{20} \end{pmatrix}$$

#### 3. Giải thích & Chứng minh nghiệm bằng Quy tắc Cramer
- **Bước 1: Tính định thức của ma trận hệ số ($\Delta$)**
  $$\Delta = \det \begin{pmatrix} d_{11} & d_{01} \\ d_{01} & d_{00} \end{pmatrix} = d_{00} d_{11} - d_{01}^2$$
  *(Nếu $\Delta \approx 0$, ba đỉnh $A, B, C$ thẳng hàng $\implies$ tam giác suy biến).*

> [!NOTE] Công thức nghiệm Cramer (Dot Products)
> $$u = \frac{d_{00} d_{21} - d_{01} d_{20}}{\Delta}$$
> $$v = \frac{d_{11} d_{20} - d_{01} d_{21}}{\Delta}$$
> $$w = 1 - u - v$$
> 
> **Bảng quy ước biến & Ý nghĩa đại lượng:**
> - **$\vec{v_0} = C - A$:** Vector cạnh $AC$
> - **$\vec{v_1} = B - A$:** Vector cạnh $AB$
> - **$\vec{v_2} = P - A$:** Vector nối từ đỉnh gốc $A$ đến điểm cần tính $P$
> 
> **Chi tiết các tích vô hướng (Dot Products):**
> - **$d_{00} = \vec{v_0} \cdot \vec{v_0} = |\vec{v_0}|^2$:** Bình phương độ dài cạnh $AC$
> - **$d_{01} = \vec{v_0} \cdot \vec{v_1}$:** Tích vô hướng giữa hai cạnh $AC$ và $AB$
> - **$d_{11} = \vec{v_1} \cdot \vec{v_1} = |\vec{v_1}|^2$:** Bình phương độ dài cạnh $AB$
> - **$d_{20} = \vec{v_2} \cdot \vec{v_0}$:** Tích vô hướng giữa vector $\vec{AP}$ và cạnh $AC$
> - **$d_{21} = \vec{v_2} \cdot \vec{v_1}$:** Tích vô hướng giữa vector $\vec{AP}$ và cạnh $AB$
> - **$\Delta = d_{00} d_{11} - d_{01}^2$:** Định thức ma trận hệ số (bằng $0$ khi tam giác suy biến)
>

#### 4. Ý nghĩa thực tế
Phương pháp này hoạt động hoàn hảo trực tiếp trong **không gian 3D tổng quát** mà không cần chiếu phẳng tam giác về 2D, rất phù hợp cho xử lý va chạm vật lý (Physics Collision) và xử lý lưới đa giác (Mesh Processing).

---

### Phương pháp 2: Hàm cạnh Pineda (Edge Functions & 2D Cross Product)

#### 1. Khái niệm & Định nghĩa
- **Khái niệm:** Hàm cạnh (Pineda Edge Function) là một hàm số giải tích đại diện cho một đường thẳng có hướng đi qua hai đỉnh tam giác. Giá trị của hàm cạnh tại điểm $P$ biểu diễn **khoảng cách có dấu** từ $P$ đến cạnh đó, đồng thời tương ứng với **hai lần diện tích có dấu** của tam giác tạo bởi $P$ và cạnh đó.
- **Định nghĩa toán học:** Cho đoạn thẳng định hướng từ $A(x_A, y_A)$ đến $B(x_B, y_B)$ và một điểm kiểm tra $P(x, y)$, hàm cạnh $E_{AB}(P)$ được định nghĩa là thành phần $z$ của tích có hướng 2D:

> [!NOTE] Công thức Hàm cạnh Pineda (2D Cross Product)
> $$E_{AB}(P) = (P_x - A_x)(B_y - A_y) - (P_y - A_y)(B_x - A_x)$$

- **Ý nghĩa dấu của hàm cạnh:**
  - $E_{AB}(P) > 0$: Điểm $P$ nằm ở nửa mặt phẳng bên "trong" của cạnh có hướng (quy ước ngược chiều kim đồng hồ - CCW).
  - $E_{AB}(P) = 0$: Điểm $P$ nằm chính xác trên đường thẳng $AB$.
  - $E_{AB}(P) < 0$: Điểm $P$ nằm ở nửa mặt phẳng bên "ngoài".

#### 2. Giải thích & Chứng minh công thức tỉ cự
- **Bước 1: Tính diện tích tam giác gốc $ABC$**
  Thay tọa độ đỉnh $C$ vào hàm cạnh $E_{AB}$:
  $$E_{AB}(C) = (C_x - A_x)(B_y - A_y) - (C_y - A_y)(B_x - A_x) = 2 \cdot \text{SignedArea}(ABC)$$

- **Bước 2: Tính diện tích các tam giác con tạo bởi $P$**
  - $E_{BC}(P) = 2 \cdot \text{SignedArea}(PBC)$
  - $E_{CA}(P) = 2 \cdot \text{SignedArea}(PCA)$
  - $E_{AB}(P) = 2 \cdot \text{SignedArea}(PAB)$

- **Bước 3: Suy ra tọa độ tỉ cự**

> [!NOTE] Công thức Tọa độ tỉ cự qua Hàm cạnh
> $$w_A = \frac{E_{BC}(P)}{E_{AB}(C)}, \quad w_B = \frac{E_{CA}(P)}{E_{AB}(C)}, \quad w_C = \frac{E_{AB}(P)}{E_{AB}(C)}$$

#### 3. Tối ưu gia số (Incremental Evaluation - Bí quyết render siêu nhanh)
Thay vì tính lại toàn bộ phép nhân/trừ phức tạp cho từng pixel $(x, y)$, ta quan sát quy luật thay đổi khi dịch chuyển giữa các pixel liền kề:

- **Khai triển nhóm theo $x$ và $y$:**
  $$E(x, y) = (B_y - A_y) \cdot x - (B_x - A_x) \cdot y + \text{Hằng số}$$

> [!TIP] Công thức bước nhảy vi phân (Incremental Stepping)
> - **Khi bước sang phải $1$ pixel ($x \to x + 1$):**
>   $$E(x + 1, y) = E(x, y) + (B_y - A_y)$$
> - **Khi bước xuống dưới $1$ dòng ($y \to y + 1$):**
>   $$E(x, y + 1) = E(x, y) + (A_x - B_x)$$

#### 4. Ý nghĩa thực tế
GPU và Software Rasterizer chỉ cần tính công thức gốc **1 lần** tại góc trên-trái của tam giác. Sau đó khi quét qua toàn bộ màn hình, phần cứng chỉ cần thực hiện **phép cộng liên tiếp** mà không tốn phép nhân hay chia nào.

---

### Phương pháp 3: Tích có hướng trực giao (Orthogonal Cross Product)

#### 1. Khái niệm & Định nghĩa
- **Khái niệm:** Kỹ thuật này chuyển việc tìm hệ số tỉ cự về bài toán tìm một vector đồng thời vuông góc (trực giao) với hai vector độc lập tuyến tính. Khi đó, vector cần tìm chính là **tích có hướng (Cross Product)** của hai vector đó.
- **Định nghĩa toán học:** Xét phương trình vector $P - A = u(B - A) + v(C - A)$. Tách phương trình theo 2 trục $x$ và $y$:
  $$\begin{cases}
  u (B_x - A_x) + v (C_x - A_x) + (A_x - P_x) = 0 \\
  u (B_y - A_y) + v (C_y - A_y) + (A_y - P_y) = 0
  \end{cases}$$

#### 2. Thiết lập phương trình trực giao
Biểu diễn hai phương trình trên dưới dạng tích vô hướng của vector ẩn $[u, v, 1]^T$ với hai vector tọa độ:
$$\begin{bmatrix} u \\ v \\ 1 \end{bmatrix} \cdot \begin{bmatrix} B_x - A_x \\ C_x - A_x \\ A_x - P_x \end{bmatrix} = 0 \quad \text{và} \quad \begin{bmatrix} u \\ v \\ 1 \end{bmatrix} \cdot \begin{bmatrix} B_y - A_y \\ C_y - A_y \\ A_y - P_y \end{bmatrix} = 0$$

Đặt:
- $\vec{X} = \begin{bmatrix} B_x - A_x, & C_x - A_x, & A_x - P_x \end{bmatrix}^T$
- $\vec{Y} = \begin{bmatrix} B_y - A_y, & C_y - A_y, & A_y - P_y \end{bmatrix}^T$

#### 3. Giải thích & Chứng minh

> [!NOTE] Công thức Tích có hướng trực giao
> Tính tích có hướng của $\vec{X}$ và $\vec{Y}$:
> $$\vec{K} = \vec{X} \times \vec{Y} = \begin{bmatrix} K_0 \\ K_1 \\ K_2 \end{bmatrix}$$
> Chuẩn hóa chia cho thành phần thứ ba $K_2$:
> $$u = \frac{K_0}{K_2}, \quad v = \frac{K_1}{K_2}, \quad w = 1 - u - v$$
> *(Nếu $|K_2| < 10^{-5}$, tam giác suy biến thành đoạn thẳng hoặc điểm).*

#### 4. Ý nghĩa thực tế
Phương pháp này có cấu trúc đại số cực kỳ ngắn gọn và đẹp mắt, thường được sử dụng trong các engine dựng hình nhỏ gọn (như *TinyRenderer*).

---

### Phương pháp 4: Thuật toán Möller–Trumbore (Ray-Triangle Intersection)

#### 1. Khái niệm & Định nghĩa
- **Khái niệm:** Möller–Trumbore là thuật toán nhanh và phổ biến nhất trong **Ray Tracing** để tìm giao điểm giữa một tia sáng và một tam giác 3D. Thuật toán không cần tính trước phương trình mặt phẳng chứa tam giác, mà gộp thẳng phương trình tia sáng và phương trình tọa độ tỉ cự thành một hệ phương trình tuyến tính $3 \times 3$ duy nhất.
- **Định nghĩa toán học:** Cho tia sáng $R(t) = O + t\vec{D}$ (với gốc $O$, hướng $\vec{D}$, khoảng cách $t > 0$) và tam giác $ABC$. Giao điểm $P$ nằm trên tam giác thỏa mãn:
  $$O + t\vec{D} = (1 - u - v)A + uB + vC$$

#### 2. Thiết lập hệ phương trình ma trận
Chuyển vế các số hạng để đưa biến $t, u, v$ về cùng một vế:
$$-t\vec{D} + u(B - A) + v(C - A) = O - A$$

Đặt các vector:
- $\vec{E_1} = B - A$ (cạnh 1)
- $\vec{E_2} = C - A$ (cạnh 2)
- $\vec{T} = O - A$ (vector từ đỉnh $A$ đến gốc tia sáng)

Hệ phương trình trở thành dạng ma trận $3 \times 3$:
$$\begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{E_2} \end{bmatrix} \begin{bmatrix} t \\ u \\ v \end{bmatrix} = \vec{T}$$

#### 3. Giải thích & Chứng minh chi tiết (Quy tắc Cramer & Tích hỗn tạp)

**Bước 1: Áp dụng quy tắc Cramer cho hệ phương trình $3 \times 3$**
Theo quy tắc Cramer, nghiệm của hệ ma trận $\begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{E_2} \end{bmatrix} \begin{bmatrix} t \\ u \\ v \end{bmatrix} = \vec{T}$ được tính qua tỉ số giữa các định thức:
$$t = \frac{\det \begin{bmatrix} \vec{T} & \vec{E_1} & \vec{E_2} \end{bmatrix}}{\det \begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{E_2} \end{bmatrix}}, \quad u = \frac{\det \begin{bmatrix} -\vec{D} & \vec{T} & \vec{E_2} \end{bmatrix}}{\det \begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{E_2} \end{bmatrix}}, \quad v = \frac{\det \begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{T} \end{bmatrix}}{\det \begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{E_2} \end{bmatrix}}$$

**Bước 2: Tính chất Tích hỗn tạp (Scalar Triple Product)**
Định thức của 3 vector $\begin{bmatrix} \vec{a} & \vec{b} & \vec{c} \end{bmatrix}$ chính là thể tích có dấu (tích hỗn tạp) và có tính chất hoán vị vòng quanh (cyclic permutation):
$$\det \begin{bmatrix} \vec{a} & \vec{b} & \vec{c} \end{bmatrix} = (\vec{a} \times \vec{b}) \cdot \vec{c} = (\vec{b} \times \vec{c}) \cdot \vec{a} = (\vec{c} \times \vec{a}) \cdot \vec{b}$$
Đồng thời khi đổi chỗ 2 vector bất kỳ thì định thức đổi dấu: $(\vec{a} \times \vec{b}) \cdot \vec{c} = -(\vec{b} \times \vec{a}) \cdot \vec{c}$.

**Bước 3: Biến đổi rút gọn từng định thức**

1. **Chứng minh Mẫu số ($\text{det}$):**
   $$\text{det} = \det \begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{E_2} \end{bmatrix} = (-\vec{D} \times \vec{E_1}) \cdot \vec{E_2} = (\vec{E_1} \times \vec{E_2}) \cdot (-\vec{D}) = (\vec{D} \times \vec{E_2}) \cdot \vec{E_1}$$
   Đặt vector trung gian: $\vec{P} = \vec{D} \times \vec{E_2}$
   $$\implies \text{det} = \vec{P} \cdot \vec{E_1}$$

2. **Chứng minh Tử số của $u$:**
   $$\det \begin{bmatrix} -\vec{D} & \vec{T} & \vec{E_2} \end{bmatrix} = (-\vec{D} \times \vec{T}) \cdot \vec{E_2} = (\vec{T} \times \vec{D}) \cdot \vec{E_2} = (\vec{D} \times \vec{E_2}) \cdot \vec{T}$$
   Vì đã có $\vec{P} = \vec{D} \times \vec{E_2}$ từ mẫu số:
   $$\implies \text{Tử số}(u) = \vec{P} \cdot \vec{T} \implies u = \frac{\vec{P} \cdot \vec{T}}{\text{det}}$$

3. **Chứng minh Tử số của $v$:**
   $$\det \begin{bmatrix} -\vec{D} & \vec{E_1} & \vec{T} \end{bmatrix} = (-\vec{D} \times \vec{E_1}) \cdot \vec{T} = (\vec{E_1} \times \vec{D}) \cdot \vec{T} = (\vec{T} \times \vec{E_1}) \cdot \vec{D}$$
   Đặt vector trung gian thứ hai: $\vec{Q} = \vec{T} \times \vec{E_1}$
   $$\implies \text{Tử số}(v) = \vec{Q} \cdot \vec{D} \implies v = \frac{\vec{Q} \cdot \vec{D}}{\text{det}}$$

4. **Chứng minh Tử số của $t$:**
   $$\det \begin{bmatrix} \vec{T} & \vec{E_1} & \vec{E_2} \end{bmatrix} = (\vec{T} \times \vec{E_1}) \cdot \vec{E_2}$$
   Tận dụng lại vector $\vec{Q} = \vec{T} \times \vec{E_1}$ vừa tính ở trên:
   $$\implies \text{Tử số}(t) = \vec{Q} \cdot \vec{E_2} \implies t = \frac{\vec{Q} \cdot \vec{E_2}}{\text{det}}$$

*(Nhờ sự khéo léo trong hoán vị vector, toàn bộ thuật toán chỉ tốn đúng 2 phép tích có hướng $\vec{P}, \vec{Q}$ và 3 phép tích vô hướng).*

> [!NOTE] Công thức nghiệm Möller–Trumbore (Ray Tracing)
> $$u = \frac{\vec{P} \cdot \vec{T}}{\text{det}}$$
> $$v = \frac{\vec{Q} \cdot \vec{D}}{\text{det}}$$
> $$t = \frac{\vec{Q} \cdot \vec{E_2}}{\text{det}}$$
> $$w = 1 - u - v$$
> 
> **Bảng quy ước biến & Ý nghĩa đại lượng:**
> - **$O$:** Điểm gốc phát ra tia sáng (Ray Origin)
> - **$\vec{D}$:** Vector hướng truyền của tia sáng (Ray Direction)
> - **$\vec{E_1} = B - A$:** Vector cạnh $AB$ của tam giác
> - **$\vec{E_2} = C - A$:** Vector cạnh $AC$ của tam giác
> - **$\vec{T} = O - A$:** Vector khoảng cách từ đỉnh gốc $A$ đến nguồn tia sáng $O$
> 
> **Các vector trung gian & Định thức:**
> - **$\vec{P} = \vec{D} \times \vec{E_2}$:** Tích có hướng giữa hướng tia $\vec{D}$ và cạnh $AC$
> - **$\vec{Q} = \vec{T} \times \vec{E_1}$:** Tích có hướng giữa vector dịch chuyển $\vec{T}$ và cạnh $AB$
> - **$\text{det} = \vec{P} \cdot \vec{E_1} = (\vec{D} \times \vec{E_2}) \cdot \vec{E_1}$:** Định thức ma trận hệ số (bằng $0$ khi tia sáng song song với mặt phẳng tam giác)
> 
> **Ý nghĩa nghiệm đầu ra:**
> - **$t$:** Khoảng cách từ gốc tia sáng $O$ đến giao điểm $P$ ($P = O + t\vec{D}$)
> - **$\alpha = w = 1 - u - v$:** Trọng số tỉ cự tương ứng với đỉnh **$A$**
> - **$\beta = u$:** Trọng số tỉ cự tương ứng với đỉnh **$B$**
> - **$\gamma = v$:** Trọng số tỉ cự tương ứng với đỉnh **$C$**
> 
> **Điều kiện xác nhận giao điểm hợp lệ:**
> $$\begin{cases}
> t > 0 \quad (\text{giao điểm nằm phía trước nguồn tia sáng}) \\
> u \ge 0, \quad v \ge 0, \quad u + v \le 1 \quad (\text{giao điểm nằm bên trong tam giác})
> \end{cases}$$
> $$\implies \text{Giao điểm } P = O + t\vec{D} = w A + u B + v C$$

#### 4. Ý nghĩa thực tế
Möller–Trumbore là tiêu chuẩn vàng trong mọi bộ dò tia (Path Tracer / Ray Tracer) từ game engine đến phần mềm dựng phim 3D (Blender Cycles, Unreal Engine Lumen, V-Ray) vì chỉ cần **2 phép Cross Product và 3 phép Dot Product** để tính gộp toàn bộ thông tin giao điểm.

---

## 3. So sánh tổng hợp các phương pháp

| Phương pháp | Không gian | Chi phí tính toán / Điểm | Ưu điểm nổi bật | Ứng dụng chính |
| :--- | :---: | :--- | :--- | :--- |
| **Dot Products + Cramer** | 2D / 3D | 5 Dot Products + giải Cramer | Hoạt động trực tiếp trên 3D, không cần chiếu phẳng | Physics, Collision, Mesh Processing |
| **Pineda Edge Functions** | 2D | 0 phép nhân (chỉ phép cộng gia số) | Tốc độ cực nhanh, dễ song song hóa SIMD/GPU | GPU Rasterization, Software Rendering |
| **Orthogonal Cross Product** | 2D | 1 Cross Product 3D | Code cực kỳ ngắn gọn, dễ hiểu | TinyRenderer, CPU Toy Engines |
| **Möller–Trumbore** | 3D | 2 Cross Products + 3 Dot Products | Tính gộp khoảng cách $t$ và tỉ cự $(u, v)$ | Ray Tracing, Path Tracing |

---

## 4. Các yếu tố sống còn khi Render

### A. Nội suy chuẩn phối cảnh (Perspective-Correct Interpolation)
Khi chiếu từ 3D lên màn hình 2D (Perspective Projection), tọa độ tỉ cự tính trên màn hình $(w_A, w_B, w_C)$ **không tỉ lệ tuyến tính** với không gian camera do phép chia $Z$.

> [!NOTE] Công thức nội suy chuẩn phối cảnh
> 1. Nội suy độ sâu nghịch đảo:
>    $$\frac{1}{Z_P} = w_A \frac{1}{Z_A} + w_B \frac{1}{Z_B} + w_C \frac{1}{Z_C}$$
> 2. Nội suy thuộc tính kết hợp độ sâu:
>    $$I_P = Z_P \left( w_A \frac{I_A}{Z_A} + w_B \frac{I_B}{Z_B} + w_C \frac{I_C}{Z_C} \right)$$

### B. Quy tắc Top-Left (Top-Left Tie-Breaking Rule)
Khi hai tam giác liền kề dùng chung một cạnh, các pixel nằm chính xác trên cạnh đó sẽ thỏa mãn cả hai tam giác $\to$ dẫn tới việc pixel bị vẽ 2 lần (gây lỗi khi blending trong suốt hoặc lãng phí shader).
- **Quy tắc:** Chỉ render pixel nằm trên cạnh nếu cạnh đó là:
  - **Top Edge:** Cạnh nằm ngang hoàn toàn và nằm phía trên đỉnh còn lại.
  - **Left Edge:** Cạnh có hướng đi lên (trong hệ trục tọa độ màn hình).