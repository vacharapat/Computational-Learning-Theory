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
