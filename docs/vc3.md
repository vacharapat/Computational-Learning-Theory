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
