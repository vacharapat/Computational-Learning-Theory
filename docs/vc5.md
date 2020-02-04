{% include lib/mathjax.html %}
# VC Generalization Bound สำหรับ Consistent Hypothesis

จากหัวข้อที่แล้ว เราเห็นแล้วว่าอัตราการโตของ $\Pi_H(m)$ นั้นเป็น polynomial บน $m$
ซึ่งทำให้เรามีความหวังที่จะนำค่า $\Pi_H(m)$ มาใช้เป็นเครื่องแสดงความซับซ้อนของ hypothesis space $H$
แทนขนาดของ $H$ ได้ อย่างไรก็ดีเราไม่สามารถทำการวิเคราะห์ generalization bound ของ hypothesis
ที่ได้จากการเรียนรู้โดยใช้ union bound เช่นเดิมได้เนื่องจากขนาดของ $H$ อาจมีค่าเป็นอนันต์  ในหัวข้อนี้เราจะมาดูวิธีการวิเคราะห์ generalization bound ให้อยู่ในรูปของ $\Pi_H(m)$ แทน

## Consistent hypothesis
เราจะเริ่มพิจารณาในกรณีที่เราทราบว่ามี concept เป้าหมาย $c\in H$ อยู่จริง และเราทำการเรียนรู้โดยการหา
hypothesis $h\in H$ ที่ consistent กับตัวอย่างข้อมูลทั้งหมดที่ได้มา ซึ่งแทนด้วย $$S=\{(x_1,y_1),\dots,(x_m,y_m)\}$$

หากเราต้องการให้ hypothesis $h$ ที่ได้เป็นผลจากการเรียนรู้ของเรามี error $R(h)\leq\epsilon$
เราสามารถทำได้โดยหาขอบเขตของความน่าจะเป็นที่จะมี hypothesis อย่างน้อยตัวหนึ่งใน $H$ ที่มี error มากกว่า $\epsilon$
แต่ยังสามารถเป็นคำตอบจากอัลกอริทึมการเรียนรู้ของเราได้ นั่นคือ hypothesis ดังกล่าวต้อง consistent กับ $S$ ด้วย
เรากล่าวได้อีกอย่างว่าเป้าหมายของเราคือการหาขอบเขตของความน่าจะเป็น

$$
\Pr[\exists h\in H: R(h)>\epsilon \text{ และ } h \text{ consistent กับ } S]
$$

ในกรณีที่ $H$ มีขนาดจำกัด เราสามารถจำกัดขอบเขตของความน่าจะเป็นนี้ได้โดยหาความน่าจะเป็นที่ hypothesis
$h$ ที่ $R(h)>\epsilon$ จะ consistent กับ $S$ และใช้ union bound จำกัดขอบเขตที่จะเกิดเหตุการณ์ดังกล่าวกับ
hypothesis อย่างน้อยหนึ่งตัวได้ แต่เมื่อ $H$ มีขนาดเป็นอนันต์วิธีการนี้ก็ไม่สามารถทำได้แล้ว

## Ghost sample

