> [!NOTE] Định nghĩa
> **Hộp bao quanh trục tọa độ (Axis-Aligned Bounding Box - AABB)** là khối hộp chữ nhật 3D có các mặt luôn song song với các mặt phẳng tọa độ ($XY, YZ, ZX$). Hộp được xác định hoàn toàn bởi 2 điểm cực trị:
> - $\mathbf{p}_{\min} = (x_{\min}, y_{\min}, z_{\min})$: Tọa độ góc nhỏ nhất.
> - $\mathbf{p}_{\max} = (x_{\max}, y_{\max}, z_{\max})$: Tọa độ góc lớn nhất.

---

## 1. Thiết lập bài toán

- **Phương trình tia sáng (Ray):**
  $$\vec{r}(t) = \mathbf{o} + t\vec{d} \quad (t \ge 0)$$
  - $\mathbf{o} = (o_x, o_y, o_z)$: Gốc của tia (Ray Origin).
  - $\vec{d} = (d_x, d_y, d_z)$: Vector hướng tia (Ray Direction).
- **Miền không gian của hộp AABB:**
  $$\text{AABB} = \big\{ (x, y, z) \in \mathbb{R}^3 \mid x_{\min} \le x \le x_{\max}, \; y_{\min} \le y \le y_{\max}, \; z_{\min} \le z \le z_{\max} \big\}$$

---

## 2. Nguyên lý Phương pháp Tấm phẳng (Slab Method)

### 2.1. Khái niệm "Slab" (Tấm phẳng kẹp)
Một **Slab** là vùng không gian 3D bị kẹp giữa hai mặt phẳng song song vô hạn vuông góc với một trục tọa độ:
- **Slab X:** Giới hạn bởi $x = x_{\min}$ và $x = x_{\max}$.
- **Slab Y:** Giới hạn bởi $y = y_{\min}$ và $y = y_{\max}$.
- **Slab Z:** Giới hạn bởi $z = z_{\min}$ và $z = z_{\max}$.

$$\text{Khối hộp AABB} = \text{Slab X} \cap \text{Slab Y} \cap \text{Slab Z}$$

> [!TIP] Ý tưởng cốt lõi
> Tia sáng giao cắt với AABB khi và chỉ khi **khoảng giao cắt của tia với cả 3 Slab có phần chung (giao nhau khác rỗng)**.

---

### 2.2. Tính khoảng tham số $t$ trên từng trục

Xét riêng trên trục $X$: Tia sáng cắt 2 mặt phẳng biên $x = x_{\min}$ và $x = x_{\max}$ tại:
$$x(t) = o_x + t \cdot d_x \implies t = \frac{x - o_x}{d_x}$$

Do đó:
$$t_{x1} = \frac{x_{\min} - o_x}{d_x}, \quad t_{x2} = \frac{x_{\max} - o_x}{d_x}$$

Vì $d_x$ có thể âm hoặc dương:
- **Khoảng tia đi vào Slab X ($t_{x\_\text{near}}$):** $t_{x\_\text{near}} = \min(t_{x1}, t_{x2})$
- **Khoảng tia đi ra khỏi Slab X ($t_{x\_\text{far}}$):** $t_{x\_\text{far}} = \max(t_{x1}, t_{x2})$

Tương tự cho trục $Y$ và trục $Z$:
$$\begin{cases}
t_{y\_\text{near}} = \min\left(\dfrac{y_{\min} - o_y}{d_y}, \dfrac{y_{\max} - o_y}{d_y}\right), & t_{y\_\text{far}} = \max\left(\dfrac{y_{\min} - o_y}{d_y}, \dfrac{y_{\max} - o_y}{d_y}\right) \\[10pt]
t_{z\_\text{near}} = \min\left(\dfrac{z_{\min} - o_z}{d_z}, \dfrac{z_{\max} - o_z}{d_z}\right), & t_{z\_\text{far}} = \max\left(\dfrac{z_{\min} - o_z}{d_z}, \dfrac{z_{\max} - o_z}{d_z}\right)
\end{cases}$$

---

## 3. Điều kiện giao cắt & Thuật toán Hợp nhất khoảng

