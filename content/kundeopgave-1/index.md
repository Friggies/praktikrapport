---
title: Kundeopgave 1
type: task
dato: 15/1/24
kategorier: [sogefunktion, produktfeed]
weight: 100
---
## Opgaven
Min første rigtige opgave som praktikant i [Hello Retail](https://helloretail.com) var for en webshop, som skulle have deres produktflise i deres søgning opdateret. Der skulle nemlig gerne være et label på produktflisen, hvis produktet var GOTS’ *([Global Organic Textile Standard](https://global-standard.org))* certificeret. Dette label skulle vises både på laptop- og mobilsøgninger. 

## Process

For at kunne vise GOTS label var det nødvendigt at vi fik dataen igennem kundens produktfeed. Jeg havde ikke haft en komplet [introduktion til produktfeedet](/introduktion-til-produktfeed) endnu, men jeg havde siddet og leget lidt med det i et testmiljø. Efter at have tjekket deres produktfeed fandt jeg dog ud af, at der ikke var et eksplicit felt, som kunne fortælle mig, om produktet skulle have labelet eller ej. Efter at have snakket med nogle af de andre fastansatte udviklere, endte jeg med at fange dataen på denne måde:

```js
extraData.isGOTS: $("root > handle").text().matches(/-gots-/i)
```
Det som sker her er, at vi crawler dataen fra produktets handle/slug, og gemmer det i en `extradata.isGOTS` variabel *(hvis produktet har "-gots-" i sin url, så er variablen "true")*. Dette er dog ikke den optimale måde at gøre det på, da produktet til hver en tid kan ændre sit handle. Men eftersom kunden ikke ellers giver os den eksplicitte dataen i deres produktfeed, og ikke har den tekniske kunnen til at tilføje det, er dette det bedste alternativ. 

For at opdatere produktflisen skulle der så ændres i den del af liquidkoden, som viser produktflisen. Dette sker i alt 4 steder; 2 gange i mobilsøgningen og 2 gange i laptopsøgningen. Disse steder tilføjede jeg dette kode, som tjekkede den nye `extraData.isGOTS` variabel jeg lavede:

```html
{% if product.extraData.isGOTS and product.extraData.isGOTS == 'true' %}
	<div class="gotsicon-collection">
		<img src="https://cdn.shopify.com/s/files/1/0570/0514/6302/files/GOTS_web_logo.svg?v=1704712237">
	</div>
{% endif %}
```

## Resultat

Efter koden blev tilføjet, var alt som det skulle være. Selve stylingen kunne nemlig genbruges fra kundens eget stylesheet. Her ses et udklip af hvordan produktflisen så ud før *(første billede)* og efter *(sidste billede)* tilføjelsen af koden:

{{< img-row >}}
	{{< img src="produktflise-foer.png" alt="Produktflisen uden label" >}}
	{{< img src="produktflise-efter.png" alt="Produktflisen med label" >}}
{{< /img-row >}}

## Afrunding

Alt i alt en yderst fornem opgave at start ud med. Den var ikke for stor og overvældende, men var heller ikke for teknisk nem. Jeg skulle danne mig et overblik over kundes produktfeed, og jeg skulle finde en løsning på den manglende data i kundens produktfeed.

Efter jeg havde løst problemet med den manglende data, skulle jeg så skabe mig et overblik over hjemmesidens søgefunktion. Her skulle jeg lokalisere, hvor søgningens produktflise blev genereret, og opdatere layoutet så det kunne vise labelet.

En meget fornem opgave med fokus på struktureret arbejde, at danne sig et overblik og udtænke professionelle løsningsmulighedder. 
