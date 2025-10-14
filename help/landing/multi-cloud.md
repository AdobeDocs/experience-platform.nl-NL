---
solution: Experience Platform
title: Overzicht van meerdere Adobe Experience Platform-cloud
description: Leer wat de verschillen zijn tussen het uitvoeren van Experience Platform op Microsoft Azure en Amazon Web Services.
source-git-commit: d3654573cec338f173d151fd5e62ef5c8b893c11
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---


# Overzicht van meerdere Adobe Experience Platform-cloud

Adobe Experience Platform is een multi-wolkenproduct, dat u de keus tussen het lopen op [[!DNL Microsoft Azure] geeft &#x200B;](https://azure.microsoft.com/en-us) of [[!DNL Amazon Web Services (AWS)] &#x200B;](https://aws.amazon.com/). Dankzij deze flexibiliteit kunt u kiezen wat het beste past bij uw zakelijke en technische vereisten.

>[!AVAILABILITY]
>
>Adobe Experience Platform die op Amazon Web Services (AWS) wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Neem contact op met het accountteam van uw Adobe voor meer informatie over Experience Platform op AWS.

Deze pagina biedt een overzicht op hoog niveau van de twee beschikbare cloudinfrastructuur en bevat richtlijnen voor het kiezen van de juiste infrastructuur voor uw bedrijf.

## Welke wolkenimplementatie is geschikt voor mij? {#which-cloud-is-right}

De keuze tussen Experience Platform in Azure of AWS is afhankelijk van verschillende factoren die specifiek zijn voor uw bedrijf:

* **Bedrijfs en technische behoeften**: Evalueer de vereisten van uw organisatie en de wolkenstrategie op lange termijn.
* **Bestaande infrastructuur**: Overweeg uw huidige wolkeninfrastructuur en integratiebehoeften.
* **de technologievertrouwen van de Wolk**: Als uw zaken sterk op de technologieën van Microsoft baseert, zou Azure beter kunnen zijn passen. Als je meer vertrouwt op Amazon services, kan AWS de beste optie zijn.
* **de residentieoverwegingen van Gegevens**: Evalueer de vereisten van de gegevensingezetenschap voor uw organisatie en verzeker het gekozen wolkenplatform gebieden aanbiedt die aan deze verordeningen voldoen.

Gezien de bovenstaande factoren, gebruik deze vereenvoudigde beslissingstructuur om te helpen beslissen over de juiste cloud-implementatie voor uw bedrijfsbehoeften.

![&#x200B; Beeld dat de geografische distributie van het ontvangen plaatsen toont.](assets/multi-cloud/diagram-cloud.png){align="center" zoomable="yes"}

## Hostlocaties {#available-cloud-regions}

Het kiezen van de juiste wolkenregio is van cruciaal belang om te voldoen aan de vereisten voor gegevensresistentie en om optimale prestaties te garanderen.

![&#x200B; Beeld dat de geografische distributie van het ontvangen plaatsen toont.](assets/multi-cloud/hosting-locations-map.png){align="center" zoomable="yes"}

Het Experience Platform is beschikbaar in zes Microsoft Azure het ontvangen plaatsen, één Amazon Web Services (AWS) het ontvangen plaats, en routegegevens aan de diensten van Adobe door zeven [&#x200B; Edge Network knopen &#x200B;](../collection/home.md#edge) die over de wereld worden verdeeld.

### Microsoft Azure-regio&#39;s {#azure-regions}

De onderstaande tabel geeft de Microsoft Azure-regio&#39;s aan waar Experience Platform wordt gehost.

| Land | Gebiedscode | Locatie |
|---------|-------------|----------|
| Verenigde Staten | VA7 | Virginia |
| Verenigd Koninkrijk | GBR9 | Londen |
| Nederland | NDL2 | Amsterdam |
| Canada | CAN2 | Toronto |
| India | IND2 | Maharashtra |
| Australië | AUS5 | New South Wales |

{style="table-layout:auto"}

### Amazon Web Services (AWS)-regio&#39;s {#aws-regions}

In de onderstaande tabel worden de AWS-gebieden aangegeven waar Experience Platform wordt gehost. Controleer regelmatig of er extra locaties zijn toegevoegd.

| Land | Gebiedscode | Locatie |
|---------|-------------|----------|
| Verenigde Staten | VA6 | Virginia |

{style="table-layout:auto"}

## pariteit onderdeel {#feature-parity}

De Adobe streeft ernaar om functiepariteit aan te bieden op cloudplatforms, voor alle toepassingen die op het Experience Platform worden uitgevoerd, zoals:

* [Real-Time Customer Data Platform](../rtcdp/home.md)
* [&#x200B; Adobe Journey Optimizer &#x200B;](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/ajo-home)
* [Customer Journey Analytics](https://experienceleague.adobe.com/nl/docs/analytics-platform/using/cja-landing)

Bepaalde functies kunnen echter afwijken voor de implementaties van Azure en AWS. Deze verschillen worden beschreven in de onderstaande sectie en in andere delen van de productdocumentatie, indien van toepassing.

### Verschillen tussen het uitvoeren van Experience Platform op Microsoft Azure en AWS {#azure-aws-differences}

In de onderstaande tabel worden de belangrijkste verschillen aangegeven tussen het uitvoeren van Experience Platform op Microsoft Azure en AWS.

| Functionaliteit | Microsoft Azure | Amazon Web Services |
| --- | --- | --- |
| [&#x200B; naleving van HIPAA &#x200B;](https://www.adobe.com/trust/compliance/hipaa-ready.html) | Ondersteund | Niet ondersteund |
| [&#x200B; Catalogus van bronschakelaars &#x200B;](/help/sources/home.md) | Alle connectors in de broncatalogus worden ondersteund | Een beperkt aantal bronschakelaars is beschikbaar. Om het even welke bronschakelaars beschikbaar voor de implementaties van AWS worden geroepen uit in een top-of-page nota in hun respectieve documentatiepagina&#39;s. |

{style="table-layout:auto"}

<!-- To be determined if we need to add this part about the AI Assistant 

| [Experience Platform AI Assistant](/help/ai-assistant/home.md) | Supported | Not supported |

-->

## Conclusie {#conclusion}

Experience Platform biedt flexibiliteit en keuzemogelijkheden door u de mogelijkheid te bieden om op Microsoft Azure of Amazon Web Services te draaien. Evalueer uw bedrijfsbehoeften en bestaande infrastructuur om een geïnformeerde beslissing te nemen over welk cloudplatform moet worden gebruikt.
