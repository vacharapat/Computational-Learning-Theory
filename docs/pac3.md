{% include lib/mathjax.html %}
# ปัญหาการเรียนรู้ boolean conjunction

ในหัวข้อนี้เราจะมาดูตัวอย่างปัญหาการเรียนรู้อีกปัญหาหนึ่งที่สามารถเรียนรู้ได้อย่างมีประสิทธิภาพตามกรอบของ PAC

ปัญหาที่เราจะสนใจนี้เรียกว่าปัญหาการเรียนรู้ boolean conjunction เรากำหนดให้ concept class $C$
เป็นเซตของ conjunction ทั้งหมดที่สร้างได้จาก literal ของตัวแปร boolean $x_1,\dots,x_n$
โดยที่ literal ของ $x_i$ อาจเป็น $x_i$ หรือ $\bar{x}_i$ และให้ input space $$X=\{0,1\}^n$$
เป็นเซตของการกำหนดค่าให้กับตัวแปร $x_i$ ในทุกรูปแบบ

ให้ $c$ เป็น conjunction หนึ่งใน $C$ เราจะกำหนดให้ $c(a)=1$ สำหรับ $a\in X$ ถ้าการกำหนดค่าให้ตัวแปร $x_1,\dots,x_n$ ตามแบบ $a$
นั้นทำให้ conjunction $c$ เป็นจริง และให้ $c(a)=0$ ถ้าการกำหนดค่าดังกล่าวทำให้ conjunction $c$ เป็นเท็จ
ตัวอย่างเช่น ถ้า $n=4$ และ concept เป้าหมายเป็น conjunction

$$
x_1\land\bar{x}_3\land x_4
$$

เราจะได้ว่า $(1,0,0,1)$ เป็นตัวอย่างข้อมูลที่มี label เป็น 1 และ $(1,1,1,0)$ มี label เป็น 0

เราอาจนิยามให้ขนาดของ conjunction $c$ ใด ๆ เป็นจำนวน literal ใน $c$ ซึ่งจะทำให้เราได้ว่า $size(c)\leq 2n$
และเนื่องจากขนาดของตัวอย่างข้อมูล $a\in X$ แต่ละตัวเป็น $n$ ดังนั้น เราจะสามารถเรียนรู้ boolean conjunction
จากตัวอย่างข้อมูลได้อย่างมีประสิทธิภาพหากมีอัลกอริทึมการเรียนรู้ตามกรอบ PAC ที่ใช้จำนวนตัวอย่างข้อมูลเป็น polynomial บน
$n$, $1/\epsilon$ และ $1/\delta$

## อัลกอริทึมการเรียนรู้ conjunction

จากตัวอย่าง conjunction ด้านบน สังเกตว่าตัวอย่างข้อมูลที่มี label เป็น 0 เช่น $(1,1,1,0)$ นั้นบอกเราได้เพียงว่า จะต้องมี literal ที่ขัดแย้งกับการกำหนดค่าอย่างน้อยหนึ่งตัวใน conjunction เป้าหมาย นั่นคือ ใน $c$ จะต้งมี $\bar{x}_1$
หรือ $\bar{x}_2$ หรือ $\bar{x}_3$ หรือ $x_4$ อย่างน้อยหนึ่งตัว แต่เรายังไม่สามารถระบุได้ว่าต้องมีตัวใดบ้าง
ในขณะที่ตัวอย่างข้อมูลที่มี label เป็น 1 เช่น $(1,0,0,1)$ นั้นสามารถบอกเราได้ว่าใน $c$ จะไม่สามารถมี literal
$\bar{x}_1,x_2,x_3,\bar{x}_4$ อยู่ได้แม้สักตัวเดียว จากตรงนี้นำเรามาสู่อัลกอริทึมหนึ่งในการเรียนรู้ conjunction ที่มีการทำงานดังนี้

อัลกอริทึมเริ่มต้นจากการกำหนด hypothesis conjunction เป็น

$$
h=x_1\land \bar{x}_1\land\dots\land x_n\land\bar{x}_n
$$

ซึ่งจะเห็นว่า hypothesis เริ่มต้นนี้จะไม่สอดคล้องกับการกำหนดค่าให้กับตัวแปรใด ๆ เลย ถัดมา สำหรับเซตของตัวอย่างข้อมูล
$S$ ที่มีสมาชิก $m$ ตัว เมื่ออัลกอริทึมรับตัวอย่างข้อมูล $(a,c(a))\in S$ มาตัวหนึ่ง
หากตัวอย่างข้อมูลดังกล่าวเป็น positive example หรือ $c(a)=1$ อัลกอริทึมจะทำการปรับปรุง hypothesis $h$
โดยการลบ literal ที่ขัดแย้งกับ $a$ ออกไป กล่าวคือ สำหรับ $i=1,\dots,n$ ถ้า $a_i=0$ เราจะลบ $x_i$ ออกจาก $h$
แต่ถ้า $a_i=1$ เราจะลบ $\bar{x}_i$ ออกจาก $h$ ในขณะที่ หากตัวอย่างข้อมูลที่พิจารณาเป็น negative example ($c(a)=0$)
อัลกอริทึมจะไม่มีการปรับปรุง hypothesis

สมมติว่า $n=4$ และ $c$ เป็น conjunction $x_1\land\bar{x}_4$ โดยเซตของตัวอย่างข้อมูล $S$ มีสมาชิกดังตาราง

<center>

|     $a$     | $c(a)$ |
|:-----------:|:------:|
| $(0,1,1,1)$ |    0   |
| $(1,1,0,0)$ |    0   |
| $(1,0,1,0)$ |    1   |
| $(0,0,1,0)$ |    0   |
| $(1,1,1,0)$ |    1   |

</center>