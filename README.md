Download Link: https://assignmentchef.com/product/solved-stat823-homework-11-logistic-regression
<br>



<h1>Directions</h1>

Using RMarkdown in RStudio, complete the following questions. Launch RStudio and open a new RMarkdown file or use the class RMarkdown template provided and save it on your working directory as a .Rmd file. At the end of the activity, save your <strong>pdf </strong>generated from RMarkdown+Knitr and submit your homework on the Blackboard.

<strong>Only question 1 is required. Question 2 is optional.</strong>

If you have questions, please post them on the <strong>lesson discussion board</strong>.

Some <strong>R-codes </strong>and <strong>output </strong>from the code have been provided for you. R codes and output must be clearly shown.

<strong>Homework submitted after the due date will attract a penalty of </strong><strong>10 points per day after the due date.</strong>

<h1>1           Logistic Regression Analyses</h1>

<ol>

 <li>Use R to complete the following:</li>

</ol>

(a) Plot the mean response function of a logistic regression model,

<em>exp</em>(<em>β</em><sub>0 </sub>+ <em>β</em><sub>1</sub><em>X<sub>i</sub></em>)

<em>Pr</em>(<em>Y<sub>i </sub></em>= 1) =

1 + <em>exp</em>(<em>β</em><sub>0 </sub>+ <em>β</em><sub>1</sub><em>X<sub>i</sub></em>)

when <em>β</em><sub>0 </sub>= <em>−</em>25 and <em>β</em><sub>1 </sub>= 0<em>.</em>2. <strong>Hint: </strong>generate values of <em>X </em>over the range <em>∼ </em>90 <em>≤ X ≤∼ </em>160, then plug <em>X </em>into the mean response function and use the plot(x,y,type = “l”) command.

<table width="670">

 <tbody>

  <tr>

   <td width="670">x &lt;- <strong>seq</strong>(90, 160, 1) b0 &lt;- -25 b1 &lt;- 0.2 y &lt;- <strong>exp</strong>(b0 <strong>+ </strong>b1 <strong>* </strong>x)<strong>/</strong>(1 <strong>+ </strong><strong>exp</strong>(b0 <strong>+ </strong>b1 <strong>* </strong>x))<em># ilogit is a function that does: exp(x)/(1+exp(x))</em></td>

  </tr>

 </tbody>

</table>

<ul>

 <li>For what value of <em>X </em>is <em>Pr</em>(<em>Y </em>) = 0<em>.</em>5?</li>

 <li>Find the odds:</li>

</ul>

<em>Pr</em>(<em>Y </em>= 1)

1 <em>− Pr</em>(<em>Y </em>= 1)

Page -1- of 2

when <em>X </em>= 150 and when <em>X </em>= 151, and the ratio of the odds when <em>X </em>= 151 (numerator) to the odds when <em>X </em>= 150 (denominator). Is this odds ratio equal to exp(<em>β</em><sub>1</sub>) as it should be?

Optional 2. A marketing research firm was engaged by an automobile manufacturer to conduct a pilot study to examine the feasibility of using logistic regression for predicting whether a family will purchase a new car during the next year. A random sample of 33 suburban families was selected. Data on annual family <em>income </em>(<em>X</em><sub>1</sub>, in thousand dollars) and the current <em>age </em>of the oldest family automobile (<em>X</em><sub>2</sub>, in years) were obtained. A follow-up interview conducted 12 months later was used to determine whether the family actually purchased a new car (<em>Y </em>= 1 or did not purchase a new car (<em>Y </em>= 0) during the year. Use the attached dataset Q2 to answer the following. Assume that a multiple logistic regression model with two predictor variables is appropriate:

<ul>

 <li>Fit the model and find the estimates of <em>β</em><sub>0</sub>, <em>β</em><sub>1</sub>, and <em>β</em><sub>2</sub>. Plot the estimated function over the data.</li>

</ul>

<table width="670">

 <tbody>

  <tr>

   <td width="670"><strong>rm</strong>(list = <strong>ls</strong>(all = TRUE)[<strong>!</strong><strong>grepl</strong>(“global.var.A”, <strong>ls</strong>(all = TRUE))]) q2 &lt;- <strong>read.table</strong>(“data/Q2.txt”, quote = “””, comment.char = “”) <strong>str</strong>(q2) <strong>colnames</strong>(q2) &lt;- <strong>c</strong>(“y”, “income”, “age”) <strong>require</strong>(epiDisplay) <strong>summ</strong>(q2) mod2 &lt;- <strong>glm</strong>(y <strong>~ </strong>income <strong>+ </strong>age, family = <strong>binomial</strong>(link = “logit”), data = q2)<strong>summary</strong>(mod2) <strong>library</strong>(epiDisplay)</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Find and interpret estimates of exp(<em>β</em><sub>1</sub>) and exp(<em>β</em><sub>2</sub>).</li>

 <li>What is the estimated probability that a family with annual income of 50 thousand and an oldest car of 3 years will purchase a new car next year? Compute a 95% interval estimate for this probability.</li>

</ul>

<table width="670">

 <tbody>

  <tr>

   <td width="670"><em># predicted probability for income = 50, age = 3 </em><strong>library</strong>(faraway)<strong>ilogit</strong>(b0 <strong>+ </strong>b1 <strong>* </strong>50 <strong>+ </strong>b2 <strong>* </strong>3) <em># Approach 1 # A 60.9% predicted chance of buying a car x0 &lt;-</em><em># c(1, 50, 3) eta0 &lt;- sum(x0*coef(mod2))</em><em># ilogit(eta0)</em><strong>predict</strong>(mod2, newdata = <strong>data.frame</strong>(income = 50, age = 3), type = “response”)(pr1 &lt;- <strong>predict</strong>(mod2, newdata = <strong>data.frame</strong>(income = 50, age = 3), se = T))<em># predicted 95% interval for this probability </em><strong>ilogit</strong>(<strong>c</strong>(pr1<strong>$</strong>fit <strong>– </strong>1.96 <strong>* </strong>pr1<strong>$</strong>se.fit, pr1<strong>$</strong>fit <strong>+ </strong>1.96 <strong>* </strong>pr1<strong>$</strong>se.fit))</td>

  </tr>

 </tbody>

</table>

<ul>

 <li>Calculate the confidence intervals for exp(<em>β</em><sub>1</sub>) and exp(<em>β</em><sub>2</sub>) and interpret.</li>

 <li>Assess model goodness of fit. Explain your results.</li>

</ul>