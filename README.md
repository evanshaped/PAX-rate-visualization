# Visualizing ThorLABS polarimeter measurement rate

## Introduction
The THORLABS PAX1000 digital polarimeter is a rotating wave plate based polarimeter with a nominal measurement rate up to 400 Hz when using a supplementary power supply. While many would like to use this product for precise and consistent measurement of time-varying polarization signals, the PAX1000 unfortunately fails expectations in both measurement rate and, more importantly, rate consistency.

Many signal processing applications like noise quantification and signal stability analysis benefit from (if not require) evenly spaced points and high measurement rate to obtain accurate and useful results. The [Allan Deviation](https://en.wikipedia.org/wiki/Allan_variance) metric, for example, provides much less reliable noise quantification information when its input data points are not evenly spaced in time; I was only able to make use of this metric after understanding the measurement rate of the datasets I was taking.

This repository contains code I wrote to easily quantify and visualize the PAX's measurement rate (or more acurately, the time difference between points (tdbp)). It helped me to understand the quality and utility of my datasets, and may be of further use for others wishing to do the same.
<!-- Include picture of PAX, sample dataset with varying rate consistency, and rate histogram. -->
<!-- ![OpenAI Logo](https://example.com/openai_logo.png "OpenAI") -->

## Measurement rate instability
Ideally, the PAX1000 should take measurements evenly spaced in time - if the measurement rate is 20Hz, it should take a measurement every 0.05 seconds. Especially for higher measurement rates on the PAX (>80Hz), this "time difference between points" (TDBP) does not live up to expectations, and is furthermore widely varying throughout a given run.

Below is an example of poor behavior in a typical polarization dataset. I measured the output of a 10mW, 1345nm telecom laser at a nominal rate of 200Hz for 120 seconds. Shown is an arbitrary 1 second segment of the normalized [Stokes parameters](https://en.wikipedia.org/wiki/Stokes_parameters) that were recorded.

![Measurement plot](pax_hist_photos/meas_1.png "Measurement plot")

Notice the uneven spacing between data points. Calculating the time difference between each measurement in the whole dataset and plotting these values on a log-scale histogram, we can see how the distribution of these time differences compares to the nominal tdbp value of 0.005 seconds, marked in red. The average tdbp of the actual distribution is marked in blue, and the standard deviation in purple.

![Log Histogram plot](pax_hist_photos/hist_1.png "Log Histogram plot")

![Histogram plot](pax_hist_photos/hist_nolog_1.png "Histogram plot")

Keep in mind that the log scaling of the y-axis (frequency of occurrence) emphasizes uncommon occurrences, like the large gaps beyond 0.04 seconds.
