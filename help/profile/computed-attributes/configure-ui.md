---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: Hoe te om een Berekend Veld van Attributen te vormen
type: Documentation
description: Berekende kenmerken zijn functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Om een gegevens verwerkt attribuut te vormen, moet u eerst het gebied identificeren dat de gegevens verwerkte attributenwaarde zal houden. Dit veld kan worden gemaakt met behulp van een schemaveldgroep om het veld toe te voegen aan een bestaand schema of door een veld te selecteren dat u al in een schema hebt gedefinieerd.
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
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
>Berekende kenmerken kunnen niet worden toegevoegd aan velden binnen door Adobe gedefinieerde veldgroepen. Het veld moet zich binnen het `tenant` naamruimte, wat betekent dat het een veld moet zijn dat u definieert en toevoegt aan een schema.

Om een gegevens verwerkt attributengebied met succes te bepalen, moet het schema worden toegelaten voor [!DNL Profile] en worden weergegeven als onderdeel van het samenvoegingsschema voor de klasse waarop het schema is gebaseerd. Voor meer informatie over [!DNL Profile]-enabled schema&#39;s en vakbonden, gelieve te herzien de sectie van [!DNL Schema Registry] ontwikkelaarsgids, sectie over [het toelaten van een schema voor Profiel en het bekijken verenigingsschema&#39;s](../../xdm/api/getting-started.md). Het wordt ook aanbevolen de [vakgebied](../../xdm/schema/composition.md) in de documentatie van de schemacompositie basiscs.

De workflow in deze zelfstudie gebruikt een [!DNL Profile]-enabled schema en volgt de stappen voor het bepalen van een nieuwe gebiedsgroep die het gegevens verwerkte attributengebied bevat en ervoor zorgt dat het correcte namespace is. Als u al een gebied hebt dat in correcte namespace binnen een profiel-toegelaten schema is, kunt u aan de stap rechtstreeks te werk gaan voor [een berekend kenmerk maken](#create-a-computed-attribute).

## Een schema weergeven

In de volgende stappen wordt de Adobe Experience Platform-gebruikersinterface gebruikt om een schema te zoeken, een veldgroep toe te voegen en een veld te definiëren. Als u liever het [!DNL Schema Registry] API, gelieve te verwijzen naar [Handleiding voor ontwikkelaars van het schema Register](../../xdm/api/getting-started.md) voor stappen op hoe te om een gebiedsgroep tot stand te brengen, voeg een gebiedsgroep aan een schema toe en laat een schema voor gebruik toe met [!DNL Real-Time Customer Profile].

Klik in de gebruikersinterface op **[!UICONTROL Schemas]** in het linkerspoor en gebruik de zoekbalk op het **[!UICONTROL Browse]** om snel het schema te zoeken dat u wilt bijwerken.

![](../images/computed-attributes/Schemas-Browse.png)

Als u het schema hebt gevonden, klikt u op de naam van het schema om het dialoogvenster [!DNL Schema Editor] waar u het schema kunt bewerken.

![](../images/computed-attributes/Schema-Editor.png)

## Een veldgroep maken

Als u een nieuwe veldgroep wilt maken, klikt u op **[!UICONTROL Add]** naast **[!UICONTROL Field groups]** in de **[!UICONTROL Composition]** aan de linkerkant van de editor. Hierdoor wordt het **[!UICONTROL Add field group]** waar u bestaande veldgroepen kunt zien. Klik op het keuzerondje voor **[!UICONTROL Create new field group]** om uw nieuwe veldgroep te definiëren.

Geef de veldgroep een naam en een beschrijving en klik op **[!UICONTROL Add field group]** wanneer voltooid.

![](../images/computed-attributes/Add-field-group.png)

## Een berekende kenmerkveld toevoegen aan het schema

Uw nieuwe veldgroep moet nu worden weergegeven in het gedeelte &quot;[!UICONTROL Field groups]&quot; sectie onder &quot;[!UICONTROL Composition]&quot;. Klik op de naam van de veldgroep en meerdere **[!UICONTROL Add field]** knoppen worden weergegeven in het dialoogvenster **[!UICONTROL Structure]** van de editor.

Selecteren **[!UICONTROL Add field]** naast de naam van het schema om een veld op hoofdniveau toe te voegen. U kunt ook opgeven dat u het veld overal in het schema wilt toevoegen.

Na klikken **[!UICONTROL Add field]** er wordt een nieuw object geopend met de naam van uw huurder-id. Dit geeft aan dat het veld zich in de juiste naamruimte bevindt. Binnen dat object kunt u een **[!UICONTROL New field]** wordt weergegeven. Dit als het veld waarin u het berekende kenmerk wilt definiëren.

![](../images/computed-attributes/New-field.png)

## Het veld configureren

Met de **[!UICONTROL Field properties]** aan de rechterkant van de editor geeft u de benodigde informatie voor het nieuwe veld op, zoals de naam, weergavenaam en het type.

>[!NOTE]
>
>Het type voor het veld moet van hetzelfde type zijn als de berekende kenmerkwaarde. Als de berekende kenmerkwaarde bijvoorbeeld een tekenreeks is, moet het veld dat in het schema wordt gedefinieerd, een tekenreeks zijn.

Klik wanneer gereed **[!UICONTROL Apply]** en de naam van het veld en het type worden weergegeven in het dialoogvenster **[!UICONTROL Structure]** van de editor.

![](../images/computed-attributes/Apply.png)

## Schema inschakelen voor [!DNL Profile]

Controleer voordat u doorgaat of het schema is ingeschakeld voor [!DNL Profile]. Klik op de naam van het schema in het dialoogvenster **[!UICONTROL Structure]** van de editor zodat de **[!UICONTROL Schema Properties]** wordt weergegeven. Als de **[!UICONTROL Profile]** schuifregelaar is blauw, het schema is ingeschakeld voor [!DNL Profile].

>[!NOTE]
>
>Een schema inschakelen voor [!DNL Profile] kan niet ongedaan worden gemaakt, dus als u op de schuifregelaar klikt nadat deze is ingeschakeld, hoeft u niet het risico te nemen dat deze wordt uitgeschakeld.

![](../images/computed-attributes/Profile.png)

U kunt nu **[!UICONTROL Save]** om het bijgewerkte schema op te slaan en verder te gaan met de rest van de zelfstudie met behulp van de API.

## Volgende stappen

Nu u een veld hebt gemaakt waarin de berekende kenmerkwaarde wordt opgeslagen, kunt u het berekende kenmerk maken met het `/computedattributes` API-eindpunt. Voer de stappen in het dialoogvenster [API-eindpuntgids voor berekende kenmerken](ca-api.md).