### 3.1. Hợp nhất khoảng vào/ra trên cả 3 trục
Tia sáng bắt đầu đi vào AABB tại thời điểm nó **đã đi vào tất cả các Slab**, và bắt đầu rời khỏi AABB tại thời điểm nó **vừa thoát ra khỏi bất kỳ Slab đầu tiên nào**:

$$t_{\text{enter}} = \max(t_{x\_\text{near}}, \; t_{y\_\text{near}}, \; t_{z\_\text{near}})$$
$$t_{\text{exit}} = \min(t_{x\_\text{far}}, \; t_{y\_\text{far}}, \; t_{z\_\text{far}})$$

### 3.2. Điều kiện va chạm hợp lệ
Tia sáng giao cắt với AABB khi và chỉ khi thỏa mãn đồng thời hai điều kiện:
1. **Khoảng giao cắt tồn tại (không bị rỗng):**
   $$t_{\text{enter}} \le t_{\text{exit}}$$
2. **Giao điểm nằm phía trước nguồn tia (hoặc nằm trong đoạn xét $[t_{\min}, t_{\max}]$):**
   $$t_{\text{exit}} \ge t_{\min} \quad \text{và} \quad t_{\text{enter}} \le t_{\max}$$

*(Nếu tia xuất phát từ bên trong hộp AABB thì $t_{\text{enter}} < 0$, khi đó điểm ra $t_{\text{exit}} > 0$ vẫn xác nhận là có giao cắt).*

---

## 4. Kỹ thuật Tối ưu hóa Phần cứng (Fast Ray-AABB / Amy Williams)

Trong Ray Tracing, hàm kiểm tra AABB được gọi hàng triệu lần mỗi khung hình (khi duyệt cây BVH). Do đó thuật toán cần được tối ưu tối đa về mặt số học:

### 4.1. Thay phép chia bằng phép nhân với Nghịch đảo hướng tia
Tính trước vector nghịch đảo $\text{inv\_d} = \left(\dfrac{1}{d_x}, \dfrac{1}{d_y}, \dfrac{1}{d_z}\right)$ cho mỗi tia:
$$t_{x1} = (x_{\min} - o_x) \cdot \text{inv\_d}_x, \quad t_{x2} = (x_{\max} - o_x) \cdot \text{inv\_d}_x$$

### 4.2. Tận dụng chuẩn số thực IEEE-754 (Xử lý $d_i = 0$ không cần phân nhánh)
- Khi tia sáng song song với một trục tọa độ ($d_x = 0$):
  - $\text{inv\_d}_x = \pm\infty$ (Infinity).
  - Phép nhân cho ra $\pm\infty$.
  - Hàm $\min/\max$ vẫn so sánh đúng khoảng cách mà không gây lỗi Crash hay `NaN` (nếu nguồn tia không nằm đúng trên mặt biên).

### 4.3. Loại bỏ phân nhánh điều kiện (Branchless Min/Max)
Sử dụng trực tiếp các chỉ thị phần cứng `std::min/std::max` hoặc hàm nội tại GPU (`fminf`, `fmaxf` trong CUDA) giúp pipeline GPU thực thi liên tục không bị gián đoạn do rẽ nhánh dự đoán sai.

---

## 5. Ví dụ Minh họa Số học Chi tiết

Cho hộp AABB có:
$$\mathbf{p}_{\min} = (1, 1, 1), \quad \mathbf{p}_{\max} = (3, 3, 3)$$
Và tia sáng xuất phát từ $\mathbf{o} = (0, 2, 2)$ với hướng $\vec{d} = (1, 0.5, 0)$:

### Bước 1: Tính khoảng giao cắt trên từng trục
- **Trục X:**
  $$t_{x1} = \frac{1 - 0}{1} = 1, \quad t_{x2} = \frac{3 - 0}{1} = 3 \implies [t_{x\_\text{near}}, t_{x\_\text{far}}] = [1, 3]$$
- **Trục Y:**
  $$t_{y1} = \frac{1 - 2}{0.5} = -2, \quad t_{y2} = \frac{3 - 2}{0.5} = 2 \implies [t_{y\_\text{near}}, t_{y\_\text{far}}] = [-2, 2]$$
