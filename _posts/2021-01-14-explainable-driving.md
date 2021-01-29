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


<!-- 
## Post-hoc explanation

When a deep learning model in general --- or a self-driving model more specifically --- comes as an opaque black-box as it has not been designed with a specific explainability constraint, *post-hoc* methods have been proposed to gain interpretability from the network processing and its representations.
Post-hoc explanations have the advantage of giving an interpretation to black-box models without conceding any predictive performance.
In this section, we assume that we have a model $f$ which is already trained.
Two main categories of post-hoc methods can be distinguished to explain $f$: *local* methods which explain the prediction of the model for a specific instance, and *global* methods that seek to explain the model in its entirety, *i.e.* by gaining a finer understanding on learned representations and activations. 

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

While saliency methods enable visual explanations for deep black-box models, they come with some limitations. First, they are hard to evaluate. For example, human evaluation can be employed, but this comes with the risk of selecting methods which are more *persuasive* than *faithful*. Second, recent work of {%cite sanity_check_saliency %} tend to show that some saliency methods can provide heat maps that are independrnt both of the model and the data. Indeed, they show that some saliency methods behave like edge-detectors even when they are applied to a model with random weights. Lastly, different saliency methods produce different results and it is not obvious to know which one is correct, or better than others. In that respect, a potential research direction is to learn to combine explanations coming from various explanation methods. 

#### Local approximations

The idea of a local approximation method is to approach the behavior of the black-box model in the vicinity of the instance to be explained, with a simpler model.
In practice, a separate model, inherently interpretable, is built to act as a proxy for the input/output mapping of the main model locally around the instance.
Such methods include the Local Interpretable Model-agnostic Explanations (LIME) approach {%cite lime %}, which learns an interpretable-by-design input/output mapping, mimicking the behavior of the main model in the neighborhood of an input.
In practice, such mapping can be instantiated by a decision tree or a linear model.
Note that in the case of LIME, the interpretable student model does not necessarily use the raw instance data but rather an interpretable input, such as a binary vector indicating the presence or absence of a superpixel in an image.
The SHapley Additive exPlanations (SHAP) approach {%cite shap %} has later been introduced to generalize LIME, as well as other additive feature attribution methods, and provides more consistent results.

In the autonomous driving literature, we are not aware of any work that aims to explain a self-driving model by locally approximating it with an interpretable model. 
This is likely due to the cost of local approximation strategies, as a set of perturbed inputs are sampled and forwarded in the main model to collect their corresponding labels.
Besides, these methods operate on a simplified input representation instead of the raw input. This interpretable semantic basis should be chosen wisely, as it constitutes the vocabulary that can be used by the explanation system.
Finally, these techniques were shown to be highly sensitive to hyper-parameter choices.

#### Counterfactual explanations

Recently, a lot of attention has been put on counterfactual analysis, a field from the causal inference literature.
A counterfactual analysis aims at finding features $X$ within the input $x$ that *caused* the decision $y=f(x)$ to be taken, by imagining a new input instance $x'$ where $X$ is changed and a different outcome $y'$ is observed. 
The new imaginary scenario $x'$ is called a *counterfactual example* and the different output $y'$ is a contrastive class. 
The new counterfactual example, and the change in $X$ between $x$ and $x'$, constitute *counterfactual explanations*.
In other words, a counterfactual example is a modified version of the input, in a minimal way, that changes the prediction of the model to the predefined output $y'$. 
In an autonomous driving context, it corresponds to questions like ''What should be different in this scene, such that the car would have stopped instead of moving forward?''

