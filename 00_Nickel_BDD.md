---
title: TDD to BDD - Principles and Tools with an Impact on Business Value and Communications
subtitle: A brief essay on behavior-driven development
author: Robert Nickel
date: 2020-11-15
fontsize: 11pt
numbersections: true
listings: true
bibliography: bibliography.bib
csl: chicago-author-date.csl
---

## Table of Contents <!-- omit in toc -->
1. [Introduction](#introduction)
2. [Why Behavior-driven development?](#why-behavior-driven-development)
3. [The Principles of Behavior-driven development](#the-principles-of-behavior-driven-development)
4. [The Tools of Behavior-driven development](#the-tools-of-behavior-driven-development)
5. [Advantages of Behavior-driven development](#advantages-of-behavior-driven-development)
6. [Conclusion](#conclusion)

## Introduction
The ultimate goal for every agile process is to turn work into value in a sustainable way. In the context of software engineering, humans automate solutions to problems by explaining them in much detail to machines, that do not have a common sense. Thus, the machines can solve the automatable problems and humans can focus on the not automatable tasks: To further explain the right solutions to problems to a machine in the right way. This discipline is software engineering. The result of explaining the right solution to a machine the right way is good software. In all this there are (at least) two major problems:

1. Misunderstandings in inter-human communication

Often communication between people is required before software can be built, because in many cases some people have the skills to explain a solution to a machine, and other people have a deep understanding of the solution itself. The classical approach to to solve this problem is called specification.

2. Perceived functional dissonance of software

Sometimes people think that software works in a certain way but it doesn't. While or after building software, some features might work at some point in time and then break without humans recognizing it. The software might stop (or even worse: not stop) in critical, unexpected moments which can cost, depending on the software, a lot of customers, money or even lifes. The common approach to solve this problem is called quality assurance and contains testing the software repeatedly.

The fundamental idea of BDD is to focus on the behavior of a software system while moving the solutions to the above mentioned problems, specification and quality assurance, closer together.[@nagy2018discovery, p.3] Interestingly these are the first stage and one of the last stages in a classical waterfall process. 

// TODO: add pictures and reference to waterfall process

In this essay I want to elaborate on how BDD leverages this idea into building sustainable software, which principles and tools it uses to do so and to what extent it can be assumed that BDD works.

## Why Behavior-driven development?
Quantify the industries interest in behavior-driven development (BDD)

Year | Version | Employment | listed as
:-: | :-: | :-: | :-:
2007 | 2 | None | None
2008 | 3rd | 7% | agile method
2009 | 4th | None | agile technique
2010 | 5th | 9% | agile technique
2011 | 6th | 9% | agile technique
2012 | 7th | 10% | agile technique
2013 | 8th | 12% | agile technique
2014 | 9th | 9% | agile technique
2015 | 10th | 10% | agile technique
2016 | 11th | 16% | engineering practice
2017 | 12th | 17% | engineering practice
2018 | 13th | 22% | engineering practice
2019 | 14th | 19% | engineering practice

Search engine statistics?

## The Principles of Behavior-driven development
- To what extent is BDD an advancement to test-driven development (TDD)?
  - TDD as origin
  - Differences & Similarities
  - Does BDD contain or extend TDD?
  - Do they solve the same problem?
  - Does the testing scope shift (Unit -> Acceptance tests)?
- Which goals are defined?
- Which areas are affected by BDD?
  - Specification - a contract?
    - Context(Given) Event(When) Outcomes(Then)
    - becomes executable
    - Scenarios
    - Gherkin language
    - by example (which enables making it executable) not in general
  - Quality Assurance
  - Development
  - Documentation
- Do the roles change?
  - Dev team is invited to participate in business discussions.
  - What about responsibility segregation?

## The Tools of Behavior-driven development
- Name a few examples like JBehave and/or Cucumber
- what do the tools do?
- importance of tools
 
## Advantages of Behavior-driven development
- motivation
  - Does devteam win by invitation to business participation?
  - Does a deeper (than a scrum user story) understanding of the business questions increase the dev team's motivation?
- specification
- business value
  - Five whys
- communications
  - Business experts can read the specification code (aka test code)
- coding
  - Does BDD prevent too much code or code that does too much and help focus on the actual requirements?
- quality assurance (getting closer to specification)
  - Do passing tests mean anything in terms of business value?
  - Is it more useful to have higher level tests than lower level unit tests? Are both testing levels required? Examples?
- documentation
  - Executable specification as living documentation

## Conclusion
- Qualitative
  - limitations
  - possibility (Useful aspects of BDD)
- Quantitative proof that BDD works?
- From the industry point of view: How can BDD be approached?
  - Is it possible to start with tech only or business only adoption, or does it have to happen simultaniously?
- Different layers of adoption
  - Consider: https://dzone.com/articles/the-five-stages-of-bdd-and-agile-adoption
  - What are the important understandings of each layer?
  - Which roles are involved & affected? What about the motivation of each of those roles?
  - Is it possible to quantify the adoption of BDD in terms of those layers?
- Does BDD work?
- Should everyone do BDD?