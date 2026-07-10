# MLTS-009 Validation Engine

## Eesmärk
Validation Engine kontrollib, kas MLTS-i loodud treeningkava on kliendile loogiline, ohutu, ajaliselt teostatav ja eesmärgiga kooskõlas.

Validation Engine ei loo kava ise, vaid kontrollib teiste moodulite otsuseid enne lõpliku treeningkava väljastamist.

## Sisend
Validation Engine saab kontrollimiseks järgmised andmed:

- kliendi profiil;
- treeningu eesmärk;
- treeningkogemus;
- vigastused ja piirangud;
- treeningpäevade arv;
- treeningu kestus;
- valitud treeningjaotus;
- valitud harjutused;
- seeriad ja kordused;
- puhkeajad;
- tempo;
- progressioon;
- alternatiivharjutused.

## Peamised kontrollivaldkonnad

### 1. Kliendi taseme kontroll
Kava peab vastama kliendi treeningkogemusele.

Algaja puhul kontrollitakse, et:
- harjutused ei oleks liiga keerulised;
- seeriate arv ei oleks liiga suur;
- treening ei sisaldaks liiga palju uusi liigutusi korraga;
- põhifookus oleks tehnika, harjumuse ja kontrolli arendamisel.

Edasijõudnu puhul võib kava sisaldada:
- suuremat mahtu;
- keerukamaid harjutusi;
- täpsemat progressiooniloogikat;
- rohkem lihasgrupipõhist jaotust.

### 2. Vigastuste ja piirangute kontroll
Kava ei tohi sisaldada harjutusi, mis on vastuolus kliendi piirangutega.

Kontrollitakse:
- põlvevalu;
- alaseljavalu;
- õlapiirkonna probleemid;
- puusapiirangud;
- randme- või küünarliigese probleemid;
- operatsioonijärgsed piirangud;
- muud individuaalsed piirangud.

Kui harjutus ei sobi:
- märgitakse see sobimatuks;
- valitakse alternatiiv;
- vähendatakse liikumisulatust;
- kasutatakse regressiooni;
- lisatakse treenerile hoiatus.

### 3. Treeningmahu kontroll
Kontrollitakse, kas töömaht on kliendile sobiv.

Arvestatakse:
- seeriate arv treeningu kohta;
- seeriate arv lihasgrupi kohta;
- treeningpäevade arv nädalas;
- kliendi kogemus;
- taastumine;
- eesmärk;
- treeningu kestus.

Liiga suure mahu korral:
- eemaldatakse vähemoluline abiharjutus;
- vähendatakse seeriaid;
- lühendatakse treeningut;
- muudetakse harjutuste prioriteeti.

### 4. Ajapiirangu kontroll
Treening peab mahtuma kliendi soovitud ajaraami.

Arvestatakse:
- soojendus;
- harjutuste arv;
- seeriate arv;
- puhkeajad;
- üleminekud harjutuste vahel;
- juhendamise või tehnika õppimise aeg.

Kui treening ei mahu ajapiirangusse:
- vähendatakse harjutuste arvu;
- vähendatakse seeriaid;
- valitakse lihtsamad harjutused;
- kasutatakse superset'e ainult siis, kui see on kliendile sobiv.

### 5. Liigutusmustrite tasakaal
Kontrollitakse, et kavas oleks sobiv tasakaal peamiste liigutusmustrite vahel.

Peamised mustrid:
- kükk;
- puusapainutus / hinge;
- tõuge;
- tõmme;
- ühe jala töö;
- kere stabilisatsioon;
- kandmine;
- rotatsioon või antirotatsioon.

Kava ei tohiks põhjendamatult üle koormata ühte mustrit ja jätta teist täiesti välja.

### 6. Lihasgruppide tasakaal
Kontrollitakse, et lihasgrupid oleksid eesmärgile vastavalt kaetud.

Kontrollitakse:
- alakeha eesmine ahel;
- alakeha tagumine ahel;
- tuharalihased;
- selg;
- rind;
- õlad;
- käed;
- kere.

