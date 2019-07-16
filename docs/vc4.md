{% include lib/mathjax.html %}
# ขอบเขตของ Growth Function

หากเราย้อนกลับมาดู generalization bound ของ error ของ hypothesis ที่ได้จากการเรียนรู้แบบ PAC
ในกรณีที่ hypothesis space $H$ มีขนาดจำกัด เราสรุปได้ว่าหากมี hypothesis $c\in H$ ที่ $R(c)=0$ อยู่จริง
เราสามารถทำการเรียนรู้โดยการหา hypothesis $h$ ที่ consistent กับตัวอย่างข้อมูลทั้งหมด
ซึ่งจะทำให้ได้ผลลัพธ์เป็น $h\in H$ ที่รับประกันได้ว่า ด้วยความน่าจะเป็นไม่น้อยกว่า $1-\delta$

$$
R(h)\leq \frac{1}{m}(\ln|H| + \ln\frac{1}{\delta})
$$

ในขณะที่กรณีของ Agnostic-PAC สำหรับ hypothesis $h\in H$ ใด ๆ ที่มี empirical error เป็น $\hat{R}(h)$
เราสามารถสรุปขอบเขตของ error จริงของ $h$ ได้ว่า ด้วยความน่าจะเป็นไม่น้อยกว่า $1-\delta$

$$
R(h)\leq \hat{R}(h) + \sqrt{\frac{1}{2m}(\ln |H| + \frac{2}{\delta})}
$$
