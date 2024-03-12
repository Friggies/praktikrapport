---
title: Kundeopgave 8
type: task
dato: 19/2/24
kategorier: [nyhedsbrev]
weight: 93
---

## Opgaven

Jeg skulle opsætte e-mail triggers og nyhedsbreve til denne svenske kunde. Produktfliserne i nyhedsbrevet skulle være de samme som på deres hjemmeside, og designet for triggersne skulle tage udspring fra triggers, som tidligere var blevet implementeret hos en anden svensk kunde, bare med kundens eget visuelle udtryk og design.

## Process

### Nyhedsbrev

Jeg startede med at kode produktflisens udseende. Den skulle gerne ligne den produktflise, som de allerede havde på deres hjemmeside. Jeg oprettede flisen ud fra en standardskabelon, men der skulle mange ændringer til, før den lignede kundens egen produktflise. Her er et udsnit af den kode, som jeg skrev:

```html
<html>
	<head>
		<style>
            [...]
            /* Kunne genbruge fra en tidligere (kundeopg. 4) kundes løsning: */
			image {
                position: relative;
				background-image: url("{{ product.imgUrl }}");
				background-size: contain;
				background-position: center;
				background-repeat: no-repeat;
				width: 100%;
				height: {{ height | times : 0.4 }}px;
			}
            /* Et udsnit af de tilføjede stylings: */
			.price--old{
				font-size: 13px;
				color: #777;
				text-decoration: line-through;
				letter-spacing: -1px;
				text-align: center;
			}
            .label{
				position: absolute;
				color: white;
				border-radius: 3px;
				border-top-right-radius: 10px;
				box-shadow: 1px 1px 2px 0 rgba(0,0,0,0.1);
				padding: 5px 10px;
				text-transform: uppercase;
				font-size: 11px;
				font-weight: 700;
				z-index: 1
            }
			.label--nyhet{
				top: 5px;
                background-color: black;
			}
			.label--sell{
				top: 30px;
				background-color: #e94141;
			}
		</style>
	</head>
    <!-- Min færdigudviklede produktflise: -->
	<body>
        <div 
			id="inner">
            {% if product.extraData.isNew %}
                <div 
					class="label label--nyhet">
					Nyhet</div>
            {% endif %}
            {% if product.isOnSale %}
                <div 
					class="label label--sell">
                    -{{ product.oldPrice|minus:product.price|times:100.0|divided_by:product.oldPrice|round }}%
                </div>
            {% endif %}
            <div 
				class="image">
				<!-- Produktbillede som baggrundsbillede ligesom i kundeopg. 4 -->
			</div>
            <div 
				class="container">
                {% if product.isOnSale %}
                    <div 
						class="price--old">
                        {{ product.oldPrice | price }} {{ product.currency }}
                    </div>
                {% endif %}
            	<div
                	class="price"
                	{% if product.isOnSale %} style="color:red" {% endif %}>
                    	{{ product.price | price }} {{ product.currency }}
                </div>
            </div>
            <div 
				class="button">
                Köp
            </div>
        </div>
	</body>
</html>
```

Jeg kunne ikke, som jeg fandt ud af under mit arbejde med [en tidligere kunde](/kundeopgave-4), tilføje ikoner fra [Font Awesome](https://fontawesome.com). Der var også andre problemer med, at det ikke var muligt at bruge flexbox, rgba og transform.
Her kan du se hvordan slutresultatet endte med at blive, det første billede er af to af Dalarna Designs egne produktfliser, og billede nummer 2 er af to af mine færdigudviklede produktfliser:

{{< img-row >}}
	{{< img src="sidens-egne-produktfliser.png" alt="Dalarna Designs egne produktfliser" >}}
	{{< img src="nye-produktfliser.png" alt="Mine færdigudviklede produktfliser" >}}
{{< /img-row >}}

### Triggers

Der skulle også opsættes 5 triggers for kunden. Jeg kunne, for at lætte arbejdsbyrden, genbruge allerede opsatte svenske triggers fra en tidligere svensk kunde. 

1. **Base**
2. **Post conversion**
3. **Abandoned cart**
4. **Back in stock**
5. **Price drop**

Base-triggeren er en overordet trigger, som wrapper alle de andre triggers. Her skulle der kodes bl.a. en header med et logo og en footer til e-mailen, og der skulle også indsættes brandfarver.
    
Jeg skulle hente billede fra kundens hjemmeside, og genbruge de samme farver, som kunden allerede havde implementeret på hjemmesiden. Efter jeg havde opsat Base-triggeren, skulle jeg konfigurere de resterende triggers. Der skulle også indsættes svensk tekst i triggersne. Du kan se på disse billeder, hvordan Post Conversion *(første)* og Abandoned Cart *(sidste)* endte med at se ud *(uden header & footer)*:

{{< img-row >}}
	{{< img src="post-conversion-trigger.png" alt="Tekst til post conversion" >}}
	{{< img src="abandoned-card-trigger.png" alt="Tekst til abandoned card" >}}
{{< /img-row >}}

Der skete dog yderligere ændringer i produktfliserne, da kundens Customer Success Manager gerne ville have mindre whitespace mellem titlen på produktet og produktets pris. Ydermere skulle køb-knapperne også være på samme linje, om produktet var på udsalg eller ej. Dette blev selvfølelig fikset hurtigst muligt.

## Afrunding

Alt den viden og erfaring, som jeg fik fra [en tidligere kundeopgaves](/kundeopgave-4) nyhedsbrev, har gjort hele arbejdsprocessen mere overskuelig og forudsigelig. Der har ikke været samme frustrationer igennem udviklingsprocessen af produktflisen til nyhedsbrevet, da jeg vidste, at visse mere moderne CSS-tekonlogier ikke var tilgængelige. At opsætte triggers i et andet sprog er heller ikke kompliceret, hvis man har tekst fra en tidligere kunde, som man kan genbruge.