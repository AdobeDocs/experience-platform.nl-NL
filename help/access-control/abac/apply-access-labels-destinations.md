---
title: De toegangslabels van het gebruik om gebruikerstoegang tot bestemmingsdataflows te beheren
description: Leer hoe te om toegangslabels te gebruiken om gebruikerstoegang tot bestemmingsdataflows te beheren zodat slechts een ondergroep van gebruikers in uw organisatie toegang tot specifieke bestemmingsdataflows krijgt.
badgePrivateBeta: label="Private Bèta" type="Informative"
hide: true
hidefromtoc: true
role: Developer, Admin, User
source-git-commit: 5e5dc2f755be0f396dec1d3f19c166bae3bc9575
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---


# De toegangslabels van het gebruik om gebruikerstoegang tot bestemmingsdataflows te beheren

Als onderdeel van het [!UICONTROL Attribute-based access control] in Real-Time CDP kunt u nu toegangslabels toepassen op doelgegevensstromen. Zo zorgt u ervoor dat alleen een subset van gebruikers in uw organisatie toegang krijgt tot specifieke doelgegevens.

Wanneer u een toegangslabel aan een bepaalde bestemming toevoegt, slechts kunnen de gebruikers die toegang tot een rol hebben die dat etiket wordt toegewezen die bestemmingsdataflow zien en uitgeven. Als een bestemmingsdataflow niet met om het even welke etiketten wordt gemerkt, is het zichtbaar aan alle gebruikers die tot uw organisatie behoren.

Lees deze pagina om voorbeelden van gebruiksgevallen, eerste vereisten te begrijpen alvorens u toegangslabels op bestemmingsdataflows kunt toepassen, en andere belangrijke callouts wanneer het gebruiken van deze functionaliteit.

## Vereisten {#prerequisites}

U moet aan de volgende voorwaarden voldoen voordat u deze functionaliteit gaat gebruiken. Ga als volgt te werk om vertrouwd te maken met [!UICONTROL Attribute-based access control] Adobe raadt u ook aan de volgende artikelen te lezen:

* [Overzicht van toegangsbeheer op basis van kenmerken](/help/access-control/abac/overview.md)
* [Op attributen-gebaseerde toegangsbeheergids van begin tot eind](/help/access-control/abac/end-to-end-guide.md)

### Toegang tot de interface voor machtigingen {#access-permissions-ui}

