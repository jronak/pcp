# GSoC 17 - Final Report


This page concludes the last three months of the Google Summer of Code experience with open source organization _Performance Co-Pilot_(PCP). The experience was amazing as it involved  incredible amount of learning and coding (obviously :P). There was a lot of emphasis given to scalable design, QA, code sanity, etc. I would like to thank _Nathan Scott_ for being such a great mentor and helping me through out the project.


## Prometheus Metrics importer and exporter

[Performance co-pilot](http://pcp.io/) is a system performance and analysis framework which mainly involves collecting the metrics and analyzing the metrics. I was working on the collection part of the PCP and in simple terms my work involved implementing a bridge between PCP and Prometheus for inter-usability of the metrics.

Overall project can be divided into three phases/parts:
* Implement a Performance metrics domain agent (PMDA) for importing the Prometheus metrics into PCP (pmdaprometheus)
*  Implement a tool for exporting the PCP metrics in the format of Prometheus metircs.
*  Extending the PCP Python APIs to support the upcoming Labels for metrics.


#### PMDA Prometheus

I started with the PMDA as a proof of concept very early (April iirc) with very basic features and it gave a very good start. By the end of the community bonding period I was able to get the first version of PMDA.

[PR 285](https://github.com/performancecopilot/pcp/pull/285): <span style="color:#2ecc71">Merged</span>

PR includes first version of PMDA, config generator and QA. Initial design of the PMDA involved synchronous HTTP fetches from the Prometheus endpoints.

[PR 303](https://github.com/performancecopilot/pcp/pull/303) and [PR 305](https://github.com/performancecopilot/pcp/pull/305): <span style="color:#2ecc71">Merged</span>

PR includes QA for Prometheus Docker container and injection against PMDA.

[PR 323](https://github.com/performancecopilot/pcp/pull/323): <span style="color:#2ecc71">Merged</span>

Pr includes completely different scalable design for Parallel Http fetches and auto config generation during the runtime of the PMDA. This design was finalized after undergoing multiple design proposal ([PR 323](https://github.com/performancecopilot/pcp/pull/322): <span style="color:#e74c3c">Closed</span> and [PR 320](https://github.com/performancecopilot/pcp/pull/320): <span style="color:#e74c3c">Closed</span>)

#### Prometheus Exporter

According to the proposal the exporter was supposed to be a separate tool with only purpose of exporting the PCP metrics in the Prometheus format. After a good discussion with mentors it was decided to extend the existing PCP tool called _pmwebd_ (provides restful APIs to access PCP metrics) as it avoids blocking another and redundant effort for implementing similar APIs. I would like to thank _Frank Ch. Eigler_ for helping me out with pmwebd.

[PR 323](https://github.com/performancecopilot/pcp/pull/323): <span style="color:#2ecc71">Merged</span>

PR includes pmwebd with Prometheus exporter, caching the API results in the session and batch fetches.

[PR 335](https://github.com/performancecopilot/pcp/pull/335): <span style="color:#2ecc71">Merged</span>

PR includes QA for pmwebd Prometheus exporter.

[PR 336](https://github.com/performancecopilot/pcp/pull/336): <span style="color:#f39c12">Closed (Deferred)</span>

PR included addition of the labels to the existing pmwebd APIs, but has been deferred till PCP has stable labels support.

#### PCP Python APIs

PCP Python library uses ctypes for binding with core PCP APIs written in C. It was my first ever experience on working with Python and C bindings. Most of the work was extending the Python API to support Labels.


[PR 299](https://github.com/performancecopilot/pcp/pull/299) and [PR 306](https://github.com/performancecopilot/pcp/pull/306): <span style="color:#2ecc71">Merged</span>

PR included minor changes to the Python APIs to handle duplicates

[PR 318](https://github.com/performancecopilot/pcp/pull/318): <span style="color:#2ecc71">Merged</span>

PR included addition of Python APIs to support the Labels.

## Current Work


