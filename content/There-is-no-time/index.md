+++
title = "There is no time for that"
description = "How to quantify and sell an investment on improving on technical debt to your organization"
date = 2023-01-09
draft = false
slug = "there-is-no-time"

[taxonomies]
categories = ["lean","project-management"]
tags = ["time-management","waste","managing-up"]

[extra]
comments = true
+++

# "There is no time for that":.

Whatever role you are in as a technical person you are usually in a context where you are a cost center to an organization on a budget in the public sector or with a profit goal in the private sector. The only profit center for a company is possibly maybe even only a paying customer according to Peter Drucker. Or a satisfied taxpayer if you are in the public sector. Not everyone works at a FAANG/MAMAA company where you have the privilige to spend 20% on your time on "n'importe quoi" be it a hobby project or some necessary improvement. Sometimes from your expert point of view you can identify certain improvements that think would benefit your organization and maybe also look good on your CV. Usually you are managed at by somebody who does not talk in the same language like you about software architecture and engineering. You can however talk in a common language of fungible things like time or money. Unless you are a solo start-up founder and then the following is still relevant knowledge to have if you want to keep you business from running up high costs. When you are in a constrained environment you can use the below ascribed technique to negotiate budget or budgetted time to be spent on a necessary technical improvements. Here we try to show a way how to put a number on technical debt and what a return of investment would be when trying to decrease this technical debt. 

Some managers have read the lean start-up and follow the conviction that echnical debt does not exists. This is however in the assumption that one can cashout the start-up before that and exit the business before you have to pay back on that debt. If you are not working in a start-up with a short term exit scenario you can counter that argument by quantify this debt in the long term.

## Background: lean cost calculation

Usually we are working in teams where agile methodologies are used like Scrum or Kanban. These methodologies have it's roots in lean manufacturing. Software development is knowledge work and also with a lot of unknowns because of reasons like social and orginizational interactions or the rapid evolution of technological tools. That's why deeply quantitative methods or calculations for extensive planning is quite taboo in opposition to the waterfall software methodology. We mostly use the methodology of Kanban by using story points or t-shirts sizes that have no direct link to quantities of time. Kanban has it's origin in a three-bin system or other physical tokens which were added to halfproducts for a workstation and the return of physical token to the stock was a trigger to replenish that workstation. These tokens were an indirect way to measure the physical flow of materials. 

### Kaizen event

Another tool in the toolbox of lean manufacturing is the Kaizen event. The purpose of this not to monitor the stability of quality continuously but rather it is literally a focused event to improve your process dramatically in a short timespan. In a manufacturing environment this could be a shopfloor or warehouse manager focusing one certain operation in collaboration with the operators on the floor. This is done in a single DMAIC cycle. This has differnt steps where you Define your objective to improve on, Measure an indicator for that objective, Analyze this measuement, Improve on this indicator and Control for this improvement. It's a bit like a hackathon but in a production environment and the purpose is not necessarily trying something new or innovative but to specifically improve quality.

Another concept that is helpfull here is looking at wastes or muda in your process that could be useful in choosing a metric for the measurement phase. For manufacturing muda are classified under the mnemonic TIMWOODS which stands for Transportation, Inventory, Motion, Waiting, Overproduction, Over processing, Defects and Skills which is pretty self-explanatory.

### Back of the envelope

