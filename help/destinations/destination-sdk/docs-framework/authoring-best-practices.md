---
title: Aanbevolen werkwijzen ontwerpen
description: Leer welke regels en tips u moet volgen wanneer u de pagina met doeldocumentatie ontwerpt, om te controleren of deze voldoet aan de kwaliteitsnormen voor Adobe Experience Platform-documentatie.
exl-id: b12059f1-6635-41cd-acc5-6ff471111164
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Aanbevolen werkwijzen ontwerpen

## Overzicht {#overview}

Deze pagina beschrijft regels die u zou moeten volgen wanneer [ creërend uw pagina van de bestemmingsdocumentatie ](./documentation-instructions.md), om ervoor te zorgen dat het aan de normen van de documentatiekwaliteit van Adobe Experience Platform voldoet.

## Algemene richtsnoeren {#general-guidance}

* Wanneer het invullen van het [ malplaatje ](./self-service-template.md) voor uw bestemmingsdocumentatie, verwijs naar de de bijdragegids van Adobe voor informatie over [ het verbinden ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=nl-NL), [ lijsten ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=nl-NL#tables), de [ gesteunde prijsdalingssyntaxis ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=nl-NL), [ het schrijven van begeleiding ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=nl-NL), en meer.
* Plaats geen opmerkingen en schattingen in de productdocumentatie.
* In de documentatie van Experience Platform, gebruiken de schrijvers van Adobe **gewaagde het formatteren** om naar gebruikersinterfacecontroles, als dit te verwijzen:
   * Ga naar **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** en selecteer de tab **[!UICONTROL Catalog]** . Bekijk een voorbeeld van hoe de controles van het gebruikersinterface in a [ bestemmingsleerprogramma ](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=nl-NL#select-destination) worden gedocumenteerd.

## Schrijfstijl

>[!IMPORTANT]
>
>Lees [ het Schrijven begeleiding voor de Documentatie van Adobe ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/general-writing-guidance.html?lang=nl-NL) alvorens u begint de pagina van de bestemmingsdocumentatie te ontwerpen.

* Houd je zinnen kort en kom snel op. Als uw zin langer is dan 20 woorden of meerdere komma&#39;s gebruikt, kunt u het opsplitsen in aparte zinnen. Zinnen van meer dan 20 woorden kunnen vooral lastig zijn voor lezers.
* Wees niet al te beleefd. Vermijd het gebruik van &quot;alstublieft&quot; of &quot;vriendelijk ...&quot; in technische documentatie.

## Koppelen {#linking}

Volg de meegeleverde documentatiesjabloon en bewerk de bestaande koppelingen in de sjabloon niet. Wanneer het omvatten van nieuwe verbindingen, lees [ gebruikend verbindingen in documentatie ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/linking.html?lang=nl-NL) in de bijdragegids.

## Richtlijnen voor branding {#branding}

* AEP is geen algemeen aanvaarde term. Gebruik Adobe Experience Platform voor het eerste gebruik, Experience Platform en Experience Platform.
   * **gebruik niet**: Alvorens u gegevens van AEP naar YourDestination kunt uitvoeren, zorg ervoor u leest en deze eerste vereisten voltooit.
   * **Gebruik**: Alvorens u gegevens van Adobe Experience Platform naar YourDestination kunt uitvoeren, zorg ervoor u leest en deze eerste vereisten voltooit.

## Afbeeldingen en screenshots {#images-and-screenshots}

* Voor informatie over [ hoe te om aan beelden ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/writing-essentials/markdown.html?lang=nl-NL#images) te verbinden, verwijs naar de bijdragegids.
* Wanneer u screenshots gebruikt, dient u ervoor te zorgen dat in uw schermafbeelding het volledige scherm van de gebruikersinterface van Experience Platform wordt vastgelegd.
* Wanneer u afbeeldingen markeert om een bepaald besturingselement of label op de pagina te markeren, probeert u de markeringsstijl te volgen die wordt gebruikt door het Experience Platform-documentatieteam. Bericht hoe op profiel-gebaseerd in [ dit schermafbeelding ](/help/destinations/catalog/cloud-storage/amazon-s3.md#export-type-frequency) wordt benadrukt.
* Gebruik afbeeldingen in de `png` -indeling.
* Gebruik geen genummerde schermafbeeldingen als bestandsnamen. Namen van afbeeldingsbestanden moeten beschrijvend zijn.
   * **gebruikt niet**: `1.png`, `2.png`, `3.png`
   * **Gebruik**: `yourdestination-authentication-details.png`, `yourdestination-destination-details.png`
* Gebruik alt-tekst voor alle afbeeldingen die u aan de documentatie toevoegt en gebruik de juiste grammatica in de alt-tekst.
   * **gebruikt niet**: De details van de bestemmingsverbinding
   * **Gebruik**: Beeld van Experience Platform UI, tonend de details van de bestemmingsverbinding die in worden gevuld.

## Proces {#process}

* Het [ documentatiemalplaatje ](./self-service-template.md) wordt bijgewerkt niet vaak, gebaseerd op partner terugkoppelt. Alvorens u met het ontwerpen van documentatie voor uw bestemming begint, zorg ervoor dat u de [ recentste versie van het malplaatje ](../assets/docs-framework/yourdestination-template.zip) hebt gedownload.
* Auteur de documentatie en creeer het verzoek van de documentatietrek (PR) van een tak in uw vork *buiten de belangrijkste tak*. Verwijs naar voorlegt bestemming voor overzichtssectie wanneer het ontwerpen in de [ interface GitHub ](./use-github-interface-to-create-documentation.md#submit-review) of in [ uw lokaal milieu ](./work-in-local-environment.md#submit-review).
