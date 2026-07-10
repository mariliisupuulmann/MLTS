# MLTS-005 – Client Profile Engine

## Purpose

Client Profile Engine defines what information MLTS must collect about a client before generating a training plan.

This module does not create the training plan directly. Its role is to convert client information into structured inputs that the Core Engine, Decision Engine, Exercise Engine, Progression Engine and Validation Engine can use.

## Core principle

A training plan is only as good as the client profile behind it.

MLTS must never generate a program from only one variable such as goal or training frequency. It must consider the full client context: experience, capacity, limitations, schedule, equipment, recovery and preferences.

---

# 1. Client identity

These fields identify the client but should not directly determine training decisions unless relevant.

| Field | Type | Required | Notes |
|---|---|---|---|
| client_id | string | yes | Unique internal ID |
| first_name | string | optional | For display only |
| last_name | string | optional | For display only |
| date_created | date | yes | Profile creation date |
| last_updated | date | yes | Last profile update |

---

# 2. Basic body data

| Field | Type | Required | Notes |
|---|---|---|---|
| age | integer | yes | Used for recovery and risk rules |
| sex | enum | yes | female / male / other / not_specified |
| height_cm | number | optional | Useful for body composition context |
| weight_kg | number | optional | Useful for progress and loading context |
| body_fat_percent | number | optional | Only if measured |
| resting_heart_rate | number | optional | Useful for endurance/recovery context |

## Rules

- Age must influence recovery assumptions, not automatically reduce capability.
- Body weight must not be used as a judgment variable.
- Body composition data is optional and should not block plan creation.

---

# 3. Primary goal

| Field | Type | Required | Allowed values |
|---|---|---|---|
| primary_goal | enum | yes | fat_loss / muscle_gain / strength / general_fitness / endurance_support / rehabilitation_support / posture / confidence / sport_support |
| secondary_goals | list | optional | Same values as above |
| goal_priority | enum | optional | health / performance / appearance / consistency / pain_free_movement |

## Goal logic

Primary goal affects:

- training split
- exercise selection
- set and rep ranges
- rest periods
- volume
- intensity
- progression method
- cardio inclusion

Example:

```text
fat_loss + beginner + 3 days/week
→ full body or upper/lower/full body
→ moderate volume
→ technique-first approach
→ manageable intensity
```

---

# 4. Training experience

| Field | Type | Required | Allowed values |
|---|---|---|---|
| training_level | enum | yes | beginner / novice / intermediate / advanced |
| gym_experience_months | integer | optional | Total approximate experience |
| currently_training | boolean | yes | Whether client currently trains |
| current_training_frequency | integer | optional | Sessions per week |
| previous_personal_training | boolean | optional | Has worked with trainer before |
| technique_confidence | enum | yes | low / moderate / high |

## Level definitions

### Beginner

- Little or no gym experience.
- Needs clear instructions and simple exercise selection.
- Technique and confidence are primary priorities.

### Novice

- Has some gym experience.
- Can perform common machine exercises.
- May still need support with free weights and progression.

### Intermediate

- Understands main movement patterns.
- Can train independently.
- Needs more structured progression and volume control.

### Advanced

- Strong training history.
- Can tolerate higher volume and intensity.
- Needs more individualised programming.

---

# 5. Movement competence

| Field | Type | Required | Scale |
|---|---|---|---|
| squat_competence | enum | yes | unknown / poor / acceptable / good |
| hinge_competence | enum | yes | unknown / poor / acceptable / good |
| push_competence | enum | yes | unknown / poor / acceptable / good |
| pull_competence | enum | yes | unknown / poor / acceptable / good |
| single_leg_competence | enum | yes | unknown / poor / acceptable / good |
| core_control | enum | yes | unknown / poor / acceptable / good |

## Rules

- If competence is unknown, MLTS must choose safer, simpler options first.
- Poor movement competence should trigger regression, not exclusion.
- Complex free-weight exercises require acceptable or good competence unless supervised.

---

# 6. Pain, injuries and limitations

| Field | Type | Required | Notes |
|---|---|---|---|
| has_current_pain | boolean | yes | General pain flag |
| pain_areas | list | optional | knee / hip / low_back / shoulder / neck / wrist / ankle / other |
| injury_history | list | optional | Previous injuries or operations |
| medical_clearance_needed | boolean | optional | True if uncertain or higher risk |
| movement_restrictions | list | optional | Exercises or patterns to avoid |

## Safety rules

- MLTS does not diagnose.
- Pain must trigger conservative exercise selection.
- If pain is acute, worsening or unexplained, MLTS must recommend professional assessment before progression.
- Injury history should influence exercise selection, volume and progression speed.

