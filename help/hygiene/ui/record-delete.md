---
title: Records verwijderen
description: Leer hoe u records verwijdert in de gebruikersinterface van Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
hide: true
hidefromtoc: true
source-git-commit: a20afcd95d47e38ccdec9fba9e772032e212d7a4
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 0%

---

# Records verwijderen

De [[!UICONTROL Data Hygiene] werkruimte](./overview.md) in Adobe Experience Platform UI staat u toe om verslagen te schrappen die aan de Dienst van de Identiteit en het Profiel van de Klant in real time deelnemen. Deze gegevens kunnen worden gekoppeld aan individuele consumenten of aan elke andere entiteit die in de identiteitsgrafiek is opgenomen.

>[!IMPORTANT]
>
>Aanvragen voor het verwijderen van records zijn alleen beschikbaar voor organisaties die deze hebben aangeschaft **Adobe Healthcare Shield**.
>
>
>Gegevens verwijderen uit records moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Ze zijn **niet** te gebruiken voor verzoeken om rechten van betrokkenen (naleving) met betrekking tot privacyvoorschriften zoals de algemene gegevensbeschermingsverordening (GDPR). Gebruik voor alle gevallen waarin aan de eisen wordt voldaan [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) in plaats daarvan.

## Vereisten

Voor het verwijderen van records moet u goed begrijpen hoe identiteitsvelden in Experience Platform werken. Specifiek, moet u de primaire identiteitswaarden van de entiteiten kennen waarvan verslagen u wilt schrappen, afhankelijk van de dataset (of datasets) u hen van schrapt.

Raadpleeg de volgende documentatie voor meer informatie over identiteiten in Platform:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden bepaald die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
   * [Identiteitsnaamruimten](../../identity-service/namespaces.md): Naamruimten definiëren de verschillende typen identiteitsgegevens die betrekking kunnen hebben op één persoon en die een vereiste component zijn voor elk identiteitsveld.
* [Klantprofiel in realtime](../../profile/home.md): Gebruikt identiteitsgrafieken om verenigde consumentenprofielen te verstrekken die op samengevoegde gegevens van veelvoudige bronnen worden gebaseerd, die in bijna-real-time worden bijgewerkt.
* [Experience Data Model (XDM)](../../xdm/home.md): Verstrekt standaarddefinities en structuren voor Platform gegevens door het gebruik van schema&#39;s. Alle datasets van het Platform zijn in overeenstemming met een specifiek schema XDM, en het schema bepaalt welke gebieden identiteiten zijn.
   * [Identiteitsvelden](../../xdm/ui/fields/identity.md): Leer hoe een identiteitsgebied in een XDM schema wordt bepaald.

## Een nieuwe aanvraag maken

Selecteer **[!UICONTROL Create request]** van de hoofdpagina in de werkruimte.

![Afbeelding die de [!UICONTROL Create request] knop die wordt geselecteerd](../images/ui/record-delete/create-request-button.png)

Het dialoogvenster Aanvragen wordt geopend. Standaard worden de **[!UICONTROL Delete consumer]** optie is geselecteerd onder de optie **[!UICONTROL Requested Action]** sectie. Laat deze optie ingeschakeld.

![Afbeelding waarin de optie Consumenten verwijderen wordt weergegeven die is geselecteerd in het dialoogvenster Maken](../images/ui/record-delete/consumer-action.png)

## Gegevenssets selecteren

Onder de **[!UICONTROL Consumer Details]** sectie, de volgende stap is te bepalen of u verslagen van één enkele dataset of alle datasets wilt schrappen.

Als u **[!UICONTROL Select dataset]**, selecteert u het databasepictogram (![Afbeelding van het databasepictogram](../images/ui/record-delete/database-icon.png)) en er wordt een dialoogvenster weergegeven waarin u de gewenste gegevensset in de lijst kunt selecteren.

![Afbeelding die het dialoogvenster voor de selectie van gegevenssets weergeeft](../images/ui/record-delete/select-dataset.png)

Als u records uit alle gegevenssets wilt verwijderen, selecteert u **[!UICONTROL All datasets]**.

