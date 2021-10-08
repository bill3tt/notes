# The SPACE of Developer Productivity Notes

_These are my personal notes from [The SPACE of Developer Productvity](https://queue.acm.org/detail.cfm?id=3454124). All credit to the authors._

Developer productivity is necessary to improve the well-being & satisfaction of developers. Producivity & satisfaction are linked.

> The most important takeaway from exposing these myths is that productivity cannot be reduced to a single dimension (or metric!).
  * [Developer Productivity Myths](#developer-productivity-myths)
    + [Myth: Productivity is all about developer activity](#myth--productivity-is-all-about-developer-activity)
    + [Myth: Productivity is only about individual performance](#myth--productivity-is-only-about-individual-performance)
    + [Myth: One productivity metric can tell us everything](#myth--one-productivity-metric-can-tell-us-everything)
    + [Myth: Productivity Measures are useful only for managers](#myth--productivity-measures-are-useful-only-for-managers)
    + [Myth: Productivity is only about engineering systems and developer tools](#myth--productivity-is-only-about-engineering-systems-and-developer-tools)
  * [SPACE: A Framework for Understanding Developer Productivity](#space--a-framework-for-understanding-developer-productivity)
    + [Satisfaction and well-being](#satisfaction-and-well-being)
    + [Performance](#performance)
    + [Activity](#activity)
    + [Communication and collaboration](#communication-and-collaboration)
    + [Efficiency and flow](#efficiency-and-flow)
  * [How to use the framework](#how-to-use-the-framework)
    + [What to watch out for](#what-to-watch-out-for)
  * [Example](#example)
  * [Why this matters now](#why-this-matters-now)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## Developer Productivity Myths

### Myth: Productivity is all about developer activity

Higher volume of activity could be masking longer work hours dur to bad systems or poor planning to meet a release schedule.

Increased activity could be indicative of a range of things:
* Working longer hours to "brute-force" work to overcome bad systems or poor planning to meet a predefined release schedule.
* Better engineering systems, providing developers with the tools they need to do their jobs effectively.

Activity metrics should never be used in isolation.

### Myth: Productivity is only about individual performance

A developer who optimizes only for their own personal productivity may hurt the productivity of the team.
Finding the right balance in optimizing for individual, team, and organizational productivity, as well as understanding possible tradeoffs, is key.

### Myth: One productivity metric can tell us everything

Productivity represents several important dimensions of work and is greatly influenced by the context in which the work is done.

### Myth: Productivity Measures are useful only for managers

The idea that productivity measures are not useful often stems from the misue of measures by leaders or managers, particularly when implemented and measured poorly.

Research has shown that high productivity is highly correlated with feeling satisfied and happy with work.

### Myth: Productivity is only about engineering systems and developer tools

Human factors such as environment & culture can have a big impact too.

Things such as: morale building, mentoring, knowledge sharing are all critical to supporting a productive environment, but are rarely measured.

The "invisible" work that benefits the overall productivity of the team is just as important as other more commonly-measured dimensions

## SPACE: A Framework for Understanding Developer Productivity

### Satisfaction and well-being

*Satisfaction*: how fulfilled developers feel with thei work, team, tools or culture.
*Well-being*: how happy, healthy developer are and how their work imapcts it.

Productivity and satisfaction are correlated, it can even serve as a leading indicator for productivity.

To assess the satisfaction dimension, measure the following via surveys:
* Employee satisfaction. The degree of satisfaction among employees, and whether they would recommend their team to others.
* Developer efficacy. Whether developers have the tools and resources they need to get their work done.
* Burnout. Exhaustion caused by excessive and prolonged workplace stress.

### Performance

Performance of software developers is hard to measure:
* Lots of code, may not be good quality code.
* High quality code, may not deliver customer value.

Even if a developer's contribution can be tied to a business outcome, it is not _necessarily_ a reflection of performance as they may have been assigned a less impactful task.

Software is the sum of many developer's contributions - further complicating individual evaluation.

**Performance is often best evaluated as _outcomes_ instead of _output_.**

The most simplified view could be - did the code written by the developer reliably do what is was supposed to do?
* Quality. Reliability, absence of bugs, ongoing service health.
* Impact. Customer satisfaction, customer adoption and retention, feature usage, cost reduction.

### Activity

Activity is a count of actions or outputs completed in the course of performing work.

If measured correctly, activity can provide valuable but limited insights about developer producivity, engineering systems and team efficiency.

It is almost impossible to comprehensively measure and quantify all the facets of developer activity across engineering systems and environments.

Some developer activities that can be measured easily are:
* Design and coding. Volume or count of design documents and specs, work items, pull requests, commits, and code reviews.
* Continuous integration and deployment. Count of build, test, deployment/release, and infrastructure utilization.
* Operational activity. Count or volume of incidents/issues and distribution based on their severities, on-call participation, and incident mitigation.

These can be used as some measure of tractable developer activities, but should never be used in isolation.
They should always be customized based on organisational needs & environments.

Many activites are intractable and are missed in these measures: attending meetings, whiteboarding, knowledge sharing, helping others, providing architectural guidance to name a few.

### Communication and collaboration

Communication and collaboration capture how people and teams communicate and work together.

Software development is a collaborative and creative task that relies on extensive and effective communication, coordination, and collaboration within and between teams.

Effective teams that successfully contribute to and integrate each other's work efficiently rely on high transparency and awareness of team member activities and task priorities.

Teams that are diverse and inclusive are higher performing.

Work that contributes to team outcomes or supports another team's productivity may come at the expense of an individual's productivity.

Effective collaboration, can drive down the need for some individual activities (e.g., unnecessary code reviews and rework), improve system performance (faster pull requests), and help sustain productivity and avoid burnout.

Example metrics used as proxies to measure communication, collaboration and coordination:
* Discoverability of documentation and expertise.
* How quickly work is integrated.
* Quality of reviews of work contributed by team members.
* Network metrics that show who is connected to whom and how.
* Onboarding time for and experience of new members.

### Efficiency and flow

Efficiency and flow: the ability to complete work or make progress on it with minimal interruptions or delays.

Developers often associate productivity with the ability to get complex tasks done with minimal interruptions - i.e. 'getting into the flow'.

For individual efficiency, it is important to set boundaries to get & stay productive i.e. blocking out time for focus.

For team and system level efficiency, value-stream mapping is important, which captures the steps needed to take software from idea and creation to delivering it to the end customer.

Deployment frequency measures how often an organization successfully releases to production, and lead time for changes measures the amount of time taken to getting a commit into production.

The flow of knowledge and information is important.

Some metrics to capture efficiency and flow dimensions are:
* Number of handoffs in a process; number of handoffs across different teams in a process.
* Perceived ability to stay in flow and complete work.
* Interruptions: quantity, timing, how spaced, impact on development work and flow.
* Time measures through a system: total time, value-added time, wait time.

## How to use the framework

To measure productivity, teams should capture several metrics across multiple dimensions of the framework - at least 3.

At least one metric should include perceptual measures such as survey data - this gives a much broader picture of productivity.

Often times, metrics will be in conflict, this is good as is paints a nuanced picture of your work & systems.

What do people deem important in an organisation? Find out what is being measured, as that communicates what is valued and influences the way people behave and react.

### What to watch out for

Too many metrics can lead to confusion and lower motivation - you don't need all dimensions to be helpful.

Presented with an extensive list, it will feel overwhelming for the team and lower motivation.

Any measurement should be used carefully - it is never a perfect proxy.

Teams & organizations should be cognizant of privacy and only report anonymized aggregate results at the team or group level.

## Example

SRE team.

* Satisfaction: how satisfied are SREs with the IM process, escalation, routing and on-call rotations?
* Performance: focus on system reliability, monitoring system's ability to detect and flag issues faster, before they hit the customer. MTTR.
* Activity: number of issues caught by the monitoring systems, number of incidents created, number of incidents resolved.
* Communication and collaboration: do people communicate effectively during an incident? Are things properly documented?
* Efficiency and flow: number of hops before an incident is assigned to the right individual or team.


## Why this matters now

Developer producivity is about more than an individual's activity levels or the engineering systems relied on to ship software.

This framework captures many different dimensions, without it, harmful myths about productivity may persist.

Measuring productivity requires thinking about the wider context.