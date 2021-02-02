---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;mixin;mixins;
solution: Experience Platform
title: Mengsels maken en bewerken in de gebruikersinterface
description: Leer hoe u combinaties maakt en bewerkt in de gebruikersinterface van het Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 0%

---


# Mengsels maken en bewerken in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), zijn de mengen herbruikbare componenten die één of meerdere gebieden bepalen die bepaalde functies zoals persoonlijke details, hotelvoorkeur, of adres uitvoeren. Mixins zijn bedoeld om te worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Een mix definieert met welke klasse(en) deze compatibel is, op basis van het gedrag van de gegevens die de mix vertegenwoordigt (record- of tijdreeks). Dit betekent dat niet alle mengsels beschikbaar zijn voor gebruik met alle klassen.

Adobe Experience Platform biedt een groot aantal standaardmengsels die een groot aantal verschillende gebruiksgevallen voor het in de handel brengen bestrijken. Nochtans, kunt u ook uw eigen douanemengsels tot stand brengen en uitgeven om extra concepten met betrekking tot uw zaken binnen uw schema XDM te bepalen. Deze gids verstrekt een overzicht van om, aangepaste mengen voor uw organisatie in de UI van het Platform tot stand te brengen uit te geven en te beheren.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Verwijs naar [XDM overzicht](../../home.md) voor een inleiding aan de rol van XDM binnen het Experience Platform ecosysteem, en [grondbeginselen van schemacompositie](../../schema/composition.md) voor hoe de mengelingen aan schema&#39;s bijdragen XDM.

Hoewel niet vereist voor deze gids, wordt het geadviseerd dat u het leerprogramma ook [het samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) volgt om zich met de diverse mogelijkheden van [!DNL Schema Editor] vertrouwd te maken.

## Een nieuwe mix maken {#create}

Als u een nieuwe mix wilt maken, moet u eerst een schema selecteren waaraan de mix wordt toegevoegd. U kunt verkiezen om [een nieuw schema te creëren](./schemas.md#create) of [een bestaand schema te selecteren om](./schemas.md#edit) uit te geven.

Als u het schema hebt geopend in [!DNL Schema Editor], selecteert u **[!UICONTROL Add]** naast de sectie [!UICONTROL Mixins] in de linkerrail.

![](../../images/ui/resources/mixins/add-mixin-button.png)

Er wordt een dialoogvenster weergegeven met een lijst bestaande combinaties voor uw organisatie. Selecteer **[!UICONTROL Nieuwe mix maken]** boven in het dialoogvenster. Hier kunt u een **[!UICONTROL Weergavenaam]** en **[!UICONTROL Beschrijving]** voor de mix opgeven. Als u klaar bent, selecteert u **[!UICONTROL Mengsel toevoegen]**.

![](../../images/ui/resources/mixins/create-mixin.png)

De [!DNL Schema Editor] verschijnt weer, met de nieuwe mix die in de linkerspoorstaaf wordt vermeld. Aangezien dit een gloednieuwe mix is, biedt deze momenteel geen velden aan het schema en blijft het canvas daarom ongewijzigd. U kunt nu [velden toevoegen aan de mix](#add-fields).

## Een bestaande mix bewerken {#edit}

>[!NOTE]
>
>Alleen aangepaste mixen die door uw organisatie zijn gedefinieerd, kunnen worden bewerkt.
>
>Als een mixin eenmaal is opgeslagen en in een schema voor gegevensinvoer is gebruikt, kunnen daarna alleen additieve wijzigingen in de mix worden aangebracht. Zie [regels van schemaevolutie](../../schema/composition.md#evolution) voor meer informatie.

Als u een bestaande mix wilt bewerken, moet u eerst een schema openen waarin de mix wordt gebruikt binnen [!DNL Schema Editor]. U kunt [een bestaand schema selecteren om](./schemas.md#edit) uit te geven, of u kunt [een nieuw schema ](./schemas.md#create) tot stand brengen en de mengeling in kwestie toevoegen.

Als u het schema hebt geopend in de editor, kunt u [velden toevoegen aan de mixin](#add-fields).

## Velden toevoegen aan een mix {#add-fields}

Als u velden wilt toevoegen aan een mix in [!DNL Schema Editor], selecteert u eerst de naam van de mix in de linkertrack en selecteert u vervolgens het pictogram **plus (+)** naast de naam van het schema op het canvas.

![](../../images/ui/resources/mixins/add-field-button.png)

Er verschijnt een **[!UICONTROL Nieuw veld]** op het canvas en de juiste updates per spoor om besturingselementen weer te geven waarmee de eigenschappen van het veld worden geconfigureerd. Zie de gids op [het bepalen van gebieden in UI](../fields/overview.md#define) voor specifieke stappen op om het gebied aan de mixin te vormen en toe te voegen.

Voeg zoveel velden toe als nodig zijn voor de mix. Als u klaar bent, selecteert u **[!UICONTROL Opslaan]** om zowel het schema als de mix op te slaan.

![](../../images/ui/resources/mixins/complete-mixin.png)

Als dezelfde mix al in andere schema&#39;s wordt gebruikt, worden de toegevoegde velden automatisch in die schema&#39;s weergegeven.

## Volgende stappen

Deze gids besprak hoe te om mengen tot stand te brengen en uit te geven gebruikend het Platform UI. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie [[!UICONTROL Schemas] werkruimteoverzicht](../overview.md).

Zie [Mixins eindpunthulplijn](../../api/mixins.md) voor meer informatie over het beheren van mixins met de [!DNL Schema Registry]-API.