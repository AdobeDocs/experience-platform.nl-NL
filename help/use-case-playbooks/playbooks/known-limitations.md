---
solution: Experience Platform
title: Bekende beperkingen met afspeelboeken
description: Meer informatie over de bekende problemen en algemene problemen met afspeelboeken en hoe u deze problemen kunt oplossen
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: e24334bb4ac788770abe20ec2324efa1e64bc0e8
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Bekende beperkingen {#known-limitations}

Leer hoe te om fouten problemen op te lossen wanneer het werken met de Hoofdletters van het Gebruik en de bekende beperkingen van de algemene beschikbaarheidsversie begrijpen.

## Bekende beperkingen

Er worden een aantal bekende beperkingen weergegeven wanneer u een instantie van een afspeelboek maakt en elementen genereert.

* Voor geproduceerde schema&#39;s, als een schema in één geval van playbook wordt geproduceerd, en u het uitgeeft, dan zal een ander schema *niet* worden geproduceerd als u een andere instantie van playbook toelaat. Gebruik in plaats daarvan ook het schema dat u in de instantie hebt bewerkt.

* Wanneer het gebruiken van de [&#x200B; functionaliteit van het gegevensbewustzijn &#x200B;](/help/use-case-playbooks/playbooks/data-awareness.md) om het schema van de inspirerende zandbak aan de ontwikkelingszandbak te bevorderen, zou u sommige fouten kunnen zien gelijkend op hieronder:

![&#x200B; Fouten die in het werkschema van de schemaafbeelding worden getoond.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Dit komt doordat sommige velden die zijn gegenereerd vanuit uw schema, niet aanwezig zijn in het schema in de ontwikkelingssandbox waarnaar u kopieert. Kijk eens wat die velden zijn. Ga vervolgens terug naar de ontwikkelingssandbox waar u kunt:

* Maak een nieuwe veldgroep met die velden of
* Neem in uw schema een standaard, vooraf gedefinieerde veldgroep op die de ontbrekende velden bevat.

Nadat u die gebieden in het schema in de ontwikkelingszandbak omvat, ga terug naar het werkschema om de schemagebieden van de inspirerende zandbak aan de ontwikkelingszandbak te kopiëren. De fouten zijn nu verdwenen.

Bekijk de onderstaande video voor meer informatie om groepen met schemavelden te maken.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