Rasvapõletuse või üldvormi kavas peab rõhk olema terviklikul kehal, mitte ainult üksikul lihasgrupil.

### 7. Harjutuste järjekord
Kontrollitakse, et harjutused oleksid loogilises järjekorras.

Üldine põhimõte:
1. tehnilisemad ja raskemad harjutused;
2. suuremad lihasgrupid;
3. abiharjutused;
4. isoleerivad harjutused;
5. kere- ja lisaharjutused.

Erandid on lubatud, kui need on kliendi eesmärgiga põhjendatud.

### 8. Dubleerimise kontroll
Kontrollitakse, et kavas ei oleks liiga palju sarnaseid harjutusi.

Näiteks ei ole üldjuhul vaja samas treeningus:
- kolme väga sarnast rinnalt surumise varianti;
- mitut sama nurga alt tehtavat seljatõmmet;
- liigset hulka põlvedominantseid harjutusi põlveprobleemiga kliendile.

### 9. Progressiooni kontroll
Validation Engine kontrollib Progression Engine'i soovitusi.

Progressiooni ei kinnitata, kui:
- tehnika ei ole piisav;
- valu esineb;
- taastumine on halb;
- klient on algaja ja koormuse tõus on liiga kiire;
- treeningmaht ületab sobiva piiri.

### 10. Alternatiivide kontroll
Igal olulisel harjutusel peaks olema sobiv alternatiiv.

Alternatiiv peab sobima:
- sama liigutusmustriga;
- sama eesmärgiga;
- sarnase raskusastmega;
- kliendi piirangutega;
- olemasoleva varustusega.

## Kontrolli väljundid

Validation Engine võib anda järgmisi otsuseid:

### Approved
Kava sobib ja võib kliendile väljastada.

### Approved with warnings
Kava on kasutatav, kuid treener peab märkuseid arvesse võtma.

Näide:
- treening võib minna ajaliselt pikaks;
- õlapiirkonna harjutuste puhul jälgida tehnikat;
- raskuse tõstmisel olla ettevaatlik.

### Needs adjustment
Kava vajab enne väljastamist muutmist.

Näide:
- liiga palju harjutusi;
- liiga suur maht;
- sobimatu harjutus piirangu tõttu;
- puudub oluline liigutusmuster.

### Rejected
Kava ei sobi ja tuleb uuesti genereerida.

Näide:
- ignoreerib vigastust;
- koormus on kliendi taseme jaoks liiga suur;
- treening ei mahu ajapiirangusse;
- harjutused ei vasta eesmärgile.

## Hoiatuste kategooriad

### Low priority
Väike parandus või treeneri tähelepanek.

### Medium priority
Oluline asi, mida tuleks enne kasutamist korrigeerida.

### High priority
Kava ei tohiks sellisel kujul kliendile anda.

## Näited

### Näide 1
Klient:
- algaja;
- 3x nädalas;
- eesmärk kaalulangus;
- põlvevalu.

Kava sisaldab:
- hüppega kükke;
- väljaastehüppeid;
- 25 tööseeriat alakehale.

Validation Engine:
- märgib kava sobimatuks;
- eemaldab hüppeharjutused;
- soovitab madalama mõjuga alternatiive;
- vähendab mahtu.

### Näide 2
Klient:
- kesktase;
- eesmärk lihasmass;
- treeningu kestus 60 minutit.

Kava sisaldab:
- 10 harjutust;
- pikad puhkeajad;
- liiga palju isoleerivaid harjutusi.

Validation Engine:
- märgib, et treening ei mahu ajapiirangusse;
- eemaldab madalama prioriteediga harjutused;
- säilitab põhiharjutused;
- vähendab kogumahtu.

## Seos teiste moodulitega

Validation Engine kontrollib järgmiste moodulite väljundeid:

- Client Profile Engine;
- Decision Engine;
- Exercise Intelligence;
- Program Generator;
- Progression Engine.

Validation Engine annab Program Generatorile tagasi parandused või kinnituse.

## Staatus
Versioon: v0.2  
Roll: MLTS kvaliteedikontrolli alusdokument
