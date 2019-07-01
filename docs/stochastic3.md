{% include lib/mathjax.html %}
# การเลือกแบบจำลอง

ปัญหาหลักในการออกแบบอัลกอริทึมการเรียนรู้ก็คือการเลือก hypothesis space $H$
เราเรียกปัญหานี้ว่าปัญหา _การเลือกแบบจำลอง_ (model selection) หาก $H$ ของเรามีขนาดใหญ่มาก เราก็อาจคาดหวังได้ว่า $H$
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
เมื่อ $h_{Bayes}$ เป็น Bayes hypothesis

<p align="center">
<img width="300" src="https://raw.githubusercontent.com/vacharapat/Computational-Learning-Theory/master/images/model_selection.png">
</p>

ในการเลือกแบบจำลองนั้น เราต้องเลือก hypothesis space $H$ ที่มี trade-off ระหว่าง estimation error
และ approximation error นี้ในระดับที่เราพอใจ
สังเกตว่าเราไม่สามารถประมาณค่า approximation error ได้เลย
เพราะเราไม่รู้การกระจาย $D$ ของข้อมูล ในขณะที่ค่า estimation error ของ hypothesis ที่ได้จากอัลกอริทึมการเรียนรู้นั้น
อาจจะประมาณด้วย generalization bound ได้ในบางสถานการณ์

ตัวอย่างหนึ่งของอัลกอริทึมที่สามารถประมาณค่า estimation error ได้ก็คือ empirical risk minimization (ERM)
ที่เราได้ศึกษากันไปแล้วนั่นเอง ซึ่งสามารถประมาณค่า estimation error ในรูปของขนาดของ $H$ ได้
อย่างไรก็ดี ในทางปฏิบัตินั้นอัลกอริทึม ERM มักจะไม่ประสบความสำเร็จเนื่องจากขาดการพิจารณาความซับซ้อนของ hypothesis space $H$
ทำให้เมื่อ $H$ มีความซับซ้อนต่ำ approximation error ก็มีค่ามาก ในขณะที่เมื่อ $H$ มีความซับซ้อนสูงทำให้ขนาดของ $H$ มีค่ามาก
ขอบเขตของ estimation error ก็จะกว้าง นอกจากนี้ ในหลายสถานการณ์ การหาผลลัพธ์ของ ERM
ให้ได้นั้นก็เป็นปัญหายากในมุมของประสิทธิภาพของอัลกอริทึมอีกด้วย

## Structural risk minimization
จากปัญหาการเลือกแบบจำลองที่แสดงในรูปของผลรวมระหว่าง estimation error และ approximation error
จะเห็นว่าแบบจำลองหรือ hypothesis space ที่เหมาะสมนั้นควรจะมีความซับซ้อนมากพอที่จะทำให้ approximation error มีค่าน้อย
แต่ต้องไม่ซับซ้อนมากเกินไปเพื่อให้ขอบเขตของ estimation error ไม่กว้างด้วย แนวทางหนึ่งในการหาแบบจำลองดังกล่าวคือการพิจารณา
ลำดับของ hypothesis space ที่มีความซับซ้อนมากขึ้นเรื่อย ๆ ที่ละขั้น กล่าวคือ เราจะพิจารณา hypothesis space
$H_1,H_2,H_3,\dots$ ที่

$$
H_i\subset H_{i+1}
$$

สำหรับ $i=1,2,3,\dots$ และพยายามหา hypothesis space $H_{i}$ ที่มี trade-off ระหว่าง
estimation error กับ approximation error ดีที่สุด อย่างไรก็ดี เนื่องจากค่า error ดังกล่าว
ไม่สามารถคำนวณได้ เราก็จะใช้ขอบเขตบนของผลรวมที่คำนวณได้เป็นตัวแทนในการตัดสินใจ

แนวคิดนี้นำมาสู่อัลกอริทึมที่ชื่อว่า _structural risk minimization_ (SRM) ซึ่งจะทำการวนรอบพิจารณา
hypothesis space $H_1,H_2,H_3,\dots$ ตามลำดับ และทำการหา hypothesis $h\in H_i$ ที่มีค่า

$$
\hat{R}(h)+\sqrt{\frac{\ln |H_i|}{2m}}+\sqrt{\frac{\ln i}{m}}
$$

น้อยที่สุด

เราอาจกล่าวได้ว่า ถ้า $h_{SRM}$ เป็น hypothesis ผลลัพธ์ของอัลกอริทึม SRM เราจะได้ว่า

$$
h_{SRM}=\arg\min_{i\geq 1,\\ h\in H_i} \hat{R}(h)+\sqrt{\frac{\ln |H_i|}{2m}}+\sqrt{\frac{\ln i}{m}}
$$

เราสามารถมองผลจากอัลกอริทึม SRM ว่าเป็นการหาค่า $i$ และ hypothesis space $H_i$ ที่เหมาะสมที่สุด
และอัลกอริทึมจะทำการคืนค่าเป็นผลลัพธ์ของ ERM ใน $H_i$

ในการวิเคราะห์ เราสมมติให้ $H = \cup_iH_i$ และสำหรับ $h$ ใด ๆ ใน $H$ เราจะให้ $H(h)$
เป็น hypothesis space $H_i$ ที่เล็กที่สุดที่ครอบคลุม $h$ กล่าวคือ $H(h)=\arg\min_{H_i\contains h}i$
