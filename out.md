![](img/Presentazione0.png)

__With Deep Q\-Learning__

<span style="color:#000000"> __Davide Carrara__ </span>

<span style="color:#000000"> __Francesco Romeo__ </span>

<span style="color:#000000"> __Daniela __ </span>  <span style="color:#000000"> __Zanotti__ </span>

<span style="color:#172144"> __Avoid species extinction__ </span>

__\- Alfred J\. __  __Lotka__  __\, Vito Volterra\-__

<span style="color:#172144"> __Rabbits and Lynxes__ </span>

<span style="color:#172144"> __In Canada__ </span>

<span style="color:#172144">https://www\.behance\.net/gallery/70404455/Wave\-On</span>

|  | Action 1 | Action 2 | Action 3  | Action 4 |
| :-: | :-: | :-: | :-: | :-: |
| State 1 |  |  |  |  |
| State 2 |  |  |  |  |
| State 3 |  |  |  |  |

![](img/Presentazione1.png)

<span style="color:#172144">https://unsplash\.com/photos/Tizbbx\-5esA</span>

ALGORITHM

For each episode

Obtain  __next__  __ state __ solving Lotka Volterra

and compute the  __reward__

__Evaluate__  Q for each action using Neural Network

__Improving__  __ __

__our__  __ __  __algorithm__  __ __

Experience Replay

Weights are not updated

at every iteration\,

but we  __intertwine observation and update __ for a gradual improvement

To update Q\-function\,

we random sample

from a  __buffer__  of

__past observations__

The  __observed value __ of Q

in the loss function

is computed using

a  __periodic copy __

of the Q\-network

<span style="color:#172144">https://unsplash\.com/photos/Tizbbx\-5esA</span>

![](img/Presentazione2.png)

Excessive  __variation__  of α

Evolution of the states is

__not__  __ __  __smooth__  __ __  __nor__  __ __  __periodic__

The model learns

to  __overreact__

We want it to  __stabilize__ \,

to have a more robust solution

<span style="color:#172144">https://unsplash\.com/photos/Tizbbx\-5esA</span>

![](img/Presentazione3.png)

![](img/Presentazione4.png)

<span style="color:#172144">https://unsplash\.com/photos/Tizbbx\-5esA</span>

![](img/Presentazione5.png)

α\, δ can be  __controlled__

in  __real__  case scenarios

With two parameters it’s easier to find a  __stable__  __ __  __orbit__

__No__  need of  __additional__  __ __  __penalization__

When controlling  __one __  __parameter__ \,

it is necessary to add more  __constraints__  through the rewards

With  __two__  __ __  __parameters__  __ __ the model

is able to reach  __stable__  values

Try to act on  __more __  __parameters__  __ __

__Increase__  __ __  __variance__  __ __ of the initial

numerosity of populations

__Increase__  __ __ the possible  __actions__

