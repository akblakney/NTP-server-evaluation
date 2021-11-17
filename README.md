# NTP Server Evaluation Project

## Goal
The goal of this project is to develop a set of tools to assist in evaluating the accuracy, stability, and path delay associated with particular NTP servers.

## Metrics
The metrics we would like to evaluate for different NTP servers are the
accuracy of that server's time, i.e. its mean offset from a standard timescale
like UTC, or its deviation from a realization of UTC such as UTC(NIST); the variance of that server's time; and the distribution of the path delays associated with that NTP server (in particular their mean and variance).

## Approach 
In order to record these metrics reliably, we need to take many measurements of each server's time. However, many NTP servers disallow queries in quick succession, as this generates heavy traffic which is undesirable. As such, we will have to query servers over longer periods of time.

But this strategy introduces another complication: if we were to do many queries in a short amount of time, the servers' offsets from our system clock could be reliably interpreted in reference to our system time, and used to to calculate their mean, variance, and so on. But since we are instead forced to take measurements over a longer period of time, the drift on our system clock becomes significant enough that the servers' offsets from our system time cannot be attributed to changes in the server times alone; our system clock's drift could be contributing to patterns in the offsets from the server clocks.

To get around this, we will have to measure the drift of our system clock. Due
to the difficulty of writing mathematical equations in .md files, the full mathematical derivation and model for this task is outlined instead in 
