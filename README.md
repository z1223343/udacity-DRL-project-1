[//]: # (Image References)

[image1]: https://user-images.githubusercontent.com/10624937/42135619-d90f2f28-7d12-11e8-8823-82b970a54d7e.gif "Trained Agent"

# udacity DRL project1

### Intrduction

For this project, you will train an agent to navigate (and collect bananas) in a large, square world.

![Trained Agent][image1]

A reward of +1 is provided for collecting a yellow banana, and a reward of -1 is provided for collecting a blue banana.  Thus, the goal of your agent is to collect as many yellow bananas as possible while avoiding blue bananas.  

The state space has 37 dimensions and contains the agent's velocity, along with ray-based perception of objects around agent's forward direction.  Given this information, the agent has to learn how to best select actions.  Four discrete actions are available, corresponding to:
- **`0`** - move forward.
- **`1`** - move backward.
- **`2`** - turn left.
- **`3`** - turn right.

### Instruction

The project consists of 6 files:
* navigation-main.ipynb - the main codes of this navigation project
* navigation-main.html - the HTML saving of results in jupyter notebook
* dqn_agent.py - the Agent class
* model.py - the DQN model
* checkpoint.pth - saved trained model to use
* README.md - the instructions about how to get started and what is the approach

To download the Unity Environment, you need only select the environment that matches your operating system:
* Linux: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux.zip)
* Mac OSX: [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana.app.zip)
* Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86.zip)
* Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Windows_x86_64.zip)
    
### Implementation Description

#### Learning Algorithm

The Reinforcement Learning architecture is built by [Pytorch](https://pytorch.org/).

In this navigation project, a deep Q network is trained to finish the task. Techniques like Experience Replay, Epsilon Greedy Algorithm and Fixed Q-Targets are implemented in the algorithm to make the agent more stable and intelligent.

#### Epsilon Greedy Algorithm

One challenge with Q-function above is dealing with the **exploration vs. exploitation dilemma**. Here **GLIE** (Greedy in the limit with infinite exploration) is implemented. This algorithm allows the agent to systematically manage the exploration vs. exploitation trade-off. The agent "explores" by picking a random action with some probability epsilon `𝛜`. However, the agent continues to "exploit" its knowledge of the environment by choosing actions based on the policy with probability (1-𝛜).

Furthermore, the value of epsilon is purposely decayed over time, so that the agent favors exploration during its initial interactions with the environment, but increasingly favors exploitation as it gains more experience. The starting and ending values for epsilon, and the rate at which it decays are three hyperparameters that are later tuned during experimentation.

#### Experience Replay

Experience replay allows the RL agent to learn from past experience. Each experience is stored in a replay buffer as the agent interacts with the environment. The replay buffer contains a collection of experience tuples with the state, action, reward, and next state `(s, a, r, s')`. The agent then samples from this buffer as part of the learning step. Experiences are sampled randomly, so that the data is uncorrelated.

#### Hyperparameters

* Replay buffer size = 100000
* Batch size = 64
* GAMMA (discount factor) = 0.99
* TAU (for soft update of target parameters) = 0.001
* Learning rate = 0.0005
* Update network evey 4 step

#### Results

Here is a figure showing the scores that my agent achieved during the hundreds of training episodes.

<img src="assets/best-agent-graph.png" width="75%" align="top-left" alt="" title="Best Agent Graph" />

The complete set of results and steps can be found in [here](Navigation-main.html)

### Future Improvements
Here's a list of optimizations that can be applied to the project:
1. Double DQN
2. Dueling DQN
3. Prioritized Experience Replay
4. Noisy DQN 
5. Rainbow: Combining Improvements in Deep Reinforcement Learning
