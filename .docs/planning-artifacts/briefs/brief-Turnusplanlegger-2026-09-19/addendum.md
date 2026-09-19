# Addendum: Turnusplanlegger

Dybde fra samtalen som hører hjemme i PRD/arkitektur, ikke i selve briefen.

## Tekniske føringer (skolekrav)
- Frontend: HTML/CSS/JavaScript. Backend: Python. Database: SQL.
- Leveres som nettside/webapp.

## Regelkategorier (fra bruker, uverifisert mot sjefen)
| Regel | Styrke | Merknad |
|---|---|---|
| Minimumsdekning per analyse per dag | Hard | Ved sykdom løser teamet det med ekstra innsats – unntakstilfelle |
| Rotasjon av arbeidsoppgaver | Mild, høyest av de milde | Ivaretar kompetansebredde slik at fravær enkelt dekkes |
| Ferieønsker | Mild | |
| Norsk arbeidstidslovgivning | Skal overholdes | Eksempler: ikke for mange søndager på rad, feriekrav. Konkrete regler ikke kartlagt |
| Uskrevne regler i sjefens hode | Ukjent | Skal kartlegges og konkretiseres sammen med sjefen |

## Ønsket konfliktatferd
Appen flagger konflikt; sjefen velger mellom (a) forslag til løsning fra appen eller (b) manuell løsning.

## Observasjoner fra eksempel-ukeplan (Excel-PDF, uke 37; anonymiseres før bruk i repo)
- Tre blokker: PCR (mandag–søndag), BAKT (mandag–søndag) og «Turnusfri og ferie» (kun man–fre).
- Rader = stasjoner/arbeidsoppgaver (f.eks. Mottak, Kveld, Vakthavende lege, Generell bakt, anaerobdyrk., urin, fæces, sopp, TB, substrat, spesialvask), kolonner = ukedager.
- Flere celler har mer enn ett navn (splittet dag, f.eks. «Navn/»), tidsangivelser («b14-15», «g1330», «k 1630», «9-14») og roller («Fagansvarlig …», «Informasjon til lab», «Ledere på jobb»).
- Egne rader for fravær fra laben: Fag/Hjemmekontor, Reise/Kurs, Kontordag, Fagekspert-tid.
- Navnedata er kun fornavn, delvis med initial for å skille (flere med samme fornavn) og med ulike stavemåter – navnematching mot Word-filen er en risiko.
- Implikasjon: modellen må støtte deltidsoppmøte innen dagen, flere personer per stasjon, fagansvarlig-roller og fraværstyper utover D/A/Fri.

## Kompetansemodell (fra bruker)
- Kompetanse per person per stasjon har nivåer (bl.a. under opplæring).
- Kompetanse forfaller med tid: lang tid siden sist på en oppgave gir «rustenhet». Dette er kjernen i rotasjonsregelen.
- Personer under opplæring teller ikke mot minimumsdekning; analysen må dekkes av andre i tillegg.
- Fravær midt i uken håndteres i dag muntlig av sjefen; appen skal først og fremst gjøre manuell flytting enkel.

## Rotasjon – kjente parametere (regler avklares i møte med sjefen)
- Gjelder alle stasjoner personen har kompetanse på.
- Formål: (1) vedlikeholde kompetanse, (2) unngå kjedsomhet og rutinepreg, (3) bygge kompetansebredde.
- Varierer med ansattes ønsker om hvor ofte de vil skifte, og med planlagt kompetansebygging.
- Definisjon av «rusten» (antall uker uten stasjon) er ukjent – spørsmål til sjefen.
- Ved konflikt med minimumsdekning: dekning vinner, og appen skal eksplisitt varsle at rotasjon ble utsatt.

## Tidsrytme
- Skiftplan (D/A/Fri + ferieønsker): fastsettes 2 ganger i året, utenfor appen i v1.
- Arbeidsfordeling: uke for uke; sjefen bruker minst én dag per uke i dag.

## Ferieønsker og helligdager (ny kravside, fra bruker)
- Ansatte sender inn ferieønsker; ikke alle kan innfris fordi minimumsdekning må holdes.
- Idé: prioritert ønskeliste per ansatt – hvor vil de ha fri, og hvor kan de jobbe om det trengs for å fylle inn personell.
- Helligdager: sjefen registrerer ønsker og tilgjengelighet for alle; appen foreslår helligdagspersonell.
- Helligdagsdekning er lavere enn vanlig dag (eks. fæcesanalyser trengs bare annenhver dag) → minimumsdekning må modelleres per dagtype.
- Rettferdighet: historikk over hvem som har jobbet hvilke helligdager skal påvirke forslaget.
- Deling: opprinnelig forslag var PDF delt som skjermbilde i Teams; erstattet av ønske om Excel-eksport (PDF blir fastlåst og gir versjonsforvirring).

## Ferieønsker: registrering (fra bruker)
- Ansatte sender inn ønsker (ferieuker + vilje/evne til å jobbe helligdager) via et skjema som sjefen deretter mater inn i appen. Ingen ansatt-innlogging i tidlige faser.
- Ferie- og helligdagsønsker henger sammen: ønsket om når man vil ha fri påvirker om man kan/vil jobbe helligdager.
- Kun sjefen trenger å se historikken over tidligere helligdagsvakter.

## Rettferdighet ved ferie-konflikter (uavklart)
- Hva skjer når to ansatte har første prioritet på samme periode og bare én kan innfris? Trenger en regel fra sjefen (f.eks. den som fikk ønsket sist år, går sist).
