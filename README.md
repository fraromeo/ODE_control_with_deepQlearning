# ODE Control with Deep Q-learning

## Introduction

The goal of the project is to determine a controlling procedure for the evolution of an Ordinary Differential
Equation in a Deep Reinforcement Learning Framework, with the particular approach of Deep Q-Learning. Our study case is the Lokta Volterra system of equations, which describes how the number of individuals of a population formed by preys and predators vary due to the interaction between these two species. 
<!---
PIC system eq
-->
The variables x and y represent respectively the number of individuals of the prey and the predator population, while α, β, γ, δ are positive real parameters.
It is worth noting that the preys are assumed to have infinite food resources at their disposal and thus their reproduction rate is determined only by the parameter α, without any suffering due to scarcity in case of overpopulation. On the other hand, the parameter β determines the predation rate of the prey due to the predator: this is the only case of death for the prey in the system.
γ represents the growth rate of the predator population, which is entirely defined by its interaction with the prey: notice that the term is similar to the predation rate, but the two coefficients are different. δ represents the natural decay of the predator population, either due to death or emigration.

The Lotka-Volterra system of equations admits a periodic solution for any tuple of parameters
<!---
PIC sol 
-->
we can note a serious problem when using the Lotka-Volterra system as a model for the evolution of populations. Since the values of x and y are continuous it happens often that one population reaches extremely low values, recovering after some time. This is mathematically correct but biologically false. This phenomenon is known as the atto-fox problem, with atto-fox being the 10−18 part of a fox.

The main goal of our project will be to create a model able to solve the atto-fox problem, by tuning one or more parameters during time. In more practical terms, we will consider a population to be extinct if its number of individuals drops below a certain threshold and we will teach our model how to modify the parameter in order to keep both populations constantly over this threshold.
When considering only one parameter we will modify α, the growth rate of the prey. In the multivariate case we will also include δ, the death rate of the predator. The choice of the parameters is due to a possible translation into an applicative setting: it is reasonable to imagine evolution studies where controlling α and δ via the constant addition or subtraction of some individuals would be much easier than controlling the predation rate of the groups.
