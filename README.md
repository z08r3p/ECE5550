java c
ECE5550: Applied Kalman Filtering 
NONLINEAR KALMAN FILTERS 
6.1: Extended Kalman ﬁlters 
■ We return to the basic problem of   estimating the   present   hidden   state   (vector) value of a dynamic system, using   noisy   measurements that            are somehow related to that state   (vector).
■ We   now examine the   nonlinear case, with system dynamics xk = fk−1(xk−1, uk−1,wk−1)
z k = hk (xk, uk,vk ),
where uk is a known   (deterministic/measured) input   signal,wk is   a            process-noise random input, and vk is a   sensor-noise   random   input.
■ There are three basic nonlinear   generalizations to   KF
• Extended Kalman ﬁlter (EKF): Analytic linearization of the   model at   each point   in time.   Problematic, but   still   popular.
• Sigma-point (Unscented) Kalman ﬁlter (SPKF/UKF): Statistical/ empirical linearization of the   model at each   point   in time.   Much      better than   EKF, at same computational complexity.
• Particle ﬁlters :   The   most precise, but often thousands of   times   more computations required than either   EKF/SPKF.   Directly
approximates the   integrals required to compute f (xk |   Zk )   using   Monte-Carlo integration techniques.
■ In this chapter, we   present the   EKF   and   SPKF.
The Extended Kalman Filter (EKF) 
■ The   EKF   makes two simplifying assumptions when adapting the   general sequential inference equations to a   nonlinear system:
•   In computing state estimates,   EKF assumes E[fn(x)] ≈ fn(E[x]);
•   In computing covariance estimates,   EKF uses Taylor series to
linearize the system equations around the present operating   point.
■ Here, we will show how to   apply these   approximations   and
assumptions to derive the   EKF equations from the general six steps.
EKF step 1a: State estimate   time   update.
■ The state prediction step   is approximated as
ˆ(x)   = E[fk−1(xk−1   , uk−1,wk−1)   |   Zk−1]
≈ fk−1(ˆ(x)1   , uk−1   ,   ¯(w)k−1),
where   ¯(w)k−1    = E[wk−1].   (Often,¯(w)k−1    = 0.)
■ That is, we approximate the expected value of the state   by   assuming
it is   reasonable to propagateˆ(x)1    and¯(w)k−1    through 代 写ECE5550: Applied Kalman Filtering NONLINEAR KALMAN FILTERSJava
代做程序编程语言the state eqn.
EKF step 1b: Error covariance time   update.
■ The covariance prediction   step is accomplished   by   ﬁrst   making   an
approximation for˜(x)   .
x˜k− = xk − ˆxk−
= fk−1(xk−1, uk−1, wk−1) − fk−1(xˆk+−1, uk−1, w¯ k−1).
■ The ﬁrst term is expanded as a   Taylor   series   around   the   prior
operating “point” which is the set of   values   {ˆ(x)1   , uk−1   ,   ¯(w)k−1}


Deﬁned   as k —   1

一一 
Deﬁned   as k —   1
■ k— ≈ ( k—1k(十)—1 十 ).
■ Substituting this to ﬁnd the predicted covariance:

≈ k—1Σ,k — 1 k(T)— 1 十 k—1k(T)— 1   .
■ Note, by the   chain   rule   of   total   differentials,





0

0

■ Similarly,

■ The distinction between the total differential and the   partial differential   is   not critical at this   point,   but will   be   when   we   look   at   parameter
estimation using extended   Kalman ﬁlters.
EKF step 1c: Output estimate   (where k = E[vk ]).
■ The system output is   estimated to   be
k = E[hk (xk, uk,vk )   |   Zk —   1] ≈ hk (^(x)k— , uk,   v-k ).■ That is, it is assumed that propagating xˆk− and the mean sensor noise is the best approximation to estimating the output.
EKF step 2a: Estimator gain   matrix.
■ The output prediction error   may then be   approximated


using again a Taylor-series expansion on the ﬁrst   term.
z k ≈ hk (^(x)k— , uk,   v-k )

■ Note,   much   like we saw   in   Step   1b,


■ From this, we can compute such necessary   quantities   as

z˜,k ≈ˆCk −˜x,kˆCkT +ˆDk v˜ˆDkT,−˜x˜z,k
≈ E[(x˜k−(ˆCk x˜k−ˆDkv˜k)T ] =  x−˜,kˆCkT .
■ These terms may be combined to   get the   Kalman gain
Lk =    −˜ x, kCkT 	 Cˆk x−˜,kCˆTk+ Dˆk v˜ DˆTk−1.
EKF step 2b: State estimate   measurement   update.
■ The ﬁfth step   is to compute the a posteriori state estimate by   updating the a priori estimate
^(x)k(十) =   ^(x)k— 十 Lk (z k — k ).
EKF step 2c: Error covariance measurement   update.
■ Finally, the   updated covariance is   computed   as
+˜ x, k = −˜ x, k − Lk z˜ , kLkT = (I − Lk ˆ Ck)x−˜ , k.







         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