เทคนิคที่เราจะใช้ในการวิเคราะห์ generalization bound เมื่อ $H$ มีขนาดเป็นอนันต์คือการลดรูป hypothesis space
$H$ ที่สนใจให้อยู่ในรูปแบบที่มีขนาดจำกัด สมมติให้ $S'$ เป็นเซตของตัวอย่างข้อมูล $m$
ตัวอีกชุดหนึ่งที่สมาชิกแต่ละตัวถูกสุ่มแบบ i.i.d. จากการกระจายตัวแบบเดียวกันกับ $S$
สำหรับ $h\in H$ ใด ๆ เราจะใช้ empirical error
$$\widehat{R}_{S'}(h)$$
เป็นตัวแทนของ $R(h)$ ในการวิเคราะห์
ซึ่งจะเห็นว่าถึงแม้ขนาดของ $H$ จะเป็นอนันต์ก็ตาม
หากเราพิจารณาผลลัพธ์ของ $h\in H$ ใด ๆ บน $S'$ ที่มีจำนวนจำกัด จำนวนของผลลัพธ์ที่เกิดขึ้นได้จะมีจำนวนจำกัดเสมอ
ซึ่งทำให้เราสามารถวิเคราะห์ขอบเขตบนของความน่าจะเป็นที่ต้องการโดยใช้ union bound เช่นเดิมได้
เราเรียก $S'$ นี้ว่า _ghost sample_ เนื่องจากเป็นตัวอย่างข้อมูลที่ไม่มีอยู่จริง
แต่เราสร้างขึ้นมาสำหรับใช้ในการวิเคราะห์เท่านั้น

ขั้นแรกเราจะแสดงความสัมพันธ์ระหว่าง $R(h)$ กับ
$$\widehat{R}_{S'}(h)$$
ก่อน โดยจะแสดงให้เห็นว่าสำหรับ $h\in H$ ที่ $R(h)>\epsilon$ เราจะได้ว่า
$$\widehat{R}_{S'}(h)>\epsilon m/2$$
ด้วยความน่าจะเป็นไม่น้อยกว่า $1/2$

สมมติให้ $r = R(h)$ เราจะได้ว่า
$$\mathbb{E}[\widehat{R}_{S'}(h)] = rm > \epsilon m$$ จาก Chebyshev's inequality ที่กล่าวว่า
สำหรับตัวแปรสุ่ม $X$ ใด ๆ

$$
\Pr[|X - \mathbb{E}[X]|\geq a]\leq \frac{Var[X]}{a^2}
$$

เราจะได้ว่า

$$
\begin{split}
\Pr[\widehat{R}_{S'}(h)\leq\frac{\epsilon m}{2}]&\leq\Pr[|\widehat{R}_{S'}(h)- rm|\geq\frac{\epsilon m}{2}]\\
&\leq \frac{4Var[\widehat{R}_{S'}(h)]}{\epsilon^2m^2}
\end{split}
$$

เนื่องจากตัวแปรสุ่ม
$$\widehat{R}_{S'}(h)$$
นั้นมีการกระจายตัวแบบ binomial เราจะได้ว่า
$Var[\widehat{R}_{S'}(h)] = mr(1-r)\leq m/4$ เมื่อ $0\leq r\leq 1$
ดังนั้น

$$
\Pr[\widehat{R}_{S'}(h)\leq\frac{\epsilon m}{2}]\leq \frac{1}{\epsilon^2m}
$$

ถ้าเรากำหนดให้ $m\geq 2/\epsilon^2$ เราจะได้ว่า

$$
\Pr[\widehat{R}_{S'}(h)\leq\frac{\epsilon m}{2}]\leq\frac{1}{2}
$$

คราวนี้สังเกตว่าถ้าเราสนใจเหตุการณ์ที่มี $h\in H$ อย่างน้อยหนึ่งตัวที่ consistent กับ $S$ แต่ทำนายผลลัพธ์ใน
$S'$ ผิดอย่างน้อย $\epsilon m/2$ ตัว เราจะได้ว่า

$$
\begin{split}
\Pr[\exists h\in H:& h \text{ consistent กับ } S \text{ และ } \widehat{R}_{S'}(h)\geq \frac{\epsilon m}{2}]\\
&\geq\Pr[\exists h\in H: R(h)>\epsilon, h \text{ consistent กับ } S \text{ และ } \widehat{R}_{S'}(h)\geq \frac{\epsilon m}{2}] \\
&=\Pr[\exists h\in H: R(h)>\epsilon \text{ และ } h \text{ consistent กับ } S]\cdot\Pr[\widehat{R}_{S'}(h)\geq\frac{\epsilon m}{2} | R(h)>\epsilon]\\
&\geq \frac{1}{2}\Pr[\exists h\in H: R(h)>\epsilon \text{ และ } h \text{ consistent กับ } S]
\end{split}
$$

หรือก็คือ

$$
\begin{split}
\Pr[\exists h\in H:& R(h)>\epsilon \text{ และ } h \text{ consistent กับ } S]\\
&\leq 2 \Pr[\exists h\in H: h \text{ consistent กับ } S \text{ และ } \widehat{R}_{S'}(h)\geq \frac{\epsilon m}{2}]
\end{split}
$$

ซึ่งทำให้เห็นว่า หากเราต้องการจำกัดขอบเขตความน่าจะเป็นที่จะมี hypothesis $h$ บางตัวที่ consistent กับ $S$
ทั้งที่ $R(h)>\epsilon$ เราสามารถทำได้โดยจำกัดขอบเขตความน่าจะเป็นที่จะมี $h$ ที่ consistent กับ $S$
แต่ทำนายผลลัพธ์ใน $S'$ ผิดอย่างน้อย $\epsilon m/2$ ตัว ซึ่งเหตุการณ์หลังนี้สามารถวิเคราะห์ได้ง่ายกว่า

## Permutation ของตัวอย่างข้อมูล

ถึงตรงนี้ เป้าหมายของเราคือการหาขอบเขตความน่าจะเป็นที่จะมี $h\in H$ ที่ทำนายผลลัพธ์ใน $S$ ได้ถูกต้องทั้งหมด
แต่ทำนายผลลัพธ์ใน $S'$ ผิดอย่างน้อย $\epsilon m/2$ ตัว จุดสำคัญที่ทำให้เราวิเคราะห์ขอบเขตดังกล่าวนี้ได้ก็คือ
ถึงแม้ว่า $H$ จะมีขนาดเป็นอนันต์ แต่หากเราพิจารณา hypothesis ใน $H$ ผ่านตัวอย่างข้อมูลใน $S\cup S'$ เท่านั้น
จะได้ว่าจำนวนวิธีการจำแนกข้อมูล $2m$ ตัวนี้ออกเป็นสองคลาสโดยใช้ hypothesis ใน $H$ จะไม่มีทางเกิน
$\Pi_H(2m)$ แน่นอน นั่นคือ ถ้าเราให้ $H_{S\cup S'}$ แทนเซตของ dichotomy ทั้งหมดของ $H$ บนตัวอย่างข้อมูลใน
$S\cup S'$ (หรือเซตของ hypothesis ที่เป็นไปได้ทั้งหมด ใน $H$ เมื่อพิจารณาบน input space $S\cup S'$) เราจะได้ว่า $|H_{S\cup S'}|\leq \Pi_{H}(2m)$ นอกจากนี้ สังเกตว่าเหตุการณ์ที่มี hypothesis บางตัวใน $H$
ที่ consistent กับ $S$ แต่ทำนายผลลัพธ์ใน $S'$ ผิดอย่างน้อย $\epsilon m/2$ ตัว ก็คือเหตุการณ์เดียวกันกับการมี
hypothesis ใน $H_{S\cup S'}$ ที่ให้ผลแบบเดียวกัน ดังนั้นเราจึงได้ว่า

$$
\begin{split}
\Pr[\exists h\in H:& h \text{ consistent กับ } S \text{ และ } \widehat{R}_{S'}(h)\geq\frac{\epsilon m}{2}]\\
=\Pr[\exists h\in H_{S\cup S'}:& \widehat{R}_S(h)=0 \text{ และ } \widehat{R}_{S'}(h)\geq\frac{\epsilon m}{2}]
\end{split}
$$
