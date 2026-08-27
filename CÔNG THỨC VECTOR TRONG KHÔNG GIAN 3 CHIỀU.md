

## 1. Định nghĩa và Tọa độ cơ bản
Cho $\vec{a} = (a_1, a_2, a_3)$, $\vec{b} = (b_1, b_2, b_3)$ và hai điểm $A(x_A, y_A, z_A)$, $B(x_B, y_B, z_B)$:

- **Vector đơn vị hệ trục tọa độ:** $\vec{i} = (1, 0, 0)$, $\vec{j} = (0, 1, 0)$, $\vec{k} = (0, 0, 1)$
- **Phân tích theo vector đơn vị:** 
  $$\vec{a} = a_1\vec{i} + a_2\vec{j} + a_3\vec{k}$$
- **Vector nối 2 điểm:** 
  $$\vec{AB} = (x_B - x_A, y_B - y_A, z_B - z_A)$$
- **Độ dài vector:** 
  $$|\vec{a}| = \sqrt{a_1^2 + a_2^2 + a_3^2}$$
- **Khoảng cách 2 điểm:** 
  $$AB = |\vec{AB}| = \sqrt{(x_B - x_A)^2 + (y_B - y_A)^2 + (z_B - z_A)^2}$$

---

## 2. Các phép toán đại số cơ bản
- **Cộng / Trừ:** 
  $$\vec{a} \pm \vec{b} = (a_1 \pm b_1, a_2 \pm b_2, a_3 \pm b_3)$$
- **Nhân với một số ($k \in \mathbb{R}$):** 
  $$k\vec{a} = (ka_1, ka_2, ka_3)$$
- **Hai vector cùng phương ($\vec{b} \neq \vec{0}$):** 
  $$\vec{a} \parallel \vec{b} \iff \exists k \in \mathbb{R}: \vec{a} = k\vec{b} \iff \frac{a_1}{b_1} = \frac{a_2}{b_2} = \frac{a_3}{b_3}$$

---

## 3. Chuẩn hóa Vector (Unit Vector)
- **Công thức tổng quát:** 
  $$\hat{u} = \frac{\vec{a}}{|\vec{a}|}$$
- **Biểu thức tọa độ ($\vec{a} \neq \vec{0}$):** 
  $$\hat{u} = \left( \frac{a_1}{\sqrt{a_1^2 + a_2^2 + a_3^2}}, \frac{a_2}{\sqrt{a_1^2 + a_2^2 + a_3^2}}, \frac{a_3}{\sqrt{a_1^2 + a_2^2 + a_3^2}} \right)$$
- **Tính chất:** $|\hat{u}| = 1$ và $\hat{u}$ cùng hướng với $\vec{a}$

---

## 4. Tích vô hướng (Dot / Scalar Product)
- **Định nghĩa:** 
  $$\vec{a} \cdot \vec{b} = |\vec{a}| \cdot |\vec{b}| \cdot \cos(\vec{a}, \vec{b})$$
- **Biểu thức tọa độ:** 
  $$\vec{a} \cdot \vec{b} = a_1b_1 + a_2b_2 + a_3b_3$$
- **Góc giữa 2 vector ($\vec{a}, \vec{b} \neq \vec{0}$):** 
  $$\cos(\vec{a}, \vec{b}) = \frac{\vec{a} \cdot \vec{b}}{|\vec{a}| \cdot |\vec{b}|} = \frac{a_1b_1 + a_2b_2 + a_3b_3}{\sqrt{a_1^2 + a_2^2 + a_3^2} \cdot \sqrt{b_1^2 + b_2^2 + b_3^2}}$$
- **Điều kiện vuông góc (trực giao):** 
  $$\vec{a} \perp \vec{b} \iff \vec{a} \cdot \vec{b} = 0 \iff a_1b_1 + a_2b_2 + a_3b_3 = 0$$

---

## 5. Tích có hướng (Cross / Vector Product)
- **Biểu thức tọa độ:** 
  $$\vec{a} \times \vec{b} = [\vec{a}, \vec{b}] = \left( \begin{vmatrix} a_2 & a_3 \\ b_2 & b_3 \end{vmatrix}, \begin{vmatrix} a_3 & a_1 \\ b_3 & b_1 \end{vmatrix}, \begin{vmatrix} a_1 & a_2 \\ b_1 & b_2 \end{vmatrix} \right) = (a_2b_3 - a_3b_2, a_3b_1 - a_1b_3, a_1b_2 - a_2b_1)$$
