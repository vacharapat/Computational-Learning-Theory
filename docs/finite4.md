{% include lib/mathjax.html %}
# ปัญหาการเรียนรู้ Decision List

เป้าหมายหนึ่งในการศึกษาด้านการเรียนรู้นั้น คือการหา concept class ที่ใหญ่ที่สุดที่สามารถเรียนรู้ได้จากตัวอย่างข้อมูล
ในหัวข้อนี้เราจะมาดูเทคนิคใหม่ในการ represent concept ในกลุ่ม boolean formula ที่เรียกว่า
decision list ซึ่งเราจะได้เห็นว่าสามารถ represent concept ได้กว้างกว่า concept class ที่เคยศึกษามา
และที่สำคัญคือสามารถเรียนรู้ได้อย่างมีประสิทธิภาพอีกด้วย

เรานิยามให้ _decision list_ บนตัวแปร $x_1,\dots,x_n$ คือรายการ (list) $L$ ของคู่ลำดับ

$$
(f_1,v_1),\dots,(f_r,v_r)
$$

และบิต $$v\in\{0,1\}$$
เมื่อ $f_i$ ใด ๆ เป็น boolean conjunction บนตัวแปร $x_1,\dots,x_n$ และ $$v_i\in\{0,1\}$$

สำหรับการกำหนดค่า $$a\in \{0,1\}^n$$ ใด ๆ เราจะให้ค่าของ $L(a)$ มีค่าเท่ากับ $v_j$ เมื่อ
$j$ เป็นลำดับที่น้อยที่สุดที่ $f_j(a)=1$ ถ้าไม่มี conjunction $f_i$ ใดที่การกำหนดค่าใน $a$ ทำให้เป็น 1 ได้เลย
เราจะให้ $L(a)=v$

เราสามารถมอง decision list ในรูปของลำดับการตัดสินใจแบบ `if - then - else if - then - ... else` ได้ดังนี้

$$
\begin{split}
L(a) &= \text{ if } f_1(a)=1 \text{ then } v_1 \\
& \text{ else if } f_2(a)=1\text{ then } v_2\\
& \text{ else if } \dots\\
& \text{ else if } f_r(a)=1\text{ then } v_r\\
& \text{ else } v
\end{split}
$$