[!UICONTROL Permissions] is het gebied van Experience Cloud waar de beheerders gebruikersrollen en beleid kunnen bepalen om toestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren. Lees de [machtigingensectie](/help/access-control/abac/end-to-end-guide.md#permissions) aan de slag.

### Rollen, labels maken en gebruikers toewijzen {#create-roles-labels-assign-users}

Nadat u toegang hebt gekregen tot de [!UICONTROL permissions] UI, moet u of een lid van uw team opstellingsrollen en de vereiste etiketten toevoegen aan die rollen. Tot slot moeten de gebruikers die tot middelen zouden moeten toegang hebben die met de specifieke etiketten worden geëtiketteerd aan de rol worden toegevoegd. Raadpleeg de volgende secties over documentatie:

* [Een nieuwe rol maken](/help/access-control/abac/ui/roles.md)
* [Labels toevoegen aan een rol](/help/access-control/abac/end-to-end-guide.md#label-roles)
* [Gebruikers aan een rol toevoegen](/help/access-control/ui/users.md)

### Doelgegevens maken {#create-dataflow}

U moet eerst met de gewenste bestemming verbinden en een dataflow creëren om gegevens uit te voeren, alvorens u toegangslabels op dataflow kunt toepassen.

Hulplijnen lezen op [verbinden met een doel](/help/destinations/ui/connect-destination.md) en [gegevens activeren naar het doel](/help/destinations/ui/activation-overview.md). Selecteer vervolgens het gewenste doel in het menu [catalogus van beschikbare aansluitingen](/help/destinations/catalog/overview.md).

## Reeds beschikbaar: Toegangslabels toepassen op andere bronnen van Experience Platforms {#apply-labels-other-resources}

Terwijl deze versie u toelaat om gebruikers objecten-vlakke toegang tot specifieke bestemmingsdataflows te verlenen, is de functionaliteit om toegangsbeheer op een objecten niveau te verlenen reeds algemeen beschikbaar voor andere middelen van het Experience Platform, zoals [publiek](/help/access-control/abac/end-to-end-guide.md#apply-labels-to-segments).

## Voorbeeld van hoofdletters gebruiken {#use-case-example}

Met voorwerp-vlakke toegangsbeheer voor bestemmingen, beperk specifieke teams van marketers om toegang tot hun specifieke slechts bestemmingen te krijgen. Bijvoorbeeld, als uw organisatie klantengegevens in verscheidene geografische plaatsen, zoals de Verenigde Staten en het Verenigd Koninkrijk heeft, kunt u een marketing team beperken om de gegevensstromen voor de plaats van de V.S. slechts te bekijken en uit te geven, en een ander marketing team om de gegevensstromen voor de plaats van het VK te bekijken en uit te geven.

## Toegangslabels toepassen op doelgegevensstromen {#apply-labels-to-destination-dataflow}

Om toegangslabels op een specifieke gegevensstroom toe te passen:

1. Navigeren naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en bepaal de plaats van de bestemmingsgegevensstroom die u de toegang van gebruikers wilt beperken tot.
1. De ovaal selecteren (`...`) in de [!UICONTROL Name] en gebruikt u de ![Detailbesturingselement bewerken](/help/access-control/images/olac/key-icon.svg) **[!UICONTROL Apply access labels]** besturingselement voor het toevoegen van nieuwe labels en het beheren van bestaande labels voor de gegevensstroom.
   ![Selecteer Toegangslabels toepassen in Browse mening van bestemmingswerkruimte.](/help/access-control/images/olac/apply-access-labels.png)
1. Selecteer de labels die u aan de doelgegevensstroom wilt toevoegen en selecteer **[!UICONTROL Save]**.
   ![Selecteer de toegangslabels in die op de bestemmingsgegevensstroom zouden moeten van toepassing zijn.](/help/access-control/images/olac/view-access-labels.png)
1. Bericht hoe dataflow nu een toegangsetiket heeft dat in UI wordt getoond.
   ![De mening van verscheidene bestemmingsgegevens stroomt met de geselecteerde gegevensstroom hoe het tonen van een toegangslabel.](/help/access-control/images/olac/dataflow-with-access-label.png)

Als een doelgegevensstroom niet met om het even welke etiketten wordt gemerkt, zal het voor alle gebruikers tonen. Als de gegevensstroom met één of meerdere toegangslabels duidelijk is, zal het slechts voor gebruikers tonen die tot een rol behoren die het zelfde etiket of de combinatie etiketten heeft.

U kunt standaard- en aangepaste labels toevoegen aan de gegevensstroom van de bestemming. Nadat u een label aan bestemmingsgegevens toevoegt:

* De gebruikers die aan rollen met toegang tot het zelfde etiket worden toegewezen kunnen dataflow met het nieuwe etiket in UI bekijken. Ze kunnen de doelgegevensstroom weergeven en bewerken in de gebruikersinterface of via API&#39;s.

* Gebruikers die *niet* toegewezen aan rollen met toegang tot hetzelfde label hebben geen toegang tot de doelgegevensstroom om deze in de gebruikersinterface of via API&#39;s weer te geven of te bewerken.

## Belangrijke callouts en onderdelen die u moet weten {#important-callouts}

Toegangslabels kunnen momenteel alleen worden toegepast op bestaande gegevensstromen. Dit betekent dat iemand dataflow aan de bestemming moet tot stand brengen alvorens de toegangslabels kunnen worden toegepast.

U kunt geen toegangslabel op een bestemmingsgegevensstroom toepassen als u geen toegang tot dat etiket hebt.

Wanneer het toevoegen van veelvoudige etiketten aan een bestemmingsdataflow, moeten de gebruikers die de dataflow zouden moeten kunnen bekijken en uitgeven aan een rol met minstens de zelfde combinatie etiketten worden toegevoegd. Bijvoorbeeld, als u de etiketten C1, I2, en een ander douanelabel op een bestemmingsdataflow toepast, slechts kunnen de gebruikers die aan rollen met toegang tot de combinatie deze drie etiketten worden toegevoegd deze specifieke bestemmingsdataflow bekijken en uitgeven.

![Een koppelingsdiagram dat aangeeft hoe alleen bepaalde gebruikers toegang hebben tot bestemmingen waarop meerdere labels zijn toegepast.](/help/access-control/images/olac/multiple-labels-venn.png)

## Volgende stappen {#next-steps}

Door de stappen in dit document te volgen, weet u nu hoe te om toegangslabels op bestemmingsdataflows toe te passen zodat slechts een ondergroep van gebruikers in uw organisatie toegang tot specifieke bestemmingsdataflows krijgt.

Vervolgens kunt u meer lezen over andere functies die worden ondersteund door [!UICONTROL Attribute-based access control] wanneer het activeren van gegevens aan bestemmingen. U kunt bijvoorbeeld de toegang van gebruikers beperken tot [alleen specifieke velden weergeven en activeren](/help/access-control/abac/overview.md#destinations).