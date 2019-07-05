{% include lib/mathjax.html %}
# Growth Function

ในการวิเคราะห์ sample complexity หรือ generalization bound ที่ผ่านมาทั้งหมดนั้น
ขนาดของ hypothesis space $H$ ที่เราเลือกใช้มีบทบาทสำคัญอย่างมาก ตัวอย่างเช่นในการเรียนรู้แบบ
agnostic-PAC เราสามารถสรุปได้ว่า สำหรับ hypothesis $h\in H$ ใด ๆ เมื่อเราทำการเรียนรู้จากตัวอย่างข้อมูลจำนวน $m$ ตัว
เราจะได้ว่า

$$
R(h)\leq \hat{R}(h)+\sqrt{\frac{1}{2m}(\ln|H|+\ln\frac{2}{\delta})}
$$
