# AI Curriculum Planner Adaptive Academic Advising for 100 Simulated Students

This project implements a simulation-based academic advising system that leverages *graph theory* and *reinforcement learning* to recommend university courses to students. The goal is to build an intelligent advisor that can personalize course suggestions based on a student’s academic history, GPA, and interests, while respecting prerequisite constraints defined by a curriculum structure.

---

## Project Objectives

- Represent a university curriculum as a directed graph of courses and prerequisites.
- Simulate academic advising using both rule-based logic and a learning agent.
- Use Q-learning to learn optimal course recommendation strategies over time.
- Enable personalization based on students’ interests and academic profiles.

---

## Why Reinforcement Learning?

Traditional advising systems rely on fixed rules or manually designed recommendation paths. These methods:

- Do not adapt based on historical outcomes.
- Cannot optimize recommendations across multiple semesters.
- Do not improve over time from past student interactions.

*Reinforcement Learning (RL)* is well-suited for this task because:

- It models sequential decision-making (e.g., multiple terms of course selection).
- It can adapt to individual student needs and preferences.
- It optimizes for long-term reward (graduation progress + interest alignment).
- It balances exploration (trying new paths) and exploitation (using known good strategies).

In this project, we use *Q-learning*, a simple yet powerful RL algorithm, to train an academic advisor that improves its recommendations through repeated simulation of student paths.

---

## Key Features

- *Curriculum Graph Modeling*: Represents course dependencies using a Directed Acyclic Graph (DAG).
- *Personalized Advising*: Matches students with eligible and interest-aligned courses.
- *Q-Learning Agent*: Learns which courses lead to better outcomes for different student profiles.
- *Training Simulation*: Simulates multi-term academic progress and adjusts recommendations accordingly.
- *Performance Visualization*: Tracks improvement of the agent across epochs.

---

## Project Workflow

### Step 1: Curriculum Graph Construction

- Defined a dictionary of courses and their prerequisites.
- Used networkx.DiGraph() to construct a Directed Acyclic Graph (DAG).
- Each node represents a course, and each directed edge indicates a prerequisite relationship.
- The graph was visualized using matplotlib, with a fallback to spring_layout if the graph is not planar.
- This forms the static curriculum structure on which all advising simulations and decisions are based.

### Step 2: Rule-Based Personalization Agent

- Designed a basic simulation environment (AcademicAdvisorEnv) for course advising.
- Implemented logic to check a student's *eligibility* for courses (i.e., prerequisites are completed).
- Defined a *reward function* that gives:
  - A bonus if a selected course matches the student’s area of interest (e.g., "AI", "DS").
  - A small bonus for simply making progress (completing more courses).
- Simulated the advising process for 30 synthetic students using random course selections from their eligible options.
- This provided a baseline and helped validate the correctness of the curriculum logic and student modeling.

### Step 3: Q-Learning Agent for Course Recommendation

- Developed a Q-learning agent (QLearningAdvisor) that learns a course recommendation policy over time.
- The agent models the advising problem as a Markov Decision Process (MDP) where:
  - *State* = a tuple of (bitstring of completed courses, GPA category, interest area)
  - *Action* = a subset of eligible courses selected in the current term
  - *Reward* = average of bonuses from interest alignment, GPA improvement, and course progress
- The Q-table is updated using the standard Q-learning update rule with learning rate (alpha), discount factor (gamma), and exploration rate (epsilon).

### Step 4: Student Simulation and Agent Training

- Created a generate_student() function to simulate students with:
  - Unique ID
  - Random interest field
  - GPA between 2.0 and 4.0
  - Random initial course history
- Simulated training over 100 epochs using 10 different students.
- For each term, the agent:
  - Chooses actions (recommended courses) using an epsilon-greedy policy.
  - Updates the student’s GPA slightly based on recommendation quality.
  - Updates the Q-values using the observed reward and the next state.
- Decreased exploration (epsilon) over time to shift toward exploitation.

### Step 5: Evaluation and Testing

- Generated 10 new students for evaluation.
- Used the trained Q-table to generate personalized top-5 course recommendations.
- Printed course recommendations for each student, along with their GPA, interest, and passed courses.
- Plotted the total reward per epoch to monitor the learning performance of the Q-learning agent over time.


---

## Setup and How to Run the Task

### Step 1: Environment Setup

Make sure you have Python 3.7 or higher installed. It's recommended to use a virtual environment to isolate dependencies.

bash
# Create and activate virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate


Then install the required libraries:
* networkx
* matplotlib
* numpy

By using
bash
pip install library_Name

### Step 2: Run the Task in Notebook

The easiest way to run the complete system is through the provided Jupyter Notebook.

bash
jupyter notebook notebook/AI_Curriculum_Planner_Ganna_Mohamed.ipynb
