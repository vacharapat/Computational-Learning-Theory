{% include lib/mathjax.html %}
# การเรียนรู้ Boolean Conjunction ด้วย Inconsistent Hypothesis

จากหัวข้อที่แล้วเราสามารถปรับปรุงอัลกอริทึมการเรียนรู้ปัญหา Boolean Conjunction ให้เรียนรู้ได้โดยมี
sample complexity เป็น $O(\frac{1}{\epsilon}\left(size(c)\log n\log\frac{size(c)\log n}{\epsilon} +\log\frac{1}{\delta}\right))$
ในหัวข้อนี้เราจะปรับปรุงอัลกอริทึมการเรียนรู้อีกเล็กน้อยเพื่อให้ได้ขอบเขตของ sample complexity ที่ดีขึ้นอีก
โดยแนวคิดเบื้องหลังการปรับปรุงนี้คือ ในความเป็นจริงเราอาจไม่จำเป็นที่จะต้องหา hypothesis ที่สอดคล้องกับตัวอย่างข้อมูลทั้งหมดเสมอไป
เช่นในอัลกอริทึมการเรียนรู้ปัญหา Boolean Conjunction ของเรานี้ ในขั้นตอนการเลือก literal ให้ครอบคลุม
negative example โดยใช้การเลือกแบบ greedy  นั้น แทนที่เราจะวนรอบเลือก literal จนกระทั่งรับประกันว่า
negative example ทั้งหมดทุกครอบคลุมแล้ว เราอาจวนรอบเลือก literal เพื่อให้มั่นใจแค่ว่าอาจมี negative example
ที่ไม่สอดคล้องอยู่ไม่มากนัก โดยเราจะมาวิเคราะห์กันว่า หากเราวนรอบเลือก literal จนรับประกันได้ว่ามี
negative example ที่ไม่สอดคล้องอยู่ไม่เกิน $\epsilon m/2$ ตัว ก็เพียงพอที่จะเรียนรู้ได้สำเร็จแล้ว

พิจารณาเมื่อเรากำหนดให้ขั้นตอนการเลือก literal แบบ greedy ถูกทำจนกระทั่งจำนวน negative example
ที่ยังไม่ถูกครอบคลุมเหลือไม่เกิน $\epsilon m/2$ เราจะได้ว่าการวนรอบนี้จะสิ้นสุดเมื่อ

$$
|U_i|\leq m\left(1-\frac{1}{OPT}\right)^i<me^{-i/OPT}\leq \frac{\epsilon m}{2}
$$

ซึ่งจะเป็นจริงเมื่อ

$$
i = OPT\ln\frac{2}{\epsilon}\leq size(c)\ln\frac{2}{\epsilon}
$$
