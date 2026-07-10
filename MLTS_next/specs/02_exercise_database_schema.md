# MLTS – harjutuste andmebaasi skeem

Faili eesmärk: määrata ühtne struktuur, mille alusel MLTS saab harjutusi lugeda, filtreerida ja treeningkavadesse valida.

## Põhimõte

Iga harjutus on süsteemis eraldi kirje. Harjutust ei kirjeldata ainult nime järgi, vaid ka liikumismustri, lihasgruppide, varustuse, raskusastme, piirangute ja asendatavuse järgi. Nii saab süsteem valida kliendile sobiva harjutuse, mitte lihtsalt juhusliku harjutuse samale lihasele.

## Kohustuslikud väljad

| Väli | Selgitus |
|---|---|
| exercise_id | Unikaalne ID, nt EX0001 |
| name_et | Harjutuse nimi eesti keeles |
| name_en | Harjutuse nimi inglise keeles |
| category | Harjutuse kategooria: jõuharjutus, liikuvus, aktivatsioon, kardio, core |
| movement_pattern | Peamine liikumismuster: kükk, puusatõuge/hinge, horisontaalne surumine, vertikaalne surumine, horisontaalne tõmbamine, vertikaalne tõmbamine, väljaaste, kandmine, rotatsioonivastane core jne |
| primary_muscles | Peamised töötavad lihased |
| secondary_muscles | Abistavad lihased |
| stabilizers | Stabiliseerivad lihased |
| equipment | Vajalik varustus |
| difficulty | algaja, kesktase, edasijõudnu |
| goal_fit | Sobivad eesmärgid: jõud, lihasmass, rasvakaotus, üldvorm, taastumine |
| contraindications | Olukorrad, kus harjutust vältida või kohandada |
| substitutions | Võimalikud asendusharjutused ID või nime järgi |
| coaching_notes | Treeneri juhised ja tähelepanekud |
| setup | Algne asend / seadistus |
| execution | Soorituse kirjeldus |
| common_mistakes | Levinud vead |
| gif_or_image | Pildi/GIF-i failinimi või link |
| source | Allikas või märge, kust info pärineb |
| review_status | draft, reviewed, approved |

## Valikuloogika

MLTS peaks harjutuse valimisel kasutama vähemalt järgmisi kihte:

1. kliendi eesmärk;
2. treeningtase;
3. treeningpäevade arv nädalas;
4. sessiooni pikkus;
5. varustus;
6. vigastused ja piirangud;
7. liikumismustri tasakaal;
8. lihasgruppide koormuse jaotus;
9. harjutuse tehniline keerukus;
10. võimalus harjutust vajadusel asendada.

## Review-protsess

- `draft` – sisestatud, aga kontrollimata.
- `reviewed` – kontrollitud nime, lihasgruppide ja juhiste osas.
- `approved` – sobib kasutamiseks kliendikavades.

