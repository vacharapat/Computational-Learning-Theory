{% include lib/mathjax.html %}
# การเลือกแบบจำลอง

ปัญหาหลักในการออกแบบอัลกอริทึมการเรียนรู้ก็คือการเลือก hypothesis space $H$
เราเรียกปัญหานี้ว่าปัญหาการเลือกแบบจำลอง หาก $H$ ของเรามีขนาดใหญ่มาก เราก็อาจคาดหวังได้ว่า $H$
จะครอบคลุม Bayes hypothesis อย่างไรก็ดี จากการวิเคราะห์การเรียนรู้แบบ Agnostic PAC ก็จะเห็นว่าเมื่อ $H$
มีขนาดใหญ่ ขอบเขตของ generalization error ที่ได้จากการเรียนรู้ก็ยิ่งมากตามไปด้วย นั่นคือ hypothesis
ที่ได้จากการเรียนรู้อาจมี error ไม่ใกล้เคียงกับ Bayes error เท่าที่ต้องการก็ได้
ในหัวข้อนี้เราจะมาวิเคราะห์ trade-off นี้ในรูปของ estimation error และ approximation error

## Estimation error และ Approximation error
สำหรับ hypothesis $h\in H$ ใด ๆ เราสามารถเขียนผลต่างระหว่าง $R(h)$ และ Bayes error $R^*$
แบบแยกองค์ประกอบได้เป็น

$$
R(h)-R^* = \left(R(h) - R(h^*)\right) + \left(R(h^*) - R^*\right)
$$

เมื่อ $h^*$ เป็น hypothesis ที่มี error น้อยที่สุดใน $H$

เราเรียก
$$R(h)-R(h^*)$$
ว่า estimation error และเรียก
$$R(h^*)-R^*$$
ว่า approximation error
โดย estimation error นั้นทำการวัด error ของ $h$ เทียบกับ error ที่น้อยที่สุดที่สามารถสร้างได้จาก $H$
สังเกตว่าในการเรียนรู้แบบ Agnostic PAC นั้น เรามุ่งเป้าไปที่การลด estimation error นี้เป็นหลัก

สำหรับ approximation error นั้นเป็นตัวที่บอกเราว่า $H$ นั้นสามารถประมาณค่า Bayes error $$R^*$$
ได้มากแค่ไหน หากเราเลือก $H$ ที่มีความซับซ้อนสูงซึ่งทำให้ $H$ มีขนาดใหญ่ ก็มีแนวโน้มที่จะได้ค่า approximation error
ที่น้อย ในขณะที่ estimation error นั้นจะสูงตามขนาดของ $H$ รูปด้านล่างแสดงตัวอย่าง estimation error
และ approximation error โดยเส้นทึบแทน estimation error และเส้นประแทน approximation error

<p align="center">
<img width="250" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/model_selection.png">
</p>
