{% include lib/mathjax.html %}
# การเรียนรู้แบบ Agnostic PAC

เนื่องจากในแบบจำลองการจำแนกข้อมูลแบบ stochastic นี้ เราไม่สามารถหา concept เป้าหมายที่มี
error เป็นศูนย์ได้ ดังนั้น สำหรับ hypothesis space $H$ ใด ๆ เราจะมุ่งเป้าไปที่การหา hypothesis $h\in H$
ที่มี error $R(h)$ ใกล้เคียงค่าที่น้อยที่สุดที่เป็นไปได้ แนวคิดนี้ทำให้เราสามารถนิยามอัลกอริทึมการเรียนรู้แบบ
agnostic-PAC ได้ดังนี้

สำหรับ hypothesis space $H$ เราจะกล่าวว่าอัลกอริทึม $A$ เป็นอัลกอริทึมการเรียนรู้แบบ agnostic-PAC
ถ้าสำหรับค่า $\epsilon>0$ และ $\delta>0$ ใด ๆ และสำหรับการกระจายของข้อมูล $D$ บน $X\times Y$ ใด ๆ
เมื่ออัลกอริทึม $A$ รับตัวอย่างข้อมูล $$S=\{(x_1,y_1),\dots,(x_m,y_m)\}$$ จาก $D$
อัลกอริทึม $A$ จะให้ผลลัพธ์เป็น hypothesis $h_S$ ที่สอดคล้องกับเงื่อนไขต่อไปนี้ เมื่อ $m\geq m_0$
โดย $m_0$ เป็น polynomial บน $1/\epsilon$, $1/\delta$, $n$ และ $size(h^*)$

$$
\Pr[R(h_S)-R(h^*)]\leq\epsilon]\geq 1-\delta
$$

โดย $n$ เป็นขนาดของ input $x\in X$ และ $h^*$ เป็น hypothesis ที่มีค่า error น้อยที่สุดใน $H$ หรือ

$$
h^* = \arg\min_{h\in H}R(h)
$$

ถ้าอัลกอริทึม $A$ สามารถให้ผลลัพธ์ดังกล่าวได้โดยใช้เวลาทำงานเป็น polynomial บน $1/\epsilon$,
$1/\delta$, $n$ และ $size(h^*)$ เราจะเรียกว่าเป็นอัลกอริทึมการเรียนรู้แบบ agnostic ที่มีประสิทธิภาพ

## Inconsistent Hypothesis
ในการเรียนรู้บน stochastic scenario นี้ เราไม่สามารถรับประกันได้ว่าจะสามารถหา hypothesis $h\in H$
ที่สอดคล้องกับตัวอย่างข้อมูลทั้งหมดใน $S$ ได้เสมอ อย่างไรก็ดี เราได้เห็นตัวอย่างใน [การเรียนรู้ Boolean Conjunction ด้วย Inconsistent Hypothesis](https://vacharapat.github.io/Computational-Learning-Theory/docs/finite3)
มาแล้วว่า hypothesis ที่ไม่ได้สอดคล้องกับตัวอย่างข้อมูลทั้งหมด แต่มีความผิดพลาดบนตัวอย่างข้อมูลน้อย
ก็มีประโยชน์สำหรับเราได้เช่นกัน

ในหัวข้อนี้เราจะแสดงให้เห็นว่าในความเป็นจริง สำหรับ hypothesis $h\in H$ ใด ๆ
เราพอที่จะสามารถหาขอบเขตของ error $R(h)$ จาก empirical error $\hat{R}(h)$ ได้
เมื่อ $\hat{R}(h)$ มีนิยามดังนี้

สำหรับเซตของตัวอย่างข้อมูล $$S=\{(x_1,y_1),\dots,(x_m,y_m)\}$$

$$
\hat{R}(h)=\frac{1}{m}|\{(x,y)\in S: h(x)\neq y\}| = \frac{1}{m}\sum_{i=1}^m1_{h(x_i)\neq y}
$$
