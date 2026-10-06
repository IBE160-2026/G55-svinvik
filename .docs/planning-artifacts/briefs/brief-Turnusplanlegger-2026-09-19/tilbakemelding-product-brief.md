# Tilbakemelding på product brief

| | |
|---|---|
| **Gruppe** | G55 – G55-svinvik |
| **Product brief** | `.docs/planning-artifacts/briefs/brief-Turnusplanlegger-2026-09-19/brief.md` (commit `e577947`), med `addendum.md` i samme mappe |
| **Tilbakemelding fra** | Faglærer i IBE160 (utarbeidet med KI-støtte) |
| **Dato** | 2026-10-06 |

## Samlet vurdering

- **Bør revideres før dere går videre.** Rett punktene markert «Endre» før dere lager PRD og arkitektur.

**Det som er bra:**

1. Prosjektet har en ekte bruker med et konkret problem: lablederen som bruker minst én dag i uka på å fordele ansatte på stasjoner i bakteriologi og PCR. Addendumet med observasjoner fra ukeplanen for uke 37 (flere navn per celle, deltid innen dagen, fraværsrader) viser at dere har satt dere grundig inn i hvordan arbeidet faktisk gjøres.
2. Briefen er ærlig om risiko og begrensninger: én utvikler med full jobb ved siden av, ukjent Word-format, uavklarte rotasjonsregler og at bare anonymiserte data kan ligge i et offentlig repo. Prinsippet om at appen flagger konflikter i stedet for å skjule dem, og at lederen alltid tar beslutningen, er godt.

**De viktigste endringene:**

1. Reglene som kjerneflyten bygger på, er ikke kartlagt ennå. Minimumsdekning per stasjon, hva som teller som «rusten» kompetanse, og hvordan rotasjon prioriteres, må avklares med lablederen før PRD-en kan beskrive hva forslaget skal gjøre. Uten disse reglene kan verken Claude Code bygge riktig logikk eller dere teste at den er riktig.
2. Suksesskriteriene må kunne testes innen emnet. «Good UI/UX» og «hun bruker appen i fire uker» er vanskelige å sjekke før innlevering. Legg til funksjonelle kriterier, for eksempel «når en stasjon mangler minimumsdekning en dag, vises en advarsel for den dagen» og «en person under opplæring telles ikke mot minimumsdekningen».
3. Kutt v1 ned til det én person rekker. Ta ut Word-import (bruk manuell registrering eller CSV), og forenkle Excel-eksporten til en ryddig ukeoversikt i stedet for en kopi av dagens ark med sammenslåtte celler.

## Vanskelighetsgrad og gjennomførbarhet

### Vurdert vanskelighetsgrad

- **Vanskelig**

**Sammenlignbart med:** 3) KI-styrt simulering av prosjektledelse (vanskelig), særlig delen om ressursallokering. Appen har ingen KI, men fordelingslogikken med harde og myke regler, kompetansenivåer og historikk er omfattende domenelogikk som må stemme.

**Begrunnelse:**

| Faktor | Nivå (lav / middels / høy) | Kommentar |
|---|---|---|
| Domenelogikk – hvor mange og hvor kompliserte regler og beregninger må stemme? | Høy | Fordeling av personer på stasjoner med minimumsdekning (hard), kompetansenivåer, opplæring som ikke teller, rotasjon med kompetanseforfall (myk) og konfliktvarsler. Reglene er ennå ikke skrevet ned. |
| Datamodell – antall entiteter og relasjoner mellom dem | Høy | Ansatt, stasjon, kompetanse per ansatt og stasjon med nivå, oppmøte per dag med deltid, minimumsdekning per stasjon og dagtype, tildeling og historikk. |
| Brukere, roller og innlogging | Lav | Bare innlogging for lablederen i v1. |
| KI-funksjonalitet i appen, f.eks. kall til språkmodell, prompts i koden og håndtering av usikre svar | Lav | Ingen KI i appen. Det er et greit valg, siden emnet handler om å styre KI i utviklingen. |
| Integrasjoner og eksterne tjenester, f.eks. API-er, betaling og e-post | Lav | Ingen eksterne tjenester. |
| Sanntid, samtidighet eller flere brukere som påvirker hverandre | Lav | Én bruker. «Live coverage feedback» er lokal oppdatering i grensesnittet, ikke sanntid mellom brukere. |
| Filhåndtering, f.eks. opplasting, PDF-lesing og eksport | Høy | Word-import uten kjent format og Excel-eksport i samme layout som dagens ark er to krevende filoppgaver. |
| Sikkerhet og personvern | Middels | Reelle ansattdata kan ikke ligge i det offentlige repoet. Testdata må anonymiseres, og ekte bruk krever en egen avklaring. |

