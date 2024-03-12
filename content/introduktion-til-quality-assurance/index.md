---
title: Introduktion til quality assurance
type: task
dato: 31/1/24
kategorier: [introduktion]
---
## Hvorfor?

For at være sikker på, at der blev leveret acceptable og robuste løsninger til kunderne, blev jeg inviteret til et møde med QA d. 31/1. Her blev der bl.a. forklaet, at grunden til vi har en intern QA-afdeling er, så vi kan leverer digitale løsninger af højeste kvalitet. Her er en liste med noget af det, som QA-afdelingen arbejder med:

- Udvikle interne standarder og QA guidelines
- Udføre QA tests på relevante kundeløsninger
- Sikre at medarbejder får nødvendig træning 

## Møde med Quality Assurance

Inden mødet skulle vi læse den interne dokumentation for QA-afdelingen, og have nedskrevet 5 spørgsmål til processen for QA. Her er mine 5 spørgsmål *(på engelsk inkl. svar)*:

1. **How does a card get to be marked with the "high priority" label?**

    You need to ask your manager for permission and explain why the card needs special treatment *(eg. has the custommer already gone live?)*. You can not add the lable yourself because you need a quick QA.

2. **Why is it necessary to have a scoring system for onboardings?**

    The scoring system is old and is currently getting restructured. The new system will focus more on avoiding common pitfalls and general errors.

3. **Which cards *(onboardings, newsletters, redesings or AIP-soltions)* have the most errors?**

    It is hard to say. The projects with the most issues would usually be onboarding custommers with multiple domains wanting both the search, the remonnendation boxes and the pages solution.

4. **What is the minimun and maximum screen sizes tested, and are there any devices/browsers what we do not prioritize?**

    We only but always check for compatability with the [Safari](https://www.apple.com/safari/) and [Chrome](https://chrome.com) browser. This means the solution is not checked on neither [Firefox](https://firefox.com) nor [Edge](https://www.microsoft.com/en-gb/edge). Furthermore, there is no version-checking for the browsers. Regarding screen sizes; The lowest tested screen size we test for is 375px, and the highest is just a standard desktop monitor. This means we do not test for neither any Samsung Galaxy S models nor the Iphone 5 model. Likewise any issues with wider monitors and curved screens will not be caught in the QA process.

5. **Tell me more about the accessibility testing** 

    The QA Department does not do a very thorough accessibility check of the digital solution. There is no color contrast check, no tab order navigation check, no screen reader check and no check for understandable alternative text for images.

### Noter fra mødet

Inde til selve mødet fik vi en masse information. Eftersom den interne QA-afdeling ikke har mange fastansatte medarbejdere, er den slået sammen med vores afdeling. Der er også visse kundeløsninger, som ikke behøver at gå igennem afdelingen. Dette er mindre løsninger som for eksempel [nyhedsbreve](/kategorier/nyhedsbrev).

Man skal først sende sin løsning til test hos afdelingen, når alt er lavet færdig på den. Man skal tjekke, at man har læst og forstået hele projektkortet, og at man har lavet en "self-QA" inden. Når alt er, som det skal være, skal man markere kortet med en QA-label og skrive en besked til QA-afdelingen.

Når man får sit projekt tilbage fra QA-afdelingen, er der vedhæftet en checkliste med forbedringer/rettelser til løsningen. Når disse er løst/implementeret, skal man tale med kundens Custommer Success Manager. De kan aftale med kunden, om løsningen skal gå live, og om projektet så kan afsluttes.

Der blev også nævnt specifikke fokuspunkter til hver af vores løsninger:

### Produktfeeds

- Når vi sætter et nyt produktfeed op for en kunde, skal det altid være i den nye version *(V2)*. Det nye feed skal nemlig være bedre til at håndtere de informationer, som kunderne giver os.

- Vi skal for alt i verden undgå at crawle data. Hvis vi har brug for data til at vise bl.a. labels, så skal vi bede kunden om at gøre denne data tilgængelig i produktfeedet. Ydermere skal dette feed gerne køre så ofte som muligt, så vi fanger opdateringer på produkter med det samme.

### Anbefalingsbokse

- Vi skal stræbe efter at have en ryddet og overskuelig oversigt over kundens forskellige designs til deres anbefalingsbokse. For meget rod kan nemlig skabe forvirring.

- Vi skal altid spørge om kunden selv kan indsætte vores placement-selectors på deres hjemmeside. Det er en mere stabil løsning ind at prøve at vedhæfte anbefalingsboksen til et hjemmesidedesign der er ude af vores kontrol og kan ændres hele tiden.

- Vi skal altid stræbe efter at replikere kundens egne anbefalingsbokse *(dog ikke hvis de er leveret af en konkurrerende virksomhed!)*.

- Det er meget vigtigt at anbefalingsboksene er sat op med de rigtige sprog. 

- Vær sikker på at anbefalingsbokse er sat op, så de kun viser produkter i den nuværende kategori. Dette sker ved en korrekt sat hirachies-selector.

I anbefalingsboksene er der også nogle generelle problemer med produktfliserne. Problemerne opstår primært i centreret indhold, overlappende elementer, for lange titler som skubber til resten af produktflisens indhold og forkerte sprog.

### Søgning

- Hvis en søgning viser udsolgte produkter, skal de altid boostes med en negativ værdi, så de stadig kan ses, men ligger i bunden af søgeresultaterne.

- Man skal være sikker på, at der altid er en søgning til både kundens hjemmeside på mobil, og til deres side på laptop. 

- Vær sikker på at søgningen er på det rigtige sprog. Det gælder også filtreringen og resultatsiden med 0 resultater.

- Sørg for at opdatere søgningens design, så den har kundens egne farver og stil. Tjek også om kunden vil have deres logo med i søgningen.

## Afrunding

Der er meget fokus på, at der skal være en struktureret arbejdsprocess for at sikre kvalitetsløsninger. Det er jo noget man godt lidt kan glemme, men det er ekstra vigtigt når man har så mange kunder.

Det er også interessant, hvordan de har udvalgt specifikke browsere og skærmstørrelse at QA-teste. Det er altså ikke alle muligt tilgange til produktet, som bliver testet. I mindre personlige projekter kan det være, at der er tid til altomfattende tests, men i større projekter bliver det oftest nedprioriteret, fordi der simpelthen er for mange skærmstørrelser og browsermulighedder.

Eventuelt kunne man også teste Firefox browseren, da den hverken kører på Safaris [WebKit](https://webkit.org) eller Googles [Blink](https://www.chromium.org/blink/), men i stedet Mozillas [Geko](https://developer.mozilla.org/en-US/docs/Glossary/Gecko). Det er dog kun [3,3% af internettrafik der kommer fra Firefox](https://gs.statcounter.com/browser-market-share), så igen er det en prioriteringssag.

Der er rigtig meget fokus på sprog og oversættelser i QA-processen. Når man bare laver enkle private løsninger er det nemt at bagatellisere sproget, men i større og mere strukturerede opgaver er det vigtigt for basal funktionalitet.