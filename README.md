# ODE Control with Deep Q-learning

## Introduction

The goal of the project is to determine a controlling procedure for the evolution of an Ordinary Differential Equation in a Deep Reinforcement Learning Framework, with the particular approach of Deep Q-Learning. Our study case is the Lokta Volterra system of equations, which describes how the number of individuals of a population formed by preys and predators vary due to the interaction between these two species. 

<img width="142" alt="Schermata 2022-11-02 alle 17 53 22" src="https://user-images.githubusercontent.com/64698911/199552125-39faa4ea-f846-438c-8784-2350320744f9.png">

The variables x and y represent respectively the number of individuals of the prey and the predator population, while α, β, γ, δ are positive real parameters.
It is worth noting that the preys are assumed to have infinite food resources at their disposal and thus their reproduction rate is determined only by the parameter α, without any suffering due to scarcity in case of overpopulation. On the other hand, the parameter β determines the predation rate of the prey due to the predator: this is the only case of death for the prey in the system.
γ represents the growth rate of the predator population, which is entirely defined by its interaction with the prey: notice that the term is similar to the predation rate, but the two coefficients are different. δ represents the natural decay of the predator population, either due to death or emigration.
The Lotka-Volterra system of equations admits a periodic solution for any tuple of parameters

<img width="616" alt="Schermata 2022-11-02 alle 17 58 22" src="https://user-images.githubusercontent.com/64698911/199553364-2100ab33-b348-421f-9d02-71265fc27b35.png">

The two graphs show us an issue that arises when using the Lotka-Volterra system of equations as a model for the evolution of populations: the atto-fox problem, which consist in one of the two population reaching a mathematically feasible but biologically false value, i.e. 1e-18 part of a fox.

The main goal of our project will be to create a model able to solve the atto-fox problem, by tuning one or more parameters during time. In more practical terms, we will consider a population to be extinct if its number of individuals drops below a certain threshold and we will teach our model how to modify a set of the parameters in order to keep both populations constantly over this threshold.
When considering only one parameter we will modify α, the growth rate of the prey. In the multivariate case we will also include δ, the death rate of the predator. The choice of the parameters is due to a possible translation into an applicative setting: it is reasonable to imagine evolution studies where controlling α and δ via the constant addition or subtraction of some individuals would be much easier than controlling the predation rate of the groups.

In order to act in a realistic scenario, reasonable starting values for the four parameters are needed: we will thus refer to the standard case of the two populations of lynxes and snowshoe hares in Hudson Bay in Canada.

<!---
PIC lynxes and rabbits 
-->

The values for the parameters are the following: α = 0.55, β = 0.028, γ = 0.026, δ = 0.84

## Algorithm

The main algorithm used to reach our goals is Deep Q-learning, a reinforcement learning technique that is derived from vanilla Q-learning by replacing the Q function with a neural network. This step is necessary in our framework because the state-action space is continuous, thus cannot be fully represented using a discrete function like in vanilla Q-learning. A thorough explanation about how Q-learning and deep Q-learning work can be found in the report of the project. Let's see the main characteristics of our reinforcement learning environment: 

* We chose as state variables the numerosity of the two populations
* The actions that the agent can perform in order to modify the state variables consist in varying the parameters of the Lotka-Volterra system of equations by choosing their values on fixed grids. The numerosity of the grid changes based on how many parameters the agent is allowed to vary. Each time the agent has to choose an action, he selects one value on the grids.
* The reward reflects the goal of the agent: keeping the two populations alive. The rewards are the following: 
    1. if one of the two populations becomes extinct, we give a reward of -1000. A population is considered extinct if its numerosity drops below 4 units
    2. if the agent manages to keep the two populations alive for 400 time steps of the Lotka-Volterra system of equation, he obtains a reward of +500
    3. for the other steps, the reward is equal to -1

The algorithm consists in a training phase of 2000 episodes and a test phase of 200 episode, where an episode coincides with an entire simulation of Lokta-Volterra, until extinction of one of the two population or until the gol is reached. The initial state of the system is initialized randomly from a gaussian distribution. At every iteration, we select an action using an ε-greedy policy. Then, the values of the  parameters are changed accordingly and the Lotka-Volterra system of equation is run for two time step. This procedure will give a new state, according to which the previous state-action pair will receive a reward.

The details about the neural network and some other techniques used in the algorithm are better explained in the report. 

## Results 


We started considering only one parameter: α. We obtained the following results: 

<img width="445" alt="Schermata 2022-11-02 alle 21 48 44" src="https://user-images.githubusercontent.com/64698911/199599572-8a773865-6de3-46cc-93d5-fe4d732c3091.png">


The evolution of the states is too noisy, does not present any periodic pattern and α does not stabilize, but changes almost at every iteration. This is due to the fact that the model learns to overreact, while we want it to find a stable solution. To solve this issue we modified the reward and added a penalization term
which depends on the maximum range between the numerousity of the two populations: the greater this range is, the worse the reward. 
In this way we managed to reach our goal: 


<img width="445" alt="Schermata 2022-11-02 alle 21 48 08" src="https://user-images.githubusercontent.com/64698911/199599480-b2152f6f-585d-4ba8-8c4a-08cf6331cb2a.png">


We then tried to control two parameters: α and δ. The model is able to find a stable pair of parameters after just a few iterations, even without the introduction of the additional penalization term. The plots of the evolution of the populations and of the parameters are the follwoing: 


<img width="433" alt="Schermata 2022-11-02 alle 21 47 41" src="https://user-images.githubusercontent.com/64698911/199599400-edf35dc6-0a85-4685-a2bc-523183170151.png">