- **Trục Z ($d_z = 0, o_z = 2 \in [1, 3]$):**
  $$t_{z1} = \frac{1 - 2}{0} = -\infty, \quad t_{z2} = \frac{3 - 2}{0} = +\infty \implies [t_{z\_\text{near}}, t_{z\_\text{far}}] = [-\infty, +\infty]$$

### Bước 2: Hợp nhất các khoảng
- $t_{\text{enter}} = \max(t_{x\_\text{near}}, t_{y\_\text{near}}, t_{z\_\text{near}}) = \max(1, -2, -\infty) = 1$
- $t_{\text{exit}} = \min(t_{x\_\text{far}}, t_{y\_\text{far}}, t_{z\_\text{far}}) = \min(3, 2, +\infty) = 2$

### Bước 3: Đánh giá kết quả
Vì $t_{\text{enter}} = 1 \le t_{\text{exit}} = 2$ và $t_{\text{exit}} > 0$:
$$\implies \text{Tia sáng CẮT hộp AABB trong khoảng } t \in [1, 2].$$

---

## 6. Chỉ thị phần cứng & Kỹ thuật Khử phân nhánh (Branchless) trên CUDA GPU

Trong bộ dò tia trên GPU (CUDA Path Tracer), hàm giao cắt Ray-AABB được thực thi hàng triệu đến hàng tỷ lần mỗi khung hình khi duyệt cây BVH. Việc tối ưu hóa ở cấp độ lệnh máy phần cứng (Hardware Instructions) là yếu tố sống còn để đạt tốc độ thời gian thực.

---

### 6.1. Tại sao phân nhánh (`if/else`) là "kẻ thù" số 1 trên GPU?

* **Mô hình SIMT & Warp:** GPU không xử lý từng luồng độc lập như CPU mà gom **32 threads** liền kề thành một nhóm gọi là **Warp**. Tất cả các thread trong 1 Warp bắt buộc phải thực thi **cùng một dòng lệnh tại cùng một chu kỳ xung nhịp**.
* **Hiện tượng Lệch luồng (Warp Divergence):**
  * Nếu trong Warp có một số tia sáng cắt AABB (nhánh `true`) và các tia khác trượt (nhánh `false`), GPU không thể rẽ hai nhánh song song.
  * GPU buộc phải **thực thi tuần tự (Serialized)**: Chạy nhánh `true` (các thread `false` bị tạm ngắt), rồi sau đó chạy nhánh `false` (các thread `true` bị tạm ngắt).
  * Hậu quả: Thời gian xử lý bị đội lên gấp đôi hoặc gấp nhiều lần, lãng phí tài nguyên tính toán của hàng chục nhân CUDA.

---

### 6.2. Các chỉ thị phần cứng & Intrinsics cốt lõi trong CUDA

Để loại bỏ hoàn toàn Warp Divergence, ta sử dụng các **lệnh nội tại phần cứng (Hardware Intrinsics)** của kiến trúc NVIDIA GPU:

#### 1. Lệnh tính Min/Max phần cứng: `__fminf(a, b)` và `__fmaxf(a, b)`
* **Bản chất phần cứng:** Trình biên dịch `nvcc` ánh xạ trực tiếp các hàm này sang lệnh máy SASS (Streaming Assembler) như `FMNMX`, `FMIN` hoặc `FMAX` trên Streaming Multiprocessor (SM).
* **Đặc điểm:**
  * Thực thi chỉ trong **đúng 1 chu kỳ xung nhịp (Single Cycle)**.
  * Không sinh ra lệnh nhảy điều kiện (`BRA - Branch`), không làm gián đoạn đường ống lệnh (Instruction Pipeline).
  * Tuân thủ chuẩn IEEE-754 khi xử lý các giá trị đặc biệt ($\pm\infty, \pm 0.0$).

#### 2. Kỹ thuật loại bỏ `swap(t0, t1)` hoàn toàn
* Trên CPU thông thường, người ta hay viết:
  ```cpp
  if (invD < 0.0f) swap(t0, t1); // Gây phân nhánh!
  ```
