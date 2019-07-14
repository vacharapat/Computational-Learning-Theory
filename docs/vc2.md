{% include lib/mathjax.html %}
# Growth Function

หลังจากที่เราได้รู้จัก dichotomy กันมาแล้ว สังเกตว่าเมื่อเรากำหนดเซตของตัวอย่างข้อมูลไว้
hypothesis space แต่ละตัวอาจมีจำนวน dichotomy แตกต่างกันได้ โดย hypothesis space
ที่มีความซับซ้อนมากก็จะสามารถสร้างจำนวน dichotomy ได้มากกว่า hypothesis space ที่มีความซับซ้อนน้อย
จากตรงนี้ทำให้เราเห็นว่า จำนวน dichotomy ที่สร้างได้จาก hypothesis space นั้นสามารถเป็นตัวแทนในการบอกความซับซ้อนของ
hypothesis space ที่เราสนใจได้ จึงเป็นที่มาของ growth function ซึ่งมีนิยามดังนี้

**นิยาม** growth function ของ hypothesis space $H$ บนข้อมูล $m$ ตัว เขียนแทนด้วย
$\Pi_H(m)$ มีค่าเท่ากับ

$$
\Pi_H(m)=\max_{x_1,\dots,x_m\in X}|H(x_1,\dots,x_m)|
$$  

หรือกล่าวได้ว่า $\Pi_H(m)$ คือจำนวน dichotomy ที่มากที่สุดบนตัวอย่างข้อมูล $m$ จุดใด ๆ
ที่สามารถสร้างได้จาก $H$ โดยในการคำนวณ $\Pi_H(m)$ นั้น เราต้องพิจารณาตัวอย่างข้อมูล $m$ จุดทุกรูปแบบ
และตอบจำนวน dichotomy ของรูปแบบที่จำแนกได้หลากหลายที่สุด สังเกตว่า $\Pi_H(m)$ นี้จะเป็นเหมือนขอบเขตบนของขนาดของ $H$
เมื่อ input space ของเราเป็น subspace ของ $X$ ที่มีขนาดเท่ากับ $m$ ซึ่งจะเห็นว่าสำหรับ $H$ ใด ๆ

$$
\Pi_H(m)\leq 2^m
$$

เพื่อทำความเข้าใจ growth function ให้มากขึ้น เราจะมาดูตัวอย่าง hypothesis space ง่าย ๆ ดูเล็กน้อย

## Positive rays
กำหนดให้ $X=\mathbb{R}$ และให้ $H$ เป็นเซตของฟังก์ชัน $$h:\mathbb{R}\to\{0,1\}$$ ที่อยู่ในรูป

$$ h=\text{sign}(x-a)\cdot\frac{1}{2} + \frac{1}{2}$$

หรือก็คือ

$$
h=\begin{cases}
1 &\text{ ถ้า } x\geq a\\
0 &\text{ กรณีอื่น ๆ }
\end{cases}
$$
