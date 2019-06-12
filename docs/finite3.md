{% include lib/mathjax.html %}
# การเรียนรู้ Boolean Conjunction ด้วย Inconsistent Hypothesis

จากหัวข้อที่แล้วเราสามารถปรับปรุงอัลกอริทึมการเรียนรู้ปัญหา Boolean Conjunction ให้เรียนรู้ได้โดยมี
sample complexity เป็น $O(\frac{1}{\epsilon}\left(size(c)\log n\log\frac{size(c)\log n}{\epsilon} +\log\frac{1}{\delta}\right))$
ในหัวข้อนี้เราจะปรับปรุงอัลกอริทึมการเรียนรู้อีกเล็กน้อยเพื่อให้ได้ขอบเขตของ sample complexity ที่ดีขึ้นอีก
โดยแนวคิดเบื้องหลังการปรับปรุงนี้คือ ในความเป็นจริงเราอาจไม่จำเป็นที่จะต้องหา hypothesis ที่สอดคล้องกับตัวอย่างข้อมูลทั้งหมดเสมอไป
เช่นในอัลกอริทึมการเรียนรู้ปัญหา Boolean Conjunction ของเรานี้ ในขั้นตอนการเลือก literal ให้ครอบคลุม
negative example โดยใช้การเลือกแบบ greedy  นั้น แทนที่เราจะวนรอบเลือก literal จนกระทั่งรับประกันว่า
negative example ทั้งหมดทุกครอบคลุมแล้ว เราอาจวนรอบเลือก literal เพื่อให้มั่นใจแค่ว่าอาจมี negative example
ที่ไม่สอดคล้องอยู่ไม่มากนัก โดยเราจะมาวิเคราะห์กันว่า หากเราวนรอบเลือก literal จนรับประกันได้ว่ามี
negative example ที่ไม่สอดคล้องอยู่ไม่เกิน $\epsilon m/2$ ตัว ก็เพียงพอที่จะเรียนรู้ได้สำเร็จแล้ว

พิจารณาเมื่อเรากำหนดให้ขั้นตอนการเลือก literal แบบ greedy ถูกทำจนกระทั่งจำนวน negative example
ที่ยังไม่ถูกครอบคลุมเหลือไม่เกิน $\epsilon m/2$ เราจะได้ว่าการวนรอบนี้จะสิ้นสุดเมื่อ

$$
|U_i|\leq m\left(1-\frac{1}{OPT}\right)^i<me^{-i/OPT}\leq \frac{\epsilon m}{2}
$$

ซึ่งจะเป็นจริงเมื่อ

$$
i = OPT\ln\frac{2}{\epsilon}\leq size(c)\ln\frac{2}{\epsilon}
$$

ดังนั้นจะเห็นว่า ด้วยวิธีนี้อัลกอริทึมของเราจะให้ผลลัพธ์เป็น hypothesis ที่มีขอบเขตของจำนวน literal เป็น
$size(c)\ln\frac{2}{\epsilon}$ แทนที่จะเป็น $size(c)\ln m$ เนื่องจาก literal แต่ละตัวสามารถระบุได้โดยใช้พื้นที่
$\log_2 (2n)$ บิต เราจึงได้ว่า hypothesis space ของอัลกอริทึมที่ปรับปรุงใหม่นี้มีขนาดไม่เกิน

$$
2^{size(c)\ln(2/\epsilon)\log_2(2n)}
$$

คราวนี้เราต้องมาวิเคราะห์ดูว่าสำหรับ hypothesis $h$ ที่ $R(h)>\epsilon$ นั้น
มีความน่าจะเป็นมากน้อยแค่ไหนที่จะกลายมาเป็นคำตอบของอัลกอริทึมของเราได้
ในการวิเคราะห์ส่วนนี้เราจะใช้การจำกัดขอบเขตตัวหนึ่งที่สำคัญมากในทฤษฎีความน่าจะเป็น ซึ่งมีชื่อเรียกว่า
_ขอบเขตของ Chernoff_ หรือ Chernoff Bound ซึ่งกล่าวไว้ดังนี้

## ขอบเขตของ Chernoff
ให้ $X_1,\dots,X_m$ เป็นตัวแปรสุ่มที่มีค่าเป็น 1 ด้วยความน่าจะเป็น $p$ และเป็น 0 ด้วยความน่าจะเป็น $1-p$ เหมือนกันทั้งหมด
ถ้าให้ $X=\sum_{i=1}^mX_i$ และให้ $\mu=\text{E}[X]=mp$ เราจะได้ว่า

$$
\Pr[X\geq(1+\gamma)\mu]\leq e^{-\frac{\gamma^2\mu}{3}}, \gamma > 0\\
$$

และ

$$
\Pr[X\leq(1-\gamma)\mu]\leq e^{-\frac{\gamma^2\mu}{2}}, 0 < \gamma < 1
$$

ดังนั้น สมมติให้ $h$ เป็น hypothesis ที่ $R(h)>\epsilon$ และให้ $W$ แทนจำนวนตัวอย่างข้อมูลใน $S$
ที่ไม่สอดคล้องกันกับ $h$ เราจะได้ว่า $\mu=\text{E}[W]= mR(h)>m\epsilon$ ดังนั้น

$$
\begin{split}
\Pr[W<\frac{\epsilon m}{2}] &= \Pr[W<(1-\frac{1}{2})\epsilon m]\\
&\leq \Pr[W<(1-\frac{1}{2})\mu]\\
&\leq e^{-\mu/8}\\
&= e^{-mR(h)/8}\\
&\leq e^{-m\epsilon/8}
\end{split}
$$

จากตรงนี้เราสรุปได้ว่า สำหรับ hypothesis $h$ ที่มี $R(h)>\epsilon$ ความน่าจะเป็นที่ $h$ จะสอดคล้องกับตัวอย่างข้อมูลใน $S$
อย่างน้อย $(1-\epsilon/2)m$ ตัว จะมีค่าไม่เกิน $e^{-m\epsilon/8}$ ดังนั้น ความน่าจะเป็นที่จะมี hypothesis ดังกล่าวอย่างน้อยหนึ่งตัวจะมีค่าไม่เกิน

$$
|H|e^{-m\epsilon/8} = 2^{size(c)\ln(2/\epsilon)\log_2(2n)}e^{-m\epsilon/8}
$$

ถ้าเราอยากให้ความน่าจะเป็นดังกล่าวมีไม่เกิน $\delta$ ก็ทำได้โดยกำหนดให้

$$
2^{size(c)\ln(2/\epsilon)\log_2(2n)}e^{-m\epsilon/8}\leq \delta
$$

ซึ่งจะได้

$$
size(c)\ln\frac{2}{\epsilon}\frac{\ln (2n)}{\ln 2}\ln 2 - \frac{m\epsilon}{8}\leq\ln \delta
$$

หรือได้เป็น

$$
m\geq\frac{8}{\epsilon}\left(size(c)\ln\frac{2}{\epsilon}\ln(2n) +\ln\frac{1}{\delta}\right)
$$
