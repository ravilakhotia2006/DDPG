## Learning algorithm
Since we have continous action space, I have used vanilla DDPG algorithm. Both the agents share common replay buffer and actor-critic network. Have used Ornstein-Uhlenbeck process for generating Gaussian noise.


## Network acrhitecture

### Actor Network:

* Input layer size is 33 as there are 22 states.
* Relu activation is used for hidden layer.
* Output layer size as there are 2 actions (2 agents)

*NOTE*: Adding dropout was sometimes degrading the performance or had no affect on this network

[22]------>[128]------(Relu)------>[2]

### Critic Network:

* Network have 3 hidden layer(128, 64, 32 units), 
* Output layer of size 1
* Relu activation is used for hidden layer

[22]----->[128]----(Relu)---->[4]

[64 + 2]----(Relu)----->[32]----(Relu)---->[1]

### Hyperparameters:
* TAU (for soft update of target parameters) = 0.001
* LR-Actor (learning rate) = 0.001
* LR-Critic (learning rate) = 0.003
* GAMMA (discount factor) = 0.99
* BATCH_SIZE (minibatch size) = 1024
* BUFFER_SIZE (replay buffer size) = 1000000

### Reward Plot
![Reward plot](https://github.com/ravilakhotia2006/DDPG/blob/master/score-episode-plot.png)

* Agent starts to recieve high reward from around 2100 episodes. It took aournd 2200 episode to solve the environment.

### Other experiments
* When I added dropout in actor network, rewards fluctuated a bit and achieved .5+ at 5400 episodes.
* By adding 2 hidden layers in actor network and dropouts for both, .5+ was sometimes achieved at 2500 episodes. Not consistent though. Not sure why.

### Ideas to improve the performance of the agent in future
* We can try parameter space noise rather than noise on action. This seems to give better performance. https://vimeo.com/252185862
* Prioritized experience buffer would make more sense rather a dumb replay buffer.
* We can try using different replay buffer for each agent.
* Tuning hyperparameters might increase performance.
* We can try changing actor/critic network architecture.
* We can also try adding dropout in network. I did and performance degraded for me. But with different network and hyperparameters, dropout could increase performance
