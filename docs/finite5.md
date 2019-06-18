{% include lib/mathjax.html %}
# Decision Tree

ในหัวข้อนี้เราจะมารู้จักการนำเสนอ boolean function อีกลักษณะหนึ่งที่เรียกว่า decision tree
ซึ่งเป็นหนึ่งในแบบจำลองที่นิยมใช้ในปัญหาด้าน machine learning ในทางปฏิบัติจริง ๆ
เราจะมาวิเคราะห์ความสามารถของ decision tree ในการ represent ฟังก์ชันทาง boolean
และศึกษาประสิทธิภาพในการเรียนรู้แบบจำลอง decision tree นี้

ก่อนอื่น เราจะให้นิยาม decision tree อย่างเป็นทางการเสียก่อน
สำหรับตัวแปร boolean $x_1,\dots,x_n$ ใด ๆ เราจะกล่าวว่า $T$ เป็น decision tree บน
$x_1,\dots,x_n$ เมื่อ $T$ เป็น full binary tree (binary tree ที่ internal node
ทั้งหมดมีจำนวน node ลูกเท่ากับ 2) โดยที่แต่ละ internal node จะถูก label ด้วยตัวแปร $x_i$
ตัวหนึ่ง และแต่ละ leaf node ถูก label ด้วย 0 หรือ 1

สำหรับ decision tree $T$ ใด ๆ
$T$ จะทำหน้าที่ represent ฟังก์ชัน $f_T$ บน input $$a\in\{0,1\}^n$$ ที่สามารถนิยามแบบ recursive ได้ดังนี้
ถ้า $T$ เป็น tree ที่มีเพียง node เดียว ซึ่งถูก label ด้วย $$b\in\{0,1\}$$ $f_T$ จะเป็นฟังก์ชันที่คืนค่าเป็นค่าคงที่
$b$ เสมอไม่ว่าจะรับ input เป็นอะไรก็ตาม แต่หาก $T$ มี root ที่ถูก label ด้วยตัวแปร $x_i$
และมี $T_0$ และ $T_1$ เป็นต้นไม้ย่อยด้านซ้ายและขวาของ root ของ $T$ ตามลำดับ เราจะได้ว่า
$f_T(a)$ จะมีค่าเท่ากับ $f_{T_0}(a)$ ถ้า $a_i$ มีค่าเป็น 0 และมีค่าเป็น $f_{T_1}(a)$
ถ้า $a_i$ มีค่าเป็น 1 รูปต่อไปนี้แสดงตัวอย่าง decision tree บนตัวแปร $x_1,x_2,x_3,x_4$
ซึ่งจะให้ค่าเป็น 1 หาก input เป็น $(0,1,1,0)$ แต่จะให้ค่าเป็น 0 หาก input เป็น $(1,0,1,1)$

<p align="center">
<img width="300" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/decisiontree.png">
</p>

เราสามารถมองเห็นได้ไม่ยากนักว่า decision tree ต้นนี้ represent ฟังก์ชัน

$$
\bar{x}_1\bar{x}_2\lor x_2x_3\bar{x}_4\lor x_1x_2x_4
$$
