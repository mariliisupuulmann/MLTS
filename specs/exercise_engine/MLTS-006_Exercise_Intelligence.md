# MLTS-006 – Exercise Intelligence

## Purpose

Exercise Intelligence defines how MLTS understands, classifies, selects, rejects, substitutes and orders exercises inside a training plan.

This module is not only an exercise list. It is the decision layer that tells the system when an exercise is appropriate for a specific client, goal, limitation, training level and training environment.

---

## Core responsibility

The Exercise Intelligence module must answer five questions for every exercise:

1. What is the exercise training?
2. Who is it suitable for?
3. When should it be used?
4. When should it be avoided or modified?
5. What can replace it if needed?

---

## Exercise classification fields

Each exercise should eventually contain the following information.

### Identification

- exercise_id
- exercise_name_et
- exercise_name_en
- category
- description
- instruction_summary
- coaching_cues

### Movement pattern

- squat
- hinge
- push_horizontal
- push_vertical
- pull_horizontal
- pull_vertical
- lunge
- single_leg
- carry
- rotation
- anti_rotation
- anti_extension
- anti_lateral_flexion
- isolation
- locomotion

### Primary training target

- main_muscles
- secondary_muscles
- stabilizers
- joint_actions
- movement_plane
- unilateral_or_bilateral

### Equipment

- bodyweight
- machine
- cable
- dumbbell
- barbell
- kettlebell
- resistance_band
- bench
- suspension_trainer
- medicine_ball
- cardio_machine
- other

### Difficulty level

- beginner
- beginner_plus
- intermediate
- advanced

Difficulty is not based only on load. It also depends on coordination demand, stability demand, technique complexity, mobility requirement and risk of compensation.

### Training goal suitability

Each exercise may be marked as suitable, neutral or unsuitable for:

- strength
- hypertrophy
- fat_loss
- endurance
- general_fitness
- rehabilitation_support
- technique_learning
- athletic_performance

### Risk and limitation flags

Exercises should include flags for situations where caution is needed:

- knee_sensitive
- hip_sensitive
- lower_back_sensitive
- shoulder_sensitive
- wrist_sensitive
- neck_sensitive
- balance_demand_high
- mobility_demand_high
- impact_high
- axial_load_high
- technical_complexity_high

These flags do not automatically ban an exercise. They tell the decision engine to evaluate client context before selection.

---

## Exercise selection logic

The system should select exercises in this order:

1. Match client goal.
2. Match training level.
3. Match available equipment.
4. Match movement pattern needs.
5. Check injury and limitation flags.
6. Check session time budget.
7. Check total weekly training balance.
8. Add alternatives.
9. Send selection to Validation Engine.

---

## Exercise ordering principles

Within a workout, exercises are generally ordered as follows:

1. Warm-up or activation when needed.
2. Main compound movement.
3. Secondary compound movement.
4. Unilateral or accessory movement.
5. Isolation movement.
6. Core or stability work.
7. Conditioning or finisher, if appropriate.

Exceptions are allowed when the client has pain, poor technique, low confidence or a specific rehabilitation-support goal.

---

## Beginner exercise rules

For beginners, the system should prefer:

- machines before complex free-weight lifts when technique is unknown;
- stable positions before unstable positions;
- controlled tempo before heavy loading;
- fewer exercises with clearer execution;
- full-body or upper/lower structures before highly fragmented splits;
- repeatable exercises that help build confidence and consistency.

The system should avoid giving beginners too many new exercises in one session.

---

## Intermediate exercise rules

For intermediate clients, the system may use:

- more free-weight exercises;
- more unilateral work;
- more specific accessory work;
- progressive overload structures;
- moderate variation blocks;
- more goal-specific exercise selection.

Technique quality must still be checked before selecting complex exercises.

---

## Advanced exercise rules

For advanced clients, the system may use:

- heavier compound lifts;
- more specific hypertrophy targeting;
- advanced progression methods;
- higher weekly volume;
- more detailed split structures;
- more precise exercise rotation.

Advanced methods should only be used when recovery, technique and training history support them.

---

## Substitution logic

Every important exercise should have substitutions in several categories:

### Same pattern substitution

Used when equipment is unavailable but the movement goal remains the same.

Example:

- leg press → goblet squat
- lat pulldown → assisted pull-up
- cable row → machine row

### Easier regression

Used when technique, pain, confidence or strength level is insufficient.

Example:

- barbell squat → box squat
- push-up → incline push-up
- Romanian deadlift → hip hinge drill

### Harder progression

Used when the client has mastered the current version.

Example:

- goblet squat → front squat
- machine chest press → dumbbell bench press
- plank → weighted plank

### Pain-aware substitution

Used when the client reports discomfort.

Example:

- walking lunges → split squat with support
- overhead press → landmine press
- barbell hip thrust → machine glute bridge

---

## Volume and fatigue awareness

Exercise Intelligence must consider how fatiguing an exercise is.

High-fatigue exercises usually include:

- heavy compound lower-body lifts;
- deadlift variations;
- high axial-load movements;
- high-impact conditioning;
- complex full-body movements.

Low-to-moderate fatigue exercises usually include:

- machine isolation work;
- controlled cable exercises;
- supported rows;
- basic core stability work.

The system should not overload one session with too many high-fatigue movements unless the program goal clearly requires it.

---

## Exercise placement by goal

### Strength

Prefer technically reliable compound lifts early in the session, with longer rest and lower repetition ranges.

### Hypertrophy

Use a combination of compound and isolation exercises, moderate repetition ranges and sufficient weekly volume per muscle group.

### Fat loss

Use strength training as the base. Add efficient full-body structure, moderate density and optional conditioning without sacrificing technique.

### General fitness

Use balanced movement patterns, manageable volume and exercises the client can perform consistently.

### Rehabilitation support

Use controlled, low-risk, progressive movements that support function. The system must not diagnose or replace medical rehabilitation.

---

## Red-flag handling

If an exercise conflicts with a serious client limitation, the system should not select it automatically.

Examples:

- high-impact jumps for knee-sensitive clients;
- unsupported heavy hinging for lower-back-sensitive beginners;
- overhead pressing for shoulder pain without screening;
- complex balance exercises for clients with poor stability.

In these cases, the system should either:

1. select a safer alternative; or
2. mark the exercise for trainer review.

---

## Output requirements

When Exercise Intelligence sends an exercise to the Program Generator, it should provide:

- selected exercise;
- reason for selection;
- main target;
- sets and reps suggestion range;
- rest suggestion range;
- tempo suggestion;
- coaching note;
- substitution list;
- caution flags if any.

---

## Version status

v0.2 draft. This document defines the logic layer for exercise understanding and selection. The next step is to connect this with Program Generator and Validation Engine.
