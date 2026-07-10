# MLTS-004 – Exercise Database Standard v1.0

## Eesmärk

See standard määrab, kuidas MLTS kirjeldab iga harjutust.  
Kõik tulevased harjutused peavad kasutama sama struktuuri, et AI saaks neid kasutada treeningkavade koostamisel, asendamisel, progressioonis ja kvaliteedikontrollis.

## Põhimõte

Harjutust ei kirjeldata ainult nime ja lihaste järgi.  
Harjutusel on funktsioon, biomehaanika, õpetatavus, sobivus kliendile, koormusprofiil, alternatiivid ja juhendamise info.

## Peamised andmeplokid

1. Identity
2. Classification
3. Biomechanics
4. Muscle Load
5. Suitability
6. Programming
7. Coaching
8. Alternatives
9. Safety
10. Metadata

## Kohustuslikud väljad

- exercise_id
- name_et
- name_en
- movement_pattern_primary
- training_function
- biomechanical_function
- exercise_type
- equipment_primary
- primary_muscles
- secondary_muscles
- stabilizers
- beginner_suitability
- intermediate_suitability
- advanced_suitability
- instructions_et
- breathing_et
- common_mistakes_et
- coaching_cues_et
- alternatives

## Kliendile kuvatavad väljad

- name_et
- sets
- reps
- tempo_numeric
- tempo_text_et
- rest_seconds
- instructions_et
- breathing_et
- common_mistakes_et
- coaching_cues_et
- what_to_feel_et
- alternatives

## AI sisemised väljad

- movement_pattern_primary
- movement_pattern_secondary
- training_function
- biomechanical_function
- direct_load_weights
- indirect_load_weights
- fatigue_cost
- time_cost
- technical_complexity
- stability_requirement
- learning_difficulty
- substitution_group
- contraindications
- progression_candidates
- regression_candidates
