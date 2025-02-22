# **An Agent Based Model of the Dark Forest Conjecture**

# Project Overview

The purpose of this project is to develop an agent based model through which the user can explore the [Dark Forest Conjecture](https://en.wikipedia.org/wiki/Dark_forest_hypothesis) as developed by [Liu Cixin](https://en.wikipedia.org/wiki/Liu_Cixin) in his science fiction novel of the same name. This model will allow users to maniulate a number of parameters related to the environment, resource availability, and numerous aspects effecting the behavior of agents and their interactions. The model is currently being developed using the opensource [Netlogo](https://ccl.northwestern.edu/netlogo/) software for agent based model development. 

## Developers
This project is currently being developed by [Michael Heinle](heinle.michaeld@gmail.com) as a thought experiment and practice in the design and execution of more advanced agent based models. The code for this model is shared freely and contributions, fixes, and requests/suggestions for additional functionalities are welcome. Contact is accept either via email or the [project GitHub repository.](https://github.com/mheinle1/dark_forest_abm)

# Model Overview

## Synopsis
### Agents, Development, Environment
In this model, agents, representing space faring civilizations, will navigate an evironment in order to secure resources. Basic resource acquisition is necessary to replenish a basic resource pool or score which depletes at a regular interval. Each agent has a number of attributes such as speed and detection which are determined by a technological development score. The technological development score (TDS) increases by a standard increment every x iterations of the model to a user determined maximum. Once a user defined threshold for the TDS is reached, basic resources will no longer suffice and the agent will need to focus on locating rarer advanced resources, causing the agent to explore further from its homebase. Users will have the ability to control when and where new agents spawn, the density of both basic and advanced resources, and how quickly each resource type regenerates.

### Agent Interaction
At the crux of the model is the interaction between agents. Agents begin with no knowledge of other agents. As the model iterates and agents are forced to travel further through the environment insearch of resources, the probability of becoming aware of other agents increases. An agent may detect another agent or the homebase of another agent. This allows agents with lower TDS the ability to detect those of higher TDS without themselves being detected. The ability to detect other agents is a function of the agent's TDS, agents with higher TDS will have a broader field of detection. This allows for situations where an agent may become aware of another agent without being itself detected provided that the second agent is of a sufficiently lower TDS. Once an agent detects another agent, the homebase of the second agent is known to the original agent. The TDS of the detected agent is not known to the detecting agent. At this point, the detecting agent will have a number of actions it can take.
  - Destroy
  - Contact
  - Observe
  - Hide
  - Broadcast

#### Destroy
As the detecting agent is aware of the homebase position of the second agent, the detecting agent may choose to destroy this homebase. The TDS level of the agent taking the destroy action determines the number of iterations between the action being taken and the actual destruction of the detected agent's homebase. This allows for futher interactions to take place, for instance, the second agent may have an opportunity to detect the first and take an action prior to the destruction of its homebase. 

#### Contact
The decting agent can contact the second agent. If this action is taken, both agents will be aware of the location of each other's homebase. The contact action is effectively a request for cooperation. The second agent may accept this request in which case both agent's TDS will be set to the higher of the two. These agents will no longer be able to take the Destroy or Broadcast action against one another. Alternatively, the second agent may take the Destroy, Hide, or Broadcast action in responce to being contacted. 

### Observe
This action is not fully flushed out yet conceptually. A rough implementation might be that the detecting agent takes the Observe action to monitor the dected agent and respond to the detected agent based on that agent's interaction with a third agent. For example, agent 1 observes agent 2 until agent 2 uses the Destroy action on agent 3, causing agent 1 to take the Destroy action against agent 2. 

### Hide
The Hide action becomes available to any agent as soon as they make a detection of any other agent. After an intial detection, the detecting agent may take the Hide action at any time. Taking this action immediately reduces the agent's TDS to 1. All associated attributes are also reduced accordingly. The agent returns to homebase and does not leave. This reflects the purpose of the Hide action which is preservation of the civilizations by giving up all technology and space travel, effectively going dark.

### Broadcast
An agent may choose to take the Broadcast action at any point in time after an initial detection of another agent. The Broadcast action makes all agents currently active in the model aware of the location of all homebases of which the broadcaster is aware, including its own.
