---
layout: post
title: Uncertainty and sensitivity analysis
description: Performing uncertainty and sensitivity analyses of scientific models is an essential aspect of the development process. This post introduces a short monograph on different sensitivity and uncertainty quantification methodologies which can be used to investigate quantitative models.
---

I performed a literature review of uncertainty and sensitivity analysis methods at an early stage of my PhD. The lit review never made it into the final thesis due to the nature of research, but I'd like to share it so I can pretend that the effort wasn't wasted!

Uncertainty and sensitivity analysis are interlinked but seperate tasks. An uncertainty analysis quantifies how uncertainty in input variables of a scientific model influence the total uncertainty. A sensitivity analysis identifies how individual variables influence the output of the total model. 

I have turned the specific section of the literature review into a monograph which can be found [here]({{ site.url }}/assets/monos/uncertainty_and_sensitivity_analysis.pdf). I found the [thesis](https://www.researchgate.net/publication/308618624_The_Value_of_Learning_about_Critical_Energy_System_Uncertainties) by Will Usher very useful as a starting point for my research. The [Python library](https://github.com/SALib/SALib) is the implementation of multiple methods for actually running sensitivity analysis models.