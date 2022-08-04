---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui guide;mapper;mapping;data prep;data voorbereiden;voorbereiden van gegevens;
solution: Experience Platform
title: Overzicht van Data Prep
topic-legacy: overview
description: Dit document introduceert Data Prep in Adobe Experience Platform.
exl-id: f15eeb50-a531-4560-a524-1a670fbda706
source-git-commit: 7042c6f5e3061fee7183b1befa447333f116c125
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 0%

---


# Overzicht van Data Prep

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model). De Prep van gegevens verschijnt als &quot;Kaart&quot;stap in de processen van de Ingestie van Gegevens, met inbegrip van CSV Ingestiewerkschema. De ingenieurs van gegevens kunnen Prep van Gegevens gebruiken om de volgende gegevensmanipulatie tijdens opname uit te voeren:

- Eenvoudige doorvoertoewijzingen definiëren om invoerkenmerken toe te wijzen aan XDM-kenmerken
- Berekende velden maken voor het uitvoeren van berekeningen in rijen die kunnen worden toegewezen aan XDM-kenmerken
- Transformeer de gegevens door tekenreeks-, numerieke of datummanipulatiefuncties toe te passen
- XDM-hiërarchieën maken met behulp van hiërarchische functies
- Een voorvertoning weergeven van de gegevens terwijl deze worden bewerkt in Voorvertoning gegevens

De Prep van gegevens past verscheidene intrinsieke gegevensbevestigingen toe om ervoor te zorgen dat de gegevensintegriteit wordt gehandhaafd aangezien het wordt opgenomen. Waar mogelijk worden met Gegevensvoorbeeld de inkomende gegevensschema&#39;s automatisch toegewezen aan XDM. De ingenieurs van gegevens kunnen, de voorgestelde afbeeldingen veranderen verbeteren en schrappen en hen vervangen met de afbeeldingen zoals aangewezen.

>[!NOTE]
>
>Tenzij het resulterende bericht ongeldige XDM zal zijn, zullen om het even welke transformatiefouten in Prep van Gegevens in die attributen resulteren die worden geplaatst aan `null`, terwijl de rest van de rij wordt ingeslikt. Als de rij wordt omgezet in ongeldige XDM, wordt de rij **niet** worden opgenomen. In beide gevallen wordt de fout gedocumenteerd.

## Toewijzing

Een afbeelding is een koppeling van een invoerkenmerk of berekend veld naar één XDM-kenmerk. Eén kenmerk kan aan meerdere XDM-kenmerken worden toegewezen door afzonderlijke toewijzingen te maken.

Lees voor meer informatie over de verschillende toewijzingsfuncties de [handleiding voor toewijzingsfuncties](./functions.md).

### Berekende velden

Met berekende velden kunnen waarden worden gemaakt op basis van de kenmerken in het invoerschema. Deze waarden kunnen vervolgens aan kenmerken in het doelschema worden toegewezen en een naam en beschrijving worden gegeven om de referentie eenvoudiger te maken.

Lees voor meer informatie over berekende velden de [hulplijn voor berekende velden](./functions.md#calculated-fields).

### Speciale tekens voor Escape

U kunt speciale tekens in een veld laten ontsnappen door `${...}`. JSON-bestanden die echter velden met een punt (`.`) worden niet ondersteund door dit mechanisme. Wanneer het in wisselwerking staan met hiërarchieën, als een kindattribuut een periode (`.`), moet u een backslash gebruiken (`\`) gebruiken om speciale tekens te verwijderen. Bijvoorbeeld: `address` is een object dat het kenmerk bevat `street.name`, dan kan worden verwezen naar `address.street\.name` in plaats van `address.street.name`.

## Toewijzingsset

Een reeks afbeeldingen die een schema in een ander schema omzetten, wordt samen een toewijzingsset genoemd. Er wordt één toewijzingenset gemaakt als onderdeel van elke gegevensstroom. Een toewijzingenset is een integraal onderdeel van de gegevensstromen en wordt gemaakt, bewerkt en bewaakt als onderdeel van de gegevensstromen.

Als u meer wilt weten over toewijzingssets, zoals het gebruik van de velden in een toewijzingsset, leest u de [hulplijn voor toewijzingenset](./mapping-set.md). Als u wilt leren hoe u een toewijzingenset maakt en andere API-aanroepen kunt gebruiken die betrekking hebben op toewijzingssets, leest u de sectie voor de toewijzingenset in het dialoogvenster [ontwikkelaarsgids](./api/mapping-set.md).

## Gegevensverwerking

De Prep van gegevens kan robuust verschillende formaten van gegevens behandelen die in Platform worden opgenomen. Als u meer wilt weten over de manier waarop Data Prep omgaat met verschillende gegevenstypen, leest u de [overzicht van de verwerking van gegevensformaten](./data-handling.md).

## gedeeltelijke rijupdates verzenden met [!DNL Data Prep]

Streaming updates in [!DNL Data Prep] staat u toe om gedeeltelijke rijupdates te verzenden naar [!DNL Profile Service] gegevens te maken en nieuwe identiteitskoppelingen te maken met één API-aanvraag. Meer informatie over het streamen van upserts in [!DNL Data Prep], zie het document op [gedeeltelijke rijupdates verzenden](./upserts.md).

## Op kenmerken gebaseerd toegangsbeheer in [!DNL Data Prep]

Met toegangsbeheer op basis van kenmerken in Adobe Experience Platform kunnen beheerders de toegang tot specifieke objecten en/of mogelijkheden beheren op basis van kenmerken.

Op attribuut-gebaseerde toegangscontrole zorgt ervoor dat u slechts de attributen kunt in kaart brengen die u toegang tot hebt. Kenmerken waartoe u geen toegang hebt, kunnen niet worden gebruikt in doorvoertoewijzingen en berekende velden. Als u dus geen toegang hebt tot een vereist veld, kunt u geen toewijzing opslaan. Bovendien kunt u geen objecten of objectarrays toewijzen als u geen toegang hebt tot een van de onderliggende kenmerken. U kunt echter andere elementen binnen de object- of objectarray afzonderlijk toewijzen.

Zie de [op attributen-gebaseerd toegangsbeheeroverzicht](../access-control/abac/overview.md) voor meer informatie .

## Volgende stappen

In dit document worden de basisbeginselen van Data Prep in Adobe Experience Platform besproken. Voor meer informatie over verschillende toewijzingsfuncties leest u de [handleiding voor toewijzingsfuncties](./functions.md). Als u meer wilt weten over de manier waarop Data Prep omgaat met verschillende gegevenstypen, leest u de [handleiding voor gegevensverwerking](./data-handling.md#dates). Voor meer informatie over het gebruik van de Data Prep API, leest u de [Handleiding voor ontwikkelaars van Data Prep](api/overview.md).
