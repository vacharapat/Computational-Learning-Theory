{% include lib/mathjax.html %}
# Inconsistent Hypothesis

ในทางปฏิบัติ เรามักจะไม่สามารถหา hypothesis ใน $H$ ที่สอดคล้องกับตัวอย่างข้อมูลทั้งหมดที่รับมาได้
ซึ่งปัญหาอาจเกิดจากความซับซ้อนของปัญหาที่ทำให้ hypothesis class $H$ นั้นไม่ครอบคลุม concept ที่เรากำลังเรียนรู้
อย่างไรก็ดี เราได้เห็นตัวอย่างใน [การเรียนรู้ Boolean Conjunction ด้วย Inconsistent Hypothesis](https://vacharapat.github.io/Computational-Learning-Theory/docs/finite3) แล้วว่า hypothesis ที่ไม่จำเป็นต้องสอดคล้องกับตัวอย่างข้อมูลทั้งหมด
แต่มีความผิดพลาดไม่มากนักก็มีประโยชน์สำหรับเราเช่นกัน ในหัวข้อนี้เราจะมาวิเคราะห์เกี่ยวกับ inconsistent hypothesis
เหล่านี้ในสถานการณ์ที่ hypothesis class $H$ ยังคงมีขนาดจำกัด
