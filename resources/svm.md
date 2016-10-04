## Multi-Class SVM

多类SVM希望对于正确类别的预测score值比其它错误类别的预测score值至少大于`delta`, 如下图表示:

![mc-svm](http://cs231n.github.io/assets/margin.jpg mc-svm)

损失函数可以表示为:

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
<semantics>
<mrow>
<msub>
<mi>L</mi>
<mi>i</mi>
</msub>
<mo>=</mo>
<munder>
<mo>&#x2211;<!-- ∑ --></mo>
<mrow class="MJX-TeXAtom-ORD">
<mi>j</mi>
<mo>&#x2260;<!-- ≠ --></mo>
<msub>
<mi>y</mi>
<mi>i</mi>
</msub>
</mrow>
</munder>
<mo movablelimits="true" form="prefix">max</mo>
<mo stretchy="false">(</mo>
        <mn>0</mn>
        <mo>,</mo>
        <msubsup>
        <mi>w</mi>
        <mi>j</mi>
        <mi>T</mi>
        </msubsup>
        <msub>
        <mi>x</mi>
        <mi>i</mi>
        </msub>
        <mo>&#x2212;<!-- − --></mo>
        <msubsup>
        <mi>w</mi>
        <mrow class="MJX-TeXAtom-ORD">
        <msub>
        <mi>y</mi>
        <mi>i</mi>
        </msub>
        </mrow>
<mi>T</mi>
</msubsup>
<msub>
<mi>x</mi>
<mi>i</mi>
</msub>
<mo>+</mo>
<mi mathvariant="normal">&#x0394;<!-- Δ --></mi>
<mo stretchy="false">)</mo>
</mrow>
<annotation encoding="application/x-tex">L_i = \sum_{j\neq y_i} \max(0, w_j^T x_i - w_{y_i}^T x_i + \Delta)</annotation>
</semantics>
</math>