- **Độ dài tích có hướng:** 
  $$|\vec{a} \times \vec{b}| = |\vec{a}| \cdot |\vec{b}| \cdot \sin(\vec{a}, \vec{b})$$
- **Tính chất:**
  - $(\vec{a} \times \vec{b}) \perp \vec{a}$ và $(\vec{a} \times \vec{b}) \perp \vec{b}$
  - $\vec{a} \times \vec{b} = -(\vec{b} \times \vec{a})$
  - $\vec{a} \parallel \vec{b} \iff \vec{a} \times \vec{b} = \vec{0}$

---

## 6. Tích hỗn tạp (Triple Scalar Product)
- **Biểu thức tọa độ:** 
  $$(\vec{a} \times \vec{b}) \cdot \vec{c} = [\vec{a}, \vec{b}] \cdot \vec{c} = \begin{vmatrix} a_1 & a_2 & a_3 \\ b_1 & b_2 & b_3 \\ c_1 & c_2 & c_3 \end{vmatrix}$$
- **Điều kiện đồng phẳng của 3 vector:** 
  $$\vec{a}, \vec{b}, \vec{c} \text{ đồng phẳng} \iff (\vec{a} \times \vec{b}) \cdot \vec{c} = 0$$

---

## 7. Ứng dụng hình học
- **Diện tích tam giác $ABC$:** 
  $$S_{\triangle ABC} = \frac{1}{2} |\vec{AB} \times \vec{AC}|$$
- **Diện tích hình bình hành $ABCD$:** 
  $$S_{ABCD} = |\vec{AB} \times \vec{AD}|$$
- **Thể tích khối tứ diện $ABCD$:** 
  $$V_{ABCD} = \frac{1}{6} |(\vec{AB} \times \vec{AC}) \cdot \vec{AD}|$$
- **Thể tích khối hộp $ABCD.A'B'C'D'$:** 
  $$V = |(\vec{AB} \times \vec{AD}) \cdot \vec{AA'}|$$
- **Khoảng cách từ điểm $M$ đến đường thẳng $\Delta$ (qua $A$, VTCP $\vec{u}$):**
  $$d(M, \Delta) = \frac{|\vec{AM} \times \vec{u}|}{|\vec{u}|}$$
- **Khoảng cách giữa hai đường thẳng chéo nhau ($\Delta_1$ qua $A_1$, VTCP $\vec{u}_1$; $\Delta_2$ qua $A_2$, VTCP $\vec{u}_2$):**
  $$d(\Delta_1, \Delta_2) = \frac{|(\vec{u}_1 \times \vec{u}_2) \cdot \vec{A_1A_2}|}{|\vec{u}_1 \times \vec{u}_2|}$$

---

## 8. Tọa độ các điểm đặc biệt
- **Trung điểm $M$ của đoạn thẳng $AB$:** 
  $$M\left(\frac{x_A + x_B}{2}, \frac{y_A + y_B}{2}, \frac{z_A + z_B}{2}\right)$$
- **Trọng tâm $G$ của tam giác $ABC$:** 
  $$G\left(\frac{x_A + x_B + x_C}{3}, \frac{y_A + y_B + y_C}{3}, \frac{z_A + z_B + z_C}{3}\right)$$
- **Trọng tâm $G$ của tứ diện $ABCD$:** 
  $$G\left(\frac{x_A + x_B + x_C + x_D}{4}, \frac{y_A + y_B + y_C + y_D}{4}, \frac{z_A + z_B + z_C + z_D}{4}\right)$$
- **Điểm $M$ chia đoạn thẳng $AB$ theo tỉ số $k$ ($\vec{MA} = k\vec{MB}, k \neq 1$):** 
  $$M\left(\frac{x_A - kx_B}{1 - k}, \frac{y_A - ky_B}{1 - k}, \frac{z_A - kz_B}{1 - k}\right)$$