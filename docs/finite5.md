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

## Decision tree ความสูง $k$ represent ได้ด้วย $k$-DNF

สำหรับ decision tree $T$ ใด ๆ
$T$ จะทำหน้าที่ represent ฟังก์ชัน $f_T$ บน input $$a\in\{0,1\}^n$$ ที่สามารถนิยามแบบ recursive ได้ดังนี้
ถ้า $T$ เป็น tree ที่มีเพียง node เดียว ซึ่งถูก label ด้วย $$b\in\{0,1\}$$ $f_T$ จะเป็นฟังก์ชันที่คืนค่าเป็นค่าคงที่
$b$ เสมอไม่ว่าจะรับ input เป็นอะไรก็ตาม แต่หาก $T$ มี root ที่ถูก label ด้วยตัวแปร $x_i$
และมี $T_0$ และ $T_1$ เป็นต้นไม้ย่อยด้านซ้ายและขวาของ root ของ $T$ ตามลำดับ เราจะได้ว่า
$f_T(a)$ จะมีค่าเท่ากับ $f_{T_0}(a)$ ถ้า $a_i$ มีค่าเป็น 0 และมีค่าเป็น $f_{T_1}(a)$
ถ้า $a_i$ มีค่าเป็น 1 รูปต่อไปนี้แสดงตัวอย่าง decision tree บนตัวแปร $x_1,x_2,x_3,x_4$
ซึ่งจะให้ค่าเป็น 1 หาก input เป็น $(0,1,1,0)$ แต่จะให้ค่าเป็น 0 หาก input เป็น $(1,0,1,1)$
สังเกตว่าตัวแปร $x_i$ แต่ละตัวอาจถูก label ที่ internal node ใน decision tree มากกว่าหนึ่ง node ก็ได้
อย่างไรก็ดี หากใน decision tree มี path จาก root ไปยัง leaf node ใด ที่มีตัวแปร $x_i$ บางตัวปรากฏมากกว่าหนึ่งครั้ง
เราจะสามารถลดรูป decision tree ดังกล่าวให้ตัวแปรทั้งหมดปรากฏไม่เกินหนึ่งครั้งในแต่ละ path ได้

<p align="center">
<img width="500" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/decisiontree.png">
</p>

เราสามารถมองเห็นได้ไม่ยากนักว่า decision tree ต้นนี้ represent ฟังก์ชันที่แสดงได้ด้วย DNF ดังนี้

$$
\bar{x}_1\bar{x}_2\lor x_2x_3\bar{x}_4\lor x_1x_2x_4
$$

จากตัวอย่างนี้ สังเกตว่าหากเราให้ความสูงของ decision tree แทนจำนวน internal node ที่มากที่สุดใน path
จาก root ไปยัง leaf node ใด ๆ เราจะได้ว่า ฟังก์ชันที่ represent ได้ด้วย decision tree ที่มีความสูงไม่เกิน
$k$ จะสามารถ represent ด้วย $k$-DNF ได้เช่นกัน เราสามารถลดรูปจาก decision tree ความสูงไม่เกิน $k$
มาเป็น $k$-DNF ได้โดยการสร้าง conjunction หนึ่ง term สำหรับแต่ละ leaf ที่มี label เป็น 1
ซึ่ง conjunction ดังกล่าวประกอบด้วย $x_i$ หรือ $\bar{x}_i$ ที่อยู่ใน path จาก root มายัง leaf นั้น
โดยการเลือก $x_i$ หรือ $\bar{x}_i$ พิจารณาจากทิศทางของ path ขณะที่ผ่าน node ที่ label ด้วย $x_i$ นั่นเอง
ดังนั้นฟังก์ชันใด ๆ ที่ represent ด้วย decision tree ความสูงไม่เกิน $k$ ได้ก็จะสามารถ represent ด้วย
$k$-DNF ได้เสมอ เราจึงสามารถสรุปตามมาได้ว่า ปัญหาการเรียนรู้ decision tree ที่มีความสูงไม่เกิน $k$
นั้นสามารถลดรูปให้เป็นปัญหาการเรียนรู้ $k$-DNF ได้ ซึ่งเรารู้ว่ากลุ่มของฟังก์ชันดังกล่าวสามารถเรียนรู้ได้โดยใช้
$k$-decision list เป็น representation

อย่างไรก็ดี การลดรูปจาก decision tree ความสูง $k$ ไปเป็น $k$-DNF ดังกล่าวอาจยังมีประสิทธิภาพไม่ดีนัก
พิจารณาตัวอย่าง decision tree ความสูงเท่ากับ 3 ดังรูปต่อไปนี้

<p align="center">
<img width="200" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/decisiontree2.png">
</p>

จะเห็นว่าด้วยวิธีการดังกล่าว เราจะสามารถลดรูปให้กลายเป็น
3-DNF

$$
x_2\lor \bar{x}_2x_3\lor\bar{x}_2\bar{x}_3x_1
$$

ซึ่ง represent ได้ด้วย 3-decision list ในขณะที่เราเห็นได้ชัดเจนว่า decision tree
ต้นนี้มีลักษณะการตัดสินใจแบบเดียวกับ 1-decision list

$$
(x_2,1),(x_3,1),(x_1,1) \text{ และค่า default เป็น } 0
$$

จะเห็นว่าการแปลง decision tree เป็น 1-decision list นี้มีความเรียบง่ายกว่าและใช้พื้นที่ของ representation น้อยกว่าแบบก่อน
ซึ่งนำไปสู่ประสิทธิภาพในการเรียนรู้ decision tree ที่ดีกว่า
เนื่องจากถ้าเราสามารถลดรูปปัญหาการเรียนรู้ให้ concept class มีขนาดเล็กลงได้
ก็จะทำให้ประสิทธิภาพในการเรียนรู้ยิ่งดีขึ้น

## Rank-$r$ decision tree represent ได้ด้วย $r$-decision list

ในหัวข้อนี้เราจะแสดงให้เห็นวิธีการแปลง decision tree ให้เป็น decision list ที่ represent ฟังก์ชันเดียวกัน
โดย decision list ที่ได้จะมีขนาดของ representation ที่รัดกุมมากกว่าการแปลงเป็น DNF ก่อนหน้านี้
การแปลง representation ดังกล่าวจะทำให้เราสามารถเรียนรู้ decision tree ได้โดยใช้อัลกอริทึมในการเรียนรู้
decision list ได้ ซึ่งอัลกอริทึมดังกล่าวมีความเรียบง่ายเป็นอย่างมาก

สำหรับ decision tree $T$ เรานิยาม _rank_ ของ $T$ ให้ $rank(T)$ มีค่าเป็น 0 ถ้า $T$ เป็นต้นไม้ที่มี node เดียว
ไม่เช่นนั้นให้ $T_0$ และ $T_1$ เป็นต้นไม้ย่อยด้านซ้ายและขวาของ root ของ $T$ เรากำหนดให้

$$
rank(T)=\begin{cases}
\begin{array}{ll}
\max(rank(T_0), rank(T_1)) &\text{ ถ้า } rank(T_0)\neq rank(T_1)\\
rank(T_0)+1 &\text{ กรณีอื่น ๆ }
\end{array}
\end{cases}
$$
