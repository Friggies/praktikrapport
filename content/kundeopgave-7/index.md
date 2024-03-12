---
title: Kundeopgave 7
type: task
dato: 14/2/24 - 7/3/24
kategorier: [sogefunktion, produktfeed]
weight: 94
---

## Opgaven

Denne kunde havde allerede en søgefunktion, men ville gerne opgradere til en ny og bedre, som inkluderede filtre og små ændringer i deres produktfliser. Deres nye søgefunktionstype var en Embeded Overlay Search til laptop, og en Grid Overlay Search til mobiltelefonen. Her er, hvordan deres søgefliser så ud i deres gamle søgefunktion *(første)*, og her er, hvordan de gerne skulle ende med at se ud *(sidste)*:

{{< img-row >}}
	{{< img src="gammel-sogeflise.png" alt="Kundens gamle produktflise i deres søgning" >}}
	{{< img src="egen-produktflise.png" alt="Produktflisen hos kunden" >}}
{{< /img-row >}}


## Process

For at kunde implementere de nye fliser og den nye søgning, valgte jeg at tage et kig i, hvilken data som vi fik fra kunden. Jeg ledte primært efter data til produktflise-labels og data til filtrene i deres nye søgning.

### Produktfeed

Der var en del data, som vi desværre ikke fik i kundens produktfeed. For at kunne vise labels i produktfliserne skulle vi gerne have den data i produktfeedet. Vi kunne godt trække "PRE-ORDER" labelen ud af produktets beskrivelse, men ikke om produktet var en "Nyhed":

```js
extraData.preOrder: $("description").text().matches("FORUDBESTILLING")
```

Ydermere var der meget bøvl med produktfeedet ift. opsætningen af filtre i søgningen. To ud af fem værdier kunne bruges out-of-the-box; `brand` og `price`. Produktets `type` kunne måske væves ud ud produktet hierarkier, men hierarkierne havde også en masse andet unødvendig data. For både `color` og `sizes` fik vi kun én enkel værdi i produktfeedet, så produkter med flere forskellige farver/størrelser, ville ikke have den rigtige data. Dog kunne jeg evt. crawle størrelserne fra produktsiden, selvom det ikke ville være best-practise, fordi hvis vores crawler først kørte efter deres script *(som indsatte de tilgængelige størrelser på produktet)*, ville vi ikke få nogle størrelser på produktet.

For hurtigt at kunne implementere løsningen, blev opgaven sendt til en af vores fastansatte udviklere. Vi snakkede om problemerne med produktfeedet, og implementeringsprocessen kunne godt opstartes, samtidig med at kunden fik opsat sit produktfeedet korrekt.

{{< end-of-internship-notice >}}