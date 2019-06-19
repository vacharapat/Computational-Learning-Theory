{% include lib/mathjax.html %}
# การเรียนรู้แบบ Agnostic PAC

เนื่องจากในแบบจำลองการจำแนกข้อมูลแบบ stochastic นี้ เราไม่สามารถหา concept เป้าหมายที่มี
error เป็นศูนย์ได้ ดังนั้น สำหรับ hypothesis space $H$ ใด ๆ เราจะมุ่งเป้าไปที่การหา hypothesis $h\in H$
ที่มี error $R(h)$ ใกล้เคียงค่าที่น้อยที่สุดที่เป็นไปได้ แนวคิดนี้ทำให้เราสามารถนิยามอัลกอริทึมการเรียนรู้แบบ
agnostic-PAC ได้ดังนี้

สำหรับ hypothesis space $H$ เราจะกล่าวว่าอัลกอริทึม $A$ เป็นอัลกอริทึมการเรียนรู้แบบ agnostic-PAC
ถ้าสำหรับค่า $\epsilon>0$ และ $\delta>0$ ใด ๆ และสำหรับการกระจายของข้อมูล $D$ บน $X\times Y$ ใด ๆ
เมื่ออัลกอริทึม $A$ รับตัวอย่างข้อมูล $$S=\{(x_1,y_1),\dots,(x_m,y_m)\}$$ จาก $D$
อัลกอริทึม $A$ จะให้ผลลัพธ์เป็น hypothesis $h_S$ ที่สอดคล้องกับเงื่อนไขต่อไปนี้ เมื่อ $m\geq m_0$
โดย $m_0$ เป็น polynomial บน $1/\epsilon$, $1/\delta$, $n$ และ $size(h^*)$

$$
\Pr[R(h_S)-R(h^*)]\leq\epsilon]\geq 1-\delta
$$

โดย $n$ เป็นขนาดของ input $x\in X$ และ $h^*$ เป็น hypothesis ที่มีค่า error น้อยที่สุดใน $H$ หรือ

$$
h^* = \arg\min_{h\in H}R(h)
$$

ถ้าอัลกอริทึม $A$ สามารถให้ผลลัพธ์ดังกล่าวได้โดยใช้เวลาทำงานเป็น polynomial บน $1/\epsilon$,
$1/\delta$, $n$ และ $size(h^*)$ เราจะเรียกว่าเป็นอัลกอริทึมการเรียนรู้แบบ agnostic ที่มีประสิทธิภาพ

