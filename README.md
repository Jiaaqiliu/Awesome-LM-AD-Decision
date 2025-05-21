# **Awesome LM for Autonomous Driving Decision-Making**

A comprehensive list of awesome research, resources, and tools for leveraging Large Language Models (LLMs), Vision-Language Models (VLMs), and Vision-Language-Action (VLA) models in autonomous driving decision-making and motion planning.
Contributions are welcome! 

## Table of Contents

- [Survey papers](#survey-papers)
- [Research Papers](#research-papers) 
    - [Categorization by Model Type](#categorization-by-model-type)
        - [LLM-based Approaches](#llm-based-approaches)
        - [VLM-based Approaches](#vlm-based-approaches)
        - [VLA-based Approaches](#vla-based-approaches)
    - [Categorization by Research Direction](#categorization-by-research-direction) 
        - [End-to-End Driving Models](#end-to-end-driving-models)
        - [Interpretability and Explainable AI (XAI)](#interpretability-and-explainable-ai-xai)
        - [Safety-Critical Decision-Making & Long-Tail Scenarios](#safety-critical-decision-making--long-tail-scenarios) 
        - [Reinforcement Learning for Decision-Making](#reinforcement-learning-for-decision-making)
        - [World Models for Prediction and Planning](#world-models-for-prediction-and-planning)
        - [Hierarchical Planning and Control](#hierarchical-planning-and-control)
    - [Categorization by Application Field in Decision-Making](#categorization-by-application-field-in-decision-making) 
        - [Perception-Informed Decision-Making](#perception-informed-decision-making) 
        - [Behavioral Planning & Prediction](#behavioral-planning--prediction) 
        - [Motion Planning & Trajectory Generation](#motion-planning--trajectory-generation) 
        - [Direct Control Signal Generation](#direct-control-signal-generation)
        - [Human-AI Interaction & Command Understanding](#human-ai-interaction--command-understanding)
    - [Categorization by Technical Route](#categorization-by-technical-route) 
        - [Transformer Architectures & Variants](#transformer-architectures--variants) 
        - [Multimodal Fusion Techniques](#multimodal-fusion-techniques) 
        - [Prompt Engineering](#prompt-engineering-eg-chain-of-thought) 
        - [Knowledge Distillation & Transfer Learning](#knowledge-distillation--transfer-learning) 
- [Datasets and Benchmarks](#datasets-and-benchmarks) 
- [Other Awesome Lists](#other-awesome-lists)



## **Survey papers**

- End-to-end Autonomous Driving: Challenges and Frontiers [[paper](https://ieeexplore.ieee.org/abstract/document/10614862)][[project](https://github.com/OpenDriveLab/End-to-end-Autonomous-Driving)]![](https://img.shields.io/github/stars/OpenDriveLab/End-to-end-Autonomous-Driving.svg?style=social&label=Star&maxAge=2592000)
- A Superalignment Framework in Autonomous Driving with Large Language Models
- Foundation Models in Robotics: Applications, Challenges, and the Future
- Toward General-Purpose Robots via Foundation Models: A Survey and Meta-Analysis
- A Survey on Vision-Language-Action Models for Embodied AI
- Visual Large Language Models for Generalized and Specialized Applications 
- On the Prospects of Incorporating Large Language Models (LLMs) in Automated Planning and Scheduling
- Foundation Models for Decision Making: Problems, Methods, and Opportunities

## **Research Papers**


### **Categorization by Model Type**

This section further elaborates on papers based on the primary type of foundation model employed for decision-making.


#### **LLM-based Approaches**

LLMs are primarily leveraged for their reasoning, planning, and natural language understanding/generation capabilities to guide autonomous driving decisions. A dominant trend in this area is the hybridization or agentic use of LLMs. Pure LLM-driven control is rare due to challenges in real-time performance, safety assurance, and precise numerical output. Instead, LLMs often function at a strategic or tactical level, acting as a "supervisor," "planner," or "reasoner" that guides more traditional or specialized modules like DRL agents or MPC controllers. This hierarchical system leverages the LLM's strengths in high-level reasoning and contextual understanding while offloading operational, real-time aspects to other components. This approach aims to augment specific parts of the AD stack, particularly those requiring human-like commonsense, reasoning about novel situations, or providing interpretable justifications for actions.



* **TeLL-Drive** : This work proposes a hybrid framework where a "teacher" LLM guides an attention-based "student" Deep Reinforcement Learning (DRL) policy. The LLM utilizes Chain-of-Thought (CoT) reasoning, incorporates risk metrics, and retrieves historical scenarios to produce high-level driving strategies. This approach aims to improve the DRL agent's sample complexity and robustness while ensuring real-time feasibility, a common challenge for LLMs when used in isolation for decision-making.
* **LanguageMPC** : This system employs an LLM as a high-level decision-making component, particularly for complex AD scenarios that demand human commonsense understanding. The LLM processes environmental data through scenario encoding, provides action guidance, and adjusts confidence levels. These high-level decisions are then translated into precise parameters for a low-level Model Predictive Controller (MPC), thereby enhancing interpretability and enabling the system to handle complex maneuvers, including multi-vehicle coordination.
* **Agent-Driver** : This framework positions an LLM as a cognitive agent. The agent has access to a versatile tool library (for perception and prediction tasks), a cognitive memory storing commonsense knowledge and past driving experiences, and a reasoning engine. The reasoning engine is capable of chain-of-thought reasoning, task planning, motion planning, and self-reflection, showcasing a more integrated and sophisticated agentic approach to autonomous driving.
* **LLM for Safety Perspective (Empowering Autonomous Driving with Large Language Models: A Safety Perspective)** : This research explores the integration of LLMs as intelligent decision-makers within the behavioral planning module of AD systems. A key feature is the augmentation of LLMs with a safety verifier shield, which facilitates contextual safety learning. The paper presents studies on an adaptive LLM-conditioned MPC and an LLM-enabled interactive behavior planning scheme using a state machine, demonstrating improved safety metrics.
* **Traffic Regulation Retrieval Agent for Interpretable Autonomous Driving Decision-Making** : This framework introduces an interpretable decision-maker that leverages a Traffic Regulation Retrieval (TRR) Agent, built upon Retrieval-Augmented Generation (RAG). This agent automatically retrieves relevant traffic rules and guidelines from extensive documents. An LLM-powered reasoning module then interprets these rules, differentiates between mandatory regulations and safety guidelines, and assesses actions for legal compliance and safety, enhancing transparency.
* **DiLu (A Knowledge-Driven Approach to Autonomous Driving with Large Language Models)** : DiLu proposes a knowledge-driven framework for autonomous driving that combines Reasoning and Reflection modules within an LLM. This enables the system to make decisions based on common-sense knowledge and to continuously evolve its understanding and strategies through experience.
* **LLM-Planners (General)** : Broader research into LLMs for planning tasks, such as the LLM-Planner for few-shot grounded planning for embodied agents , provides foundational concepts and techniques that can be adapted for AD planning. These works often explore how LLMs can decompose complex tasks and generate sequences of actions.


#### **VLM-based Approaches**

VLMs bring visual understanding to the decision-making process, allowing for richer interpretations of the driving scene and enabling actions based on both visual percepts and linguistic instructions or reasoning. A key challenge for VLMs in AD decision-making is bridging the gap between their often 2D-centric visual-linguistic understanding and the precise, 3D spatio-temporal reasoning essential for safe driving. Many current VLMs are adapted from models pre-trained on large, static 2D image-text datasets , and they can struggle with the dynamic, three-dimensional nature of real-world driving scenarios. This means that while they might excel at describing a scene, their practical performance in actual driving tasks can be concerning. Effective VLMs for AD decision-making will likely need to incorporate stronger 3D visual backbones, improved mechanisms for temporal modeling beyond simple frame concatenation, and potentially integrate more structured environmental representations like Bird's-Eye-View (BEV) maps or scene graphs directly into their reasoning processes.



* **TS-VLM** : This work introduces a lightweight VLM designed for efficient multi-view reasoning in autonomous driving. It features a novel Text-Guided SoftSort Pooling (TGSSP) module that dynamically ranks and fuses visual features from multiple camera views based on the semantics of input queries. This query-aware aggregation aims to improve contextual accuracy and reduce computational overhead, making it more practical for real-time deployment.
* **LightEMMA** : LightEMMA serves as a lightweight, end-to-end multimodal framework and benchmark for evaluating various state-of-the-art commercial and open-source VLMs (such as GPT-4o, Gemini, Claude) in autonomous driving planning tasks. It uses consistent prompting strategies, including Chain-of-Thought (CoT), for structured reasoning and control action prediction on datasets like nuScenes. The findings indicate that despite strong scenario interpretation capabilities, the practical performance of current VLMs in AD tasks remains a concern.
* **DriveGPT4** : This Multimodal Large Language Model (MLLM) is designed for interpretable end-to-end autonomous driving. It processes multi-frame video inputs and textual queries to interpret vehicle actions, provide relevant reasoning, and predict low-level control signals. A bespoke visual instruction tuning dataset aids its capabilities.
* **ADAPT** : While primarily a transformer architecture, ADAPT functions similarly to a VLM by generating natural language narrations and reasoning for driving actions based on video input. It jointly trains the driving captioning task and the vehicular control prediction task, enhancing interpretability in decision-making.
* **LeapAD** : This system uses a VLM for scene understanding, specifically to provide descriptions of critical objects that may influence driving decisions. This visual-linguistic understanding then feeds into a dual-process decision-making module composed of an Analytic LLM and a Heuristic lightweight language model.
* **AlphaDrive** : AlphaDrive is a VLM tailored for high-level planning in autonomous driving. It integrates a Group Relative Policy Optimization (GRPO)-based reinforcement learning strategy with a two-stage reasoning training approach (Supervised Fine-Tuning followed by RL) to boost planning performance and training efficiency.
* **DriveVLM** : This system leverages VLMs for enhanced scene understanding and planning capabilities. It also proposes DriveVLM-Dual, a hybrid system that combines the strengths of DriveVLM with traditional AD pipelines to address VLM limitations in spatial reasoning and computational requirements, particularly for long-tail critical objects.
* **LingoQA** : This project introduces a benchmark and a large dataset (419.9k QA pairs from 28K unique video scenarios) for video question answering specifically in the autonomous driving domain. It focuses on evaluating a VLM's ability to perform reasoning, justify actions, and describe scenes, and proposes the Lingo-Judge metric for evaluation.
* **VLM-E2E** : This framework aims to enhance end-to-end autonomous driving by using VLMs to provide driver attentional cues. It integrates textual representations into Bird's-Eye-View (BEV) features for semantic supervision, enabling the model to learn richer feature representations that capture driver attentional semantics. It also introduces a BEV-Text learnable weighted fusion strategy.
* **VLM-AD** : This method positions VLMs as "teachers" to generate reasoning-based text annotations and structured action labels. These annotations serve as supplementary supervisory signals for training end-to-end AD models, aiming to improve their understanding beyond simple trajectory labels without requiring the VLM at inference time.
* **VL-SAM** : This training-free framework combines a VLM (for generalized object recognition, e.g., recognizing rare objects in AD scenarios) with the Segment-Anything Model (SAM, for generalized object localization). It uses attention maps from the VLM as prompts for SAM to address open-ended object detection and segmentation, which is crucial for robust perception feeding into decision-making systems.


#### **VLA-based Approaches**

VLAs aim to create more generalist agents that can perceive, reason, and act, often in an end-to-end fashion. For autonomous driving, this means models that can take raw sensor data and high-level goals to produce driving actions. While VLAs offer the promise of true end-to-end decision-making by unifying perception, reasoning, and action generation , their application in safety-critical autonomous driving faces a significant hurdle: ensuring the reliability and verifiability of actions generated by these complex, often black-box, generative models. The potential for "hallucinated" or unexpected outputs from generative models is a recurring concern. A major research direction for VLAs in AD will involve developing methods for safety validation, uncertainty quantification, and robust fallback mechanisms. This might include hybrid approaches where VLA outputs are monitored or constrained by traditional safety layers, or novel training paradigms that explicitly optimize for safety and predictability.



* **OpenDriveVLA** : This is an end-to-end VLA model specifically designed for autonomous driving. It generates reliable driving actions conditioned on 3D environmental perception, ego vehicle states, and driver commands. Key methodological contributions include a hierarchical vision-language alignment process to bridge the modality gap between driving visual representations and language embeddings, and an autoregressive agent-env-ego interaction process to ensure spatially and behaviorally informed trajectory planning.

### **Categorization by Research Direction**

This section groups papers based on overarching research themes and objectives within AD decision-making.


#### **End-to-End Driving Models**

These models aim to learn a direct mapping from sensor inputs to driving actions or high-level plans, often minimizing handcrafted intermediate representations. The pursuit of end-to-end (E2E) models in autonomous driving is driven by the ambition to reduce error propagation inherent in modular pipelines and to potentially uncover novel, more effective driving strategies that might not emerge from separately optimized components. However, the "black box" nature and significant data requirements of traditional E2E deep learning models have been persistent challenges. The integration of LLMs, VLMs, and VLAs into E2E frameworks represents an effort to mitigate these issues by infusing these models with enhanced reasoning capabilities, better generalization from pre-training, and avenues for interpretability. This suggests a future where E2E AD systems are not purely opaque mappings but incorporate a semantic layer or reasoning backbone provided by foundation models, thus addressing key criticisms of earlier E2E approaches.



* **LightEMMA** : This framework is specifically designed for evaluating various VLMs in an end-to-end fashion for autonomous driving planning tasks. It provides an open-source baseline workflow for integrating VLMs into E2E planning, enabling rapid prototyping.
* **DriveGPT4** : DriveGPT4 is presented as an interpretable end-to-end autonomous driving system based on LLMs. It processes multi-frame video inputs and textual queries, predicts low-level vehicle control signals, and offers reasoning for its actions.
* **OpenDriveVLA** : This VLA model is explicitly designed for end-to-end autonomous driving. It generates reliable driving trajectories conditioned on multimodal inputs including 3D environmental perception, ego vehicle state, and driver commands.
* **ADAPT** : ADAPT proposes an end-to-end transformer-based architecture that jointly trains a driving captioning task and a vehicular control prediction task through a shared video representation, aiming for user-friendly narration and reasoning.
* **LMDrive** : This work focuses on closed-loop end-to-end driving specifically with large language models, indicating a direct application of LLMs in the E2E driving pipeline.
* **VLM-E2E** : This research aims to enhance end-to-end autonomous driving by using VLMs to provide attentional cues and fusing multimodal information (BEV and text features) for semantic supervision.
* **VLM-AD** : This method leverages VLMs as teachers to provide reasoning-based text annotations, which serve as supplementary supervisory signals to train end-to-end AD pipelines, extending beyond standard trajectory labels.
* **GenAD** : GenAD models autonomous driving as a trajectory generation problem, adopting an instance-centric scene tokenizer and a variational autoencoder for trajectory prior modeling in an E2E setup.



#### **Interpretability and Explainable AI (XAI)**

Focuses on making the decision-making processes of AD systems transparent and understandable to humans. The integration of LLMs and VLMs is pushing XAI in autonomous driving beyond simple attention maps or feature visualizations towards generating natural language explanations and justifications that are genuinely comprehensible to human users, including passengers and regulators. This is crucial for building public trust, facilitating regulatory approval, and enabling more effective human-AI collaboration in the driving context. The challenge, however, lies in ensuring that these generated explanations are faithful to the model's actual decision-making process and are not merely plausible-sounding rationalizations generated post-hoc. Future work will need to concentrate on methods that tightly couple the reasoning and explanation generation with the core decision logic of the AD system.



* **LanguageMPC** : The use of LLM-generated high-level decisions is explicitly stated to improve interpretability in complex autonomous driving scenarios. The system aims to make the "thinking process" visible.
* **LightEMMA** : This VLM framework employs Chain-of-Thought (CoT) prompting. CoT is used to enhance interpretability and facilitate structured reasoning within the VLM-based driving agents, allowing the model to output its reasoning steps.
* **DriveGPT4** : A primary goal of DriveGPT4 is to develop an interpretable end-to-end autonomous driving solution. The MLLM is designed to interpret vehicle actions, offer pertinent reasoning, and address user queries, thereby making the system's behavior understandable.
* **ADAPT** : This framework provides user-friendly natural language narrations and reasoning for each decision-making step of autonomous vehicular control and action. For example, it can output "[Action narration:] the car pulls over to the right side of the road, because the car is parking".
* **LingoQA** : By benchmarking video question answering, LingoQA facilitates the development of models that can justify actions and describe scenes in natural language, directly contributing to the explainability of driving decisions.
* **Traffic Regulation Retrieval Agent** : The reasoning module in this framework is explicitly designed to be interpretable, enhancing transparency in how traffic rules are identified, interpreted, and applied to driving decisions.
* **General XAI in AVs** : These resources provide a broader context on XAI in autonomous vehicles. They emphasize that XAI serves to bridge complex technological capabilities with human understanding, addressing safety assurance, regulatory compliance, and public trust. XAI can provide real-time justifications for actions (e.g., sudden braking) and post-hoc explanations (e.g., visual heat maps, natural language descriptions).
* **RAG-Driver** : This work aims to provide generalisable driving explanations by employing retrieval-augmented in-context learning within Multi-Modal Large Language Models.

#### **Safety-Critical Decision-Making & Long-Tail Scenarios**

Addresses the paramount challenge of ensuring safety, especially in rare, unforeseen (long-tail) situations where traditional, purely data-driven systems often falter due to lack of representative data. Effectively handling these scenarios requires more than just scaling up models; it demands robust reasoning, the integration of explicit and implicit knowledge (including safety rules and commonsense), and rigorous validation methodologies. The integration of LLMs and VLMs offers a promising avenue by leveraging their potential for abstract reasoning and broad knowledge. However, the inherent risk of these models generating incorrect or "hallucinated" outputs in critical situations necessitates a cautious approach. Future progress in this area will likely depend on hybrid architectures that combine the generalization capabilities of foundation models with explicit safety layers or verifiers, methods for effectively injecting structured safety knowledge (like traffic laws or physical constraints) into the decision-making loop, and the development of advanced simulation and testing protocols specifically designed to probe behavior in diverse long-tail scenarios and rigorously evaluate safety.



* **LanguageMPC** : Aims to improve generalization to rare events by leveraging the commonsense reasoning capabilities of LLMs, which is crucial for safety in unexpected situations.
* **OpenDriveVLA** : This VLA model specifically targets the challenges of limited generalization to long-tail scenarios and insufficient understanding of high-level semantics within complex driving scenes, which are critical for safe decision-making.
* **Survey on GenAI for AD (Generative AI for Autonomous Driving: Frontiers and Opportunities)** : This survey identifies comprehensive generalization across rare cases and the development of robust evaluation and safety checks as key obstacles and future opportunities for GenAI in autonomous driving.
* **Empowering Autonomous Driving with Large Language Models: A Safety Perspective** : This work directly focuses on enhancing safety by proposing methodologies that employ LLMs as intelligent decision-makers in behavioral planning, augmented with a safety verifier shield for contextual safety learning.
* **TOKEN (Tokenize the World into Object-level Knowledge)** : This MM-LLM is designed to address long-tail events by tokenizing the world into object-level knowledge, enabling better utilization of an LLM's reasoning capabilities for enhanced autonomous vehicle planning in such scenarios.
* **VLM-AD (Leveraging Vision-Language Models as Teachers for End-to-End Autonomous Driving)** : This method addresses the limitations of E2E models in handling diverse real-world scenarios by using VLMs as teachers to provide reasoning-based supervision, which can help in understanding and reacting to less common situations.



#### **Reinforcement Learning for Decision-Making**

Utilizes Reinforcement Learning (RL) techniques, often guided or enhanced by foundation models (LLMs/VLMs), to learn optimal driving policies through interaction with simulated or real-world environments. The synergy between foundation models and RL represents a powerful emerging trend in autonomous driving. Foundation models can address key RL challenges, such as high sample complexity and difficult reward design, by providing high-level guidance, superior state representations, or even by directly shaping the reward function itself. This combination can lead to more data-efficient learning of complex driving behaviors, improved generalization to novel scenarios by leveraging the pre-trained knowledge embedded in foundation models, and more interpretable reward structures, especially if derived from linguistic goals. The primary research focus in this area will likely be on optimizing the structure of this synergy—for example, determining whether the LLM should act as a planner for an RL agent, a reward shaper, or if end-to-end RL fine-tuning of a VLM is the most effective approach.



* **TeLL-Drive** : This framework explicitly combines a "teacher" LLM with a "student" Deep Reinforcement Learning (DRL) agent. The LLM, using Chain-of-Thought reasoning and incorporating risk metrics and historical data, guides the DRL policy. This guidance aims to accelerate policy convergence and boost robustness across diverse driving conditions, mitigating DRL's high sample complexity and the LLM's real-time decision-making challenges.
* **AlphaDrive** : AlphaDrive proposes a VLM-based reinforcement learning and reasoning framework specifically for autonomous driving planning. It introduces four Group Relative Policy Optimization (GRPO)-based RL rewards tailored for planning (planning accuracy, action-weighted, planning diversity, planning format) and employs a two-stage planning reasoning training strategy that combines Supervised Fine-Tuning (SFT) with RL. This approach is shown to significantly improve planning performance and training efficiency.
* **LORD (Large Models Based Opposite Reward Design)** : This work introduces a novel approach to reward design in RL for autonomous driving. Instead of defining desired linguistic goals (e.g., "drive safely"), which can be ambiguous, LORD leverages large pretrained models (LLMs/VLMs) to focus on concrete *undesired* linguistic goals (e.g., "collision"). This allows for more efficient use of these models as zero-shot reward models, aiming for safer and enhanced autonomous driving with improved generalization.
* **NaVILA** : While the high-level decision-making in NaVILA is handled by a VLA generating linguistic commands, the low-level locomotion policy responsible for executing these commands is trained using RL. This demonstrates a hierarchical approach where RL handles the dynamic execution based on VLA guidance.
* **VLM RL for general decision-making (Fine-tuning Vision-Language Models with Task Rewards for Multi-Step Goal-Directed Decision Making)** : This research explores fine-tuning VLMs with RL for general multi-step goal-directed tasks. The VLM generates Chain-of-Thought reasoning leading to a text-based action, which is then parsed and executed in an interactive environment to obtain task rewards for RL-based fine-tuning. This general methodology is highly relevant for training decision-making agents in autonomous driving.


#### **World Models for Prediction and Planning**

Involves building internal representations of the environment and its dynamics to predict future states and plan actions accordingly. Foundation models, particularly generative models like Diffusion Models, GANs, LLMs, and VLMs, are becoming key enablers for constructing more powerful and versatile world models for autonomous driving. These advanced world models are evolving beyond simple state prediction to encompass rich semantic understanding, the generation of diverse future scenarios (including long-tail events), and even interaction with language-based instructions or goals. This fusion of generative world models with the reasoning capabilities of LLMs/VLMs can lead to AD systems that perform sophisticated "what-if" analyses, anticipate a broader range of future possibilities, and plan more robustly by "imagining" the consequences of actions within a semantically rich, simulated future. This also has profound implications for creating highly realistic and controllable simulation environments for training and testing AD systems.



* **General Mentions of World Models in AD** : Numerous sources highlight the increasing importance of world models for perception, prediction, and planning in autonomous driving. Workshops and challenges, such as the CVPR 2024 and 2025 OpenDriveLab Tracks on Predictive World Models, underscore this trend. These models are seen as fundamental for enabling capabilities like decision-making, planning, and counterfactual analysis.
* **3D-VLA** : This framework explicitly incorporates a generative world model within its 3D vision-language-action architecture. It allows the model to "imagine" future scenarios by predicting goal images and point clouds, which then guide action planning. The model is built on a 3D-LLM and uses interaction tokens to engage with the environment.
* **DriveDreamer / DriveDreamer-2** : DriveDreamer utilizes a powerful diffusion model to construct a comprehensive representation of the driving environment. It can generate future driving videos and driving policies, effectively acting as a multimodal world model. DriveDreamer-2 enhances this by incorporating an LLM to generate user-defined driving videos with improved temporal and spatial coherence.
* **GAIA-1** : Developed by Wayve, GAIA-1 is a generative world model that leverages video, text, and action inputs to generate realistic driving scenarios. It serves as a valuable neural simulator for autonomous driving.
* **Drive-WM (Driving into the Future: Multiview Visual Forecasting and Planning with World Model for Autonomous Driving)** : This is a multiview world model capable of generating high-quality, controllable, and consistent multiview videos in autonomous driving scenes. It also explores applications in end-to-end planning.
* **TrafficBots** : This research aims towards developing world models specifically for autonomous driving simulation and motion prediction.
* **UniWorld** : Focuses on autonomous driving pre-training via world models, suggesting that learning a world model can provide a foundational understanding for downstream AD tasks.
* **Occ-LLM (Enhancing Autonomous Driving with Occupancy-Based Large Language Models)** : While not explicitly a "world model" in the generative sense of predicting future full scenes, Occ-LLM uses occupancy representations with LLMs, which is a form of modeling the current state of the world for decision-making.
* **Sora (Video generation models as world simulators)** : OpenAI's Sora, while a general video generation model, is highlighted for its potential as a world simulator, which has implications for generating dynamic driving scenarios.


#### **Hierarchical Planning and Control**

Decomposes the complex driving task into multiple levels of abstraction, often with foundation models handling higher-level reasoning and planning, and other specialized modules executing lower-level control actions. This approach mirrors human cognitive strategies where high-level goals are broken down into manageable sub-tasks. In autonomous driving, this means LLMs or VLMs might determine a strategic maneuver (e.g., "prepare to change lanes and overtake"), which is then translated into a sequence of tactical actions (e.g., check mirrors, signal, adjust speed, steer) executed by a more traditional planner or controller. This layered approach allows for leveraging the strengths of foundation models in complex reasoning and language understanding, while relying on established methods for precise, real-time vehicle control, potentially offering a more robust and interpretable path to autonomy.



* **OpenDriveVLA** : This VLA model employs a hierarchical vision-language alignment process. While aiming for end-to-end action generation, its internal mechanisms likely involve different levels of representation and processing for perception, reasoning, and action generation, contributing to spatially and behaviorally informed trajectory planning.
* **NaVILA** : This is a prime example of hierarchical control in a VLA framework. The high-level VLM processes visual input and natural language instructions to generate mid-level actions expressed in natural language (e.g., "turn right 30 degrees," "move forward 75cm"). These linguistic commands are then interpreted and executed by a separate low-level visual locomotion policy trained with reinforcement learning. This decouples complex reasoning from real-time motor control.
* **LanguageMPC** : This system uses an LLM for high-level decision-making (scenario encoding, action guidance). These high-level textual decisions are then translated into precise mathematical representations and parameters that guide a low-level Model Predictive Controller (MPC) responsible for the actual driving commands. This clearly separates strategic decision-making from operational control.
* **TeLL-Drive** : Here, a "teacher" LLM produces high-level driving strategies through chain-of-thought reasoning. These strategies then guide an attention-based "student" DRL policy, which handles the final decision-making and action execution. This represents a hierarchical guidance mechanism.
* **DriveVLM** : DriveVLM integrates reasoning modules for scene description, scene analysis, and hierarchical planning. The DriveVLM-Dual system further exemplifies this by using low-frequency motion plans from the VLM as initial plans for a faster, traditional refining planner.
* **LeapAD** : This system incorporates a dual-process decision-making module. The Analytic Process (System-II, using an LLM) performs thorough analysis and reasoning, accumulating experience. This experience is then transferred to a lightweight Heuristic Process (System-I) for swift, empirical decision-making. This can be seen as a cognitive hierarchy.
* **Hierarchical Framework for Mixing Driving Data** : While focused on data compatibility for trajectory prediction, this work proposes a hierarchical framework, suggesting that different levels of processing or adaptation might be needed when dealing with complex data sources, which can inform hierarchical planning approaches.
* **Hierarchical Planning Engine (General LLM Agent Concept)** : This describes a general concept for LLM agents where a high-level goal is decomposed into a structured, actionable plan (Phases -> Tasks -> Steps), which is a core idea in hierarchical planning.

### **Categorization by Application Field in Decision-Making**

This section organizes papers based on the specific aspect of the autonomous driving decision-making pipeline they primarily address.


#### **Perception-Informed Decision-Making**

These works focus on how enhanced perception, often through LLMs/VLMs, directly informs or enables better downstream decision-making. This involves not just detecting objects but understanding their context, relationships, and potential impact on driving strategy.



* **TS-VLM** : Improves multi-view driving reasoning by dynamically fusing visual features based on text queries. This enhanced scene understanding directly supports more informed decision-making by providing better contextual accuracy from multiple viewpoints.
* **OpenDriveVLA** : Conditions driving actions on 3D environmental perception, ego vehicle states, and driver commands. The hierarchical vision-language alignment projects 2D and 3D visual tokens into a unified semantic space, enabling perception to directly guide trajectory generation.
* **DriveGPT4** : Processes multi-frame video inputs to interpret vehicle actions and offer reasoning. The decision to predict control signals is directly informed by its multimodal understanding of the visual scene and textual queries.
* **LeapAD** : The VLM component is crucial for scene understanding, providing descriptions of critical objects that influence driving decisions. This perception output is the direct input to the dual-process decision-making module.
* **DriveVLM** : Leverages VLMs for enhanced scene understanding (scene description, scene analysis) which then feeds into its hierarchical planning modules. The perception of long-tail critical objects is a key focus.
* **VL-SAM** : Combines VLM recognition with SAM segmentation for open-ended object detection. While primarily a perception method, accurate detection and localization of all objects, including rare ones, is fundamental for safe decision-making.
* **VLM-E2E** : Integrates textual representations (driver attentional cues from VLMs) into Bird's-Eye-View (BEV) features for semantic supervision, enabling the model to learn richer feature representations that explicitly capture driver's attentional semantics, directly impacting driving decisions.
* **HiLM-D** : Focuses on high-resolution understanding in MLLMs for AD, specifically for identifying, explaining, and localizing risk objects (ROLISP task), which is a critical perceptual input for safe decision-making.
* **Talk2BEV** : Provides a language-enhanced interface for BEV maps, allowing natural language queries to interpret complex driving scenes represented in BEV, thus informing situational awareness for decision-making.

#### **Behavioral Planning & Prediction**

Concerns predicting the future behavior of other road users (vehicles, pedestrians, cyclists) and planning the ego-vehicle's behavior in response, often involving understanding intentions and social interactions.



* **LanguageMPC** : The LLM performs scenario encoding, which includes predicting future trajectories of other vehicles and selecting the most likely one. This predictive capability informs its high-level action guidance for the ego vehicle.
* **OpenDriveVLA** : Models dynamic relationships between the ego vehicle, surrounding agents, and static road elements through an autoregressive agent-env-ego interaction process. This explicit modeling of interactions is key for behavioral planning and prediction.
* **AlphaDrive** : Tailored for high-level planning in autonomous driving, which inherently involves deciding on driving behaviors (e.g., lane changes, yielding) based on the current scene and predicted future states. The emergent multimodal planning capabilities also hint at understanding complex interactions.
* **DriveVLM** : Includes modules for scene analysis that analyze possible intent-level behavior of critical objects, feeding into its hierarchical planning. This is directly related to predicting other agents' behaviors.
* **Empowering AD with LLMs: A Safety Perspective** : Focuses on LLMs as intelligent decision-makers in behavioral planning, augmented with safety verifiers. This includes an LLM-enabled interactive behavior planning scheme.
* **Agent-Driver** : The LLM agent performs task planning and motion planning based on perceived and predicted states of the environment, including interactions with other agents.
* **LC-LLM (Explainable Lane-Change Intention and Trajectory Predictions with LLMs)** : Specifically uses LLMs for predicting lane-change intentions and trajectories, providing explainable predictions for this critical driving behavior.
* **LLMs Powered Context-aware Motion Prediction** : Leverages GPT-4V to comprehend complex traffic scenarios and combines this contextual information with traditional motion prediction models (like MTR) to improve behavioral prediction.
* **GPT-4V for Pedestrian Behavior Prediction** : Evaluates GPT-4V's capabilities for predicting pedestrian behavior, a crucial aspect of behavioral planning in urban environments.


#### **Motion Planning & Trajectory Generation**

Focuses on generating safe, comfortable, and feasible paths or sequences of waypoints for the autonomous vehicle to follow.



* **LanguageMPC** : While the LLM provides high-level decisions, these are translated to guide a Model Predictive Controller (MPC) which performs the fine-grained trajectory planning and control.
* **OpenDriveVLA** : A core capability is generating reliable driving trajectories conditioned on multimodal inputs, ensuring spatially and behaviorally informed trajectory planning through its agent-env-ego interaction model.
* **LightEMMA** : Evaluates VLMs on the nuScenes *prediction* task, where predicted control actions are numerically integrated to produce a predicted trajectory, which is then compared against ground truth. This is a form of motion planning.
* **DriveGPT4** : Predicts low-level vehicle control signals (speed, turning angle) in an end-to-end fashion, which implicitly defines a trajectory.
* **AlphaDrive** : Specifically designed for autonomous driving planning, generating high-level plans that would then be refined into detailed trajectories. The rewards are tailored for planning accuracy and action importance.
* **DriveVLM** : Features hierarchical planning modules. The DriveVLM-Dual system uses coarse, low-frequency waypoints from the VLM as an initial plan for a faster refining planner.
* **GPT-Driver** : Models motion planning as a language modeling problem, leveraging the LLM to generate driving trajectories by aligning its output with human driving behavior.
* **GenAD** : Models autonomous driving as a trajectory generation problem using an instance-centric scene tokenizer and a variational autoencoder for trajectory prior modeling.
* **VLP (Vision Language Planning for Autonomous Driving)** : Proposes a Vision Language Planning model composed of ALP (Action Localization and Prediction) and SLP (Safe Local Planning) components to improve ADS from BEV reasoning and decision-making for planning.


#### **Direct Control Signal Generation**

Involves models that directly output low-level control commands for the vehicle, such as steering angle and acceleration/braking.



* **DriveGPT4** : Explicitly states that it predicts low-level vehicle control signals (vehicle speed and turning angle) in an end-to-end fashion.
* **LightEMMA** : The final stage of its Chain-of-Thought prompting explicitly outputs a sequence of predicted control actions (e.g., [(v1, c1), (v2, c2),...]) which are then numerically integrated to produce the predicted trajectory.
* **ADAPT** : Jointly trains a vehicular control signal prediction task alongside driving captioning. The CSP head predicts control signals (e.g., speed, acceleration) based on video frames.
* **QUAR-VLA** : For quadruped robots, QUART (the VLA model) generates rich control commands including base velocity, posture, and gait parameters, which are analogous to direct control signals for a vehicle.


#### **Human-AI Interaction & Command Understanding**

Focuses on enabling autonomous vehicles to understand and respond to human language commands, preferences, or queries, facilitating more natural and intuitive interaction.



* **DriveGPT4** : Capable of processing textual queries from users and providing natural language responses, such as describing vehicle actions or explaining reasoning.
* **LanguageMPC** : Allows driving behavior adjustment (e.g., conservative vs. aggressive) based on textual inputs from users or high-precision maps.
* **Dolphins (Multimodal Language Model for Driving)** : Developed as a VLM-based conversational driving assistant, capable of understanding and responding to human interaction.
* **Talk2BEV** : Provides a large vision-language model interface for bird’s-eye view maps, allowing users to interpret driving contexts through freeform natural language queries.
* **Drive as You Speak / Talk-to-Drive** : Introduces an LLM-based framework to process verbal commands from humans and make autonomous driving decisions that satisfy personalized preferences for safety, efficiency, and comfort.
* **Human-Centric Autonomous Systems With LLMs for User Command Reasoning** : Proposes leveraging LLMs' reasoning capabilities to infer system requirements from in-cabin users’ commands, using the UCU Dataset.
* **ChatGPT as Your Vehicle Co-Pilot** : Designs a universal framework embedding LLMs as a vehicle "Co-Pilot" to accomplish specific driving tasks based on human intention and provided information.
* **LingoQA** : While a benchmark, its focus on video question answering (including action justification and scene description) directly supports the development of systems that can interactively explain their understanding and decisions to humans.

### **Categorization by Technical Route**

This section classifies papers based on the core AI techniques or methodologies they employ or innovate upon.


#### **Transformer Architectures & Variants**

Many LLMs, VLMs, and VLAs are based on the Transformer architecture, known for its efficacy in handling sequential data and capturing long-range dependencies.



* **ADAPT (Action-aware Driving Caption Transformer)** : Explicitly an end-to-end transformer-based architecture. It uses a Video Swin Transformer as the visual encoder and vision-language transformers for text generation and motion prediction.
* **TeLL-Drive** : While the core "teacher" is an LLM (typically Transformer-based), it guides an *attention-based* Student DRL policy. Self-attention mechanisms are integral to Transformers.
* **LanguageMPC** : Leverages Large Language Models (LLMs), which are predominantly Transformer-based, for high-level decision-making.
* **TS-VLM** : While focusing on a novel pooling module, it's designed for Vision-Language Models, many of which have Transformer backbones for either vision, language, or fusion. The paper contrasts its pooling with costly attention mechanisms (core to Transformers).
* **LightEMMA** : Evaluates various state-of-the-art VLMs, the majority of which (e.g., GPT-4o, Gemini, Claude, LLaMA-3.2-Vision, Qwen2.5-VL) are Transformer-based.
* **OpenDriveVLA** : Builds upon open-source pre-trained large Vision-Language Models (VLMs) and language foundation models, which are typically Transformer architectures.
* **DriveGPT4** : Based on Multimodal Large Language Models (MLLMs), which are extensions of Transformer-based LLMs.
* **LeapAD** : The Analytic Process uses an LLM (Transformer-based), and the Heuristic Process uses a lightweight language model, which could also be Transformer-based.
* **AlphaDrive** : Proposes a VLM (typically Transformer-based) tailored for high-level planning.
* **DriveVLM** : Uses Vision Transformers (ViT) as the image tokenizer and Qwen (a Transformer-based LLM) as the LLM backbone.
* **3D-VLA** : Built on top of a 3D-based Large Language Model (LLM), which implies a Transformer architecture.
* **QUAR-VLA** : Proposes QUAdruped Robotic Transformer (QUART), explicitly naming its VLA model as Transformer-based.


#### **Multimodal Fusion Techniques**

These works explore or propose novel ways to combine information from different modalities (e.g., vision, language, LiDAR, radar, vehicle states) for improved decision-making. Effective fusion is critical for VLMs and VLAs. The challenge in multimodal fusion lies in effectively aligning and integrating information from disparate sources, such as pixel-level visual data and semantic language features. This becomes even more complex when dealing with multiple sensor inputs (cameras, LiDAR, radar) and dynamic temporal information inherent in driving.



* **TS-VLM** : Introduces Text-Guided SoftSort Pooling (TGSSP) as a novel method for dynamic and query-aware multi-view visual feature aggregation, aiming for more efficient fusion than costly attention mechanisms.
* **OpenDriveVLA** : Proposes a hierarchical vision-language alignment process to project both 2D and 3D structured visual tokens into a unified semantic space, explicitly addressing the modality gap for language-guided trajectory generation.
* **DriveGPT4** : As an MLLM, it inherently processes and fuses multi-frame video inputs with textual queries to inform its reasoning and control signal prediction. It tokenizes video sequences and text/control signals.
* **VLM-E2E** : Focuses on multimodal driver attention fusion. It integrates textual representations (attentional cues from VLMs) into Bird's-Eye-View (BEV) features for semantic supervision and introduces a BEV-Text learnable weighted fusion strategy to balance contributions from visual and textual modalities.
* **DriveVLM** : The VLM architecture takes multiple image frames as input and uses Qwen as the LLM backbone, implying fusion of visual features with the language model's processing. The DriveVLM-Dual system also fuses perception information from the VLM with a traditional AV 3D perception module.
* **3D-VLA** : Links 3D perception (point clouds, images, depth) with language and action through a generative world model. It uses a projector to efficiently align LLM output features with diffusion models for generating multimodal goal states.
* **QUAR-VLA** : Integrates visual information (first-person camera images) and natural language instructions as inputs to generate rich, multi-dimensional control commands for quadruped robots.
* **Holistic Autonomous Driving Understanding by Bird’s-Eye-View Injected Multi-Modal Large Models (BEV-InMLMM)** : Proposes integrating instruction-aware BEV features with existing MLLMs to improve holistic understanding.
* **COMPASS (COntrastive Multimodal Pre-training for AutonomouS Systems)** : While a general pre-training approach for autonomous systems, COMPASS constructs a multimodal graph to connect signals from different modalities (e.g., camera, LiDAR, IMU, odometry) and maps them into factorized spatio-temporal latent spaces for motion and state representation. This is relevant for learning fused representations for decision-making.


#### **Prompt Engineering (e.g., Chain-of-Thought)**

Focuses on designing effective prompts to guide foundation models, especially LLMs and VLMs, to elicit desired reasoning processes and outputs for decision-making tasks. Chain-of-Thought (CoT) prompting, which encourages models to generate intermediate reasoning steps, is a prominent technique in this area. This method simulates human-like reasoning by breaking down complex problems into a sequence of manageable steps, leading to more accurate and transparent outputs, particularly for tasks requiring multi-step reasoning.



* **TeLL-Drive** : Explicitly uses Chain-of-Thought (CoT) reasoning in its Teacher LLM. The LLM incorporates risk metrics, historical scenario retrieval, and domain heuristics into context-rich prompts to produce high-level driving strategies. The CoT approach helps the model iteratively evaluate collision severity, maneuver consequences, and broader traffic implications, reducing logical inconsistencies.
* **LanguageMPC** : Devises cognitive pathways to enable comprehensive reasoning with LLMs, which involves sophisticated prompting to guide the LLM through scenario encoding, action guidance, and confidence adjustment. The system's reasoning ability is affirmed by its chain-of-thought approach.
* **LightEMMA** : Employs a Chain-of-Thought (CoT) prompting strategy for its VLM-based autonomous driving agents. This is used to enhance interpretability and facilitate structured reasoning, with the final stage of the CoT explicitly outputting a sequence of predicted control actions.
* **Agent-Driver** : The reasoning engine of this LLM-based agent is capable of chain-of-thought reasoning, among other capabilities like task planning and motion planning.
* **VLM-AD** : Leverages VLMs as teachers to generate reasoning-based text annotations. The annotation process involves prompting a VLM (GPT-4o) with visual input (front-view image with projected future trajectory) and specific instructions to interpret the scenario, generate reasoning, and identify ego-vehicle actions.
* **LLMs Powered Context-aware Motion Prediction** : Designs and conducts prompt engineering to enable unfine-tuned GPT-4V to comprehend complex traffic scenarios for motion prediction.
* **Fine-tuning Vision-Language Models with Task Rewards for Multi-Step Goal-Directed Decision Making** : This work prompts the VLM to generate chain-of-thought (CoT) reasoning to enable efficient exploration of intermediate reasoning steps that lead to the final text-based action in an RL framework.
* **OmniDrive** : Designs prompts for GPT-4 to generate coherent Q&A data for driving tasks by using simulated trajectories for counterfactual reasoning to identify key traffic elements and assess outcomes.


#### **Knowledge Distillation & Transfer Learning**

Involves transferring knowledge from larger, more capable models (like powerful proprietary LLMs/VLMs) or from diverse data sources to smaller, more efficient models suitable for deployment in autonomous vehicles, or adapting models trained in one domain (e.g., general web text/images) to the specific domain of autonomous driving.



* **AlphaDrive** : Employs a two-stage planning reasoning training strategy that explicitly involves knowledge distillation. In the first stage, a large model (e.g., GPT-4o) generates a high-quality dataset of planning reasoning processes, which is then used to fine-tune the AlphaDrive model via Supervised Fine-Tuning (SFT), effectively distilling knowledge from the larger model.
* **LeapAD** : The Analytic Process (System-II), which uses a powerful LLM, accumulates linguistic driving experience. This experience is then transferred to the lightweight language model of the Heuristic Process (System-I) through supervised fine-tuning. This is a form of knowledge transfer from a more capable reasoning system to a more efficient one.
* **VLM-AD (Leveraging Vision-Language Models as Teachers for End-to-End Autonomous Driving)** : This method explicitly uses VLMs as "teachers" to automatically generate reasoning-based text annotations. These annotations then serve as supplementary supervisory signals to train end-to-end AD models. This process distills driving reasoning knowledge from the VLM to the student E2E model.
* **Domain Knowledge Distillation from Large Language Model: An Empirical Study in the Autonomous Driving Domain** : This paper directly investigates distilling domain knowledge from LLMs (specifically ChatGPT) for the autonomous driving domain, developing a web-based distillation assistant.
* **General VLM/VLLM Surveys** : These surveys often discuss how foundation models like CLIP are pre-trained on large-scale data and then their knowledge is transferred to downstream tasks through techniques like prompt tuning, visual adaptation, or knowledge distillation. This is a core concept in leveraging foundation models.
* **Mixing Left and Right-Hand Driving Data in a Hierarchical Framework with LLM Generation** : While focused on data compatibility, this work uses an LLM-based sample generation method and techniques like MMD to reduce the domain gap between datasets from different driving rule domains (left-hand vs. right-hand drive). This can be seen as a form of domain adaptation or transfer learning for trajectory prediction models.

## **Datasets and Benchmarks**


* **nuScenes** : A large-scale multimodal dataset widely used for various AD tasks, including 3D object detection, tracking, and prediction. It features data from cameras, LiDAR, and radar, along with full sensor suites and map information. Several works like LightEMMA , OpenDriveVLA , and GPT-Driver  utilize nuScenes for evaluation or data generation. It is also used for tasks like BEV retrieval  and dense captioning.
* **BDD-X (Berkeley DeepDrive eXplanation)** : This dataset provides textual explanations for driving actions, making it particularly relevant for training and evaluating interpretable AD models. DriveGPT4  and ADAPT  are evaluated on BDD-X. It contains video sequences with corresponding control signals and natural language narrations/reasoning.
* **Waymo Open Dataset (WOMD)** : A large and diverse dataset with high-resolution sensor data, including LiDAR and camera imagery. Used in works like OmniDrive for Q&A data generation  and by LLMs Powered Context-aware Motion Prediction. Also used for scene simulation in ChatSim. WOMD-Reasoning is a language dataset built upon WOMD focusing on interaction descriptions and driving intentions.
* **DriveLM** : A benchmark and dataset focusing on driving with graph visual question answering. TS-VLM is evaluated on DriveLM. It aims to assess perception, prediction, and planning reasoning through QA pairs in a directed graph, with versions for CARLA and nuScenes.
* **LingoQA** : A benchmark and dataset specifically designed for video question answering in autonomous driving. It contains over 419k QA pairs from 28k unique video scenarios, covering driving reasoning, object recognition, action justification, and scene description. It also proposes the Lingo-Judge evaluation metric.
* **CARLA Simulator & Datasets** : While a simulator, CARLA is extensively used to generate data and evaluate AD models in closed-loop settings. Works like LeapAD , LMDrive , and LangProp  use CARLA for experiments and data collection. DriveLM-Carla is a specific dataset generated using CARLA.
* **Argoverse** : A dataset suite with a focus on motion forecasting, 3D tracking, and HD maps. Argoverse 2 is used in challenges like 3D Occupancy Forecasting.
* **KITTI** : One of the pioneering datasets for autonomous driving, still used for tasks like 3D object detection and tracking.
* **Cityscapes** : Focuses on semantic understanding of urban street scenes, primarily for semantic segmentation.
* **UCU Dataset (In-Cabin User Command Understanding)** : Part of the LLVM-AD Workshop, this dataset contains 1,099 labeled user commands for autonomous vehicles, designed for training models to understand human instructions within the vehicle.
* **MAPLM (Large-Scale Vision-Language Dataset for Map and Traffic Scene Understanding)** : Also from the LLVM-AD Workshop, MAPLM combines point cloud BEV and panoramic images for rich road scenario images and multi-level scene description data, used for QA tasks.
* **NuPrompt** : A large-scale language prompt set based on nuScenes for driving scenes, consisting of 3D object-text pairs, used in Prompt4Driving.
* **nuDesign** : A large-scale dataset (2300k sentences) constructed upon nuScenes via a rule-based auto-labeling methodology for 3D dense captioning.
* **SUP-AD** : A dataset created for the DriveVLM project, constructed through a data mining and annotation pipeline, focusing on scene understanding for planning tasks.
* **LaMPilot** : An interactive environment and dataset designed for evaluating LLM-based agents in a driving context, containing scenes for command tracking tasks.
* **DRAMA (Joint Risk Localization and Captioning in Driving)** : Provides linguistic descriptions (with a focus on reasons) of driving risks associated with important objects.
* **HAD (Human-To-Vehicle Advice for Self-Driving Vehicles)** : A dataset for grounding human advice for self-driving vehicles.
* **Rank2Tell** : A multimodal ego-centric dataset for ranking importance levels of objects/events and generating textual reasons for the importance.
* **OpenX-Embodiment Dataset** : While broader, it's a large-scale robotics dataset used in training generalist VLA models like RT-X, which have implications for AD.
* **HighwayEnv** : A collection of environments for autonomous driving and tactical decision-making research, often used for RL-based approaches and LLM decision-making evaluations (e.g., by DiLu, MTD-GPT).






### **Other Awesome Lists**

These repositories offer broader collections of resources that may overlap with or complement the focus of this list.

* **Awesome-LLM4AD (LLM for Autonomous Driving)**:
    * GitHub:([https://github.com/Thinklab-SJTU/Awesome-LLM4AD](https://github.com/Thinklab-SJTU/Awesome-LLM4AD)) 
    * Alternative Link:(http://codesandbox.io/p/github/sorokinvld/Awesome-LLM4AD) 
    * Description: A curated list of research papers about LLM-for-Autonomous-Driving, categorized by planning, perception, question answering, and generation. Continuously updated.
* **Awesome-VLLMs (Vision Large Language Models)**:
    * GitHub: [JackYFL/awesome-VLLMs](https://github.com/JackYFL/awesome-VLLMs) 
    * Description: Collects papers on Visual Large Language Models, with a dedicated section for "Vision-to-action" including "Autonomous driving" (Perception, Planning, Prediction).
* **Awesome-Data-Centric-Autonomous-Driving**:
    * GitHub:([https://github.com/LincanLi98/Awesome-Data-Centric-Autonomous-Driving](https://github.com/LincanLi98/Awesome-Data-Centric-Autonomous-Driving)) 
    * Description: Focuses on data-driven AD solutions, including datasets, data mining, and closed-loop technologies. Mentions the role of LLMs/VLMs in scene understanding and decision-making.
* **Awesome-World-Model (for Autonomous Driving and Robotics)**:
    * GitHub:(https://github.com/LMD0311/Awesome-World-Model) 
    * Description: Records, tracks, and benchmarks recent World Models for AD or Robotics, supplementary to a survey paper. Includes many VLA-related and generative model papers.
* **Awesome-Multimodal-LLM-Autonomous-Driving**:
    * GitHub:(https://github.com/IrohXu/Awesome-Multimodal-LLM-Autonomous-Driving) 
    * Description: A systematic investigation of Multimodal LLMs in autonomous driving, covering background, tools, frameworks, datasets, and future directions.
* **Awesome VLM Architectures**:
    * GitHub: [gokayfem/awesome-vlm-architectures](https://github.com/gokayfem/awesome-vlm-architectures) 
    * Description: Contains information on famous Vision Language Models (VLMs), including details about their architectures, training procedures, and datasets.

## Citation

If you find this repository useful, please consider citing this list:

```
@misc{liu2025lm4decisionofad,
    title = {Awesome-LM-AD-Decision},
    author = {Jiaqi Liu},
    journal = {GitHub repository},
    url = {https://github.com/Jiaaqiliu/Awesome-LM-AD-Decision},
    year = {2025},
}

```
