+++
title = "There is no time for that"
description = "How to convince your manager to let you spend money or time on an improving on technical debt"
date = 2022-05-20
draft = false
slug = "there-is-no-time"

[taxonomies]
categories = ["lean","project-management"]
tags = ["time-management","waste","managing-up"]

[extra]
comments = true
+++

# "There is no time for that":.

Whatever role you are in as a technical person you are usually in a context where you are a cost center to an organization on a budget in the public sector or with a profit goal in the private sector. The only profit center for a company is possibly maybe even only a paying customer according to Peter Drucker. Or a satisfied taxpayer if you are in the public sector.  Not everyone works at a FAANG where you have the privilige to spend 20% on your time on "n'importe quoi" be it a hobby project or some necessary improvement. Sometimes from your expert point of view you can identify certain improvements that think would benefit your organization and maybe also look good on your CV. Usually you are however managed at a some higher level by somebody who does not understand or zones out when you start talking about software architecture and coding. Unless you are a solo start-up founder and then the following is still relevant knowledge to have if you want to keep you business from running up high costs. When you are in a constrained environment you can use the following technique to negotiate budget or budgetted time to be spent on a necessary technical improvements. Here we try to show a way how to put a number on technical debt and what a return of investment would be when trying to decrease this technical debt. You may however work under a manager who has read the lean start-up and thinks technical debt does not exists although he's not in the position of just selling a start-up when technical debt has acrued. In that case I have only pity for you.

## Background: lean cost calculation

Usually we are working teams where agile methodologies are used like Scrum or Kanban. These methodologies have it's roots in lean manufacturing. Software development is knowledge work and also with a lot of unknowns because of reasons like social and orginizational interactions. That's why deeply quantitative methods or calculations for extensive planning is quite taboo as opposition to the waterfall software methodology. We mostly use the methodology of kanban by using story points or t-shirts sizes that have no direct link to quantities of time. Kanban has it's origin in a three-bin system or other physical tokens which were added to halfproducts for a workstation and the return of physical token to the stock was a trigger to replenish that workstation. These tokens were an indirect way to measure the physical flow of materials. 

### Kaizen event

Another tool in the toolbox of lean manufacturing is the Kaizen event. The purpose of this not to monitor the stability of quality continuously but rather it is literally a focused event to literally improve your process dramatically in a short timespan. In manufacturing environment this could be a shopfloor or warehouse manager focusing one certain operation in collaboration with the operators on the floor. This is done in a single DMAIC cycle. This has differnt steps where you Define your objective to improve on, Measure an indicator for that objective, Analyze this measuement, Improve on this indicator and Control for this improvement. It's a bit like a hackathon but in a production environment and the purpose is not necessarily trying something new or innovative but to specifically improve quality.

Another concept that is helpfull here is looking at wastes or muda in your process that could be useful in choosing a metric for the measurement phase. For manufacturing muda are classified under the mnemonic TIMWOODS which stands for Transportation, Inventory, Motion, Waiting, Overproduction, Over processing, Defects and Skills which is pretty self-explanatory.

To define your metric it is possible to do back of the envelope calculations to estimate any of these potential wastes. If you are not familiar with them there is a [good introduction](https://anchor.fm/breakingmathpodcast/episodes/P9-Give-or-Take-Back-of-the-Envelope-Estimates--Fermi-Problems-ev6tlf) for this in the breaking math podcast. This a skill that is sometimes tested by FAANG companies in the hiring process. There is a talk by Jeff Dean that shows how they use this method to make the right choices when writing code based on latency numbers:

[![google talk by Jeff Dean](https://img.youtube.com/vi/modXC5IWTJI/0.jpg)](https://www.youtube.com/watch?v=modXC5IWTJI)

This may seem crude but you may be familiar with the pareto principle which says that 20% of a system has 80% impact and the 80% is neglible in some cases. This idea is even more fundamental than only in economics where Pareto discovered that 20% of the people owned 80% of the wealth. Feynman diagrams to model quantum mechanical interactions between fundamental particles are based on perturbation theory:

[![perturbation theory Space Time](https://img.youtube.com/vi/oQ1WZ-eJW8Y/0.jpg)](https://www.youtube.com/watch?v=oQ1WZ-eJW8Y)

Even more fundamentally this phenomenon can by found in information theory with the Zipf-distribution which is covered here by Vsauce:
[![vsause zipf](https://img.youtube.com/vi/fCn8zs912OE/0.jpg)](https://www.youtube.com/watch?v=fCn8zs912OE)

To get more concretely on what to try to measure you may ask yourself what can I measure to put a figure on my technical debt. Here the late Peter Hintjes dropped a clue in his free ebook  [Culture and Empire](https://content.cultureandempire.com/index.html) that products of technological innovation have a deflationairy pressure on them as a generalization on Moore's law. 
>I've observed that Moore's Law applies to much more than silicon: it applies to all technology, and always has applied. I call this general law "cost gravity": the production cost of technology drops by half every 24 months, more or less. Ignoring materials, labor, distribution, marketing, and sales, the cost of any given technology will eventually approach zero.

The essence of automation is scalability which means you try to make unit costs of things like physical items or human tasks negligible. As a knowledge worker almost the only resource you have impact on is how you apply your labor. Estimating time during a planning phase directly is somewhat taboo in agile methodologies as mentioned early since knowledge work is rather unpredictable. Software development is in essence a human job. This is nicely illustrated in the book [Peopleware: Productive Projects and Teams](https://en.wikipedia.org/wiki/Peopleware:_Productive_Projects_and_Teams) which puts forward measuring flow time of knowledge workers. Flow time is the amount of time you can work uninterrupted. However not all tasks that a developer does is knowledge work but rather repeatable. To ensure stability and quality of software products we have CI/CD processes which includes source control and build automation. Analyzing these sources of information on your daily tasks is not an entirely new idea. [Adam Tornhill](https://github.com/adamtornhill/code-maat) has written numerous book about using source control as a data source on how to measure hotspots of possible technical debt:

[![Adam Tornhill technical debt](https://img.youtube.com/vi/fl4aZ2KXBsQ/0.jpg)](https://www.youtube.com/watch?v=fl4aZ2KXBsQ)


## Simple example: I need a new keyboard,

Putting this all together we start with a small example how this can be applied.

## More elaborate example: The entire floor is waiting for the error you made in the configuration.

A more elaborate example.


## Conclusion: how many developers does it take to turn in a light bulb
