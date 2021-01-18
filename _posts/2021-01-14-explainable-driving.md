---
toc: true
layout: post
description: "Hedi Ben younes, Eloi Zablocki"
categories: [explainability, interpretability, survey, self-driving]
title: "How can we make driving systems explainable?"
hide: true
image: images/posts/advent/qualitative_results.png
---

<!-- Research on autonomous vehicles is blooming thanks to recent advances in deep learning and computer vision \citep{imagenet_classification,deeplearning_nature}, as well as the development of autonomous driving datasets and simulators \citep{kitti,carla,YuCWXCLMD20}.
The number of academic publications on this subject is rising in most machine learning, computer vision, robotics and transportation conferences, and journals.
On the industry side, several manufacturers are already producing cars equipped with advanced computer vision technologies for automatic lane following, assisted parking, or collision detection among other things. Meanwhile, constructors are working on and designing prototypes with level 4 and 5 autonomy.
The development of autonomous vehicles has the potential to reduce congestions, fuel consumption, and crashes, and it can increase personal mobility and save lives given that nowadays the vast majority of car crashes are caused by human error \citep{anderson2014autonomous}.

The first steps in the development of autonomous driving systems are taken with the collaborative European project PROMETHEUS (Program for a European Traffic with Highest Efficiency and Unprecedented Safety) \citep{prometheus} at the end of the '80s and the Grand DARPA Challenges in the late 2000s.
At these times, systems are heavily-engineered pipelines \citep{urmson2008autonomous,thrun2006stanley} and their modular aspect decomposes the task of driving into several smaller tasks --- from perception to planning --- which has the advantage to offer interpretability and transparency to the processing. Nevertheless, modular pipelines have also known limitations such as the lack of flexibility, the need for handcrafted representations, and the risk of error propagation.
In the 2010s, we observe an interest in approaches aiming to \emph{train} driving systems, usually in the form of neural networks, either by leveraging large quantities of expert recordings \citep{pilotnet,codevilla2018end,imitation_overview} or through simulation \citep{Espi2005TORCSTO,marinaffordance,carla}.
In both cases, these systems learn a highly complex transformation that operates over input sensor data and produce end-commands (steering angle, throttle). 
While these neural driving models overcome some of the limitations of the modular pipeline stack, they are sometimes described as \emph{black-boxes} for their critical lack of transparency and interpretability.
 -->
## Contextual elements

### Why do we need explainable driving models?


### Explainability ?

Many terms are related to the concept of explainability and several definitions have been proposed for each of these terms. The boundaries between concepts are fuzzy and constantly evolving. 
In human-machine interactions, explainability is defined as the ability for the human user to understand the agent's logic {%cite RosenfeldR19 %}. 
The explanation is based on how the human user understands the connections between inputs and outputs of the model. 
According to {%cite doshi2017accountability %}, an explanation is a human-interpretable description of the process by which a decision-maker took a particular set of inputs and reached a particular conclusion. They state that in practice, an explanation should answer at least one of the three following questions: 
- *What were the main factors in the decision?*
- *Would changing a certain factor have changed the decision?* 
- *Why did two similar-looking cases get different decisions, or vice versa?*

The term explainability often co-occurs with the concept of interpretability.
Some recent work of {%cite beaudouin2020identifying %} simply advocate that explainability and interpretability are synonyms.
However, {%cite GilpinBYBSK18 %} provide a nuance between these terms that we find interesting. According to them, interpretability designate to which extent an explanation is understandable by a human. 
They state that an explanation should be designed and assessed in a trade-off between its interpretability and its completeness, which measures how accurate the explanation is as it describes the inner workings of the system. 
For example, an exhaustive and completely faithful explanation is a description of the system itself and all its processing: this is a complete explanation although the exhaustive description of the processing may be incomprehensible.
The whole challenge in explaining neural networks is to provide explanations that are both interpretable and complete. 



The relation with autonomous vehicles differs a lot depending who is interacting with the system. 
Indeed, expected explanations will be of varying nature, form and should convey different types of information regarding who is the explanation geared towards:
- **End-users** and citizens need to trust the autonomous system and to be reassured. They put their life in the hands of the driving system and thus need to gain trust in it. 
There is a long and dense line of research trying to define, characterize, evaluate, and increase the trust between an individual and a machine. 
It appears that user trust is heavily impacted by the system transparency {%cite trusthci20 %}: providing information that helps the user understand how the system functions foster his or her trust in the system. Interestingly, research on human-computer interactions argues that the timing of explanations is important for trust: they should be provided before the vehicle takes an action, in a formulation which is concise and direct. {%cite RosenfeldR19 %},{%cite haspiel2018explanations %},{%cite du2019look %}
- **Designers** of self-driving models need to understand their limitations to validate them and improve future versions \citep{deeptest}.
The concept of Operational Design Domain (ODD) is often used by carmakers to designate the conditions under which the car is expected to behave safely.
Thus, whenever a machine learning model is built to address the task of driving, it is crucial to know and understand its failure modes, and to verify that these situations do not overlap with the ODD. 
A common practice is to stratify the evaluation into situations, as is done by the European New Car Assessment Program (Euro NCAP) to test and assess assisted driving functionalities in new vehicles.
But even if these in-depth performance analysis are helpful to improve the model's performance, it is not possible to exhaustively list and evaluate every situation the model may possibly encounter. 
As a fallback solution, explainability can help delving deeper into the inner workings of the model and to understanding why it makes these errors and correct the model/training data accordingly.
- **Legal and regulator bodies** are interested in explanations for *liability* and *accountability* purposes, especially when a self-driving system is involved in a car accident. 
   Notably, explanations generated for legal or regulatory institutions are likely to be different from those addressed to the end-user. 
   As noted in {%cite beaudouin2020identifying %}, detailed explanations of all aspects of the decision process could be required to identify the reasons for a malfunction.
