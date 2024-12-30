java c
ECE5550: Applied Kalman Filtering 
THE LINEAR KALMAN FILTER
4.1: Introduction 
■ The principal goal of this course   is to   learn   how to   estimate   the
present hidden state   (vector) value of   a dynamic   system,   using   noisy   measurements that are somehow related to that state   (vector).
■ We assume a general, possibly   nonlinear,   model
xk = fk−1(xk−1, uk−1,wk−1)
z k = hk (xk, uk ,vk ),
where uk is a   known   (deterministic/measured) input signal,   wk is   a            process-noise random input, and vk is a   sensor-noise   random   input.
SEQUENTIAL PROBABILISTIC INFERENCE: Estimate the present state xk of a dynamic system using   all   measurements Zk = {z0   , z 1   ,   ···   , z k }   .

■ This notes chapter provides a   uniﬁed theoretic framework to develop   a family of estimators for this task:   particle ﬁlters,   Kalman ﬁlters, extended   Kalman ﬁlters, sigma-point (unscented)   Kalman ﬁlters. . .
A smattering of estimation theory 
■ There are various approaches to “optimal estimation” of some   unknown quantity x .
■ One says that we would like to   minimize the expected   magnitude
(length) of the error vector between x and the   estimatex(ˆ) .

■ This turns out to be the   median of   the a posteriori pdf f (x |   Z).
■ A similar   result, but easier   to derive   analytically   minimizes the   expected length squared of that   error   vector.
■ This is the   minimum mean square   error   (MMSE)   estimator

■ We solve forx(ˆ) by differentiating the cost function and   setting   the
result to   zero

■ Another approach to estimation is to   optimize a   likelihood   function

■ Yet a fourth is the   maximum a posteriori estimate

■ In   general,x(^)MME      /=x(^)MMSE      /=x(^)ML      /=x(^)MAP   ,   so   which   is “best”? 
■ Answer:   It probably depends on the   application.
■ The text gives some metrics for comparison:   bias,   MSE,   etc.
■ Here, we usex(^)MMSE    = E[x |   Z] because it “makes sense” and works
well in a   lot of   applications   and   is   mathematically tractable.
Some examples 
■ In example   1,   mean,   median, and   mode are   identical.   Any   of these   statistics would   make a good estimator of x .
■ In example 2,   mean,   median, and   mode   are   all different.   Which to   ch代 写ECE5550: Applied Kalman Filtering THE LINEAR KALMAN FILTERJava
代做程序编程语言oose is   not   necessarily obvious.
■ In example 3, the distribution   is   multi-modal.   None   of the   estimates   is   likely to   be satisfactory!

4.2: Developing the framework 
■ The   Kalman ﬁlter applies the   MMSE estimation criteria to a   dynamic   system.   That is, our state estimate   is the   conditional   mean

where Rxk is the set comprising the   range   of   possible xk .
■ To   make progress toward implementing this estimator, we must   break f (xk |   Zk ) into   simpler   pieces.
■ We ﬁrst   use   Bayes’ rule to write:

■ We then break up Zk into smaller   constituent   parts   within   the joint   probabilities as Zk−1    and z k 

■ Thirdly, we   use   the   joint   probability   rule f (a , b)   = f (a | b)f (b) on   the numerator and denominator terms

■ Next, we apply   Bayes’   rule once again   in the terms   within the   [         ]

■ We   now cancel some terms from   numerator and denominator
■ Finally, recognize that zk is conditionally   independent   of   Zk−1    given xk 

■ So, overall, we   have shown that

KEY POINT #1: This shows that we can compute the desired density   recursively with two steps per   iteration:
■ The ﬁrst step computes probability densities for predicting xk given   all past   observations

■ The second step updates the   prediction via

■ Therefore, the general sequential inference solution breaks   naturally into a   prediction/update scenario.
■ To proceed further using this approach, the   relevant   probability   densities may be   computed   as

KEY POINT #2: Closed-form. solutions to solving the   multi-dimensional   integrals is   intractable for   most real-world systems.
■ For applications that justify the computational expense, the   integrals   may be approximated using   Monte Carlo   methods   (particle ﬁlters).
■ But, besides applications using particle ﬁlters, this   approach   appears   to be   a   dead   end.
KEY POINT #3: A simpliﬁed solution   may   be obtained   if we   are willing to
make the assumption that all probability densities are Gaussian.
■ This is the basis of the   original   Kalman ﬁlter,   the   extended   Kalman
ﬁlter, and the sigma-point (unscented) Kalman ﬁlters to   be   discussed.







         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
