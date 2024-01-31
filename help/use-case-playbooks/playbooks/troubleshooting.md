---
solution: Experience Platform
title: Bekende beperkingen en problemen met afspeelboeken oplossen
description: Meer informatie over de bekende problemen en algemene problemen met afspeelboeken en hoe u deze problemen kunt oplossen
role: User, Developer, Admin
exl-id: 2604ce26-bcf9-46e1-bc10-30252a113159
source-git-commit: ecce42e2c759bda31bc37d0aae1da2c7b3d141fc
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---


# Problemen oplossen en bekende beperkingen {#troubleshooting-known-limitations}

Leer hoe te om fouten problemen op te lossen wanneer het werken met de Hoofdletters van het Gebruik en de bekende beperkingen van de algemene beschikbaarheidsversie begrijpen.

## Problemen oplossen {#troubleshooting}

Suggesties voor het oplossen van problemen weergeven voor algemene fouten wanneer u werkt met Hoofdletters gebruiken

### Adobe Journey Optimizer-oppervlakken niet geconfigureerd

Wanneer u een instantie van een afspeelboek maakt, wordt mogelijk het onderstaande bericht weergegeven.

![Problemen oplossen](/help/use-case-playbooks/assets/playbooks/troubleshooting/troubleshooting-ajo.png)

Dit komt omdat Journey Optimizer-afspeelboeken berichten maken voor e-mail-, push- en SMS-kanalen. Lees de [Aan de slag](/help/use-case-playbooks/playbooks/get-started.md#configure-sandbox-and-channel-surfaces-in-journey-optimizer) hulplijn voor het configureren van de verschillende oppervlakken.

### Status *mislukt* bij het maken van een nieuwe instantie

Als u een ontbroken bericht ziet wanneer u probeert om een geval tot stand te brengen, zou dit kunnen zijn omdat uw beheerder u niet de vereiste gebruikerstoestemmingen heeft verleend. Een afspeelboek bevat veel verschillende elementen en uw gebruiker heeft machtigingen nodig om deze elementen te maken, zodat de instantie van het afspeelboek correct kan worden gemaakt. Zie de [machtigingen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) in deze handleiding vindt u informatie over het instellen van machtigingen.

## Bekende beperkingen

Er worden een aantal bekende beperkingen weergegeven wanneer u een instantie van een afspeelboek maakt en elementen genereert.

* Voor gegenereerde schema&#39;s geldt dat als een schema wordt gegenereerd in één instantie van een afspeelboek en u het bewerkt, een ander schema *niet* wordt gegenereerd als u een andere instantie van het afspeelboek inschakelt. Gebruik in plaats daarvan ook het schema dat u in de instantie hebt bewerkt.

* Wanneer u de opdracht [functionaliteit voor gegevensbewustzijn](/help/use-case-playbooks/playbooks/data-awareness.md) om het schema van de inspirerende zandbak aan de ontwikkelingszandbak te bevorderen, zou u sommige fouten kunnen zien gelijkend op hieronder:

![Fouten weergegeven in de workflow voor schematoewijzing.](/help/use-case-playbooks/assets/playbooks/troubleshooting/schema-errors.png){width="1000" zoomable="yes"}

Dit komt doordat sommige velden die zijn gegenereerd vanuit uw schema, niet aanwezig zijn in het schema in de ontwikkelingssandbox waarnaar u kopieert. Kijk eens wat die velden zijn. Ga vervolgens terug naar de ontwikkelingssandbox waar u kunt:

* Maak een nieuwe veldgroep met die velden of
* Neem in uw schema een standaard, vooraf gedefinieerde veldgroep op die de ontbrekende velden bevat.

Nadat u die gebieden in het schema in de ontwikkelingszandbak omvat, ga terug naar het werkschema om de schemagebieden van de inspirerende zandbak aan de ontwikkelingszandbak te kopiëren. De fouten zijn nu verdwenen.

Bekijk de onderstaande video voor meer informatie om groepen met schemavelden te maken.

>[!VIDEO](https://video.tv.adobe.com/v/27013/?learn=on)
