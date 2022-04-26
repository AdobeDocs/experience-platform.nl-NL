---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;veldgroep;veldgroepen;
solution: Experience Platform
title: Groep met schemavelden maken en bewerken in de gebruikersinterface
description: Leer hoe u groepen met schemavelden maakt en bewerkt in de gebruikersinterface van het Experience Platform.
topic-legacy: user guide
exl-id: 928d70a6-0468-4fb7-a53a-6686ac77f2a3
source-git-commit: 1d4eba9f566dc1926afd7886c6ad2808ed91ea13
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Groepen schemavelden maken en bewerken in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), zijn de groepen van het schemagebied herbruikbare componenten die één of meerdere gebieden bepalen die bepaalde functies zoals persoonlijke details, hotelvoorkeur, of adres uitvoeren. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Een veldgroep definieert met welke klasse(n) het compatibel is, op basis van het gedrag van de gegevens die de veldgroep vertegenwoordigt (record- of tijdreeks). Dit betekent dat niet alle veldgroepen beschikbaar zijn voor gebruik met alle klassen.

Adobe Experience Platform biedt een groot aantal standaardveldgroepen die een groot aantal gevallen van marketinggebruik bestrijken. U kunt echter ook uw eigen aangepaste veldgroepen maken en bewerken om aanvullende concepten voor uw bedrijf in uw XDM-schema&#39;s te definiëren. Deze gids verstrekt een overzicht van om, aangepaste gebiedsgroepen voor uw organisatie in de UI van het Platform tot stand te brengen uit te geven en te beheren.

## Vereisten

Deze handleiding vereist een goed begrip van XDM System. Zie de [XDM-overzicht](../../home.md) voor een inleiding op de rol van XDM binnen het ecosysteem van het Experience Platform, en [grondbeginselen van de schemacompositie](../../schema/composition.md) voor hoe de gebiedsgroepen aan schema&#39;s XDM bijdragen.

Hoewel dit niet nodig is voor deze handleiding, wordt u aangeraden de zelfstudie ook op te volgen [samenstellen van een schema in UI](../../tutorials/create-schema-ui.md) om de verschillende mogelijkheden van de [!DNL Schema Editor].

## Een nieuwe veldgroep maken {#create}

Als u een nieuwe veldgroep wilt maken, moet u eerst een schema selecteren waaraan de veldgroep wordt toegevoegd. U kunt ervoor kiezen [een nieuw schema maken](./schemas.md#create) of [een bestaand schema selecteren om te bewerken](./schemas.md#edit).

Als u het schema eenmaal hebt geopend in het dialoogvenster [!DNL Schema Editor], selecteert u **[!UICONTROL Add]** naast de [!UICONTROL Field groups] in de linkerspoorstaaf.

![](../../images/ui/resources/field-groups/add-field-group.png)

Er wordt een dialoogvenster weergegeven met een lijst met bestaande veldgroepen voor uw organisatie. Selecteer boven in het dialoogvenster de optie **[!UICONTROL Create new field group]**. Hier kunt u een **[!UICONTROL Display name]** en **[!UICONTROL Description]** voor de veldgroep. Als u klaar bent, selecteert u **[!UICONTROL Add field group]**.

![](../../images/ui/resources/field-groups/create-field-group.png)

De [!DNL Schema Editor] komt opnieuw voor, met de nieuwe veldgroep in de linkerspoorlijn. Aangezien dit een gloednieuwe veldgroep is, biedt deze momenteel geen velden aan het schema en blijft het canvas daarom ongewijzigd. U kunt nu beginnen [velden toevoegen aan de veldgroep](#add-fields).

## Een bestaande veldgroep bewerken {#edit}

>[!NOTE]
>
>Alleen aangepaste veldgroepen die door uw organisatie zijn gedefinieerd, kunnen volledig worden bewerkt en aangepast. Voor kernveldgroepen die door Adobe worden gedefinieerd, kunnen alleen de weergavenamen voor hun velden worden bewerkt binnen de context van afzonderlijke schema&#39;s. Zie de sectie over [weergavenamen voor schemavelden bewerken](./schemas.md#display-names) voor meer informatie.
>
>Nadat een aangepaste veldgroep is opgeslagen en in een schema voor gegevensinvoer is gebruikt, kunnen daarna alleen additieve wijzigingen in de veldgroep worden aangebracht. Zie de [regels voor schemaontwikkeling](../../schema/composition.md#evolution) voor meer informatie .

Als u een bestaande veldgroep wilt bewerken, moet u eerst een schema openen waarin de veldgroep in het dialoogvenster [!DNL Schema Editor]. U kunt [een bestaand schema selecteren om te bewerken](./schemas.md#edit)of u kunt [een nieuw schema maken](./schemas.md#create) en voeg de veldgroep in kwestie toe.

Als u het schema hebt geopend in de editor, kunt u beginnen [velden toevoegen aan de veldgroep](#add-fields).

## Velden toevoegen aan een veldgroep {#add-fields}

>[!NOTE]
>
>Deze sectie richt zich op het toevoegen van velden aan aangepaste veldgroepen. Voor informatie over het toevoegen van aangepaste velden aan standaardveldgroepen raadpleegt u de [UI-hulplijn voor schema&#39;s](./schemas.md#custom-fields-for-standard-groups).

Als u velden wilt toevoegen aan een aangepaste veldgroep in het dialoogvenster [!DNL Schema Editor]selecteert u eerst de naam van de veldgroep in het linkerspoor en selecteert u vervolgens de **plus (+)** op het canvas naast de naam van het schema.

![](../../images/ui/resources/field-groups/add-field.png)

A **[!UICONTROL New field]** verschijnt in het canvas, en de juiste spoorupdates om controles te tonen om de eigenschappen van het gebied te vormen. Zie de handleiding op [velden definiëren in de gebruikersinterface](../fields/overview.md#define) voor specifieke stappen op om het gebied aan de gebiedsgroep te vormen en toe te voegen.

Voeg zo veel velden toe aan de veldgroep. Als u klaar bent, selecteert u **[!UICONTROL Save]** om zowel het schema als de veldgroep op te slaan.

![](../../images/ui/resources/field-groups/complete-field-group.png)

Als dezelfde veldgroep al in andere schema&#39;s wordt gebruikt, worden de toegevoegde velden automatisch in die schema&#39;s weergegeven.

## Volgende stappen

In deze handleiding wordt beschreven hoe u veldgroepen maakt en bewerkt met de gebruikersinterface van het Platform. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] werkruimte, zie [[!UICONTROL Schemas] werkruimte - overzicht](../overview.md).

Leren hoe u veldgroepen kunt beheren met de opdracht [!DNL Schema Registry] API, zie [eindgids voor veldgroepen](../../api/field-groups.md).
