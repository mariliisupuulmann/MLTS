# MLTS-004 – Core Architecture

## 1. Purpose

MLTS Core Architecture defines how the Mari-Liisu Training System makes training-plan decisions.

The goal of the system is to generate structured, safe, evidence-informed and coach-aligned training plans based on client profile data, training goals, available equipment, limitations and progression rules.

This document is the foundation for all later modules.

---

## 2. Core Principle

MLTS must not behave like a random exercise picker.

Every training plan must be created through a controlled decision sequence:

1. read client profile;
2. classify the client;
3. select the appropriate training structure;
4. choose movement patterns;
5. select exercises;
6. assign volume, intensity and rest periods;
7. validate safety and practicality;
8. output a finished plan with alternatives and notes.

---

## 3. Main System Modules

### 3.1 Client Profile Engine

Responsible for reading and interpreting client data.

Inputs may include:

- age;
- sex;
- height;
- body weight;
- training experience;
- goal;
- weekly training frequency;
- preferred session duration;
- injuries or limitations;
- available equipment;
- training environment;
- movement competence;
- recovery status;
- lifestyle constraints.

Output:

- client category;
- risk flags;
- training readiness level;
- suitable training style;
- restrictions for exercise selection.

---

### 3.2 Decision Engine

Responsible for making the primary programming decisions.

It decides:

- training split;
- training frequency structure;
- priority muscle groups;
- movement-pattern distribution;
- beginner/intermediate/advanced complexity;
- suitable exercise categories;
- total workload range.

The Decision Engine must always use the Client Profile Engine output before making decisions.

---

### 3.3 Exercise Engine

Responsible for selecting exercises from the exercise database.

Exercise selection must consider:

- primary muscle group;
- secondary muscle group;
- movement pattern;
- equipment;
- difficulty level;
- technical complexity;
- injury compatibility;
- goal compatibility;
- available alternatives;
- placement within the workout.

The Exercise Engine must not select exercises that conflict with client restrictions.

---

### 3.4 Program Generator

Responsible for building the actual workout plan.

It assembles:

- warm-up structure;
- main exercises;
- accessory exercises;
- core work;
- optional conditioning;
- sets;
- reps;
- rest periods;
- tempo notes;
- coaching cues;
- alternatives.

The Program Generator does not make safety decisions independently. It must rely on the Decision Engine, Exercise Engine and Validation Engine.

---

### 3.5 Progression Engine

Responsible for deciding how the plan progresses over time.

It defines:

- when to increase load;
- when to increase repetitions;
- when to increase sets;
- when to reduce volume;
- when to change exercises;
- when to deload;
- how to handle missed sessions;
- how to progress beginners safely.

Progression must be conservative for beginners and clients with limitations.

---

### 3.6 Validation Engine

Responsible for final quality control.

It checks:

- whether the plan fits the session duration;
- whether exercise order is logical;
- whether weekly volume is appropriate;
- whether injury restrictions are respected;
- whether the plan contains unnecessary duplication;
- whether movement patterns are balanced;
- whether the plan is realistic for the client;
- whether alternatives are available if equipment is missing.

If validation fails, the system must revise the plan before output.

---

## 4. Decision Flow

```text
Client Profile
      ↓
Client Profile Engine
      ↓
Decision Engine
      ↓
Exercise Engine
      ↓
Program Generator
      ↓
Progression Engine
      ↓
Validation Engine
      ↓
Final Training Plan
```

---

## 5. Required Data Sources

The Core Architecture depends on the following data groups:

```text
data/
├── exercises/
├── muscles/
├── movement_patterns/
├── equipment/
├── client_profiles/
├── decision_rules/
├── progression_rules/
└── validation_rules/
```

Each data group must later have a defined schema.

---

## 6. Training Plan Output Requirements

Every generated plan should include:

- client goal;
- training frequency;
- training split;
- workout duration target;
- workout days;
- exercise name;
- sets;
- reps;
- rest;
- tempo if needed;
- coaching notes;
- exercise alternatives;
- progression instructions;
- safety notes if applicable.

---

## 7. Non-Negotiable Rules

MLTS must always follow these rules:

1. Technique before load.
2. Client safety before exercise variety.
3. Training plan must fit the client, not the other way around.
4. Beginner plans must stay simple and repeatable.
5. Exercise order must follow training logic.
6. Pain, injury and movement limitations override goal-based exercise choices.
7. A plan must be possible to complete within the selected session duration.
8. Alternatives must be available for missing equipment or unsuitable exercises.
9. Progression must be gradual.
10. The system must avoid unnecessary complexity.

---

## 8. Example Decision Case

### Client input

```text
Sex: female
Age: 53
Level: beginner
Goal: fat loss and strength
Frequency: 3 sessions/week
Session duration: 60 minutes
Limitation: knee discomfort
Environment: gym
```

### System interpretation

```text
Client category: beginner
Training style: full-body
Exercise complexity: low to moderate
Main focus: technique, consistency, strength base
Avoid: jumping, high-impact knee-dominant exercises, excessive lower-body volume
Preferred: machines, supported movements, controlled tempo
```

### Output direction

```text
3 full-body sessions/week
5–7 exercises/session
Main patterns: squat variation, hinge, push, pull, core
Lower-body exercise choices adapted for knee tolerance
Progression through reps before load
```

---

## 9. Version Status

Version: v0.2 draft  
Status: Core architecture defined  
Next document: MLTS-005_Client_Profile_Engine.md
