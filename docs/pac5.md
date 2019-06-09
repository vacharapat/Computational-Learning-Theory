{% include lib/mathjax.html %}
# Representation และประสิทธิภาพในการเรียนรู้
ในหัวข้อนี้ เราจะแสดงให้เห็นว่า ถ้าเราเปลี่ยนรูปแบบของ representation ของ 3-term DNF
เสียใหม่ จะทำให้คลาสของ 3-term DNF สามารถทำการเรียนรู้อย่างมีประสิทธิภาพได้

เราจะใช้ความจริงที่ว่า สำหรับ 3-term DNF ใด ๆ เราสามารถเขียนให้อยู่ในรูป

$$
d_1\land\dots\land d_j
$$

ได้ โดยที่ $d_i$ ใด ๆ เป็น disjunction ของ literal ไม่เกินสามตัว เราเรียก representation
ลักษณะนี้ว่า 3-Conjunctive Normal Form หรือ 3-CNF
สำหรับ 3-term DNF $T_1\lor T_2\lor T_3$ ใด ๆ เราจะสามารถจัดให้อยู่ในรูปของ 3-CNF ได้ดังนี้

$$
T_1\lor T_2\lor T_3 = \bigwedge_{u\in T_1,\\v\in T_2,\\w\in T_3}(u\lor v\lor w)
$$

ตัวอย่างเช่น 3-term DNF

$$
(x_1)\lor (x_2\land \bar{x}_3\land x_4)\lor (\bar{x}_1\land x_4)
$$

จะสามารถเขียนในรูป 3-CNF ได้เป็น

$$
(x_1\lor x_2\lor \bar{x}_1)\land (x_1\lor x_2\lor x_4)\land
(x_1\lor \bar{x}_3\lor\bar{x}_1)\land (x_1\lor \bar{x}_3\lor x_4)\land
(x_1\lor x_4\lor \bar{x}_1)\land (x_1\lor x_4\lor x_4)
$$

ซึ่งลดรูปได้เป็น

$$
(x_1\lor x_2\lor x_4)\land (x_1\lor \bar{x}_3\lor x_4)\land (x_1\lor x_4)
$$
