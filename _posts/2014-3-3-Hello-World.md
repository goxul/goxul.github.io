---
layout: post
title: You're up and running!
---

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.





Hypothesis Testing
==================

-   When we perform a hypothesis test, we???re testing to see if the
    difference you see is due to random chance or if one is
    ???significantly??? different from another.

-   Basically, null hypothesis means that there is nothing interesting
    going on and it shows what you???d expect to see when things are
    normal.

-   Alternative hypothesis means that there is something interesting
    going on and means that the null hypothesis is wrong.

-   Null hypothesis is represented as $H_{0}$ and alternative as
    $H_{a}$.

-   Every test in statistics does the same thing: based on the sample
    data you have, it gives you the probability (P-value) that you might
    observe that data in the real world, given that the null hypothesis
    is true

-   The most commonly used test statistics are $Z-test$ and $t-test$.

-   Z- statistic is mostly used when the standard deviation of the
    population is known. Since this is rarely the case, most of the
    times we use the t-statistic in real life.

-   As sample size increases, t-distribution gets closer to the standard
    normal.

-   We can use F,Z, and T tests to create confidence intervals. Each of
    those tests is used for different samples. The T test is generally
    used when the total sample size is less than around 30. The Z test
    when it is above 30. The F test can be used for either, but this
    test is used to analyze the ratio of the variance of 2 samples.

-   To use the Z-test, the normality observation must be reasonable.

-   We can also check whether the data is normally distributed using QQ
    plots. IF it seems like a straight line, the data comes from a
    normal distribution.

-   The null hypothesis is accepted or rejected on the basis of:

    -   Rejection region approach

    -   p-value

-   The more commonly used method is the p-value approach.

-   p-value is a measure of the *strength* of the evidence against the
    null hypothesis.

-   How is the ???strength??? measured? One way of looking at it would be
    the area under the distribution.

-   How do we decide which area of the distribution we have to take? By
    the condition that evidence should be *against* the null hypothesis
    i.e using the Z-value.

-   Eg: Suppose Z = 1.53 for $$H_{0} : u = u_{0}$$ and
    $$H_{a} : u > u_{0}$$. Then, the p-value will be given as
    $$p-value = P(Z \geq 1.53)$$

-   This probability can be calculated by finding the relevant area
    under the distribution.

-   Usually, smaller the p- value, greater the evidence against the null
    hypothesis.

-   How small is small? That is decided by the *significance level* -
    given by $\alpha$.

-   Suppose a problem requires 95 $\%$ significance. That means reject
    the null hypothesis if $p-value \leq \alpha$.

-   $\alpha$ can be also interpreted as the area under the curve which
    has a corresponding Z-value.

-   Eg: For $\alpha = 0.0025$, the Z-value is 1.96 i.e
    $Z_{\alpha} = 1.96$. Z-values far out in the tails give strong
    evidence against the null hypothesis.

-   -   We can either use a 2-tail test or a 1-tail test. This decision
    comes at a trade-off. If we choose an one tail test, we completely
    loser power on the other side. For example, let
    $$H_{0}: \mu \neq 0, H_{a}: \mu < 0$$. Here, we won???t be able to
    detect if $\mu > 0$

**Musings on P values:**

-   p-values are used to test hypotheses.

-   Generally, we tend to prefer p-value which are statistically
    significant For e.g. $p < 0.05$ means it is significant and we
    reject the null hypothesis. But, they don???t give the complete
    picture and a particular decision should not be made only on the
    basis of p-values.

-   One example is : Suppose we have two paths to go home. One is a busy
    traffic way and the other is a scenic route. On a day when I have to
    go home ASAP, I conduct a statistical analysis and we get that the
    busy road is quicker with a p-value of $0.4$. This is not
    statistically significant but at that moment, it makes sense to take
    that road.

-   Suppose I do this analysis for two years. I arrive at the conclusion
    that the busy road is faster with a p-value of $0.001$ (highly
    significant) but the difference amounts to only 57 seconds. Thus,
    unless I am in an absolute hurry, I???d always choose the scenic path
    as one minute doesn???t make much of a difference.

-   Therefore, interpretation of the p-value is highly context
    dependent.


