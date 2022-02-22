---
keywords: doelpersonalisatie; bestemming; doelbestemming ervaringsplatform;doelbestemming adobe;
title: Adobe Target-verbinding
description: Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie- en experimentatiemogelijkheden biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 61a3a05466eca30ba08fcaf32a3f00e0ca49f325
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Adobe Target-verbinding {#adobe-target-connection}

## Overzicht {#overview}

Adobe Target is een toepassing die realtime, door AI aangedreven personalisatie- en experimentatiemogelijkheden biedt voor alle inkomende klantinteracties voor websites, mobiele apps en nog veel meer.

Adobe Target is een personalisatieverbinding in Adobe Experience Platform.

## Vereisten {#prerequisites}

Deze integratie wordt aangedreven door de [Adobe Experience Platform Web SDK](../../../edge/home.md). U moet deze SDK gebruiken om deze bestemming te gebruiken.

## Exporttype {#export-type}

**Profielaanvraag** - u vraagt om alle segmenten die in de Adobe Target-bestemming zijn toegewezen voor één profiel.

## Gebruiksscenario’s {#use-cases}

**Banner homepage aanpassen**

Een huisverhuurbedrijf en verkoopbedrijf willen hun homepage met een banner personaliseren, die op de kwalificaties van het klantensegment in Adobe Experience Platform wordt gebaseerd. Het bedrijf kan selecteren welk publiek een persoonlijke ervaring zou moeten krijgen en hen naar Adobe Target sturen als doelcriterium voor hun Target-aanbieding.

## Verbinden met de bestemming {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informatie over gegevensstroom-id&#39;s"
>abstract="Met deze optie bepaalt u in welke gegevensverzamelingsgegevensstroom de segmenten worden opgenomen in het antwoord op de pagina. Het drop-down menu toont slechts gegevensstromen die de toegelaten bestemmingsconfiguratie hebben. U moet een gegevensstroom vormen alvorens u uw bestemming kunt vormen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en" text="Leer hoe u een gegevensstroom configureert."

>[!IMPORTANT]
>
>Voordat u een [!DNL Adobe Target] verbinding, adviseren wij u onze gids over hoe te lezen [vorm verpersoonlijkingsbestemmingen voor zelfde-pagina en volgende-pagina verpersoonlijking](../../ui/configure-personalization-destinations.md). Deze gids neemt u door de vereiste configuratiestappen voor zelfde-pagina en volgende-paginagrootte het gebruiksgevallen van het verpersoonlijkingsgebruik, over veelvoudige Experience Platforms.

Als u verbinding wilt maken met dit doel, voert u de stappen uit die worden beschreven in het dialoogvenster [zelfstudie over doelconfiguratie](../../ui/connect-destination.md).

Adobe Experience Platform maakt automatisch verbinding met het Adobe Target-exemplaar van uw bedrijf. Er is geen verificatie vereist.

### Verbindingsparameters {#parameters}

while [opzetten](../../ui/connect-destination.md) voor deze bestemming moet u de volgende informatie opgeven:

* **Naam**: Vul de voorkeursnaam voor dit doel in.
* **Beschrijving**: Voer een beschrijving in voor uw bestemming. U kunt bijvoorbeeld opgeven voor welke campagne u deze bestemming wilt gebruiken. Dit veld is optioneel.
* **DataStream-id**: Dit bepaalt in welke gegevensstroom van de Inzameling van Gegevens de segmenten in de reactie op de pagina zullen worden omvat. In het vervolgkeuzemenu worden alleen gegevensstromen weergegeven waarvoor de doelconfiguratie is ingeschakeld. Zie [Een gegevensstroom configureren](../../../edge/fundamentals/datastreams.md) voor meer informatie .

## Segmenten naar dit doel activeren {#activate}

Lezen [Profielen en segmenten activeren om aanvraagdoelen te profileren](../../ui/activate-profile-request-destinations.md) voor instructies bij het activeren van publiekssegmenten aan deze bestemming.

## Geëxporteerde gegevens {#exported-data}

Adobe Target leest profielgegevens van het Adobe Experience Platform Edge Network, zodat er geen gegevens worden geëxporteerd.

## Gegevensgebruik en -beheer {#data-usage-governance}

Alles [!DNL Adobe Experience Platform] de bestemmingen zijn volgzaam met het beleid van het gegevensgebruik wanneer het behandelen van uw gegevens. Voor gedetailleerde informatie over hoe [!DNL Adobe Experience Platform] dwingt gegevensbeheer af, lees de [Overzicht van gegevensbeheer](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
