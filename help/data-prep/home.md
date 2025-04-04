---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui-gids;mapper;mapping;data prep;gegevens voorbereiden;gegevens voorbereiden;
solution: Experience Platform
title: Overzicht van Data Prep
description: Dit document introduceert Data Prep in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 0%

---


# Overzicht van Data Prep

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model). De Prep van gegevens verschijnt als &quot;Kaart&quot;stap in de processen van de Ingestie van Gegevens, met inbegrip van CSV Ingestiewerkschema. De ingenieurs van gegevens kunnen Prep van Gegevens gebruiken om de volgende gegevensmanipulatie tijdens opname uit te voeren:

- Eenvoudige doorvoertoewijzingen definiëren om invoerkenmerken toe te wijzen aan XDM-kenmerken
- Berekende velden maken voor het uitvoeren van berekeningen in rijen die kunnen worden toegewezen aan XDM-kenmerken
- Transformeer de gegevens door tekenreeks-, numerieke of datummanipulatiefuncties toe te passen
- XDM-hiërarchieën maken met behulp van hiërarchische functies
- Een voorvertoning weergeven van de gegevens terwijl deze worden bewerkt in Voorvertoning gegevens

De Prep van gegevens past verscheidene intrinsieke gegevensbevestigingen ook toe om ervoor te zorgen dat de gegevensintegriteit wordt gehandhaafd aangezien het wordt opgenomen. Waar mogelijk worden met Gegevensvoorbeeld de inkomende gegevensschema&#39;s automatisch toegewezen aan XDM. De ingenieurs van gegevens kunnen, de voorgestelde afbeeldingen veranderen verbeteren en schrappen en hen vervangen met de afbeeldingen zoals aangewezen.

>[!NOTE]
>
>Tenzij het resulterende bericht ongeldig XDM zal zijn, zullen om het even welke transformatiefouten in Prep van Gegevens in die attributen resulteren die worden geplaatst aan `null`, terwijl de rest van de rij zal worden opgenomen. Als de rij aan ongeldige XDM oplost, zal de rij **niet** worden opgenomen. In beide gevallen wordt de fout gedocumenteerd.

## Toewijzing

Een afbeelding is een koppeling van een invoerkenmerk of berekend veld naar één XDM-kenmerk. Eén kenmerk kan aan meerdere XDM-kenmerken worden toegewezen door afzonderlijke toewijzingen te maken.

Om meer over de verschillende kaartfuncties te leren, te lezen gelieve de [ gids van de kaartfuncties ](./functions.md).

### Berekende velden

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken. Berekende velden mogen maximaal 4096 tekens lang zijn.

Om meer over berekende gebieden te leren, te lezen gelieve de [ berekende gebiedsgids ](./functions.md#calculated-fields).

### Speciale tekens voor Escape {#escape-special-characters}

Met `${...}` kunt u speciale tekens in een veld verwijderen. JSON-bestanden die velden met een punt (`.`) bevatten, worden echter niet ondersteund door dit mechanisme. Wanneer het in wisselwerking staan met hiërarchieën, als een kindattribuut een periode (`.`) heeft, moet u backslash (`\`) gebruiken om speciale karakters te ontsnappen. `address` is bijvoorbeeld een object dat het kenmerk `street.name` bevat. U kunt dit vervolgens `address.street\.name` in plaats van `address.street.name` noemen.

## Toewijzingsset

Een reeks afbeeldingen die een schema in een ander schema omzetten, wordt samen een toewijzingsset genoemd. Er wordt één toewijzingenset gemaakt als onderdeel van elke gegevensstroom. Een toewijzingenset is een integraal onderdeel van de gegevensstromen en wordt gemaakt, bewerkt en bewaakt als onderdeel van de gegevensstromen.

Om meer over afbeeldingsreeksen, met inbegrip van te leren hoe te om de gebieden binnen een kaartreeks te gebruiken, te lezen gelieve de [ handleiding van de kaartplaatste ](./mapping-set.md). Leren hoe te om een mappingsreeks tot stand te brengen en andere API vraag te gebruiken met betrekking tot mappingsreeksen, gelieve de sectie van de mappingsreeks in de [ ontwikkelaarsgids ](./api/mapping-set.md) te lezen.

## Gegevensverwerking

Data Prep kan op krachtige wijze verschillende gegevensindelingen verwerken die in Experience Platform worden ingevoerd. Om meer over te leren hoe de Prep van Gegevens verschillende gegevenstypes behandelt, te lezen gelieve het [ overzicht van de gegevensformaat behandeling ](./data-handling.md).

## Updates van gedeeltelijke rijen verzenden met [!DNL Data Prep]

Met streaming updates in [!DNL Data Prep] kunt u gedeeltelijke rijupdates naar [!DNL Profile Service] -gegevens verzenden en tegelijkertijd nieuwe identiteitskoppelingen maken en tot stand brengen met één API-aanvraag. Meer over leren hoe te om upserts in [!DNL Data Prep] te stromen, zie het document op [ verzendend gedeeltelijke rijupdates ](./upserts.md).

## Toegangsbeheer op basis van kenmerken in [!DNL Data Prep]

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Op attribuut-gebaseerde toegangscontrole zorgt ervoor dat u slechts de attributen kunt in kaart brengen die u toegang tot hebt. Kenmerken waartoe u geen toegang hebt, kunnen niet worden gebruikt in doorvoertoewijzingen en berekende velden. Als u dus geen toegang hebt tot een vereist veld, kunt u geen toewijzing opslaan. Bovendien kunt u geen objecten of objectarrays toewijzen als u geen toegang hebt tot een van de onderliggende kenmerken. U kunt echter andere elementen binnen de object- of objectarray afzonderlijk toewijzen.

Zie het [ op attributen-gebaseerde overzicht van de toegangscontrole ](../access-control/abac/overview.md) voor meer informatie.

## Volgende stappen

In dit document worden de basisbeginselen van Data Prep in Adobe Experience Platform besproken. Om meer over verschillende kaartfuncties te leren, te lezen gelieve de [ handleiding van toewijzingsfuncties ](./functions.md). Om meer over te leren hoe de Prep van Gegevens verschillende gegevenstypes behandelt, te lezen gelieve de [ gids van de het formaatbehandeling van gegevens ](./data-handling.md#dates). Leren hoe te om de Prep API van Gegevens te gebruiken, te lezen gelieve de [ ontwikkelaarsgids van de Prep van Gegevens ](api/overview.md).
