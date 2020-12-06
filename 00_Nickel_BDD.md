---
title: TDD to BDD - Principles and Tools with an Impact on Business Value and Communications
subtitle: A brief essay on Behavior-Driven Development
author: Robert Nickel
date: 2020-11-15
fontsize: 11pt
numbersections: true
listings: true
documentclass: scrreprt
bibliography: [bibliography.bib]
csl: chicago-author-date.csl
---

## Table of Contents <!-- omit in toc -->
1. [Introduction](#introduction)
2. [Why Behavior-driven development?](#why-behavior-driven-development)
3. [From TDD to BDD](#from-tdd-to-bdd)
4. [The Principles of Behavior-driven development](#the-principles-of-behavior-driven-development)
   1. [Examples and Business Rules](#examples-and-business-rules)
   2. [Scenarios, the Gherkin Language and working software](#scenarios-the-gherkin-language-and-working-software)
   3. [Specification - a Contract?](#specification---a-contract)
   4. [Roles and Responsibilities](#roles-and-responsibilities)
5. [How to do BDD right](#how-to-do-bdd-right)
   1. [How to write good scenarios/examples](#how-to-write-good-scenariosexamples)
   2. [Three amigos/ Specification workshop / Discovery workshop](#three-amigos-specification-workshop--discovery-workshop)
   3. [The Tools of BDD](#the-tools-of-bdd)
6. [Critical evaluation of BDD](#critical-evaluation-of-bdd)
7. [References](#references)

## Introduction
The ultimate goal for every agile process is to turn work into value in a sustainable way. In the context of software engineering, humans automate solutions to problems by explaining them in much detail to machines, that do not have a common sense. Thus, the machines can solve the automatable problems and humans can focus on the not automatable tasks: To further explain the right solutions to problems to a machine in the right way. This discipline is software engineering. The result of explaining the right solution to a machine the right way is good software. In all this there are (at least) two major problems:

1. Misunderstandings in inter-human communication

Often communication between people is required before software can be built, because in many cases some people have the skills to explain a solution to a machine, and other people have a deep understanding of the solution itself. The classical approach to to solve this problem is called specification.

2. Perceived functional dissonance of software

Sometimes people think that software works in a certain way but it doesn't. While or after building software, some features might work at some point in time and then break without humans recognizing it. The software might stop (or even worse: not stop) in critical, unexpected moments which can cost, depending on the software, a lot of customers, money or even lifes. The common approach to solve this problem is called quality assurance and contains testing the software repeatedly.

The effects of these problems need to be discovered. In a waterfall-based approach the feedback cycle closes only after an increment went through specification, implementation and quality assurance, which means, that if any increment went off track, it is discovered at a late point in time.

The fundamental idea of BDD is to focus on the behavior of a software system while moving the solutions to the above mentioned problems, specification and quality assurance, closer together.[@nagy2018discovery, p.3] Thereby, the feedback cycle shortens and off-track increments are harder to produce and less impactful. In this essay I want to elaborate on how BDD leverages this idea into building sustainable software, which principles and tools it uses to do so and to what extent it can be assumed that BDD works.

## Why Behavior-driven development?
The annual "State of Agile" Report started 2007 and provides since then insights into the application of agile methodologies and practices over a large range of different companies worldwide.
For the 14th State of Agile Report 1121 surveys were collected [@stateOfAgile14, p.5] and for the Report from 2015 even 3880 surveys where collected[@stateOfAgile10, p.2]. The survey is handed out to agile practicioners and executives. It is aimed to be representative in terms of localization, company size and industries and it exists since more than 12 years, therefore it might contain a convincing insight into the employment of BDD, at least among the companies that participated in the survey. This table of percental BDD employment per year shows a significantly growing application of BDD, especially since 2015 BDD appears to gain relevance each year except 2019.[@nagy2018discovery, p.9f]

|      Report       | BDD used by |    BDD listed as     |
| :---------------: | :---------: | :------------------: |
| [@stateOfAgile3]  |     7%      |     agile method     |
| [@stateOfAgile4]  |    None     |   agile technique    |
| [@stateOfAgile5]  |     9%      |   agile technique    |
| [@stateOfAgile6]  |     9%      |   agile technique    |
| [@stateOfAgile7]  |     10%     |   agile technique    |
| [@stateOfAgile8]  |     12%     |   agile technique    |
| [@stateOfAgile9]  |     9%      |   agile technique    |
| [@stateOfAgile10] |     10%     |   agile technique    |
| [@stateOfAgile11] |     16%     | engineering practice |
| [@stateOfAgile12] |     17%     | engineering practice |
| [@stateOfAgile13] |     22%     | engineering practice |
| [@stateOfAgile14] |     19%     | engineering practice |

BDD is listed under different captions: In the earlier surveys it was listed as an agile method, then it was listed as an agile technique and since 2016 it is listed as engineering practice.

## From TDD to BDD
Dan North describes in "Introducing BDD" how BDD is his response to TDD. In order to get a deeper understanding of what that means, we must have a closer look at TDD. TDD is a narrower approach, in which mostly only technically focussed people are involved. The idea is to write a test that describes a feature which doesn't exist yet, ensure it fails, and then implement that feature until the test does not fail anymore and refactor the code afterwards. After the new test is executed successfully, the code quality is on an acceptable level and none of the existing tests is broken, the developer can move on to the next test for the next feature. This test-first approach is mentioned in the early publications about Extreme Programming[@Lindstrom2004ExtremePA].

## The Principles of Behavior-driven development
The term behavior-driven development, as it was introduced by Dan North in 2006[@north2006introducing-bdd], explicitly avoided the term "test" in order to keep business people engaged.[nagy2018discovery, p.10] This is a strong hint towards the most fundamental principle of BDD: bringing the specification and the quality assurance together or in other terms: "Bridging the Communication Gap", which is the title of the book by Gojko Adzic[@Adzic2009Bridging] that describes a very similar idea which he names "specification by example" and "agile acceptance testing".

According to the agile alliance glossary[@agileAllianceTDD], common pitfalls of a TDD using team are a "poor maintenance of the test suite – most commonly leading to a test suite with a prohibitively long running time" which sometimes leads to a "abandoned test suite (i.e. seldom or never run)[...]". Dan North explains some further pitfalls, that range from the naming of the tests, which might cause some "false sense of security"[@north2006introducing-bdd], to the scope and the actual functionality that needs to be tested. Thinking in terms of behavior solved these issues: The naming of an executable test is based on the behavior it should assure. The scope of the test is easier defined on the level of behavior (rather on the more technical level of test), because a behavior description has naturally a certain length and a functional scope that excludes all technical details. The question, which features should be tested, also became easier to answer: All of the behavior, that the software should have, needs to be tested. Lower level tests, which ensure the software uses a specific solution, step back and the testing scope shifts towards tests that describe the behavior of a system. Latter correlate to the original intent of writing the software and therefore are getting closer to stakeholders attention. Concluding this chapter: BDD is a successor of TDD in its nature, but shifts its scope towards a more behavioral and less technical level. At the same time, TDD can be used inside of BDD, so that both layers are addressed at the same time[@nagy2018discovery, p. 15].

### Examples and Business Rules
Examples are a mighty tool in BDD, which are used to illustrate business rules and therefore reduce the chance of misinterpreting them[@nagy2018discovery, p. 48]. Therefore, one or more examples belong to one business rules.

Examples consist of a context, an action and an outcome. The context is the state of the system before the action is applied to it. The action is the stimulus that causes the system to react. It might be another system, some scheduled action or the user of the system. The outcome is the updated state of the system after the action has taken place[@nagy2018discovery, p. 43]. It should focus on that part of the system that was influenced by the action, and does not need to contain irrelevant aspects. Moreover, an example always contains concrete data in contrast to variables. An example is what can be used to write a test for a system. One example of an example from the world of poker:

    - Table is preflop
    - Amy is on the button
    - Amy has a stack of 50BB
    - Bob is small blind
    - Carl is big blind
    - Amy has aces
    - Bob and Carl post the blinds
    * Amy raises 3BB  
    => Raise is accepted

*Here, the dashes stand for the context, the asterisk for the action and the bold arrow for the outcome.*

The examples alone cannot describe the behavior of a system sufficiently. Therefore, the business rules exist, which are the abstract description of the general problem. A business rule is what gets implemented in the software. When defining a business rule, it is often the case that it is deduced from a concrete situation (= example) in which the system should behave in a specific way.

### Scenarios, the Gherkin Language and working software
A scenario is a formalized interpretation of an example. To formalize the example, a business readable domain specific language (DSL)[@Fowler2008Business], for example the Gherkin language[@cucumberGherkinDocs] is used to describe behavioral descriptions of a software system. The Gherkin language has only very few (primary) keywords:
    
    Feature
    Rule (as of Gherkin 6)  
    Example (or Scenario)
    Given, When, Then, And, But for steps (or *)
    Background
    Scenario Outline (or Scenario Template)
    Examples
and even less secondary keywords used for comments, tags, data tables and doc strings, which are relevant for this principle. Interestingly, the keywords 'example' and 'scenario' are used as synonyms here, which also hints towards them being very similar. An example for a specification that contains a feature, a rule and two scenarios from the world of poker is the following.

    Feature: Pay the winner

      Rule: Player with the best hand wins

        Scenario: Last betting round over -- More than one player in the round
          Given the last betting round is over
          And there are two players in the round
          When the showdown happens
          And the first player shows a full house
          And the second player shows a flush
          Then the first player wins the pot

        Scenario: Last betting round over -- Only one player in the round
          Given the last betting round is over
          And one player is in the round
          Then the player will win the pot

These two formalized examples are structurally similar to the examples that are defined above. One or multiple rules belong to one feature (which maps to a story in Scrum terminology), and one or multiple scenarios are subordinated to a rule. The scenarios have a context that start with "Given", an action that start with "When" and a outcome, that starts with "Then". It is by design that these keywords are close to the natural language for the for this reason: The Gherkin language is the clue to a specification level that is both, executable as behavioral specification (using a BDD Tool) and at the same time readable and writable for non-technically focussed business people.

Conclusively, a scenario is an example that is formalized by a business readable DSL like the Gherkin language. The working software is the formalization of the business rules, written in a (usually high-level) programming language like Scala, Java, C# etc. And just like the examples illustrate the business rules, scenarios illustrate the software itself. Before getting closer into the tips, tricks, tools, do and don'ts, I want to conclude this very key principle of BDD.

![](images/process_illustration_formalization_bdd.png)
[Figure 2]  
  
The goal of BDD is to engineer high-quality working software (top right). To get there, we start with examples, explained by business people and discussed with all roles that engage in the process. These are inter-humanly communicated behaviors that do not need to fulfill a highly formalized structure, other than describing the context, the action and the outcome. They get formalized with a business readable DSL (bottom right) and abstracted to business rules (top left). Both steps are taken in order to get to the top right corner of the image without disconnecting the specification and the actual software. This principle is executed repeatedly in very short feedback cycles, so that it proves the right understanding of the specification (which is the implementation) and having the right specification in place. The right software is built the right way.

### Specification - a Contract?
The specification is a contract between the business and the implementation.
Its documenting the behavior if the system, tests it automatically and illustrates it.

### Roles and Responsibilities
Do the roles change?
  - Dev team is invited to participate in business discussions.
   - Uncle Bob says, that software engineers need to become domain experts (to some degree).
  - Business people are pushed towards using a more formalized language than usually
What about responsibility segregation?

## How to do BDD right

### How to write good scenarios/examples
Since scenarios are examples that are formalized by a business readable DSL, but are contentwise similar, they are considered synonym for the following section. In a Cucumber.io article [@Rose2019Brief], Seb Rose describes the traits of a good scenario with the combined acronym BRIEF.  
- Business Language  
- Real Data  
- Intention Revealing  
- Essential  
- Focused  
- Brief (Which is the acronym itself.)  

Using the _business language_ in scenarios aims to keep the business people engaged and to bring it more into line with the actual software. _Real data_ should be used for scenarios to reveal the intention of it. Another way of revealing the intention of a scenario is by focusing on _revealing the intent_ of the aspect of a system, rather than on the mechanics that lead to that result. This applies to the name of a scenario just as much as to the content. Focussing a scenario onto only the _essential_ parts of an illustrated business rule means to remove everything that does not directly contribute to the readers understanding of the system. Moreover, one scenario should _focus_ on describing only one business rule. Therefore it is possible to describe a scenario in a _brief_ way, which makes a scenario easier to understand and discuss for people of all roles.

### Three amigos/ Specification workshop / Discovery workshop

### The Tools of BDD
- Name a few examples like JBehave, Cucumber and SpecFlow
- what do the tools do?
- importance of tools

## Critical evaluation of BDD
- Advantages
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

---

## References