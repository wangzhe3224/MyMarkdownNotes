---
title: Professional Automated Trading
tags: 读书笔记
---

目的：Provide a set of tools to build a robust systematic trading business.

中心思想：The central idea is to frame systematic trading in the framework of automomous adaptive agents. For the purpose of this book, the main goal is to be able to formulate an approach to survive and thrive in the marketplace. (from Page 43.)

The central concept of this book: direct analogy between robotics and systematic automated trading strategies (on Page 49)


讨论的范围：Trading liquid instruments.

如何组织材料:
- Introductory
- Part 1: basic conceptual and programmatic framework for the design of trading strategies as trading agents.
- Part 2: Building robust trading systems that can gracefully withstand changes of regime.
- Part 3: Trading costs and slippage.
- Part 4: Implementation of a scalable and efficient lowlatency trading architecture.

Part 1&2 proposed an AAA (adaptive aumonomous agents, ) based systematic trading system. Then Part 3&4 provide a layer based framework of doing systematic trading as robust business. In this context, Part 1&2 is just an layer.

与我的关系：
- 是否可以实现策略的自动生成？放在作者的框架中，就是Swarm出新的Agent？
- 分层的软件架构有帮助
- 与强化学习的练习？Agent based trading

## Introduction

Definition: 
- discretionary: trading relying on noncomputable processes
- systematic: trading relying on objective unputs without human emotional context.

Philosophy of Trading:

* Lessons from Market:
  - Macroeconomic information unfolds gradually, therefore prices do not discount future events immediately.

The business of trading:

Discuss the cost/profit/operation of doing systematic trading fund as business

Psychology and emotions:


## Part 1: Strategy Design and Testing

The author proposed a framework based on autonomous adaptive agents, with focus on recoverability of the system (achived by finite state machines). To support the framework, this part discussed details of the programmatic framework. Then data representation is discussed. After that, portfolio optimization is discussed. At last, simulation and estimation techniques are discussed. 

The end goal is to build adaptive autonomous agents (AAA). Part 1 focus on autonomous, Part 2 focus on adaptive.

对我来说，作者主要的创新点在于：Finite-stete machine and inter-agent comm.

### 2. Socioeconomic Paradiam

Summary: First addressed the problem of current market theory, then he tried to model the market using complext system theory (agent based adaptative system?).Lastly on the light of complex system, he proposed a system with four features.

#### 2.1 Market and Reality

The author explain why current theory is not suitable for market reality.

What author said:

- Adptive reaction
    - Return, volatility, correlation are not stable.
    - CTA has good track record, mainly because it reacts fast enough, rather than predict future. This means that although market are complex, some behavioral patterns can be exploited systematically.
- Non-stationarity of dist/corr of return:
    - Accumulation vs. Divestment Games
        * Prisoner’s dilemma game: In the real markets where people do not think beyond the next minute in situations of stress. In other words, people will not choose the way which will create long-term benefit. 
    - Phase Transitions under Leverage
        * Source of trend
        * Source of non-stationarity distribution/correlation of returns
    - Derivatives
        * Hedging activity push price more away. (negative convexity)
        * Create a incimplete market because the theory is not right in reality
        * OTC derivateive price discovery is limited... 
    - Socio-Political Dynamics and Feedbacks
        * They are, by definition, non-linear.

#### 2.2 The Market is a Complex Adaptive System

Given above observation of market, the main goal is to be able to formulate an approach to survive and thrive in the marketplace.

What author said:

- Emergence, not fully predictable even though the systems from which it emerges are deterministic
- Complex adaptive system (Original): 
    - Parallelism
    - Emergence and self-similarity
    - Adaptation
    - Anticipation
- Complex adaptive system (From Market): 
    - Parallelism: all the agents in the market, traders or algos.
    - Emergence: big firms/pool, have larger impacts, thus yielding emergence and larger scale price patterns
    - Adaptation: 
    - Anticipation: Participant tries to following larger participant in order to survive
- Zero-intelligence models of agent behavior explain market microstructure much better than sophisticated models
- Adaptation is very important

### 3. Analogies between Systematic trading and Robotics

Central concept: Direct analogy between robotics and systematic automated trading strategies.

#### 3.1 Models and Robots

Adaptive autonomous agens (AAA) is a decision making process that is composed of three elements:

- Sensors: Device receives info: indicators, performance measures
- Actuators: Device by which the agent outputs: order management system
- Adaptive Control System: A goal oriented decision-making system that reads sensors and activates actuators.

#### 3.2 Trading Robot

Raw data -> sensor -> preprocessor -> control system -> actuators/postprocessor -> order/other data.

#### 3.3 Finite-state-machine representation of contral system

Features of control system:
- Make profit
- Completeness
- Recoverability

Completeness is achived by finite state machine (FSM).
This FSM is the core of strategy, the instream and outstream is delegated to other parts.

_Definition of FSM_: Let $S$ be a finite set of symbols representing abstract states, $E$ a possibly infinite set of outside observable events. A finite-state machine $FSM(S，F)$ is defined by its complete set of transitions $F(s_{in}, s_{out}, e)$ with $s_{in}, s_{out} \in S$. The transition functions are such that $\forall e \in E$ and $\forall s_{in} \in S$ and there exists only one $s_{out}$ such that $F(s_{in}, s_{out}, e) = True$ and $F(s_{in}, s, e) = False, \forall s \ne s_{out}$. The FSM, at any point in time, has a current state $s_{in}$. For an new event, $e$, it changes to only one state, $s_{out}$.

