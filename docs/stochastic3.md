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
