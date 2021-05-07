---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Hoe te om een Berekend Veld van Attributen te vormen
topic-legacy: guide
type: Documentation
description: Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit veld kan worden gemaakt met behulp van een schemaveldgroep om het veld toe te voegen aan een bestaand schema of door een veld te selecteren dat u al in een schema hebt gedefinieerd.
translation-type: tm+mt
source-git-commit: 6e0f7578d0818f88e13b963f64cb2de6729f0574
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 0%

---


# (Alpha) vorm een gegevens verwerkt attributengebied in UI

>[!IMPORTANT]
>
>De functie voor berekende kenmerken bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit veld kan worden gemaakt met behulp van een schemaveldgroep om het veld toe te voegen aan een bestaand schema of door een veld te selecteren dat u al in een schema hebt gedefinieerd.

>[!NOTE]
>
>Berekende kenmerken kunnen niet worden toegevoegd aan velden binnen door Adobe gedefinieerde veldgroepen. Het veld moet zich binnen de naamruimte `tenant` bevinden. Dit betekent dat het een veld moet zijn dat u definieert en toevoegt aan een schema.

Om een gegevens verwerkt attributengebied met succes te bepalen, moet het schema voor [!DNL Profile] worden toegelaten en als deel van het verenigingsschema voor de klasse verschijnen waarop het schema wordt gebaseerd. Voor meer informatie over [!DNL Profile]-Toegelaten schema&#39;s en vakbonden, te herzien gelieve de sectie van de [!DNL Schema Registry] sectie van de ontwikkelaarsgids op [toelatend een schema voor Profiel en het bekijken verenigingsschema&#39;s](../../xdm/api/getting-started.md). Het wordt ook geadviseerd om de [sectie over union](../../xdm/schema/composition.md) in de documentatie van de schemacompositie te herzien basiscs.

De workflow in deze zelfstudie gebruikt een schema [!DNL Profile] en volgt de stappen voor het definiëren van een nieuwe veldgroep met het berekende kenmerkveld en het controleren of dit de juiste naamruimte is. Als u reeds een gebied hebt dat in correcte namespace binnen een profiel-toegelaten schema is, kunt u aan de stap voor [het creëren van een gegevens verwerkt attribuut](#create-a-computed-attribute) direct te werk gaan.

## Een schema weergeven

In de volgende stappen wordt de Adobe Experience Platform-gebruikersinterface gebruikt om een schema te zoeken, een veldgroep toe te voegen en een veld te definiëren. Als u liever de [!DNL Schema Registry] API gebruikt, raadpleegt u de [Handleiding voor ontwikkelaars van het schemeregister](../../xdm/api/getting-started.md) voor stappen over het maken van een veldgroep, het toevoegen van een veldgroep aan een schema en het inschakelen van een schema voor gebruik met [!DNL Real-time Customer Profile].

Klik in de gebruikersinterface op **[!UICONTROL Schemas]** in de linkertrack en gebruik de zoekbalk op het tabblad **[!UICONTROL Browse]** om snel het schema te zoeken dat u wilt bijwerken.

![](../images/computed-attributes/Schemas-Browse.png)

Zodra u het schema hebt gevestigd, klik zijn naam om [!DNL Schema Editor] te openen waar u uitgeeft aan het schema kunt maken.

![](../images/computed-attributes/Schema-Editor.png)

## Een veldgroep maken

Als u een nieuwe veldgroep wilt maken, klikt u op **[!UICONTROL Add]** naast **[!UICONTROL Field groups]** in de sectie **[!UICONTROL Composition]** links in de editor. Hiermee opent u het dialoogvenster **[!UICONTROL Add field group]** waarin u bestaande veldgroepen kunt zien. Klik op het keuzerondje voor **[!UICONTROL Create new field group]** om de nieuwe veldgroep te definiëren.

Geef de veldgroep een naam en een beschrijving en klik op **[!UICONTROL Add field group]** wanneer voltooid.

![](../images/computed-attributes/Add-field-group.png)

## Een veld voor berekende kenmerken toevoegen aan het schema

Uw nieuwe veldgroep moet nu worden weergegeven in de sectie &quot;[!UICONTROL Field groups]&quot; onder &quot;[!UICONTROL Composition]&quot;. Klik op de naam van de veldgroep en meerdere **[!UICONTROL Add field]** knoppen worden weergegeven in de sectie **[!UICONTROL Structure]** van de editor.

Selecteer **[!UICONTROL Add field]** naast de naam van het schema om een veld op hoofdniveau toe te voegen, of selecteer deze optie om het veld toe te voegen binnen het schema dat u wilt gebruiken.

Nadat u op **[!UICONTROL Add field]** hebt geklikt, wordt er een nieuw object geopend met de naam van uw huurder-id. Hieruit blijkt dat het veld zich in de juiste naamruimte bevindt. Binnen dat object wordt een **[!UICONTROL New field]** weergegeven. Dit als het veld waarin u het berekende kenmerk wilt definiëren.

![](../images/computed-attributes/New-field.png)

## Het veld configureren

Gebruikend de **[!UICONTROL Field properties]** sectie op de rechterkant van de redacteur, verstrek de noodzakelijke informatie voor uw nieuw gebied, met inbegrip van zijn naam, vertoningsnaam, en type.

>[!NOTE]
>
>Het type voor het veld moet van hetzelfde type zijn als de berekende kenmerkwaarde. Als de berekende kenmerkwaarde bijvoorbeeld een tekenreeks is, moet het veld dat in het schema wordt gedefinieerd, een tekenreeks zijn.

Wanneer gedaan, klik **[!UICONTROL Apply]** en de naam van het gebied, evenals zijn type zal in **[!UICONTROL Structure]** sectie van de redacteur verschijnen.

![](../images/computed-attributes/Apply.png)

## Schema inschakelen voor [!DNL Profile]

Controleer voordat u doorgaat of het schema is ingeschakeld voor [!DNL Profile]. Klik op de schemanaam in **[!UICONTROL Structure]** sectie van de redacteur zodat **[!UICONTROL Schema Properties]** tabel verschijnt. Als de schuifregelaar **[!UICONTROL Profile]** blauw is, is het schema ingeschakeld voor [!DNL Profile].

>[!NOTE]
>
>Het toelaten van een schema voor [!DNL Profile] kan niet ongedaan worden gemaakt, zodat als u op de schuif klikt zodra het is toegelaten, moet u het risico niet het onbruikbaar maken.

![](../images/computed-attributes/Profile.png)

U kunt nu **[!UICONTROL Save]** klikken om het bijgewerkte schema op te slaan en verder te gaan met de rest van de zelfstudie met behulp van de API.

## Volgende stappen

Nu u een gebied hebt gecreeerd waarin uw gegevens verwerkte attributenwaarde zal worden opgeslagen, kunt u de gegevens verwerkte attributen tot stand brengen gebruikend het `/computedattributes` API eindpunt. Voor gedetailleerde stappen aan het creëren van een gegevens verwerkt attribuut in API, volg de stappen die in [gegevens verwerkte attributen API eindpuntgids](ca-api.md) worden verstrekt.