**Hva vanskelighetsgraden betyr for dere:**

- _Vanskelig:_ Et vanskelig prosjekt gir større mulighet for toppkarakter, men også større risiko. Definer en minimal versjon som sikkert kan bli ferdig, og legg resten i tydelige trinn etterpå. Dere har allerede tenkt i faser, men v1 er fortsatt for stor for én person med full jobb ved siden av.

### Gjennomførbarhet med BMAD og Claude Code

Dere skal planlegge med BMAD (product brief → PRD → arkitektur → epics og stories) og implementere med Claude Code. Vurderingen under tar hensyn til at det må være tid til hele denne flyten, og til testing, retting og README til slutt.

| Spørsmål | Vurdering (OK / risiko / stor risiko) | Kommentar |
|---|---|---|
| **Tid og omfang** – kan v1 realistisk bli ferdig og stabil i løpet av semesteret, med tid til flere iterasjoner? | Stor risiko | Åtte v1-punkter, inkludert Word-import, fordelingsalgoritme, live-redigering, historikk og Excel-eksport i eksisterende layout, er mye for én person på deltid. |
| **BMAD-flyten** – er briefen konkret nok til at PRD, arkitektur og stories kan lages uten store hull, og blir det overkommelig mange stories? | Risiko | Flere av de viktigste reglene står som åpne spørsmål. PRD-en vil få hull akkurat der kjernelogikken skal beskrives. |
| **Egnet for Claude Code** – bruker løsningen en vanlig, godt dokumentert teknologistakk som Claude Code håndterer godt, eller krever den nisjeteknologi, spesialmaskinvare eller mye manuell konfigurasjon? | OK | HTML/CSS/JavaScript, Python og SQL er godt egnet. Bruk SQLite, slik at det ikke trengs egen databaseserver. |
| **Kontroll på KI-ens arbeid** – kan gruppen selv avgjøre om koden gjør det riktige? Krever domenet kunnskap gruppen ikke har, f.eks. avanserte beregninger eller fagregler, så er det vanskelig å kvalitetssikre. | Risiko | Dere kjenner domenet, men uten skrevne regler kan dere ikke avgjøre om et forslag fra fordelingslogikken er riktig. Lag små testuker med kjent riktig fordeling sammen med lablederen. |
| **Testbarhet** – finnes det tydelige regler og forventede resultater som tester kan skrives mot? | Risiko | Minimumsdekning og opplæringsregelen er godt testbare når de er definert. Rotasjon er vanskeligere og trenger en konkret regel, for eksempel «velg den med flest uker siden sist på stasjonen». |
| **Kjørbar for sensor** – kan appen kjøres lokalt etter README, uten gruppens nøkler, betalte kontoer eller egen infrastruktur? | OK | Ingen eksterne tjenester. Sørg for anonymiserte seed-data og en testbruker for lederinnloggingen. |
| **Avhengigheter og kostnader** – krever løsningen betalte API-er, f.eks. språkmodeller, og finnes det en plan for kostnad, testmodus eller mock-data? | OK | Ingen betalte tjenester. |

**Konklusjon om gjennomførbarhet:**

- **Gjennomførbart med justert omfang.** Se forslagene under.

**Forslag til justering av omfang eller vanskelighetsgrad:**

1. Gjør v1 til: register over ansatte, stasjoner og kompetanse; manuell eller CSV-basert oppmøteregistrering; minimumsdekning per stasjon; automatisk forslag som respekterer kompetanse og opplæring; konfliktvarsler; manuell redigering; enkel Excel-eksport. Flytt Word-import og eksport i nøyaktig dagens layout til et senere trinn.
2. Start med én enkel og eksplisitt rotasjonsregel som kan testes, og utvid den først når lablederen har bekreftet hvordan hun vil ha det. Historikken over hvem som har jobbet hvor, kan da bygges som en del av denne regelen.

## Hvorfor product brief er viktig for mappen

Product brief er utgangspunktet for PRD, arkitektur, stories og til slutt koden. Del 1 av mappen vurderes blant annet på om sensor kan følge en sporbar vei fra plan til ferdig app. Den vurderes også på om appen gjør det dere har beskrevet, om den er testet, om den er godt designet, og om den kan kjøres etter README. Et uklart, for stort eller for lite brief gjør alt dette vanskeligere senere. Det er mye enklere å rette nå enn sent i semesteret.

## 1. Gjennomgang av briefens deler

