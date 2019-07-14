{% include lib/mathjax.html %}
# VC-Dimension

จากหัวข้อที่แล้ว จะเห็นว่าหากกำหนดจำนวนของตัวอย่างข้อมูลมาให้เท่ากับ $m$ เราสามารถพิจารณาพลังในการจำแนกข้อมูล
$m$ ตัวของ hypothesis space $H$ ใด ๆ ได้จากค่าของ growth function $\Pi_H(m)$
ในหัวข้อนี้เราจะมาทำความรู้จักกับ _VC-dimension_ (Vapnik-Chervonenkis dimension)
ซึ่งเป็นปริมาณเชิง combinatorial ที่มีความสัมพันธ์กับ growth function เป็นอย่างมาก
และสามารถใช้บอกความซับซ้อนของ hypothesis space ต่าง ๆ ได้เช่นกันไม่ว่า hypothesis space นั้นจะมีขนาดจำกัดหรือไม่
เราจะได้เห็นต่อไปว่า VC-dimension นี้มีบทบาทอย่างมากจนถือได้ว่าเป็นหนึ่งในหัวใจสำคัญของทฤษฎีการเรียนรู้เชิงคำนวณ

ในการนิยาม VC-dimension ของ hypothesis space $H$ เราจะทบทวนเกี่ยวกับ dichotomy และการ shatter กันก่อน
สำหรับ hypothesis space $H$ ใด ๆ dichotomy ของ $H$ บนตัวอย่างข้อมูล $$\{x_1,\dots,x_m\}$$
คือวิธีการที่เป็นไปได้ในการ label $x_i$ แต่ละตัวด้วย hypothesis ที่อยู่ใน $H$
ถ้าหากสำหรับการ label $x_i$ ทั้ง $2^m$ แบบนั้น มี hypothesis ใน $H$ ที่ให้ label สอดคล้องทั้งหมด
เราจะกล่าวว่า $H$ shatter  $$\{x_1,\dots,x_m\}$$

**นิยาม** VC-dimension ของ hypothesis space $H$ คือขนาดของเซตตัวอย่างข้อมูล $S$ ที่ใหญ่ที่สุดที่ถูก shatter ได้โดย $H$
นั่นคือ ถ้าให้ $d_H$ แทน VC-dimension ของ $H$

$$
d_H = \max_{S \text{ shattered by } H}|S|
$$

จากนิยามแสดงว่าจะต้องมีเซต $S$ ของตัวอย่างข้อมูลจำนวน $d_H$ อย่างน้อยเซตหนึ่งที่ $H$ shatter $S$
และหากพิจารณาเซตของตัวอย่างข้อมูลจำนวน $d_H+1$ ตัวขึ้นไป ไม่ว่าจะเป็นเซตใดก็จะไม่ถูก shatter โดย $H$ ได้แน่นอน
ดังนั้น เราอาจนิยาม VC-dimension $d_H$ ในอีกมุมหนึ่งได้เป็นค่า $m$ ที่มากที่สุดที่มี growth function เท่ากับ $2^m$ นั่นเอง
หรือเขียนได้เป็น

$$
d_H = \max\{m:\Pi_H(m)=2^m\}
$$

และถ้าสำหรับ $m\geq 0$ ใด ๆ  $\Pi_H(m)=2^m$ เสมอ เราจะกล่าวว่า $d_H=\infty$

ในการแสดงว่า VC-dimension ของ $H$ มีค่าเท่ากับ $d$ นั้น เราทำได้โดยแสดงให้เห็นว่ามีเซตของตัวอย่างข้อมูล $d$
ตัวอย่างน้อยชุดหนึ่ง ที่ถูก shatter ได้จาก $H$ (นั่นคือ แสดงว่า $d_H\geq d$)
และแสดงให้เห็นว่าสำหรับตัวอย่างข้อมูลใด ๆ ที่มีจำนวน $d+1$ ตัวจะไม่สามารถถูก shatter จาก $H$ ได้เลย
(นั่นคือ แสดงว่า $d_H<d$)

ต่อจากนี้เราลองมาดูการวิเคราะห์ VC-dimension ของตัวอย่าง hypothesis space ง่าย ๆ จำนวนหนึ่งเพื่อให้เข้าใจมากขึ้น

## Positive rays
ในกรณีของ $H$ ที่เป็นเซตของ positive rays สังเกตว่าสำหรับตัวอย่างข้อมูลเพียงจุดเดียว เราสามารถสร้าง hypothesis $h$
ที่ทำให้ตัวอย่างข้อมูลดังกล่าวมี label เป็น 1 หรือ 0 ก็ได้ดังรูปต่อไปนี้ แสดงว่า VC-dimension ของ positive rays
มีค่าไม่น้อยกว่า 1 หรือ $d_H\geq 1$

<p align="center">
<img width="400" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/positiverays_vc1.png">
</p>

สำหรับตัวอย่างข้อมูลที่มีสองจุด $x_1$ และ $x_2$ ถ้า $x_1=x_2$ เราจะได้ว่า label ของทั้งสองจุดนี้จะต้องเหมือนกันเสมอ นั่นทำให้ dichotomy ที่สองจุดนี้มี label ต่างกันไม่สามารถเกิดขึ้นได้
แสดงว่า $H$ ไม่ shatter เซตของจุดทั้งคู่นี้ สำหรับกรณีที่ $x_1\neq x_2$ สมมติให้ $x_1<x_2$ จะเห็นว่าเราไม่สามารถ
หา positive rays ที่ทำให้ได้ dichotomy ตามรูปต่อไปนี้ได้เลย ดังนั้น $H$ ก็ไม่ shatter เซตของจุดทั้งคู่นี้เช่นกัน
จากตรงนี้จะเห็นว่าเซตของตัวอย่างข้อมูลจำนวนสองจุดใด ๆ ไม่มีทางถูก shatter จาก $H$ ได้เลย
นั่นแสดงว่า $d_H<2$

<p align="center">
<img width="200" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/positiverays_vc2.png">
</p>

เนื่องจาก $d_H\heq 1$ และ $d_H<2$ เราจึงได้ว่าเมื่อ $H$ เป็นเซตของ positive rays
$H$ จะมี VC-dimension เป็น $d_H=1$
