"Wait, the singularity is just humans freaking out?" "Always has been."

Everyone in San Francisco is talking about the singularity. At dinner parties, at coffee shops, at the OpenClaw meetup where Ashton Kutcher showed up for some reason. The conversations all have the same shape: someone says it's coming, someone says it's hype, and nobody has a number.

This seems like the wrong question. If things are accelerating (and they measurably are) the interesting question isn't *whether*. It's *when*. And if it's accelerating, we can calculate exactly when.

I collected five real metrics of AI progress, fit a hyperbolic model to each one independently, and found the one with genuine curvature toward a pole. The date has millisecond precision. There is a countdown.

(I am aware this is unhinged. We're doing it anyway.)

## The Data

Five metrics, chosen for what I'm calling their *anthropic significance* (anthropic here in the Greek sense ("pertaining to humans"), not the company, though they appear in the dataset with suspicious frequency):

- **MMLU scores**: the SAT for language models

- **Tokens per dollar**: cost collapse of intelligence (log-transformed, because the Gemini Flash outlier spans 150× the range otherwise)

- **Frontier release intervals**: shrinking gap between "holy shit" moments

- **arXiv "emergent" papers** (trailing 12mo): field excitement, measured memetically

- **Copilot code share**: fraction of code written by AI

Calibrating instruments...

Each metric normalized to [0,1][0, 1][0,1]. Release intervals inverted (shorter = better). Tokens per dollar log-transformed before normalizing (the raw values span five orders of magnitude; without the log, Gemini Flash at 2.5M tokens/$ dominates the fit and everything else is noise). Each series keeps its own scale, no merging into a single ensemble.

## Why Hyperbolic

Most people extrapolate AI with exponentials. Wrong move!

An exponential f(t)=aebtf(t) = ae^{bt}f(t)=aebt approaches infinity only as t→∞t \to \inftyt→∞. You'd be waiting forever. Literally.

We need a function that hits infinity at a *finite* time. That's the whole point of a singularity: a pole, a vertical asymptote, the math breaking:

x(t)=kts−t+cx(t) = \frac{k}{t_s - t} + cx(t)=ts​−tk​+c

As t→ts−t \to t_s^-t→ts−​, the denominator goes to zero. x(t)→∞x(t) \to \inftyx(t)→∞. Not a bug. *The* feature.

Calibrating instruments...

**Polynomial** growth (tnt^ntn) never reaches infinity at finite time. You could wait until heat death and t47t^{47}t47 would still be finite. Polynomials are for people who think AGI is "decades away."

**Exponential** growth reaches infinity at t=∞t = \inftyt=∞. Technically a singularity, but an infinitely patient one. Moore's Law was exponential. We are no longer on Moore's Law.

**Hyperbolic** growth is what happens when the thing that's growing *accelerates its own growth*. Better AI → better AI research tools → better AI → better tools. Positive feedback with supralinear dynamics. The singularity is real and finite.

## The Fit

The procedure is straightforward, which should concern you.

The model fits a separate hyperbola to each metric:

yi(j)=kjts−ti+cjy_i^{(j)} = \frac{k_j}{t_s - t_i} + c_jyi(j)​=ts​−ti​kj​​+cj​

Each series jjj gets its own scale kjk_jkj​ and offset cjc_jcj​. The singularity time tst_sts​ is shared. MMLU scores and tokens-per-dollar have no business being on the same y-axis, but they can agree on when the pole is.

For each candidate tst_sts​, the per-series fits are linear in kjk_jkj​ and cjc_jcj​. The question is: which tst_sts​ makes the hyperbola fit best?

Here's the thing nobody tells you about fitting singularities: most metrics don't actually have one. If you minimize total RSS across all series, the best tst_sts​ is always at infinity. A distant hyperbola degenerates into a line, and lines fit noisy data just fine. The "singularity date" ends up being whatever you set as the search boundary. You're finding the edge of your search grid, not a singularity.

So instead, we look for the real signal. For each series independently, grid search tst_sts​ and find the R² peak: the date where hyperbolic fits *better* than any nearby alternative. If a series genuinely curves toward a pole, its R² will peak at some finite tst_sts​ and then decline. If it's really just linear, R² will keep increasing as ts→∞t_s \to \inftyts​→∞ and never peak. No peak, no signal, no vote!

One series peaks! arXiv "emergent" (the count of AI papers about emergence) has a clear, unambiguous R² maximum. The other four are monotonically better fit by a line. The singularity date comes from the one metric that's actually going hyperbolic.

This is more honest than forcing five metrics to average out to a date that none of them individually support.

Same inputs → same date. Deterministic. The stochasticity is in the universe, not the model.

## The Date

Calibrating instruments...

The fit converged! Each series has its own R² at the shared tst_sts​, so you can see exactly which metrics the hyperbola captures well and which it doesn't. arXiv's R² is the one that matters. It's the series that actually peaked.

The 95% confidence interval comes from profile likelihood on tst_sts​. We slide the singularity date forward and backward until the fit degrades past an F-threshold.

## The Countdown

Calibrating instruments...

## Sensitivity

How much does the date move if we drop one metric entirely?

Calibrating instruments...

If dropping a single series shifts tst_sts​ by years, that series was doing all the work. If the shifts are zero, the dropped series never had a signal in the first place.

The table tells the story plainly: arXiv is doing all the work. Drop it and the date jumps to the search boundary (no remaining series has a finite peak). Drop anything else and nothing moves. They were never contributing to the date, only providing context curves at the shared tst_sts​.

Note: Copilot has exactly 2 data points and 2 parameters (kkk and ccc), so it fits any hyperbola perfectly. Zero RSS, zero influence on tst_sts​. It's along for the ride!

## What tst_sts​ Actually Means

The model says y→∞y \to \inftyy→∞ at tst_sts​. But what does "infinity" mean for arXiv papers about emergence? It doesn't mean infinitely many papers get published on a Tuesday in 2034.

It means the model breaks. tst_sts​ is the point where the current trajectory's curvature can no longer be sustained. The system either breaks through into something qualitatively new, or it saturates and the hyperbola was wrong. A phase transition marker, not a physical prediction.

tst_sts​ is the moment he looks down.

But here's the part that should unsettle you: **the metric that's actually going hyperbolic is human attention, not machine capability.**

MMLU, tokens per dollar, release intervals. The actual capability and infrastructure metrics. All linear. No pole. No singularity signal. The only curve pointing at a finite date is the count of papers about emergence. Researchers noticing and naming new behaviors. *Field excitement, measured memetically.*

The data says: machines are improving at a constant rate. Humans are freaking out about it at an accelerating rate that accelerates its own acceleration.

That's a very different singularity than the one people argue about.

## The Social Singularity

If tst_sts​ marks when the rate of AI surprises exceeds human capacity to process them, the interesting question isn't what happens to the machines. It's what happens to us.

And the uncomfortable answer is: it's already happening.

**The labor market isn't adjusting. It's snapping.** In 2025, [1.1 million layoffs were announced](https://fortune.com/2025/12/09/forever-layoffs-job-security-k-shaped-economy-white-collar-recession-challenger-glassdoor/). Only the sixth time that threshold has been breached since 1993. Over [55,000 explicitly cited AI](https://www.cnbc.com/2025/11/04/white-collar-layoffs-ai-cost-cutting-tariffs.html). But [HBR found](https://hbr.org/2026/01/companies-are-laying-off-workers-because-of-ais-potential-not-its-performance) that companies are cutting based on AI's *potential*, not its performance. The displacement is anticipatory. The curve doesn't need to reach the pole. It just needs to *look like it will*.

**Institutions can't keep up.** The EU AI Act's high-risk rules have [already been delayed to 2027](https://artificialintelligenceact.eu/). The US [revoked its own 2023 AI executive order](https://www.metricstream.com/blog/ai-regulation-trends-ai-policies-us-uk-eu.html) in January 2025, then issued a new one in December trying to preempt state laws. California and Colorado are [going their own way anyway](https://www.softwareimprovementgroup.com/blog/us-ai-legislation-overview/). The laws being written today regulate 2023's problems. By the time legislation catches up to GPT-4, we're on GPT-7. When governments visibly can't keep up, trust doesn't erode. It [collapses](https://phys.org/news/2025-10-falters-weak-digital-misinformation.html). Global trust in AI has dropped to 56%.

**Capital is concentrating at dot-com levels.** The top 10 S&amp;P 500 stocks (almost all AI-adjacent) hit [40.7% of index weight](https://www.apolloacademy.com/wp-content/uploads/2025/09/ExtremeAIConcentration-090825.pdf) in 2025, surpassing the dot-com peak. Since ChatGPT launched, AI-related stocks have captured [75% of S&amp;P 500 returns, 80% of earnings growth, and 90% of capital spending growth](https://www.cnbc.com/2025/10/22/your-portfolio-may-be-more-tech-heavy-than-you-think.html). The Shiller CAPE is at [39.4](https://www.ainvest.com/news/market-concentration-500-record-year-history-warns-2026-2512/). The last time it was this high was 1999. The money flooding in doesn't require AI to actually reach superintelligence. It just requires enough people to believe the curve keeps going up.

**People are losing the thread.** Therapists are [reporting a surge](https://www.cnbc.com/2026/01/24/ai-artificial-intelligence-worries-therapy.html) in what they're calling FOBO (Fear of Becoming Obsolete). The clinical language is striking: patients describe it as *"the universe saying, 'You are no longer needed.'"* [60% of US workers](https://allwork.space/2026/01/long-term-fears-build-as-60-of-u-s-workers-say-ai-will-cut-more-jobs-than-it-adds-in-2026/) believe AI will cut more jobs than it creates. AI usage is up 13% year-over-year, but confidence in it has [dropped 18%](https://fortune.com/2026/01/21/ai-workers-toxic-relationship-trust-confidence-collapses-training-manpower-group/). The more people use it, the less they trust it.

**The epistemics are cracking.** Less than [a third of AI research is reproducible](https://research.aimultiple.com/reproducible-ai/). Under 5% of researchers share their code. Corporate labs are publishing less. The gap between what frontier labs know and what the public knows is growing, and the people making policy are operating on information that's [already obsolete](https://www.cfr.org/articles/how-2026-could-decide-future-artificial-intelligence). The experts who testify before Congress contradict each other, because the field is moving faster than expertise can form.

**The politics are realigning.** [TIME](https://time.com/7371825/trump-data-center-ai-backlash-ai-america-china/) is writing about populist AI backlash. [Foreign Affairs](https://www.foreignaffairs.com/united-states/coming-ai-backlash) published "The Coming AI Backlash: How the Anger Economy Will Supercharge Populism." [HuffPost](https://www.huffpost.com/entry/the-coming-war-over-ai-will-define-the-2026-midterms_n_6953f7fbe4b06a970133dfb7) says AI will define the 2026 midterms. MAGA is [splitting](https://www.cnn.com/2026/02/02/politics/artificial-intelligence-maga-divide-trump) over whether AI is pro-business or anti-worker. Sanders proposed a data center moratorium. The old left-right axis is buckling under the weight of a question it wasn't built to answer.

All of this is happening **eight years before tst_sts​**. The social singularity is front-running the technical one. The institutional and psychological disruption doesn't wait for capabilities to go vertical. It starts as soon as the *trajectory* becomes legible.

The pole at tst_sts​ isn't when machines become superintelligent. It's when humans lose the ability to make coherent collective decisions about machines. The actual capabilities are almost beside the point. The social fabric frays at the seams of attention and institutional response time, not at the frontier of model performance.

## Caveats

**The date comes from one series.** arXiv "emergent" is the only metric with genuine hyperbolic curvature. The other four are better fit by straight lines. The singularity date is really "the date when AI emergence research goes vertical." Whether field excitement is a leading indicator or a lagging one is the crux of whether this means anything.

**The model assumes stationarity.** Like assuming the weather will continue to be "changing." The curve will bend, either into a logistic (the hype saturates) or into something the model can't represent (genuine phase transition). tst_sts​ marks where the current regime can't continue, not what comes after.

**MMLU is hitting its ceiling.** Benchmark saturation introduces a leptokurtic compression artifact. MMLU's low R² reflects this. The hyperbola is the wrong shape for saturating data.

**Tokens per dollar is log-transformed** (values span five orders of magnitude) **and non-monotonic** (GPT-4 cost more than 3.5; Opus 4.5 costs more than DeepSeek-R1). The cost curve isn't smooth: it's Pareto advances interspersed with "we spent more on this one."

**Five metrics isn't enough.** More series with genuine hyperbolic curvature would make the date less dependent on arXiv alone. A proper study would add SWE-bench, ARC, GPQA, compute purchases, talent salaries. I used five because five fits in a table.

**Copilot has two data points.** Two parameters, two points, zero degrees of freedom, zero RSS contribution. The sensitivity analysis confirms it doesn't matter.

## Conclusion

Real data. Real model. Real date!

The math found one metric curving toward a pole on a specific day at a specific millisecond: the rate at which humans are discovering emergent AI behaviors. The other four metrics are linear. The machines are improving steadily. We are the ones accelerating!

The social consequences of that acceleration (labor displacement, institutional failure, capital concentration, epistemic collapse, political realignment) are not predictions for 2034. They are descriptions of 2026. The singularity in the data is a singularity in human attention, and it is already exerting gravitational force on everything it touches.

I see no reason to let epistemological humility interfere with a perfectly good timer.
See you on the other side!

## Correction (Feb 11, 2026)

[Connor Shepherd](https://x.com/connorshepherd/status/2021658170721222825) pointed out that three of the MMLU scores were wrong. He's right. I'm sorry. Here's what happened:

- **Claude 3.5 Sonnet:** I wrote 88.7%. The actual score is [88.3%](https://github.com/openai/simple-evals#readme). The 88.7% is GPT-4o's score. I mixed up the rows. In a post about rigorous data analysis. Yes.

- **o1:** I wrote 90.8%. That's o1-preview. The full o1 scored [91.8%](https://github.com/openai/simple-evals#readme).

- **GPT-4.5:** I wrote 89.6%. The actual score is [90.8%](https://github.com/openai/simple-evals#readme).

I have corrected all three values and rerun the fit. The new singularity date is: the same date. To the millisecond. Because MMLU, as the sensitivity analysis already told you in the table above, has exactly zero influence on tst_sts​. It's a linear series with no hyperbolic peak. Correcting the scores is like fixing a typo in the passenger manifest of a plane that's already landed.

I regret the errors. I do not regret the countdown.