### 4. Implementation of strategies as distributed agents

Top-level implementation of the chain of each trading agent:

$$Event \to Sensor \to Preprocessor \to Control Sys \to Postprocessor$$

Data Objects:
- Agent
- Event
- Transition
- FSM
  * current state
  * Transition
- FSMAGENT


Functions:
- consume(a, e)
- observe(a, e)
- update(a, e)
  * before
  * main
  * after

### 5. Inter-Agent communication

Class:
- Comm(Event)


### 6. Data Represeentation Techniques

Raw data format:
- Time series of price/volume
- Time series of orders
- Time series of News

A data filter: 
- Sampling tech
- Compression tech
- Representation tech

Sampling:
- time
- event

Compression:
- Bar
- Box, like a Box Agent!
- Distribution

Representation:
- Chart
- Symbols
- News to Numbers

### 7. Basic Trading Strategy

- Directional
    * Trend-following
    * Acceleration
- Contrarian
    * Mean-reverting
    * Market making
- News driven
- Intraday pattern

#### 7.1 Trend following

- Channel Breakout
- Moving Average
- Swing Breakout

#### 7.2 Acceleration

- Shadow Index

#### 7.3 Mean reverting

### 8. Architechture for Market Making

Leverage Agent comm to have conditional market making agent.

### 9. Combine Strategy into Portfolio

- AggregateAgent:
    * members: time series of the list of agents
    
Portfolio theory: 

### 10. Simulating Agent-Based Strategy

1. Simulate different instances of the same class of agent on one market
2. Simulate different instances of the same class of agent on different markets
3. Simulate instances of different sets of inter-communicating agents for
one market
4. Simulate instances of different sets of inter-communicating agents for
different combinations of markets

#### 10.1 The simulation problem

- Agents' reactions to exchange price updates and agent-to-agent comm
- Technical glitches, e.g. delays and order rejects
- The exhange reaction to agents's trading, delayed market impact, other agent learning and adaptation behavior.

For this sections:

- No Impact
- No Delay
- No Rejects

**Orders and Algos**

Class:

- Order <- MarketUpdate
- Algo
  * Simul(Algo)
  
**A model for OMS**

The order management system handles the execution logic of the current
orders of the agent. In the real world the OMS serves two major purposes:
1. It communicates orders from the agent to the ECN.
2. It communicates fills from the ECN back to the agent.

**Run Simulation**

- back test
- forward test

**Analysis of result**

- per trade analysis
- optimization
- overfitting


## Part 2: Evolving Strategies

Fundamental goals for AAA:
- Opportunities
- Robustness
- Flexibility

The problem author want solve in this part 2: Assuming that the set of opportunities is finite and known, how to design a strategy that will optimally exploit the current best opportunity or pattern and gracefully transition to the next behabvior when needed. 

Build swarm systems to switch different agents. Then more complexity is intruduced by reinforcement learning techniques for decision making. 

### 11. Avenues for Adaptations

1. Swarm: a set of nonadaptive (constant parameters) agents running in parallel in paper trading mode.
2. Smart: the agent learns to change its internal strategy via a reinforcement mechanism thant rewards it for good behavior and takes points away for bad bebavior.
3. Scary: the Swarm of Smart agents

(The author haven't finish work for point 3: Scary.)

> These feedbacks dynamically change the parameters of the system in order to achieve certain implicit or explicit goals. The feedbacks usually compare a current observed external state of the system with a desired state, and change the internal control parameters so as to reduce the distance between those states.


### 12. Feedback and Control

It is the basic adaptation mechanism of a trading agent to its own performance and forms the basis on which robust trading strategies are built.

The central question for a robot is how to optimally use its actuators in response to a stimulus from a sensor, in order to maximize the probability of achieving a certain pre-stated goal.

**Definition 2.** Take a strategy $S$ and an $FFC$ based on fitness function $\Phi$ resulting in the FFC-controlled strategy $FFC(S)$. 

Measures of Fitness:
- Continuous Statistics
- Per-Trade Satatistics

Measures of Robustness:

Efficiency of control:

### 13. Simple Swarm System

### 14. Implementing Swarm System

### 15. Swarm with Learning

## Part 3. Optimization of executions

### 16.

### 17.

## Part 4. Practical Implementation 

The focus here is mostly on design patterns rather than on the concrete implementation in a particular language.

### 18. Overview of scalable system

ENCs, Electronic commerce networks, is the layer outside the system, all the data from ENCs will be pushed into a Translation layer, which will generate event objects. These objects will be push into system Internal layer. The whole internal world consistutes the Persistence layer, which is implemented as a distributed memory cache that periodically flushes data to an exernal physical database. 

Layers:
- ENCs Layer
- Translation Layer
- Agg/Disagg Layer
- OMS Layer
- Control Layer
    * Human control layer
    * Automated risk management layer
    * Automated trading agent layer
- Middle/Back Office Layer
- Recovery Layer

### 19. Principal Design Patterns

### 20. Data Persistence