| Del av brief | Status | Kommentar |
|---|---|---|
| Executive Summary – er det klart hva appen er, og hvilket problem den løser? | OK | Klart at appen gjør oppmøtelisten om til et forslag til stasjonsfordeling, og at målet er å flytte arbeidet fra å bestemme til å kontrollere. Briefen er på engelsk, noe som er greit, men vær konsekvent med språket videre. |
| The Problem – er problemet konkret, med reelle situasjoner og brukere? | OK | Svært konkret: minimumsdekning, kompetanse, rotasjon, sykdom midt i uka og en dags manuelt arbeid. |
| The Solution – beskriver løsningen brukeropplevelsen, ikke bare teknologi? | OK | Beskriver flyten fra import via forslag, konfliktvalg og redigering til eksport. |
| What Makes This Different – er vurderingen ærlig og realistisk? | OK | Ærlig om at verdien er tilpasning, og at reglene ennå ikke er skrevet ned. |
| Who This Serves – er primærbrukerne tydelige, og vet vi hva de trenger? | OK | Lablederen er en tydelig primærbruker, og de ansatte er riktig plassert som lesere av eksporten. |
| Success Criteria – kan kriteriene faktisk sjekkes eller testes? | Endre | Kriteriene er generelle eller avhenger av bruk over flere uker. Legg til funksjonelle kriterier knyttet til dekning, kompetanse og konfliktvarsler. |
| Scope – er det klart hva som er med i første versjon, og hva som ikke er det? | Endre | Fasedelingen er god, men v1 er for stor og bygger på regler som ikke er avklart. Kutt Word-import og layoutkopi, og fest reglene. |
| Vision – henger visjonen sammen med resten uten å blåse opp omfanget? | OK | Feriemønster, helligdager og ansattinnsending ligger tydelig etter v1. |

## 2. Utgangspunkt for del 1 av mappen

Punktene følger kriteriene i sensorveiledningen for del 1. Vektene i parentes viser hvor mye hvert kriterium teller i del 1.

| Kriterium i del 1 | Hva briefen bør legge til rette for | Status | Kommentar |
|---|---|---|---|
| **1. Prosess og KI-styring** (30 %) | Brief som er presis nok til at PRD og stories kan bygges direkte på den, slik at krav kan spores fra brief til kode. | Juster | Briefen og addendumet er gode prosesspor. Dokumenter møtet med lablederen og reglene dere får, slik at sporet fra krav til kode blir tydelig. |
| **2. Funksjonalitet og omfang** (20 %) | Realistisk omfang for gruppen og semesteret: en tydelig kjerneflyt som kan bli ferdig og stabil, og nok innhold til å vise reell funksjonalitet. | Endre | Kjerneflyten er tydelig, men v1 er for stor for én person. En mindre v1 som virker, gir bedre grunnlag. |
| **3. Kvalitetssikring og testing** (15 %) | Suksesskriterier og funksjoner som er konkrete nok til å bli testtilfeller. | Endre | Testene krever skrevne regler og testuker med kjent riktig resultat. |
| **4. Design og brukeropplevelse** (10 %) | Tydelige brukere og brukssituasjoner som designet kan bygges rundt, gjerne med de viktigste skjermbildene eller flytene skissert. | OK | Ukeplanen med stasjoner som rader og dager som kolonner gir et godt utgangspunkt. Tenk på hvordan konflikter og utsatt rotasjon markeres visuelt. |
| **5. Kodekvalitet og arkitektur** (10 %) | Teknologivalg som er begrunnet og ikke mer komplekse enn appen trenger. | OK | Enkel stakk. Hold fordelingslogikken i en egen modul, slik at den kan testes uten grensesnitt. |
| **6. README og kjørbarhet** (10 %) | Løsning som andre kan kjøre lokalt uten betalte kontoer, og uten tilgang til gruppens egne tjenester og nøkler. | OK | Ingen betalte avhengigheter. README må forklare hvordan anonymiserte testdata og testbruker lastes inn. |
| **7. Ryddighet i repoet** (5 %) | En plan for hvor hemmeligheter, testdata og dokumentasjon skal ligge. | Juster | Viktig her: eksempel-ukeplanen og ekte navn må aldri committes. Lag en egen mappe for anonymiserte testdata, og legg ekte filer i `.gitignore`. |

## 3. Neste steg for gruppen

1. Gjennomfør møtet med lablederen og skriv ned reglene for minimumsdekning, kompetansenivåer og rotasjon. Lag to–tre anonymiserte testuker med riktig fordeling som fasit.
2. Skriv om suksesskriteriene til funksjonelle, testbare kriterier, og kutt v1 slik forslagene over beskriver.
3. Gå deretter videre til PRD, med Word-import, layoutkopi, ferie og helligdager som tydelig senere faser.

Oppdater product brief i repoet når dere har gjort endringene, slik at historikken viser hvordan planen utviklet seg. Det er en del av prosessen sensor ser etter.
