# AlphaZero-Clone

It is important that we have 2 different components - Self Play and Training
During the Self Play phase, the AlphaZero model essentially plays with itself in order to learn the game, which generates data
During training, we like to optimize the model based on the information it gains from playing with itself
This optimized model is then used to self-play. This cycle is repeated until the neural network is capable of playing a game better than a human

The neural network architecture takes the state, S, as input. In the case of a game like tic-tac-toe, the value of S would just be the board position. The state as input will receive a policy(distribution value) and value (float value that is a measure of how promising the state is as a player to be in) as output.

The general algorithm used for the self-play concept will be monte carlo tree search. Monte Carlo tree search will take a state on our board position as input and identify the action that looks most promising to us. This algorithm gets this information by declaring a root note at the initial state, and then by building up this tree into the future based on possible moves. Nodes are based on possible future actions, all based on the initial state of the root node. There are 2 variables that each node possesses: w, which counts the total number of wins achieved by playing into the future after taking an action, and n, the total visit count (total number of times we went in a certain direction). 

Iterations of the Monte-Carlo Tree Search:
Selection: Walk “down” the tree until you reach a Leaf Node. We select the child node we want to “walk down” by choosing the node with the highest UCB formula. 

Expansion: Create New Node 
Simulation: Play randomly into the future using actions until we reach the end of the game. From this, we determine if we have won, lost, or ended in a draw, which would conclude the simulation
Backpropagation: The information from the simulation is collected and back propagated all the way up to the parent nodes until we have reached the root node. The values of the wins and visits (w and n) are updated as we go. These steps are then iterated.

Alpha Monte Carlo Tree Search:
When implementing MCTS to our General AlphaZero algorithm, there are 2 key changes we implement. First, we were to incorporate the policy that was gained from our model into the search process, especially by adding to the selection step. We can do this by updating our UCB formula:

When we select a child, we also incorporate the policy assigned to it (recall that policy is just the distribution of likelihoods). This way, our model guides us through selection. The next change is using the information gained from the neural network. By getting rid of the simulation and instead using the value of the states for backpropagation after random play, we improve search.
