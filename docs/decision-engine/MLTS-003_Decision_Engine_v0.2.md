# MLTS-003 – Decision Engine v0.2

## Eesmärk

See dokument kirjeldab MLTS otsustusmootori esimest praktilist versiooni.

Decision Engine ei loo treeningkava juhuslikult. Süsteem hindab klienti, treeningu konteksti, eesmärki, piiranguid, ajaraami ja harjutuste funktsiooni ning koostab treeningkava nende põhjal.

## Otsustusprioriteedid

1. Ohutus
2. Kliendi eesmärk ja kontekst
3. Treeningjaotus
4. Liikumismustrite katvus
5. Lihaskoormuse tasakaal
6. Ajaline efektiivsus
7. Kliendi eelistused

## Põhimõte

Treeningkava ei optimeerita harjutuste arvu järgi. Treeningkava optimeeritakse maksimaalse väärtuse järgi.

## Peamised moodulid

- Client Profile Engine
- Training Split Engine
- Exercise Selection Engine
- Volume Engine
- Progression Engine
- Substitution Engine
- Recovery Engine
- Quality Validation Engine

## Failid

- `data/decision-rules/decision_rules_v0_2.json`
- `data/client-profile/client_profile_schema_v0_2.json`
- `data/exercise-selection/exercise_selection_engine_v0_2.json`
- `data/quality-validation/quality_validation_checklist_v0_2.json`