Example:

```text
knee pain + beginner
→ avoid jumping and high-impact conditioning
→ prefer controlled lower-body patterns
→ include knee-stability and hip-strengthening options
```

---

# 7. Schedule and availability

| Field | Type | Required | Notes |
|---|---|---|---|
| sessions_per_week | integer | yes | 1–6, initially MLTS supports 1–4 |
| session_duration_min | integer | yes | Usually 45–90 min |
| preferred_training_days | list | optional | Mon–Sun |
| training_time_of_day | enum | optional | morning / midday / evening / variable |
| consistency_risk | enum | optional | low / moderate / high |

## Rules

- Plan volume must fit the actual available time.
- 45-minute plans must use fewer exercises and less complex setup.
- 90-minute plans can include more accessories, warm-up and conditioning.
- Fewer weekly sessions usually require more full-body structure.

---

# 8. Training environment and equipment

| Field | Type | Required | Allowed values |
|---|---|---|---|
| training_location | enum | yes | gym / home / outdoors / mixed |
| equipment_available | list | yes | machines / cables / dumbbells / barbells / kettlebells / bands / bodyweight / cardio_machines |
| gym_type | enum | optional | commercial_gym / small_gym / 24_7_gym / home_gym |
| missing_equipment | list | optional | Equipment known to be unavailable |

## Rules

- Exercise Engine may only select exercises compatible with available equipment.
- Every program should include alternatives where possible.
- Machine-based options are often preferred for beginners, but not mandatory.

---

# 9. Recovery and lifestyle

| Field | Type | Required | Scale |
|---|---|---|---|
| sleep_quality | enum | optional | poor / moderate / good |
| average_sleep_hours | number | optional | Approximate |
| stress_level | enum | optional | low / moderate / high |
| daily_activity_level | enum | optional | sedentary / lightly_active / active / very_active |
| physical_job | boolean | optional | Whether job is physically demanding |
| shift_work | boolean | optional | Whether schedule changes often |

## Rules

- Poor sleep + high stress should reduce aggressive progression.
- Physically demanding work should reduce lower-body and total volume when needed.
- Sedentary clients may benefit from gradual conditioning and mobility support.

---

# 10. Preferences and barriers

| Field | Type | Required | Notes |
|---|---|---|---|
| exercise_preferences | list | optional | Exercises client likes |
| exercise_dislikes | list | optional | Exercises client dislikes |
| training_style_preference | enum | optional | structured / flexible / minimal / challenging |
| main_barriers | list | optional | time / motivation / fear / pain / knowledge / consistency |
| coaching_need | enum | optional | low / moderate / high |

## Rules

- Preferences can guide selection but must not override safety or effectiveness.
- If motivation is low, plan should be simple, clear and achievable.
- If confidence is low, avoid overly complex exercise names and excessive volume.

---

# 11. Output produced by Client Profile Engine

Client Profile Engine outputs a structured profile summary for the Core Engine.

```json
{
  "client_category": "beginner_fat_loss_3x_week",
  "risk_level": "moderate",
  "training_capacity": "low_to_moderate",
  "recommended_split_options": ["full_body", "upper_lower_full_body"],
  "exercise_complexity_limit": "simple_to_moderate",
  "progression_speed": "conservative",
  "validation_flags": ["knee_pain", "low_technique_confidence"],
  "program_constraints": {
    "sessions_per_week": 3,
    "session_duration_min": 60,
    "available_equipment": ["machines", "cables", "dumbbells"]
  }
}
```

---

# 12. Required validation before program generation

MLTS must check:

1. Is the primary goal defined?
2. Is training frequency defined?
3. Is session duration defined?
4. Is training level defined?
5. Is training environment defined?
6. Are current pain or injuries known?
7. Is equipment availability known?

If any required field is missing, MLTS must either:

- ask for clarification, or
- use a conservative default and mark the assumption clearly.

---

# 13. Default assumptions

If some optional data is missing, MLTS may use safe defaults.

| Missing field | Default assumption |
|---|---|
| technique confidence | low |
| movement competence | unknown |
| sleep quality | moderate |
| stress level | moderate |
| exercise preference | no preference |
| injury history | unknown |

Default assumptions must always be conservative.

---

# 14. Development priority

For v0.2, Client Profile Engine must support:

- beginner to intermediate gym clients
- 1–4 training sessions per week
- 45–90 minute workouts
- fat loss, strength, muscle gain and general fitness goals
- basic injury and pain flags
- machine, cable, dumbbell, barbell, bodyweight and band equipment

Advanced sport-specific programming can be added later.

