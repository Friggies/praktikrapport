---
title: Introduktion til produktfeed
type: task
dato: 19/1/24
kategorier: [introduktion, produktfeed]
---

## Hvorfor?

Der var ingen vej uden om produktfeeds som praktikant hos [Hello Retail](https://helloretail.com). Det er en så essentiel del af det arbejde, som bliver lavet for kunderne, at man skal kunne tale produktfeed-sproget udenad. Derfor blev der sat et sandkassemiljø op til mig, hvor jeg kunne udforske et produktfeed så meget jeg lystede. I dette miljø var der ingen risiko for at ødelægge noget på eksisterende kunders produktfeed.

## Process

Produktfeeds skulle sættes op i enten Hello Retails interne *Supervisor*-system, eller i deres nyere *Company Land*. Alle nye onboardings skal sættes op det nyere system, men der er stadig mange kunder der bruger det gamle.

### Transform

Efter at have opsat produktfeedet, skulle jeg sætte en produktvej, så jeg kunne tilfå produkterne i selve produktfeedet. For et standard [WooCommerce](https://woo.com) produktfeed er produktvejen `products > product`. Når man så kan nå produkterne, skal man vælge hvilken data, som er relevant at at trække ud af produktfeedet. Produktfeedet finder automatisk de fleste værdier ved hjælp af spread-operatoren og root produktparameteren, men de kan også selv indsættes. Det var det, som jeg først gjorde:

```js
function transform(product:any): TransformationResult {
	return {
		...product, /*auto*/
        /*mine egne*/
		url: product.url,
		productNumber: product.productnumber,
		title: product.title,
		description: product.description,
		imgUrl: product.imgurl,
		price: product.price,
		oldPrice: product.oldPrice,
		inStock: product.instock,
	};
}
```

### Ekstra information

Der er nogle standardvariabler, som bare kan gemmes direkte i produktobjektet, men der er også andre, som skal gemmes i et kontainerobject, som hedder "extraData". Jeg skulle selv finde på noget, som jeg kunne gemme i dette extraData-objekt:

```js
function transform(product:any): TransformationResult {
	return {
		...product, /*auto*/
        /*mine egene ekstra informationer*/
		extraData: {
			sku: product.sku,
			onSale: product.oldPrice !== product.price,
			hasShortDesc: product.description.length < 100,
			priceIsEven: product.price % 2 === 0,
			isCreatedAprilFirst: new Date(product.created).getMonth() === 3 && new Date(product.created).getDate() === 1,
			createdDate: new Date(product.created).toLocaleDateString('da', { weekday:"long", year:"numeric", month:"long", day:"numeric"}),
		}
	};
}
```

Man skal huske på, at extraData kun gemmer string-værdier. Hvis man skal gemme en list af elementer *(array)*, skal det ske i en "extraDataList" i stedet for den normale extraData-objekt.

### Indstillinger

- Planlagte kørsler

    Vi vil gerne have produktfeedet kører så ofte som muligt. Det gør nemlig, at vi hugtigere ved, hvornår produkter bliver tilføjet, udsolgt eller ændret. Normalt sættest det til et interval på én time.

- Tilladelser

    Et primært produktfeed er sat op til både at kunne generere produkter i vores database, og fjerne udgåede produkter fra vores database. Kun ét produktfeed må kunne dette, ellers opstår der problemer, og de ender med at overskrive hinanden. 

## Afrunding

Jeg har før arbejdet med fetched data fra en database, og at arbejde med et produktfeed virker meget sammenligneligt. Det kan være besværligt med uoverskuelige produktfeeds som kan tage timer at køre igennem, men også være enkelt med ordenlig dataopsætning og uden for mange strukturændringer.

Det virker som om at opgavens sværhedsgrad ændre sig i forhold til kvaliteten og strukturen af den data vi modtager fra produktfeedet. Og der kan ikke trylles informationer ud af den blå luft, hvis ikke vi får det i feedet, kan vi ikke bruge det i vores løsninger. Med mindre vi crawler det fra f.eks. produktsiden, men det er meget dårlig praksis *(dog er det nogle gange er det den eneste løsning)*.