These explanations are directed towards experts who will likely spend large amounts of time studying the system, and who are thus inclined to receive rich explanations with great amounts of detail. 

### Driving system ?

The history of autonomous driving systems started in the late '80s and early '90s with the European Eureka project called Prometheus.
This has later been followed by driving challenges proposed by the Defense Advanced Research Projects Agency (DARPA). The vast majority of autonomous systems competing in these challenges is characterized by their modularity.
Leveraging strong suites of sensors, these systems are composed of several sub-modules, each completing a very specific task. 
Broadly speaking, these sub-tasks deal with sensing the environment, forecasting future events, planning, taking high-level decisions, and controlling the vehicle.

As pipeline architectures split the driving task into easier-to-solve problems, they offer somewhat interpretable processing of sensor data through specialized modules (perception, planning, decision, control).
However, these approaches have several drawbacks:
- First, they rely on human heuristics and manually-chosen intermediate representations, which are not proven to be optimal for the driving task. 
- Second, they lack flexibility to account for real-world uncertainties and to generalize to unplanned scenarios.
Moreover, from an engineering point of view, these systems are hard to scale and to maintain as the various modules are entangled together.
- Finally, they are prone to error propagation between the multiple sub-modules.

To circumvent these issues, and nurtured by the deep learning revolution, researchers put more and more efforts on machine learning-based driving systems, and in particular on deep neural networks which can leverage large quantities of data.

We can distinguish four key elements involved in the design of a neural driving system: input sensors, input representations, output type, and learning paradigm

![driving_architecture]({{ site.baseurl }}/images/posts/explainable_driving/driving_architecture.png){:width="100%"}

- **Sensors**. They are the hardware interface through which the neural network perceives its environment.
Typical neural driving systems rely on sensors from two families: *proprioceptive* sensors and *exteroceptive* sensors. *Proprioceptive* sensors provide information about the internal vehicle state such as speed, acceleration, yaw, change of position, and velocity. They are measured through tachometers, inertial measurement units (IMU), and odometers.  All these sensors communicate through the controller area network (CAN) bus, which allows signals to be easily accessible. In contrast, *exteroceptive* sensors acquire information about the surrounding environment. They include cameras, radars, LiDARs, and GPS. For a more thorough review of driving sensors, we refer the reader to {%cite survey_sensors %}. 
- **Input representation**. Once sensory inputs are acquired by the system, they are processed by computer vision models to build a structured representation, before being passed to the neural driving system. In the *mediated perception* approach, several perception systems provide their understanding of the world, and their outputs are aggregated to build an input for the driving model.
An example of such vision tasks is object detection and semantic segmentation, which aim at finding and classifying relevant objects in a scene (cars, bicycles, pedestrians, stop signs, *etc.*), tracking objects accross time, extracting depth information (*i.e.* knowing the distance that separates the vehicle from each point in the space), recognition of pedestrian intent...
Mediated perception contrasts with the *direct perception* approach, which instead extracts visual affordances from an image.
Affordances are scalar indicators that describe the road situation such as curvature, deviation to neighboring lanes, or distances between ego and other vehicles.
These human-interpretable features are usually recognized using neural networks as in {%cite deepdrivingaffordance %}.
Then, they are passed at the input of a driving controller which is usually hard-coded, even if some recent approaches use affordance recognition to provide compact inputs to learning-based driving systems {%cite marinaffordance %}. 
- **Outputs**. Ultimately, the goal is to generate vehicle controls. Some approaches, called end-to-*end*, tackle this problem by training the deep network to directly output the commands.
However, in practice most methods instead predict the future trajectory of the autonomous vehicle; they are called end-to-*mid* methods. The trajectory is then expected to be followed by a low-level controller, such as the proportional–integral–derivative (PID) controller.
- **Learning**.
Two families of methods coexist for training self-driving neural models: *behavior cloning* approaches, which leverage datasets of human driving sessions, and *reinforcement learning* approaches, which train models through trial-and-error simulation.
	- Behavior cloning (BC) approaches leverage huge quantities of recorded human driving sessions to learn the input-output driving mapping by imitation. 
	In this setting, the network is trained to mimic the commands applied by the expert driver (end-to-end models), or the future trajectory (end-to-mid models), in a supervised fashion. 
	Initial attempt to behavior cloning of vehicle controls was made in {%cite Pomerleau88 %}, and continued later in {%cite pilotnet %}.
	- Reinforcement learning (RL) was alternatively explored by researchers to train neural driving systems. This paradigm learns a policy by balancing self-exploration and reinforcement.
    This training paradigm does not require a training set of expert driving but relies instead on a simulator such as CARLA {%cite carla %}.

## Post-hoc explanation

## Desigining an explainable driving model

## Use-case: generating natural language explanations

## Conclusion