# GSoC 17 - Final Report


This page concludes the last three months of the Google Summer of Code experience with open source organization _Performance Co-Pilot_(PCP). The experience was amazing as it involved  incredible amount of learning and coding (obviously :P). There was a lot of emphasis given to scalable design, QA, code sanity, etc. I would like to thank _Nathan Scott_ for being such a great mentor and helping me through out the project.


## Prometheus Metrics importer and exporter

[Performance co-pilot](http://pcp.io/) is a distributed system performance and analysis framework which mainly involves collecting the metrics and analyzing the metrics. I was working on the collection part of the PCP where a bridge had to be this summer where in I proposed to write a Performance metrics domain agent (PMDA) for importing the Prometheus metrics into PCP.
