Simple Continuous Control with DRL
==================================

How to Solve Simple Continuous Control Problem by DRL Policy-based Method(DDPG)
-------------------------------------------------------------------------------

---

We will introduce to solve simple continuous control problem by Deep Reinforcement Learning Policy-based Method like DDPG with Unity ML-Agents Reacher environment.

### Prerequisites

#### Theoretical things

-	Read about Traditional Reinforcement Learning : [Reinforcement Learning: An Introduction by Richard S. Sutton and Andrew G. Barto - Second Edition](http://incompleteideas.net/book/the-book.html)
-	Read [REINFORCE algorithm paper](http://www-anw.cs.umass.edu/~barto/courses/cs687/williams92simple.pdf) by Williams 1992.
-	Read [PPO paper](https://arxiv.org/abs/1707.06347) by Open AI 2017.
-	Read the most famous [blog post](http://karpathy.github.io/2016/05/31/rl/) on policy gradient methods.
-	Implement a policy gradient method to win at Pong in this [Medium post](https://medium.com/@dhruvp/how-to-write-a-neural-network-to-play-pong-from-scratch-956b57d4f6e0).
-	Learn more about [evolution strategies](https://blog.openai.com/evolution-strategies/) from OpenAI.

#### Technical things

-	Read about Deep Learnming with PyTorch : https://github.com/udacity/DL_PyTorch

### Optional Reference

#### Theoretical things

-	refer to [Antonio Park's blog](https://parksurk.github.io/deep/reinfocement/learning/drlnd_3_policy_based_methods-post/) about DRL Policy-based method.
-	Read [A3C paper](https://arxiv.org/abs/1602.01783) by DeepMind ICML 2016.
-	Read [Q-Prop paper](https://arxiv.org/abs/1611.02247) ICLR 2017.
-	Read [A2C - Open AI Baseline Blog post](https://blog.openai.com/baselines-acktr-a2c/).
-	Read [GAE paper](https://arxiv.org/abs/1506.02438).
-	Read [DDPG paper](https://arxiv.org/abs/1509.02971).

#### Technical things

-	Check about Deep Reinforcement Learnming GitHub with PyTorch by Shangtong Zhang : https://github.com/ShangtongZhang/DeepRL

### Project Details

For this project, you will work with the Unity ML-Agents **Reacher** environment.

![Reacher-Single Agent](assets/reacher-SingleAgent.gif)<p align="center"> Picture 1 - Reacher-Single Agent</p>

![Reacher-Distributed Agents](assets/reacher.gif)<p align="center"> Picture 2 -Reacher-Distributed Agents</p>

In this environment, a double-jointed arm can move to target locations. A reward of +0.1 is provided for each step that the agent's hand is in the goal location. Thus, the goal of our agent is to maintain its position at the target location for as many time steps as possible.

The observation space consists of 33 variables corresponding to position, rotation, velocity, and angular velocities of the arm. Each action is a vector with four numbers, corresponding to torque applicable to two joints. Every entry in the action vector should be a number between -1 and 1.

#### Note - Distributed Training

For this project, we will provide you with two separate versions of the Unity environment:

-	The first version contains a single agent.
-	The second version contains 20 identical agents, each with its own copy of the environment.

The second version is useful for algorithms like [PPO](https://arxiv.org/pdf/1707.06347.pdf), [A3C](https://arxiv.org/pdf/1602.01783.pdf), and [D4PG](https://openreview.net/pdf?id=SyZipzbCb) that use multiple (non-interacting, parallel) copies of the same agent to distribute the task of gathering experience.

#### Note - Solving the Environment

Note that our project will use two versions of the environment.

-	Option 1: Solve the First Version The task is episodic, and in order to solve the environment, our agent will get an average score of +30 over 100 consecutive episodes.

-	Option 2: Solve the Second Version The barrier for solving the second version of the environment is slightly different, to take into account the presence of many agents. In particular, our agents will get an average score of +30 (over 100 consecutive episodes, and over all agents). Specifically,

After each episode, we add up the rewards that each agent received (without discounting), to get a score for each agent. This yields 20 (potentially different) scores. We then take the average of these 20 scores. This yields an average score for each episode (where the average is over all 20 agents).

---

### Getting Started

Follow the instructions below to explore the environment on your own machine! You will also learn how to use the Python API to control your agent.

#### Step 1: Clone the DRLND Repository

If you haven't already, please follow the [instructions in the DRLND GitHub repository](https://github.com/udacity/deep-reinforcement-learning#dependencies) to set up your Python environment. These instructions can be found in README.md at the root of the repository. By following these instructions, you will install PyTorch, the ML-Agents toolkit, and a few more Python packages required to complete the project.

(For Windows users) The ML-Agents toolkit supports Windows 10. While it might be possible to run the ML-Agents toolkit using other versions of Windows, it has not been tested on other versions. Furthermore, the ML-Agents toolkit has not been tested on a Windows VM such as Bootcamp or Parallels.

#### Step 2: Download the Unity Environment

For this project, you will not need to install Unity - this is because we have already built the environment for you, and you can download it from one of the links below. You need only select the environment that matches your operating system:

-	Version 1: One (1) Agent
	-	Linux: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Linux.zip)
	-	Mac OSX: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher.app.zip)
	-	Windows (32-bit): click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86.zip)
	-	Windows (64-bit): click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/one_agent/Reacher_Windows_x86_64.zip)
-	Version 2: Twenty (20) Agents
	-	Linux: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Linux.zip)
	-	Mac OSX: click [here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher.app.zip)
	-	Windows (32-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86.zip)
	-	Windows (64-bit): [click here](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P2/Reacher/Reacher_Windows_x86_64.zip)

Then, place the file in the p2_continuous-control/ folder in the DRLND GitHub repository, and unzip (or decompress) the file.

(For Windows users) Check out [this link](https://support.microsoft.com/en-us/help/827218/how-to-determine-whether-a-computer-is-running-a-32-bit-version-or-64) if you need help with determining if your computer is running a 32-bit version or 64-bit version of the Windows operating system.

(For AWS) If you'd like to train the agent on AWS (and have not [enabled a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md)), then please use [this link](https://s3-us-west-1.amazonaws.com/udacity-drlnd/P1/Banana/Banana_Linux_NoVis.zip) to obtain the "headless" version of the environment. You will not be able to watch the agent without enabling a virtual screen, but you will be able to train the agent. (To watch the agent, you should follow the instructions to [enable a virtual screen](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Training-on-Amazon-Web-Service.md), and then download the environment for the Linux operating system above.)

#### Step 3: Explore the Environment

After you have followed the instructions above, open Continuous_Control.ipynb (located in the p2_continuous-control/ folder in the DRLND GitHub repository) and follow the instructions to learn how to use the Python API to control the agent.

Watch the (silent) [video](https://youtu.be/i2gVvXgOMnc) below to see what kind of output to expect from the notebook (for version 2 of the environment), if everything is working properly! Version 1 will look very similar (where you'll see a single agent, instead of 20!). In the last code cell of the notebook, you'll learn how to design and observe an agent that always selects random actions at each timestep. Your goal in this project is to create an agent that performs much better!

#### (Optional) Build your Own Environment

For this project, we have built the Unity environment for you, and you must use the environment files that we have provided.

If you are interested in learning to build your own Unity environments after completing the project, you are encouraged to follow the instructions [here](https://github.com/Unity-Technologies/ml-agents/blob/master/docs/Getting-Started-with-Balance-Ball.md), which walk you through all of the details of building an environment from a Unity scene.

---

### Instructions

To setup our project environment to run the code in this repository, follow the instructions below.

1.	Clone this repository

```
git clone https://github.com/parksurk/drl_policy-based_methods.git
```

1.	Create (and activate) a new environment with Python 3.6.
	-	Linux or Mac:`
		conda create --name drlnd python=3.6
		`
	-	Windows:`
		conda create --name drlnd python=3.6
		activate drlnd
		`
2.	Follow the instructions in this repository to perform a minimal install of OpenAI gym. (Skip if you done already)
	-	Next, install the classic control environment group by following the instructions here.
	-	Then, install the box2d environment group by following the instructions here.
3.	Clone the repository (if you haven't already!), and navigate to the python/ folder. Then, install several dependencies. (Skip if you done already)

```
git clone https://github.com/udacity/deep-reinforcement-learning.git
cd deep-reinforcement-learning/python
pip install .
```

1.	Create an IPython kernel for the drlnd environment. (Skip if you done already)

```
python -m ipykernel install --user --name drlnd --display-name "drlnd"
```

1.	Run Jupyter Notebook

```
jupyter notebook
```

1.	Before running code in a notebook, change the kernel to match the drlnd environment by using the drop-down Kernel menu. ![Jupyter Notebbok Kernel Setting](assets/jupyter_notebook_kernel_menu.png)
2.	Click **Report.ipynb** on root directory for "Version 1: One (1) Agent" ![Version1_Score](assets/version1_score_plt.png)

Picture 3 - Reacher-Single Agent - Score Plot

1.	Click **Report-Version2.ipynb** on root directory for "Version 2: Twenty (20) Agents" ![Version2_Score](assets/version2_score_plt.png)

Picture 4 - Reacher-Distributed Agents - Score Plot

---

### Benchmark Implementation

In case you get stuck, refer to the details of one approach that worked well.

#### Attempt 1

The first thing that we did was amend the DDPG code to work for multiple agents, to solve version 2 of the environment. The DDPG code in the DRLND GitHub repository utilizes only a single agent, and with each step:

-	the agent adds its experience to the replay buffer, and
-	the (local) actor and critic networks are updated, using a sample from the replay buffer.

So, in order to make the code work with 20 agents, we modified the code so that after each step:* each agent adds its experience to a replay buffer that is shared by all agents, and* the (local) actor and critic networks are updated 20 times in a row (one for each agent), using 20 different samples from the replay buffer. In hindsight, this wasn't a great plan, but it was a start! That said, the scores are shown below.

![benchmark-attempt1](assets/benchmark-attempt1.png)

You'll notice that we made some rapid improvement pretty early in training, because of the extremely large number of updates. Unfortunately, also due to the large number of updates, the agent is incredibly unstable. Around episode 100, performance crashed and did not recover.

So, we focused on determining ways to stabilize this first attempt.

#### Attempt 2

For this second attempt, we reduced the number of agents from 20 to 1 (by switching to version 1 of the environment). We wanted to know how much stability we could expect from a single agent. The idea was that the code would likely train more reliably, if we didn't make so many updates. And it did train much better.

![benchmark-attempt2](assets/benchmark-attempt2.png)

At one point, we even hit the target score of 30. However, this score wasn't maintained for very long, and we saw strong indications that the algorithm was going to crash again. This showed us that we needed to spend more time with figuring out how to stabilize the algorithm, if we wanted to have a chance of training all 20 agents simultaneously.

#### Attempt 3

This time, we switched back to version 2 of the environment, and began with the code from Attempt 1 as a starting point. Then, the only change we made was to use gradient clipping when training the critic network. The corresponding snippet of code was as follows:

```
self.critic_optimizer.zero_grad()
critic_loss.backward()
torch.nn.utils.clip_grad_norm(self.critic_local.parameters(), 1)
self.critic_optimizer.step()
```

The corresponding scores are plotted below.

![benchmark-attempt3](assets/benchmark-attempt3.png)

This is when we really started to feel hopeful. We still didn't maintain an average score of 30 over 100 episodes, but we maintained the score for longer than before. And the agent didn't crash as suddenly as in the previous attempts!

#### Attempt 4

At this point, we decided to get less aggressive with the number of updates per time step. In particular, instead of updating the actor and critic networks 20 times at every timestep, we amended the code to update the networks 10 times after every 20 timesteps. The corresponding scores are plotted below.

![benchmark-attempt4](assets/benchmark-attempt4.png)

And, this was enough to solve the environment! In hindsight, we probably should have realized this fix much earlier, but this long path to the solution was definitely a nice way to help with building intuition!
