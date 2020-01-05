
# DeepTraffic: MIT Deep Reinforcement Learning Competition

[DeepTraffic](https://selfdrivingcars.mit.edu/deeptraffic) - [Visualization](https://selfdrivingcars.mit.edu/deeptraffic-visualization) - [Leaderboard](https://selfdrivingcars.mit.edu/deeptraffic-leaderboard) 

DeepTraffic is a deep reinforcement learning competition hosted as part of the [MIT Deep Learning](https://deeplearning.mit.edu) courses. The goal is to create a neural network that drives a vehicle (or multiple vehicles) as fast as possible through dense highway traffic. 

```bibtex
{

author = {Simranjeet Randhawa},
title = {DeepTraffic Solution},

}
```


## Problem Statement: Traffic is Terrible
> "Traffic is soul-destroying." - Elon Musk

> "Americans will put up with anything provided it doesn’t block traffic." - Dan Rather 



In the U.S. alone, we spend 6.9 billion hours sitting in traffic each year [1] — roughly 10,000 human lifetimes [2]. Autonomous vehicles will be able to alleviate part (but not all) of the problem. Already, they show promise in reducing phantom traffic jams [3,4].

We’ve designed DeepTraffic to let people (from beginners to experts) explore the design of motion planning algorithms for autonomous vehicles and to inspire the next generation of traffic engineering. We thank the thousands of competitors who have submitted solutions and are actively participating.

## DeepTraffic Layout

<img src="https://selfdrivingcars.mit.edu/wordpress/wp-content/uploads/2018/01/Screenshot-from-2018-01-08-17-45-42.png" 
alt="DeepTraffic" width="600" />

The game page consists of four different areas:

- On the left, you can find a real time simulation of the road with different display options.

- On the upper half of the page, you can find (1) a coding area where you can change the design of the neural network which controls the agents and (2) some buttons for applying your changes, saving/loading, and making a submission.

- Below the coding area, you can find (1) a graph showing a moving average of the center red car’s reward, (2) a visualization of the neural network activations, and (3) buttons for training and testing your network.

- Between the simulated roadway and the graphs, you can find the current image of you vehicle and some options to customize it and create a visualization of your best submission.

The simulation area shows some basic information like the current speed of the car and the number of cars that have been passed since you opened the site. It also allows you to change the way the simulation is displayed.
![Display selection](http://selfdrivingcars.mit.edu/wordpress/wp-content/uploads/2017/01/normal.gif)

## DeepTraffic Simulation & Game

In short, DeepTraffic is a game in which you (a competitor) design your own motion planning algorithm in order to drive a vehicle as fast as possible through dense traffic.

Your algorithm will operate on a 7 lane highway. There are 20 vehicles on the road. Your algorithm controls some vehicles. The game controls the others.

Each autonomous agent runs a copy of your algorithm. Every 30 frames, your algorithm selects 1 of 5 actions:

1. accelerate
1. decelerate
1. change into the left lane
1. change in to the right lane
1. do nothing, i.e. maintain speed in present lane.

Your algorithm will receive, as input, an occupancy grid, representing the free space around the agent. The value of unoccupied cells is set to 80mph. The value of occupied cells is set to the speed of the occupying vehicle. For example here's an occupancy grid `(lanesSide = 1; patchesAhead=10)`:

![learning input](https://selfdrivingcars.mit.edu/wordpress/wp-content/uploads/2017/01/Screen-Shot-2017-01-03-at-16.06.29-151x300.png)

There are a few quirks to DeepTraffic’s dynamics:

### Safety System

Each vehicle has a safety system which prevents it from colliding with other vehicles. This has 2 implications for how you will design your algorithm. First, your algorithm does not need to consider collision avoidance. Second, your path will be overridden when the safety system is activated.

For example, here, the red car cannot accelerate or change into the right lane, because the collision avoidance system has detected vehicles in the way:

![safety system](https://selfdrivingcars.mit.edu/wordpress/wp-content/uploads/2017/01/Screen-Shot-2017-01-03-at-16.28.32-152x300.png)

A vehicle that is 4 cells behind another will immediately slow to match the lead vehicle, regardless of what its algorithm tries to do. (see diagram above)

A vehicle driving beside another will be unable to change into its neighbor’s lane until there is a sufficient gap, regardless of what its algorithm tries to do. (see diagram above)

### Multiple Agents

In version 2.0, the current version, you have the option to deploy a copy of your algorithm on 11 vehicles. You algorithm won’t do multi-agent planning, rather each vehicle makes a greedy choice. The challenge is to design an algorithm which does not get in its own way when controlling several vehicles.

### Where the Highway Ends

DeepTraffic follows just one of the vehicles (the ego vehicle), so you’ll notice some of the vehicles fall off the highway when they drive slower or faster than the ego vehicle. What happens to these vehicles?

When vehicles fall off the road, they are replaced by new vehicles on the opposite end of the highway. When a vehicle is replaced, its speed & lane is chosen randomly.

### Result

With this parameters I get 74.50. But there is random in submission and speed can vary between 74 and 75. So the same submission may vary about 0.5 mph. So try multiple times.