## Inconsistent Hypothesis
ในการเรียนรู้บน stochastic scenario นี้ เราไม่สามารถรับประกันได้ว่าจะสามารถหา hypothesis $h\in H$
ที่สอดคล้องกับตัวอย่างข้อมูลทั้งหมดใน $S$ ได้เสมอ อย่างไรก็ดี เราได้เห็นตัวอย่างใน [การเรียนรู้ Boolean Conjunction ด้วย Inconsistent Hypothesis](https://vacharapat.github.io/Computational-Learning-Theory/docs/finite3)
มาแล้วว่า hypothesis ที่ไม่ได้สอดคล้องกับตัวอย่างข้อมูลทั้งหมด แต่มีความผิดพลาดบนตัวอย่างข้อมูลน้อย
ก็มีประโยชน์สำหรับเราได้เช่นกัน

ในหัวข้อนี้เราจะแสดงให้เห็นว่าในความเป็นจริง สำหรับ hypothesis $h\in H$ ใด ๆ
เราพอที่จะสามารถหาขอบเขตของ error $R(h)$ จาก empirical error $\hat{R}(h)$ ได้
เมื่อ $\hat{R}(h)$ มีนิยามดังนี้

สำหรับเซตของตัวอย่างข้อมูล $$S=\{(x_1,y_1),\dots,(x_m,y_m)\}$$

$$
\hat{R}(h)=\frac{1}{m}|\{(x,y)\in S: h(x)\neq y\}| = \frac{1}{m}\sum_{i=1}^m1_{h(x_i)\neq y}
$$

เครื่องมือที่เราจะใช้ในการวิเคราะห์ขอบเขตดังกล่าวคือ Hoeffding's inequality ซึ่งกล่าวไว้ดังนี้

**Hoeffding's inequality**
ให้ $X_1,\dots,X_m$ เป็ตัวแปรสุ่มที่เป็นอิสระกัน $m$ ตัวโดยที่ $X_i$ มีค่าอยู่ในช่วง $[a_i,b_i]$ ถ้าให้ $S_m=\sum_{i=1}^mX_i$ เราจะได้ว่า

$$
\Pr[S_m-\mathbb{E}[S_m]\geq\epsilon]\leq e^{-2\epsilon^2/\sum_{i=1}^m(b_i-a_i)^2}
$$

และ

$$
\Pr[S_m-\mathbb{E}[S_m]\leq -\epsilon]\leq e^{-2\epsilon^2/\sum_{i=1}^m(b_i-a_i)^2}
$$

จาก Hoeffding's inequality เราจะได้ว่าเมื่อเราพิจารณาตัวอย่างข้อมูล $S$ และทำการเลือก hypothesis $h\in H$ ที่มีอัตราผิดพลาดบน $S$ เท่ากับ $\hat{R}(h)$ เราสามารถวิเคราะห์โอกาสที่ $h$ จะมีอัตราผิดพลาดเฉลี่ยจริง $R(h)$ แตกต่างจาก $\hat{R}(h)$ มากได้ดังนี้

$$
\Pr[\hat{R}(h)-R(h)\geq\epsilon]\leq e^{-2m\epsilon^2}
$$

และ

$$
\Pr[\hat{R}(h)-R(h)\leq -\epsilon]\leq e^{-2m\epsilon^2}
$$

ซึ่งจาก union bound เราสามารถสรุปได้เป็น

$$
\Pr[|\hat{R}(h)-R(h)|\geq \epsilon]\leq 2e^{-2m\epsilon^2}
$$

นั่นแสดงว่าหาก hypothesis space $H$ มีขนาดจำกัด เราสามารถจำกัดขอบเขตของความน่าจะเป็นที่จะมี
hypothesis $h$ บางตัวใน $H$ ที่มี empirical error $\hat{R}(h)$ แตกต่างจาก $R(h)$ เกิน $\epsilon$ ได้ดังนี้

$$
\begin{split}
\Pr[\exists h\in H: |\hat{R}(h)-R(h)|\geq\epsilon] &\leq\sum_{h\in H}\Pr[|\hat{R}(h)-R(h)|\leq\epsilon]\\
&\leq \sum_{h\in H} 2e^{-2m\epsilon^2}\\
&= 2|H|e^{-2m\epsilon^2}
\end{split}
$$

ถ้าเรากำหนดให้
$2|H|e^{-2m\epsilon^2}=\delta$
เราจะได้

$$
\epsilon = \sqrt{\frac{1}{2m}(\ln|H|+\ln\frac{2}{\delta})}
$$

นั่นคือ ด้วยความน่าจะเป็นไม่น้อยกว่า $1-\delta$ hypothesis $h$ ทุกตัวใน $H$ จะมีขอบเขตของ error ดังนี้

$$
R(h)\leq \hat{R}_S(h)+\sqrt{\frac{1}{2m}(\ln|H|+\ln\frac{2}{\delta})}
$$

หรือในมุมของ sample complexity ถ้าเรากำหนดให้ $2|H|e^{-2m\epsilon^2}\leq \delta$
เราจะรับประกันได้ว่า hypothesis $h\in H$ ใด ๆ จะมี $\hat{R}(h)$ แตกต่างจาก $R(h)$ ไม่เกิน $\epsilon$
ด้วยความน่าจะเป็นไม่น้อยกว่า $1-\delta$ ถ้าจำนวนตัวอย่างข้อมูลเป็น

$$
m\geq\frac{1}{2\epsilon^2}(\ln|H| +\ln\frac{2}{\delta})
$$


## Empirical risk minimization
เนื่องจากเราสามารถบีบความแตกต่างระหว่าง empirical error กับ expected error ได้
จะเห็นว่าหากเราอยากได้ hypothesis $h$ ที่มีอัตราความผิดพลาดโดยเฉลี่ยน้อยที่สุด ($R(h)$ น้อยที่สุด)
วิธีหนึ่งที่น่าสนใจคือการหา hypothesis ที่มีค่าความผิดพลาดบนตัวอย่างข้อมูลใน $S$ น้อยที่สุด เราเรียกแนวทางการเลือก hypothesis เช่นนี้ว่า _empirical risk minimization_ ซึ่ง หาก $h_{ERM}$ เป็น hypothesis ที่ได้จากการเลือกดังกล่าว นั่นคือ

$$
h_{ERM}=\arg\min_{h\in H}\hat{R}(h)
$$

และให้ $$h^*$$ เป็น hypothesis ที่มีอัตราความผิดพลาดโดยเฉลี่ยหรือ risk น้อยที่สุดใน $H$ เราจะสามารถหา generalization bound ของ $R(h_{ERM})$ เทียบกับ $R(h^*)$ ได้ดังนี้

$$
\begin{split}
R(h_{ERM}) - R(h^*) & = R(h_{ERM}) - \hat{R}(h_{ERM}) + \hat{R}(h_{ERM}) - R(h^*)\\
&\leq R(h_{ERM}) - \hat{R}(h_{ERM}) + \hat{R}(h^*) - R(h^*)\\
&\leq 2\epsilon
\end{split}
$$

โดยจากบรรทัดที่ 1 มาบรรทัดที่ 2 เราใช้ความจริงที่ว่า $\hat{R}(h_{ERM})\leq \hat{R}(h^*)$
เนื่องจากเราเลือก $h_{ERM}$ ที่มี empirical error น้อยที่สุด

เพราะฉะนั้น ด้วยความน่าจะเป็นไม่น้อยกว่า $1-\delta$

$$
R(h_{ERM})\leq R(h^*) + \sqrt{\frac{2}{m}(\log|H|+\log\frac{2}{\delta})}
$$

หรือกล่าวได้อีกอย่างว่า ถ้าจำนวนตัวอย่างข้อมูลเป็น

$$
m\geq\frac{1}{2\epsilon^2}(\ln|H| +\ln\frac{2}{\delta})
$$

ด้วยความน่าจะเป็นไม่น้อยกว่า $1-\delta$ อัลกอริทึม estimation risk minimization จะให้ผลลัพธ์เป็น hypothesis $h_{ERM}$ ที่มี error

$$
R(h_{ERM})\leq R(h^*)+2\epsilon
$$
