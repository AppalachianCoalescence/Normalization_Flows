# Improving the Global Fit with Normalizing Flows

LISA is future gravitational wave mission and is a very challenging data analysis problem, you can read more about it in the [LISA Red Book](https://arxiv.org/abs/2402.07571).

## The problem (short version)
When we fit for sources in the LISA data, we get a list of parameter values, with more probable parameter values occurring more often.
(This is the same as the output of an MCMC algorithm, also known as an MCMC chain).
We would like to generate new parameter values given the list of the old values, consistent with the same probability distribution as the old values.

## The problem (long version)
One of the data processing steps of LISA is to find parameters that match theoretical models to each source, also known as parameter estimation. In the LISA community, this is usually done with a process called reversible jump MCMC, where new sources with random parameters are added and subtracted from the data until they do a "good job" fitting the data. Unlike a lot of other astronomy problems, we don't know how many sources there are in the data, so we have to add and subtract them during the MCMC. This whole process is known as the LISA Global Fit, because **every source has to be fit at the same time** as every other source. 

At the end of the global fit, we are left with MCMC chains, or a list of all parameter values that we considered while trying to fit the data with our source models. In other words, these chains are just an array of points in parameter space.

We would like to be able to generate new samples from the chain that have the same distribution as the old samples.
This will let us use the existing fit to each source as an MCMC prior when new data comes in, and keep what we've learned so far.

## The current state of the art

Currently, we have a method based on fitting the chains with [Gaussian Mixture Models](https://scikit-learn.org/stable/modules/mixture.html).
These unfortunately don't work well when the distribution of the points is not close to gaussian, and we need a very accurate fit to the points.

## The solution

Normalizing flows seem to be a much better method. We should try them on some example MCMC chains, and test if they are more accurate than the Gaussian Mixture Models.
If possible, we can also contribute this code to one of the LISA Global Fit pipelines, [GLASS](https://github.com/lisa-analysis-center/glass) or [Erebor](https://github.com/mikekatz04/LISAanalysistools). 

## Mentors/Collaborators
This work could be done with Robbie (@rjrosati), Alexander (@criswellalexander), and also with collaborators at NASA Marshall in Huntsville.
