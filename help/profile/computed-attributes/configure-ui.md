---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Hoe te om een Berekend Veld van Attributen te vormen
topic-legacy: guide
type: Documentation
description: Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit veld kan worden gemaakt met een mix om het veld toe te voegen aan een bestaand schema of door een veld te selecteren dat u al in een schema hebt gedefinieerd.
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---


# (Alpha) vorm een gegevens verwerkt attributengebied in UI

>[!IMPORTANT]
>
>De functie voor berekende kenmerken bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit veld kan worden gemaakt met een mix om het veld toe te voegen aan een bestaand schema of door een veld te selecteren dat u al in een schema hebt gedefinieerd.

>[!NOTE]
>
>Berekende kenmerken kunnen niet worden toegevoegd aan velden binnen door Adobe gedefinieerde combinaties. Het veld moet zich binnen de naamruimte `tenant` bevinden. Dit betekent dat het een veld moet zijn dat u definieert en toevoegt aan een schema.

Om een gegevens verwerkt attributengebied met succes te bepalen, moet het schema voor [!DNL Profile] worden toegelaten en als deel van het verenigingsschema voor de klasse verschijnen waarop het schema wordt gebaseerd. Voor meer informatie over [!DNL Profile]-Toegelaten schema&#39;s en vakbonden, te herzien gelieve de sectie van de [!DNL Schema Registry] sectie van de ontwikkelaarsgids op [toelatend een schema voor Profiel en het bekijken verenigingsschema&#39;s](../../xdm/api/getting-started.md). Het wordt ook geadviseerd om de [sectie over union](../../xdm/schema/composition.md) in de documentatie van de schemacompositie te herzien basiscs.

Het werkschema in deze zelfstudie gebruikt een [!DNL Profile]-Toegelaten schema en volgt de stappen voor het bepalen van een nieuwe mengeling die het gegevens verwerkte attributengebied bevat en ervoor zorgt dat het correcte namespace is. Als u reeds een gebied hebt dat in correcte namespace binnen een profiel-toegelaten schema is, kunt u aan de stap voor [het creëren van een gegevens verwerkt attribuut](#create-a-computed-attribute) direct te werk gaan.

## Een schema weergeven

De stappen die volgen gebruiken het gebruikersinterface van Adobe Experience Platform om van een schema de plaats te bepalen, een mengeling toe te voegen, en een gebied te bepalen. Als u liever de [!DNL Schema Registry] API gebruikt, raadpleegt u de [Handleiding voor ontwikkelaars van het schemeregister](../../xdm/api/getting-started.md) voor stappen over hoe u een mix maakt, een mix aan een schema toevoegt en een schema voor gebruik met [!DNL Real-time Customer Profile] inschakelt.

Klik in de gebruikersinterface op **[!UICONTROL Schemas]** in de linkertrack en gebruik de zoekbalk op het tabblad **[!UICONTROL Browse]** om snel het schema te zoeken dat u wilt bijwerken.

![](../images/computed-attributes/Schemas-Browse.png)

Zodra u het schema hebt gevestigd, klik zijn naam om [!DNL Schema Editor] te openen waar u uitgeeft aan het schema kunt maken.

![](../images/computed-attributes/Schema-Editor.png)

## Een mix maken

Als u een nieuwe mix wilt maken, klikt u op **[!UICONTROL Add]** naast **[!UICONTROL Mixins]** in de sectie **[!UICONTROL Composition]** links in de editor. Hiermee opent u het dialoogvenster **[!UICONTROL Add mixin]** waarin u bestaande mixen kunt zien. Klik op het keuzerondje voor **[!UICONTROL Create new mixin]** om de nieuwe mix te definiëren.

Geef de mix een naam en een beschrijving en klik op **[!UICONTROL Add mixin]** wanneer deze is voltooid.

![](../images/computed-attributes/Add-mixin.png)

## Een veld voor berekende kenmerken toevoegen aan het schema

Uw nieuwe mix moet nu worden weergegeven in de sectie &quot;[!UICONTROL Mixins]&quot; onder &quot;[!UICONTROL Composition]&quot;. Klik op de naam van de mixin en meerdere **[!UICONTROL Add field]** knoppen worden weergegeven in de sectie **[!UICONTROL Structure]** van de editor.

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