To define your metric it is possible to do back of the envelope calculations to estimate any of these potential wastes. If you are not familiar with them there is a [good introduction](https://anchor.fm/breakingmathpodcast/episodes/P9-Give-or-Take-Back-of-the-Envelope-Estimates--Fermi-Problems-ev6tlf) for this in the breaking math podcast. This a skill that is sometimes tested by large companies in the hiring process. There is a talk by Jeff Dean that shows how they use this method to make the right choices when writing code based on latency numbers:

[![google talk by Jeff Dean](https://img.youtube.com/vi/modXC5IWTJI/0.jpg)](https://www.youtube.com/watch?v=modXC5IWTJI)

This may seem crude but you may be familiar with the pareto principle which says that 20% of a system has 80% impact and the 80% is neglible in some cases. This idea is even more fundamental than only in economics where Pareto discovered that 20% of the people owned 80% of the wealth. Similarly you have perturbation theory where you solve a simple problem exactly to approximate a complex problem. Feynman diagrams to model complex quantum mechanical interactions between fundamental particles are based on perturbation theory:

[![perturbation theory Space Time](https://img.youtube.com/vi/oQ1WZ-eJW8Y/0.jpg)](https://www.youtube.com/watch?v=oQ1WZ-eJW8Y)

Even more fundamentally this idea of a small proportion explaining a large part by approximation can by found in information theory with the Zipf-distribution which is covered here by Vsauce:

[![vsause zipf](https://img.youtube.com/vi/fCn8zs912OE/0.jpg)](https://www.youtube.com/watch?v=fCn8zs912OE)

### Measuring economies of scale of development

To get more concretely on what to try to measure you may ask yourself what can I measure to put a figure on my technical debt. Here the late Peter Hintjes dropped a clue in his free ebook  [Culture and Empire](https://content.cultureandempire.com/index.html) that products of technological innovation have a deflationairy pressure on them as a generalization on Moore's law. 

>I've observed that Moore's Law applies to much more than silicon: it applies to all technology, and always has applied. I call this general law "cost gravity": the production cost of technology drops by half every 24 months, more or less. Ignoring materials, labor, distribution, marketing, and sales, the cost of any given technology will eventually approach zero.

The essence of automation is scalability which means you try to make unit costs of things like physical items or human tasks negligible. As a low level knowledge worker almost the only resource you have impact on is how you apply your labor. Estimating time during a planning phase directly is somewhat taboo in agile methodologies as mentioned early since knowledge work is rather unpredictable. Software development is in essence a human job. This is nicely illustrated in the book [Peopleware: Productive Projects and Teams](https://en.wikipedia.org/wiki/Peopleware:_Productive_Projects_and_Teams) which puts forward measuring flow time of knowledge workers. Flow time is the amount of time you can work uninterrupted. However not all tasks that a developer does is knowledge work but rather repeatable. To ensure stability and quality of software products we have CI/CD processes which includes source control and build automation. Analyzing these sources of information on your daily tasks is not an entirely new idea. [Adam Tornhill](https://github.com/adamtornhill/code-maat) has written numerous book about using source control as a data source on how to measure hotspots of possible technical debt:

[![Adam Tornhill technical debt](https://img.youtube.com/vi/fl4aZ2KXBsQ/0.jpg)](https://www.youtube.com/watch?v=fl4aZ2KXBsQ)


## Simple example: I need a new keyboard,

Putting all this theory together we can start with a small example how this can be applied. Let's start with the following situation to illustrate the disparity between the scale of costs between you as developer and the tooling you work with everyday. The most fundamental thing you work as a knowledge worker is usually some kind of keyboard or input device. Imagine the situation where you are giving a faulty keyboard. Let's say the defect is that due to overusage of keys the colom en semicolom on your keyboard has become indistinguishable. This may be annoying since as a developer working typically in C-style languages your statements are usually terminated by semicoloms and if you make an error while blind typing it may be more difficult to get in the flow when you try to figure out which one of the two you have to push to fix your syntax error. How do you ask your manager for a new keyboard. You could just ask but if you had those soft skills why did you become a developer in the first place. 

One thing important to keep in mind that you are not comparing apples with oranges. That's why it's important to write down the full formula of your equation so we'll do this with \\( \LaTeX \\) using [\\( \KaTeX \\)](https://katex.org/).

As mentioned before you can use the power of the source here. You can look up the total amount of lines terminated with semicoloms in your code base. Doing some [tacobell programming](http://widgetsandshit.com/teddziuba/2010/10/taco-bell-programming.html) can help you with that task. Looking at the age of your source code repository you can estimate how much lines of code that end with semicoloms are added over a timeperiod. If you estimate that about half of the time your are typing a colom instead of semicolom you have a proportion of time that has a chance that you are delayed by your faulty keyboard.

$$RateOfMistyping \frac{[NumberOfMistakes]}{[Seconds]} = \frac{1}{2} * \frac{NumberOfNewLinesEndingWithSemiColom}{AgeOfRepoSeconds}$$

We do not work 24/7 so we need to adjust time for that:

$$DevelopmentRatio \frac{[DevelopmentSeconds]}{[Seconds]} =  RatioDevelopmentDuringWork \frac{1}{2} * \frac{200 [WorkingDaysPerYear]}{365 [DaysPerYear]} * \frac{8[HoursPerWorkingday]}{24[HoursPerDay]} = \frac{100}{1095}  \frac{[DevelopmentSeconds]}{[Seconds]} $$

We can transform these ratios into something more hands on for decision makers:

$$CostOfMistyping \frac{[€]}{[Workday]} = \frac{1095}{100} * RateOfMistyping * FTEdayrate  \frac{[€]}{[Workday]}  = \frac{1095}{200} * \frac{NumberOfNewLinesEndingWithSemiColom}{AgeOfRepoSeconds} * FTEdayrate  \frac{[€]}{[Workday]} $$

You can then report this to your manager and they can offset this to the cost of sourcing you a new keyboard. Using this simple formula he can calculate an earnback period for a simple keyboard.

## More elaborate example: The entire floor is waiting for the error you made in the configuration.

> You NEED to get out of this meeting NOW because you checked something into the configuration and now the ENTIRE FLOOR is waiting for you to fix that error because the sit is BROKEN.

Has this ever happened to you? Clumsy huh. Maybe also a pointer there is something deeply wrong in an organisation or an architecture. Sometimes you end up in a situation of a big ball of mud somewhere between tripleheaded monolith monstrocity and a distributed monolith pretending to be a microservices architecture that is difficult to disentangle. These eye-opening situations can spark some idea of what are the bottlenecks that are of great cost for the organization you are working for. Mo' services mo' problems and a solution to distributed configuration in microservices is the principle of control plane in a service mesh. More concretely we will take a stab at Consul as control plane as an alternative for checking configurations into source control and running it through a CI/CD pipeline tied to a monolith.

Again we can use the power of the source. Since all configuration is checked in under one folder in the monolith we can use the power of the source to lookup how many changes were done to that folder.

```
git log -- path/to/configfolder/*
```

Surely a modern organization is using git by now ;).

## Conclusion: how many developers does it take to turn in a light bulb

Using 