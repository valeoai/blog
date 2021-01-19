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
- **Designers** of self-driving models need to understand their limitations to validate them and improve future versions.
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
<div class="caption"><b>Figure 1. Overview of neural network-based autonomous driving systems.</b></div>

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

### The challenges of explainability of neural driving systems

Introducing explainability in the design of learning-based self-driving systems is a challenging task.
These concerns arise from two aspects: 
- From an **ML perspective**, explainability hurdles of self-driving models are shared with most deep learning models, across many application domains. Indeed, decisions of deep systems are intrinsically hard to explain as the functions these systems represent, mapping from inputs to outputs, are not transparent. 
In particular, although it may be possible for an expert to broadly understand the structure of the model, the parameter values, which have been learned, are yet to be explained.
There are several factors giving rise to interpretability problems for self-driving systems. First, the dataset used for training brings interpretability issues, as a finite training dataset cannot exhaustively cover all possible driving situations. It will likely under- and over-represent some specific cases, and questions such as *Has the model encounter situations like X?* are legitimate. Moreover, datasets contain numerous biases of various nature (omitted variable bias, cause-effect bias, sampling bias), which also gives rise to explainability issues related to fairness.
Second, the trained model, and the mapping function it represents, is poorly understood and is considered as a *black-box*. The model is highly non-linear and does not provide any robustness guarantee as small input changes may dramatically change the output behavior. Explainability issues thus occur regarding the generalizability and robustness aspects: *How will the model behave under these new scenarios?* Third, the learning phase is not perfectly understood. Among other things, there are no guarantees that the model will settle at a minimum point that generalizes well to new situations, and that the model does not underfit on some situations and overfit on others. Besides, the model may learn to ground its decisions on spurious correlations during training instead of leveraging causal signals. We aim at finding answers to questions like *Which factors caused this decision to be taken?*
- From a **driving perspective**, it has been shown that humans tackle this task by solving many intermediate sub-problems, at different levels of hierarchy {%cite michon1984critical %}.
In the effort towards building an autonomous driving system, researchers aim at providing the machine with these intermediate capabilities. Thus, explaining the general behavior of an autonomous vehicle inevitably requires understanding how each of these intermediate steps is carried and how it interacts with others. We can categorize these capabilities into three types:
	- *Perception*: information about the system's understanding of its local environment. This includes the objects that have been recognized and assigned to a semantic label (persons, cars, urban furniture, driveable area, crosswalks, traffic lights), their localization, properties of their motion (velocity, acceleration), intentions of other agents, *etc*.;
	- *Reasoning*: information about how the different components of the perceived environment are organized and assembled by the system. This includes global explanations about the rules that are learned by the model, instance-wise explanation showing which objects are relevant in a given scene, traffic pattern recognition, object occlusion reasoning, *etc.*;
	- *Decision*: information about how the system processes the perceived environment and its associated reasoning to produce a decision. This decision can be a high-level goal stating that the car should turn right, a prediction of the ego vehicle's trajectory, its low-level relative motion or even the raw controls, *etc*.
While the separation between perception, reasoning, and decision is clear in modular driving systems, some recent end-to-end neural networks such as {%cite pilotnet %} blur the lines and perform these simultaneously. Indeed, when an explanation method is developed for a neural driving system, it is often not clear whether it attempts to explain the perception, the reasoning, or the decision step.
Considering the nature of neural networks architecture and training, disentangling perception, reasoning, and decision in neural driving systems constitutes a non-trivial challenge.


## Post-hoc explanation

When a deep learning model in general --- or a self-driving model more specifically --- comes as an opaque black-box as it has not been designed with a specific explainability constraint, *post-hoc* methods have been proposed to gain interpretability from the network processing and its representations.
Post-hoc explanations have the advantage of giving an interpretation to black-box models without conceding any predictive performance.
In this section, we assume that we have a model $f$ which is already trained.
Two main categories of post-hoc methods can be distinguished to explain $f$: *local* methods which explain the prediction of the model for a specific instance, and *global* methods that seek to explain the model in its entirety, *i.e.* by gaining a finer understanding on learned representations and activations. 
We can also make a connection with the system validation literature which aims at automatically making a stratified evaluation of deep models on various scenarios and discovering failure situations.

### Local explanations

Given an input image $x$, a local explanation aims at justifying why the model $f$ gives its specific prediction $y=f(x)$.
We distinguish three types of approaches: saliency methods which determine regions of image $x$ influencing the most the decision,
local approximations which approach the behavior of the black-box model $f$ locally around the instance $x$,
and counterfactual analysis which aims to find the cause in $x$ that made the model predict $f(x)$.

#### Saliency methods
A saliency method aims at explaining which input image's regions influence the most the output of the model.
These methods produce a heat map that highlights regions on which the model relied the most for its decision.
By doing so, these methods mostly explain the perception part of the driving architectures.
The first saliency method to visualize the input influence in the context of autonomous driving has been developed by {%cite visualbackprop %}.
The VisualBackprop method they propose identifies sets of pixels by backpropagating activations from both late layers, which contain relevant information for the task but have a coarse resolution, and early layers which have a finer resolution. The algorithm runs in real-time and can be embedded in a self-driving car. 
This method has been used to explain PilotNet {%cite pilotnet %}, a deep end-to-end control prediction model.
As seen in **Figure 2.**, they qualitatively validate that the model correctly grounds its decisions on lane markings, edges of the road (delimited with grass or parked cars), and surrounding cars. 

![visualbackprop]({{ site.baseurl }}/images/posts/explainable_driving/visualbackprop.png){:width="100%"}
<div class="caption"><b>Figure 2. Example of salient pixels obtained by VisualBackprop. Credits to {%cite explaining_pilotnet %}</b></div>

Recently, {%cite conditionalaffordance %} propose to condition the saliency visualization on a variety of driving affordances. They employ the Grad-CAM saliency technique {%cite gradcam %} on a deep model trained to predict driving affordances on a dataset recorded from the CARLA simulator. They argue that saliency methods are particularly well suited for this type of architecture on the contrary to end-to-end models, as those models map all of the perception (*e.g.* detection of speed limits, red lights, cars, *etc.*.) to a single control output. Instead, in their case, they can analyze the saliency in the input image for each affordance.

> While saliency methods enable visual explanations for deep black-box models, they come with some limitations. First, they are hard to evaluate. For example, human evaluation can be employed, but this comes with the risk of selecting methods which are more *persuasive* than *faithful*. Second, recent work of {%cite sanity_check_saliency %} tend to show that some saliency methods can provide heat maps that are independrnt both of the model and the data. Indeed, they show that some saliency methods behave like edge-detectors even when they are applied to a model with random weights. Lastly, different saliency methods produce different results and it is not obvious to know which one is correct, or better than others. In that respect, a potential research direction is to learn to combine explanations coming from various explanation methods. 

### Global explanations 

### Fine-grain evaluation


## Desigining an explainable driving model

## Use-case: generating natural language explanations

## Conclusion

## References

{% bibliography --cited %}