Several requirements should be imposed to find counterfactual examples.
First, the prediction $f(x')$ of the counterfactual example must be close to the desired contrastive class $y'$.
Second, the counterfactual change must be *minimal*, *i.e.* the new counterfactual example $x'$ must be as similar as possible to $x$, either by making sparse changes or in the sense of some distance.
Third, the counterfactual change must be *relevant*, *i.e.* new counterfactual instances must be likely in the underlying input data distribution.

Regarding the autonomous driving literature, there only exists a limited number of approaches involving counterfactual interventions.
When the input space has semantic dimensions and can thus be easily manipulated, the causal impace of input factors can be measured by intervening on them (removing or adding).
In {%cite bansal2018chauffeutnet %}, causal factors of the driving model are studied as they test their model under various hand-designed inputs where some objects have been removed.
More recently, {%cite whomakedriversstop %} introduce a causal inference strategy for the identification of ''risk-objects'', *i.e.* objects that have a causal impact on the driver's behavior (see **Figure 3**. In this work, decisions are binary ('go' or 'stop').
The idea is that removing non-causal objects from a scene will not affect the decision.
They propose a training algorithm with interventions, where some objects are randomly removed in scenes where the output is 'go'. At inference, in a sequence where the model predicts 'stop', the risk-object is found as the one which gives the higher score to the 'go' class when removed.

![whomakesdriverstop]({{ site.baseurl }}/images/posts/explainable_driving/whomakesdriverstop.PNG){:width="100%"}
<div class="caption"><b>Figure 3. Counterfactual intervention to measure the causal impact of an input region.</b> Removing a pedestrian induces a change in the driver's decision from 'stop' to 'go', which indicates that the pedestrian is a risk-object. Credits to {%cite whomakedriversstop %}.</div>


We call the reader's attention to the fact that analyzing driving scenes and building driving models using causality is far from trivial as it requires the capacity to *intervene* on the model's inputs. This, in the context of driving, is a highly complex problem to solve for three main reasons. 
- First, the data is composed of high-dimensional tensors of raw sensor inputs (such as the camera or LiDAR signals) and scalar-valued signals that represent the current physical state of the vehicle (velocity, yaw rate, acceleration, *etc*.). Performing controlled interventions requires the capacity to perform realistic alterations of these raw high-dimensional inputs.
Even though some recent works explore realistic alterations of visual content {%cite flow_edge_guided %}, this is yet to be applied in the context of self-driving.
Interestingly, more and more neural driving systems rely on semantic representations. Alterations of the input space are simplified as the realism requirement is removed.
- Second, modified inputs must be coherent and respect the underlying causal structure of the data generation process. As an example, we may be provided with a driving scene that depicts a green light, pedestrians waiting and vehicles passing. A simple intervention consisting of changing the state of the light to red would imply massive changes on the other variables to be \emph{coherent}: pedestrians should start crossing the street and vehicles should stop at the red light. The very recent and promising work of {%cite li2020causal %} tackles the issue of unsupervised *causal discovery* in videos. We believe that the adaptation of this type of approach to real driving data is crucial for the development of causal explainability.
- Finally, we would need to have annotations for these new examples. Indeed, whether we use these altered examples to train a driving model on or to perform exhaustive and controlled evaluations, expert annotations would be required. Considering the nature of the driving data, it might be hard for a human to provide these annotations: they would need to imagine the decision they would have taken (control values or future trajectory) in this newly generated situation. 

### Global explanations 

Global explanations contrast with local explanation methods as they attempt to explain the behavior of a model in general by summarizing the information it contains. 
We distinguish three families of methods to provide global explanations. 
- **Model translation**. These techniques aim at transfering the knowledge contained in the main opaque model into a separate machine learning model that is inherently interpretable. Concretely, this involves training a simple explainable model (such as a decision tree or a rule-based system) to mimic the input-output mapping of the black-box function. 
- **Explaining representations**. The goal of these methods is to provide insights into what is captured by the internal data structures of the model (neurons, vectors, layers, *etc.*), at different granularities.
- **Prototypes**. They are specific data instances that represent well the data. Prototypes are chosen simultaneously to represent the data distribution in a non-redundant way. Global explanations can be obtained by computing and aggregating local explanations of these prototypes.

To the best of our knowledge, global explanation techniques have only been used scarcely in the autonomous driving literature. Please refer to the survey for more details.

## Desigining an explainable driving model

We remark that tools for post-hoc analysis operate on models whose design may have completely ignored the requirement of explainability. 
A good example of such models is PilotNet {%cite pilotnet %} which consists in a convolutional neural network operating over a raw video stream and producing the vehicle controls at every time step. 
Understanding the behavior of this system is only possible through external tools, but cannot be done directly by observing the model itself.

Drawing inspiration from modular systems, recent architectures place a particular emphasis on conveying understandable information about their inner workings, in addition to their performance imperatives.
The modularity of pipelined architectures allows for forensic analysis, by studying the quantities that are transferred between modules (*e.g.* semantic and depth maps, forecasts of surrounding agent's future trajectories, *etc*.). 
These modularity-inspired models exhibit some forms of interpretability, which can be enforced at three different levels in the design of the driving system: input level, intermediate level and output level.

### Input-level explanations
Input-level explanations aim at enlightening the user on which perceptual information is used by the model to take its decisions.
We identified two families of approaches that ease interpretation at the input level: attention-based models and models that use semantic inputs.

#### Attention-based models

Attention mechanisms learn a function that scores different regions of the input depending on whether or not they should be considered in the decision process. 
This scoring is often performed based on some contextual information that helps the model decide which part of the input is relevant to the task at hand. 
{%cite show_attend_tell %} are the first to use an attention mechanism for a computer vision problem, namely, image captioning. Many of such attention models were developed for other applications since then, for example in Visual Question Answering (VQA). Intuitively, the question tells the VQA model where to look to answer the question correctly.
Not only do attention mechanisms boost the performance of machine learning models, but also they provide insights into the inner workings of the system. By visualizing the attention weight associated with each input region, it is possible to know which part of the image was deemed relevant to make the decision.


Attention-based models recently stimulated interest in the self-driving community, as they supposedly give a hint about the internal reasoning of the neural network. 
In {%cite causal_attention %}, an attention mechanism is used to weight each region of an image, using information about previous frames as a context. 
Visual attention can also be used to select objects defined by bounding boxes, as in {%cite deep_object_centric %}. 
In this work, a pre-trained object detector provides regions of interest (RoIs), which are weighted using the global visual context, and aggregated to decide which action to take.
Recently, {%cite attentional_bottleneck %} extended the ChauffeurNet architecture by building a visual attention module that operates on a bird-eye view semantic scene representation. Interestingly, as shown in **Figure 4**, combining visual attention with information bottleneck results in sparser saliency maps, making them more interpretable.

![attentionbottleneck]({{ site.baseurl }}/images/posts/explainable_driving/attentionbottleneck.PNG){:width="100%"}
<div class="caption"><b>Figure 4. Comparison of attention maps from classical visual attention and from attention bottleneck</b> Attention bottleneck seems to provide tighter modes, focused on objects of interest. Credits to {%cite attentional_bottleneck %}.</div>

While these attention mechanisms are often thought to make neural networks more transparent, the recent work of {%cite attention_not_explanation %} mitigates this assumption. Indeed, they show, in the context of natural language, that learned attention weights poorly correlate with multiple measures of feature importance. They even show that it is possible to find adversarial attention weights that keep the same prediction while weighting the input words very differently. All these findings cast some doubts on the faithfulness of explanations based on attention maps.

#### Semantic inputs
Some traditional machine learning models such as linear and logistic regressions, decision trees, or generalized additive models are considered interpretable by practitioners \citep{molnar2019}. 
However these models tend to consider each input dimension as the fundamental unit on which explanations are built. 
Consequently, the input space must have a semantic nature such that explanations become interpretable.
Intuitively, each input dimension should *mean something* independently of other dimensions.
This condition is often met in tasks that deal with categorical or tabular data.
However, in computer vision, when dealing with images, videos, and 3D point clouds, the input space has not an interpretable structure.
Overall, in self-driving systems, the lack of semantic nature of inputs impacts the interpretability of machine learning systems. This observation has motivated researchers to design, build, and use more interpretable input spaces, for example by enforcing more structure or by imposing dimensions to have an underlying high-level meaning. 


Different approaches have been developed to use semantic inputs in a self-driving model, depending on the types of signals at hand. 3D point clouds, provided by LiDAR sensors, can be processed to form a top-view representation of the car surroundings. 

For instance, \citet{lidar_based_driving} propose to flatten the scene along the vertical dimension to form a top-down map, where each pixel in the \bev{} corresponds to a 10cm$\times$10cm square of the environment.
While this input representation provides information about the presence or absence of an obstacle at a certain location, it crucially lacks semantics as it ignores the nature of the obstacles (sidewalks, cars, pedestrians, \textit{etc.}).
% semantic segmentation + combined with the b-e-v 

In DESIRE \citep{desire}, the output of an image semantic segmentation model is fused with 3D points provided by a LiDAR. This gives a top-down view of the scene where static components are associated to a semantic label (*e.g.* road, sidewalk, vegetation), and moving agents are represented along with their tracked present and past positions.
The ChauffeurNet model {%cite bansal2018chauffeutnet %} relies on a similar top-down scene representation, however instead of originating from a LiDAR point cloud, the bird-eye view is obtained from city map data (such as speed limits, lane positions, and crosswalks), traffic light state recognition and detection of surrounding cars. These diverse inputs of the network are gathered into a stack of several images, where each channel corresponds to a rendering of a specific semantic attribute. 
This contrasts with more recent approaches that aggregate all information into a single RGB top-view image, where different semantic components correspond to different color channels {%cite mtp %}

### Intermediate representations

We know from {%cite doescomputervisionmatterforaction %} that sensorimotor agents benefit from predicting explicit intermediate scene representations in parallel to their main task. But besides this objective of model accuracy, predicting scene elements may give some insights about the information contained in the intermediate features.
In {%cite guidedsupervision %}, a neural network learns to predict control outputs from input images. Its training is helped with auxiliary tasks that aim at recognizing high-level action primitives (\eg ''stop'', ''slow down'', ''turn left'', *etc*.) and visual affordances.
In {%cite neural_motion_planner %}, a neural network predicts the future trajectory of the ego-vehicle using a top-view LiDAR point-cloud. In parallel to this main objective, they learn to produce an interpretable intermediate representation composed of 3D detections and future trajectory predictions. Multi-task in self-driving has been explored deeply in {%cite bansal2018chauffeutnet %}, where the authors design a system with ten losses that, besides learning to drive, also forces internal representations to contain information about on-road/off-road zones and future positions of other objects.

Instead of supervising intermediate representations with scene information, other approaches propose to directly use explanation annotations as an auxiliary branch. The driving model is trained to simultaneously decide and explain its behavior.
In the work of {%cite explainable_object_induced %}, the BDD-OIA dataset was introduced, where clips are manually annotated with *authorized* actions and their associated explanation. Action and explanation predictions are expressed as multi-label classification problems, which means that multiple actions and explanations are possible for a single example. 
While this system is not properly a driving model (no control or trajectory prediction here, but only high-level classes such as ''stop'', ''move forward'' or ''turn left''), they were able to increase the performance of action decision making by learning to predict explanations as well. 
In our very recent work {%cite beef %}, we propose to explain the behavior of a driving system by fusing high-level decisions with mid-level perceptual features. 
The fusion is performed using BLOCK, a tensor-based fusion technique designed to model rich interactions between heterogeneous features. 
We trained our model on the HDD dataset {%cite RamanishkaCMS18 %}, where 104 hours of human driving are annotated with a focus on driver behavior. 
In this dataset, video segments are manually labeled with classes that explain stops and deviations (ùe.g.* ''stop for a red light'', deviate for a parked car'', *etc*.).

Visualizing the predictions of an auxiliary head is an interesting way to give the human user an idea of what information is contained in the intermediate representation. 
Indeed, observing that internal representations of the driving network can recognize drivable areas, detect other vehicles, and predict their future positions strengthens the trust one can give to a model.
Yet, it is important to keep in mind that information contained in the representation is not necessarily used by the driving network to make its decision. 
Overall, one should be cautious about such auxiliary predictions to interpret the behavior of the driving model, as the causal link between these auxiliary predictions and the driving output is not enforced.

### Outputs

The task of autonomous driving consists in continuously producing the suitable vehicle commands.
An appealing solution is to train a neural network to directly predict these values, as is done in {%cite pilotnet %}. 
However, this may not be satisfactory in terms of interpretability, as it may fail to communicate to the end-user local objectives that the vehicle is attempting to attain. 
Understanding the intermediate near-future goals chosen by the network provides a form of interpretability that command output neural networks do not have.

To this end, many approaches break the command prediction problem into two sub-problems: trajectory planning and control. In these systems, the neural network predicts the future trajectory that the vehicle should take. 
This predicted trajectory is then passed to a controller that finds the suitable steering, brake and acceleration commands to reach the required position. 
Often in trajectory planning systems based on machine learning, the controller is considered given and optimal, and the focus is completely cast on learning to predict the correct trajectory. 
The predicted trajectory can be visualized in the same coordinate system as the input representation, which helps the human user interpret the prediction.
We split output representations of neural trajectory prediction systems into two categories: analytical representations and spatial grid representations. 
- **Analytical representations.** These are representations of future trajectory as one or more predictions, in the form of points or curves in the 2D space. For instance, {%cite lee2017desire %} propose DESIRE, a model that learns to predict multiple possible future trajectories for each scene agent. More specifically, recurrent models are trained to sample trajectories as sequences of 2D points in a bird-eye view basis, rank them, and refine them according to perceptual features. In MTP {%cite mtp %}, multiple future trajectories are predicted for a single agent using a fully-connected layer, which predicts a vector of size $(2H+1)M$ where $H$ is the temporal horizon and $M$ is the number of trajectories per agent to predict.
CoverNet {%cite phan2020covernet %} poses the trajectory prediction problem as a classification one, where each possible class is a predefined trajectory profile. Thus, by taking the $k$ most probable classes according to the model, they can generate multiple trajectory candidates for the near future. 
- **Spatial grid representations**. In the second family of trajectory prediction systems, the network scores regions of the top-down spatial grid according to their likelihood of hosting the car in the future. One of the main differences with the analytic output family is that virtually any trajectory candidate can be scored according to the model. A downside is that the model does not provide a single clear output trajectory. Finding the *best* prediction requires sampling or greedy search.
In INFER {%cite SrikanthARSMK19 %}, an auto-regressive model is trained to output a likelihood map for the vehicle's next position. At inference time, the most likely next position is chosen and a new prediction is computed from there.
% chauffeurnet
In ChauffeurNet {%cite bansal2018chauffeutnet %}, the network predicts the next vehicle position as a probability distribution over the spatial coordinates, in a semantic segmentation fashion. 
Differently, the Neural Motion Planner {%cite neural_motion_planner %} contains a neural network that outputs a cost volume, which is a spatio-temporal quantity indicating the cost for the vehicle to reach a certain position at a certain moment. Trajectories are sampled from a set of dynamically possible paths (straight lines, circles, and clothoïds) and scored according to the cost volume. Interestingly, the cost volume can be visualized, and thus provides a human-understandable view of what the system considers feasible.

## Use-case: generating natural language explanations

As was stated in the beginning of this post, some of the main requirements of explanations targeted at non-technical human users are *conciseness* and *clarity*. 
To meet these needs, some research efforts have been geared at building models that provide explanations of their behavior in the form of natural language sentences. 

The first attempt to explain the predictions of a deep network with natural language was in the context of image classification, where {%cite generating_visual_explanations %} train a neural network to generate sentence explanations from image features and class label. 
In the context of self-driving, {%cite textual_explanations %} learn to produce textual explanations justifying decisions from a self-driving system. Based on the video material of BDDV {%cite bddv %}, the authors built the BDD-X dataset where dash-cam video clips are annotated with a sentence that describes the driving decision (*e.g.* *the car is deviating from its main track*), and another one that explains why this is happening (*e.g. because the yellow bus has stopped*).
An end-to-end driving system equipped with visual attention is first trained on this dataset to predict the vehicle controls for each frame, and, in a second phase, an attention-based video-to-text captioning model is trained to generate natural language explanations justifying the system's decisions. The attention of the captioning explanation module is constrained to align with the attention of the self-driving system. We show an overview of their system in **Figure 5**. 
We note that this model is akin to a post-hoc explanation system as the explanation-producing network is trained after the driving model.

![textual_explanations]({{ site.baseurl }}/images/posts/explainable_driving/textual_explanations.PNG){:width="100%"}
<div class="caption"><b>Figure 5. Generating natural language explanations.</b> The vehicle controller predicts scalar values for commands, whereas the explanation generator provides a natural language sentence that describes the scene and explains the driving decision. Credits to {%cite textual_explanations %}.</div>
\textbf}. 

We also used the BDD-X dataset in {%cite beef %} when we adapt our explanation classification method to the setup of natural language generation. We also study the impact of the temperature parameter in the decoding softmax, classically used to control the diversity of generated sentences, on the variability of sampled explanations for the same situation. It turns out that for reasonably low values of the temperature, the model justifies a driving situation with semantically consistent sentences. These explanations differ from each other only *syntactically* and with respect to their *completeness* (some explanations are more exhaustive and precise than others), but not *semantically*. Looking at the example below in **Figure 6**, we see that all the explanations are correct as they correspond to the depicted scene, but the level of detail they convey may be different.

![beef_temp]({{ site.baseurl }}/images/posts/explainable_driving/beef_temp.PNG){:width="60%"}
<div class="caption"><b>Figure 6. Various samples of generated explanations.</b> GT stands for the the ground-truth (human gold label). Other lines are justifications generated by BEEF, with different runs obtained with various decoding temperature T: T=0 corresponds to the greedy decoding and the lines with T=0.3 correspond to random decoding with a temperature of 0.3. Credits to {%cite beef %}</div>


Using annotations of explanations to supervise the training of a neural network seems natural and effective. Yet, this practice involves some strong assumptions and the generated explanations may be limited in their faithfulness.
From a data point-of-view, as was noted in {%cite textual_explanations %}, acquiring the annotations for explanations can be quite difficult: ground-truth explanations are often post-hoc rationales generated by an external observer of the scene and not by the person who took the action. Even more disturbing: explanation annotations correspond to the reasons why a *person* made an action, and using these annotations to explain the behavior of a *machine learning model* is an extrapolation that should be made carefully. 

Moreover, evaluating natural language explanations constitutes a challenge per se.
Most approaches evaluate generated natural language explanations based on human ratings or by comparing them to ground-truth explanation, given by humans (using automated metrics like BLEU, METEOR, or CIDEr scores).
As argued by {%cite leakage_adjusted_simulatability %} and {%cite GilpinBYBSK18 %}, the evaluation of natural language explanations is delicate and automated metric and human evaluations are not satisfying as they cannot guarantee that the explanation is faithful to the model's decision-making process.
These metrics rather evaluate the plausibility of the explanation regarding human evaluations.
Overall, this evaluation protocol encourages explanations that match human expectation and it is prone to produce *persuasive explanations*, *i.e.* explanations that satisfy the human users regardless of their faithfulness to the model processing.
Potential solutions to tackle the problem of persuasive explanations can be inspired by recent works in Natural Language Processing, where several works have recently advocated for evaluating the *faithfulness* of explanations rather than their *plausibility*. 
This is the case of {%cite leakage_adjusted_simulatability %}, where authors propose the leakage-adjusted simulatability (LAS) metric, which is based on the idea that the explanation should be helpful to predict the model's output without leaking direct information about the output.


## Conclusion

Despite their differences, all the methods reviewed in this survey share the objective of exposing the *causes* behind model decisions.
Yet, only very few works directly borrow tools and concepts from the field of causal modeling {%cite pearl_causality %}. 
Taken apart methods that attempt to formulate counterfactual explanations, applications of causal inference methods to explain self-driving models are rare.
Being able to infer the causal structure in driving data has strong implications in explainability. It is also a very promising way towards more robust neural driving models. 
As was stated in {%cite causal_confusion %}, a driving policy must identify and rely solely on true causes of expert decisions if we want it to be robust enough to be deployed.
Building neural driving models that take the right decisions for the right identified reasons would yield inherently robust, explainable, and faithful systems.

 -->
## References

{% bibliography --cited %}