* Trên CUDA GPU, ta loại bỏ hoàn toàn câu lệnh `if` bằng cách tính trực tiếp:
  $$t_{\text{near}} = \text{\_\_fminf}(t_0, t_1)$$
  $$t_{\text{far}} = \text{\_\_fmaxf}(t_0, t_1)$$
  Bất kể $d_x$ âm hay dương, `__fminf` luôn tự động chọn giá trị nhỏ hơn và `__fmaxf` luôn chọn giá trị lớn hơn trong đúng 1 chu kỳ máy mà không cần kiểm tra điều kiện.

#### 3. Lệnh Nhân-Cộng kết hợp: `__fmaf_rn(x, y, z)` (Fused Multiply-Add)
* **Lệnh máy SASS:** `FFMA` (hoặc toán tử `fmaf(x, y, z)` = $x \cdot y + z$).
* **Lợi ích:**
  * Tính phép nhân và phép cộng gộp trong một chu kỳ xung nhịp duy nhất.
  * Chỉ làm tròn số đúng **1 lần duy nhất** ở kết quả cuối cùng (độ chính xác vô hạn ở bước trung gian), giúp triệt tiêu sai số trôi số học khi tính khoảng cách $t$.

#### 4. Cơ chế Predication (Thanh ghi cờ điều kiện 1-bit)
* Thay vì nhảy mã con trỏ lệnh (`Branch Jump`), GPU sử dụng các thanh ghi Predicate (như `@P0`, `@P1`).
* Lệnh được nạp thẳng vào execution unit, phần cứng chỉ đơn giản ghi kết quả nếu cờ bật hoặc bỏ qua nếu cờ tắt, loại bỏ hoàn toàn chi phí rẽ nhánh.

---

### 6.3. Cấu trúc Giải thuật Ray-AABB hoàn toàn Branchless (Không phân nhánh)

Toàn bộ quá trình kiểm tra giao cắt trên 3 trục $X, Y, Z$ được duỗi thẳng (unrolled) thành một luồng lệnh tính toán liên tục:

$$\begin{aligned}
t_{0x} &= (x_{\min} - o_x) \cdot \text{inv\_d}_x, & t_{1x} &= (x_{\max} - o_x) \cdot \text{inv\_d}_x \\
t_{\min} &= \text{\_\_fmaxf}(t_{\min}, \text{\_\_fminf}(t_{0x}, t_{1x})), & t_{\max} &= \text{\_\_fminf}(t_{\max}, \text{\_\_fmaxf}(t_{0x}, t_{1x})) \\[8pt]
t_{0y} &= (y_{\min} - o_y) \cdot \text{inv\_d}_y, & t_{1y} &= (y_{\max} - o_y) \cdot \text{inv\_d}_y \\
t_{\min} &= \text{\_\_fmaxf}(t_{\min}, \text{\_\_fminf}(t_{0y}, t_{1y})), & t_{\max} &= \text{\_\_fminf}(t_{\max}, \text{\_\_fmaxf}(t_{0y}, t_{1y})) \\[8pt]
t_{0z} &= (z_{\min} - o_z) \cdot \text{inv\_d}_z, & t_{1z} &= (z_{\max} - o_z) \cdot \text{inv\_d}_z \\
t_{\min} &= \text{\_\_fmaxf}(t_{\min}, \text{\_\_fminf}(t_{0z}, t_{1z})), & t_{\max} &= \text{\_\_fminf}(t_{\max}, \text{\_\_fmaxf}(t_{0z}, t_{1z}))
\end{aligned}$$

- **Kết quả trả về:** Biểu thức logic thuần túy $t_{\min} \le t_{\max}$.
- **Đặc tính thực thi trên CUDA:**
  - **0 lệnh phân nhánh (`BRA`)**.
  - **100% Warp Convergence:** Tất cả 32 threads trong Warp chạy cùng một số lượng chu kỳ xung nhịp như nhau mà không thread nào phải chờ đợi.
  - Tận dụng tối đa băng thông tính toán FP32 của các nhân CUDA Cores.

---

> [!NOTE] Ứng dụng trong Cây BVH (Bounding Volume Hierarchy)
> Thuật toán giao cắt Ray-AABB đóng vai trò bộ lọc thô (Broad-phase Filter). Nếu tia không cắt hộp AABB bao quanh một nhóm tam giác/vật thể phức tạp, thuật toán sẽ bỏ qua toàn bộ các phép tính giao cắt Möller–Trumbore đắt đỏ bên trong nhóm đó.