![Afbeelding die de [!UICONTROL All datasets] optie geselecteerd](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Het selecteren van **[!UICONTROL All datasets]** Deze optie kan ertoe leiden dat het verwijderen langer duurt en dat het verwijderen van records mogelijk niet correct verloopt.

## Identiteiten opgeven {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Primaire identiteit"
>abstract="Een primaire identiteit is een kenmerk dat een record koppelt aan het profiel van een consument in Experience Platform. Het primaire identiteitsgebied voor een dataset wordt bepaald door het schema dat de dataset op gebaseerd is. In deze kolom moet u het type (of de naamruimte) opgeven voor de primaire identiteit van de record, zoals `email` voor e-mailadressen en `ecid` voor Experience Cloud-id&#39;s. Meer leren, zie de gids UI van de Hygiëne van Gegevens."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Identiteitswaarde"
>abstract="In deze kolom, moet u de waarde voor de primaire identiteit van het verslag verstrekken, die met het identiteitstype moet beantwoorden dat in de linkerkolom wordt verstrekt. Als het primaire identiteitstype `email`, moet de waarde het e-mailadres van de record zijn. Raadpleeg de gebruikershandleiding voor gegevenshygiëne voor meer informatie."

Wanneer het schrappen van verslagen, moet u identiteitsinformatie verstrekken zodat kan het systeem bepalen welke verslagen moeten worden geschrapt. Voor om het even welke dataset in Platform, worden de verslagen geschrapt gebaseerd op **primaire identiteit** gebied dat door het schema van de dataset wordt bepaald.

Zoals alle identiteitsgebieden in Platform, bestaat een primaire identiteit uit twee dingen: a **type** (wordt soms ook wel naamruimte voor identiteit genoemd) en een **value**. Het identiteitstype biedt context voor de manier waarop het veld een record identificeert (zoals een e-mailadres) en de waarde vertegenwoordigt de specifieke identiteit van een record voor dat type (bijvoorbeeld `jdoe@example.com` voor de `email` type identiteit). Veelvoorkomende velden die als identiteiten worden gebruikt, zijn accountgegevens, apparaat-id&#39;s en cookie-id&#39;s.

>[!TIP]
>
>Als u niet de primaire identiteit voor een bepaalde dataset kent, kunt u het in het Platform UI vinden. In de **[!UICONTROL Datasets]** in de werkruimte, selecteert u de desbetreffende gegevensset in de lijst. Op de detailspagina voor de dataset, houd over de naam van het schema van de dataset in het juiste spoor. De primaire identiteit wordt samen met de schemanaam en beschrijving getoond.
>
>![Beeld dat de primaire identiteit van een dataset toont die in UI wordt benadrukt](../images/ui/record-delete/dataset-primary-identity.png)

Als u verslagen van één enkele dataset schrapt, moeten alle identiteiten u verstrekt het zelfde type hebben, aangezien een dataset slechts één primaire identiteit kan hebben. Als u van alle datasets schrapt, kunt u veelvoudige identiteitstypes omvatten aangezien de verschillende datasets verschillende primaire identiteiten kunnen hebben.

Er zijn twee opties om id&#39;s op te geven wanneer u records verwijdert:

* [Een JSON-bestand uploaden](#upload-json)
* [Identiteitswaarden handmatig invoeren](#manual-identity)

### Een JSON-bestand uploaden {#upload-json}

Als u een JSON-bestand wilt uploaden, kunt u het bestand naar het desbetreffende gebied slepen of **[!UICONTROL Choose files]** om in uw lokale map te bladeren en te selecteren.

![Afbeelding die de methoden voor het uploaden van JSON in de gebruikersinterface weergeeft](../images/ui/record-delete/upload-json.png)

Het JSON-bestand moet zijn opgemaakt als een array van objecten, elk object dat een identiteit vertegenwoordigt.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Eigenschap | Beschrijving |
| --- | --- |
| `namespaceCode` | Het identiteitstype. |
| `value` | De identiteitswaarde zoals aangegeven door het type. |

Nadat het bestand is geüpload, kunt u doorgaan [het verzoek indienen](#submit).

### Identiteiten handmatig invoeren {#manual-identity}

Selecteer **[!UICONTROL Add identity]**.

![Afbeelding die de [!UICONTROL Add identity] knop die wordt geselecteerd](../images/ui/record-delete/add-identity.png)

Er worden besturingselementen weergegeven waarmee u de identiteiten een voor een kunt invoeren. Onder **[!UICONTROL Primary Identity]** selecteert u het identiteitstype in het vervolgkeuzemenu. Onder **[!UICONTROL Identity Value]** geeft u de primaire identiteitswaarde voor de record op.

![Afbeelding met een handmatig toegevoegd identiteitsveld](../images/ui/record-delete/identity-added.png)

Als u meer identiteiten wilt toevoegen, selecteert u het plusteken (![Afbeelding van het plusteken](../images/ui/record-delete/plus-icon.png)) naast een van de rijen, of selecteer **[!UICONTROL Add identity]**.

![Afbeelding die laat zien hoe u meer id&#39;s aan de aanvraag kunt toevoegen](../images/ui/record-delete/more-identities.png)

## Verzend het verzoek (#submit)

Als u klaar bent met het toevoegen van identiteiten aan het verzoek, onder **[!UICONTROL Request settings]** Geef een naam en een optionele beschrijving voor de aanvraag op voordat u deze selecteert **[!UICONTROL Submit]**.

![Afbeelding die de [!UICONTROL Submit] knop die wordt geselecteerd](../images/ui/record-delete/submit.png)

U wordt gevraagd de lijst met identiteiten te bevestigen waarvan u de gegevens wilt verwijderen. Selecteren **[!UICONTROL Submit]** om uw selectie te bevestigen.

![Afbeelding met bevestigingsvenster](../images/ui/record-delete/confirm-request.png)

Nadat het verzoek is verzonden, wordt een werkorder gemaakt en wordt deze weergegeven op het tabblad [!UICONTROL Consumer] tabblad van het dialoogvenster [!UICONTROL Data Hygiene] werkruimte. Van hier, kunt u de status van de het werkorde controleren aangezien het het verzoek verwerkt.

>[!NOTE]
>
>Zie de overzichtssectie over [tijdlijnen en transparantie](../home.md#record-delete-transparency) voor details over hoe verslagen schrapt worden verwerkt zodra zij worden uitgevoerd.

## Volgende stappen

In dit document wordt beschreven hoe records in de gebruikersinterface van het Experience Platform worden verwijderd. Voor informatie over hoe te om andere taken van de gegevenshygiëne in UI uit te voeren, verwijs naar [Overzicht van de interface voor gegevenshygiëne](./overview.md).

Raadpleeg voor meer informatie over het verwijderen van records met de API voor gegevenshygiëne [eindpuntgids voor werkorders](../api/workorder.md).
