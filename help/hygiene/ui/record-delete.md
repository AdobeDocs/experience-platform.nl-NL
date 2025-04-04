---
title: Records verwijderen
description: Leer hoe u records verwijdert in de gebruikersinterface van Adobe Experience Platform.
badgeBeta: label="Beta" type="Informative"
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1507'
ht-degree: 0%

---

# Records verwijderen {#record-delete}

Gebruik de [[!UICONTROL Data Lifecycle] werkruimte ](./overview.md) om records in Adobe Experience Platform te verwijderen op basis van hun primaire identiteit. Deze gegevens kunnen worden gekoppeld aan individuele consumenten of aan elke andere entiteit die in de identiteitsgrafiek is opgenomen.

>[!IMPORTANT]
> 
>De eigenschap van de Schrapping van het Verslag is momenteel in Beta en beschikbaar slechts in a **beperkte versie**. Het is niet beschikbaar voor alle klanten. Registratie-verwijderingsverzoeken zijn alleen beschikbaar voor organisaties in de beperkte release.
> 
> 
>Recordverwijderingen moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Zij zijn **niet** om voor de verzoeken van de rechten van gegevenssubject (naleving) zoals met betrekking tot privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) te worden gebruikt. Voor alle gevallen van het nalevingsgebruik, gebruik [ Adobe Experience Platform Privacy Service ](../../privacy-service/home.md) in plaats daarvan.

## Vereisten {#prerequisites}

Voor het verwijderen van records moet u goed begrijpen hoe identiteitsvelden in Experience Platform werken. Specifiek, moet u de waarden van identiteitsnamespace van de entiteiten kennen waarvan verslagen u wilt schrappen, afhankelijk van de dataset (of datasets) u hen van schrapt.

Raadpleeg de volgende documentatie voor meer informatie over identiteiten in Experience Platform:

* [ Dienst van de Identiteit van Adobe Experience Platform ](../../identity-service/home.md): Brugshanden identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden gebaseerd die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [ Identiteit namespaces ](../../identity-service/features/namespaces.md): Identiteitsnaamruimten bepalen de verschillende soorten identiteitsinformatie die op één enkele persoon kunnen betrekking hebben, en een vereiste component voor elk identiteitsgebied zijn.
* [ Real-Time Profiel van de Klant ](../../profile/home.md): Gebruikt identiteitsgrafieken om verenigde consumentenprofielen te verstrekken die op samengevoegde gegevens van veelvoudige bronnen worden gebaseerd, in bijna-real-time wordt bijgewerkt.
* [ Model van de Gegevens van de Ervaring (XDM) ](../../xdm/home.md): Verstrekt standaarddefinities en structuren voor de gegevens van Experience Platform door het gebruik van schema&#39;s. Alle Experience Platform-gegevenssets voldoen aan een specifiek XDM-schema en het schema definieert welke velden id&#39;s zijn.
* [ de gebieden van de Identiteit ](../../xdm/ui/fields/identity.md): Leer hoe een identiteitsgebied in een XDM schema wordt bepaald.

## Een aanvraag maken {#create-request}

Selecteer **[!UICONTROL Data Lifecycle]** in de linkernavigatie van de gebruikersinterface van Experience Platform om het proces te starten. De werkruimte van [!UICONTROL Data lifecycle requests] wordt weergegeven. Selecteer vervolgens **[!UICONTROL Create request]** op de hoofdpagina in de werkruimte.

![ de [!UICONTROL Data lifecycle requests] werkruimte met [!UICONTROL Create request] geselecteerd.](../images/ui/record-delete/create-request-button.png)

De workflow voor het maken van aanvragen wordt weergegeven. Standaard is de optie **[!UICONTROL Delete record]** geselecteerd onder de sectie **[!UICONTROL Requested Action]** . Laat deze optie ingeschakeld.

>[!IMPORTANT]
> 
>Om de efficiency te verbeteren en datasetverrichtingen minder duur te maken, kunnen de organisaties die naar het formaat van Delta zijn verplaatst gegevens van de Dienst van de Identiteit, het Profiel van de Klant in real time, en het gegevenspeer schrappen. Dit type gebruiker wordt aangeduid als delta-migrated. De gebruikers van organisaties die delta-gemigreerd zijn geweest kunnen verkiezen om verslagen van of één of alle datasets te schrappen. Gebruikers van organisaties die geen delta-migratie hebben ondergaan, kunnen niet selectief records uit één gegevensset of alle gegevenssets verwijderen, zoals in de onderstaande afbeelding wordt getoond. In dit geval, blijf aan [ verstrekken identiteiten ](#provide-identities) sectie van de gids.

![ het werkschema van de verzoekverwezenlijking met de [!UICONTROL Delete record] geselecteerde en benadrukte optie.](../images/ui/record-delete/delete-record.png)

## Gegevenssets selecteren {#select-dataset}

De volgende stap is te bepalen of u verslagen van één enkele dataset of alle datasets wilt schrappen. Als deze optie niet beschikbaar aan u is, ga aan [ blijven verstrekken identiteiten ](#provide-identities) sectie van de gids.

Gebruik onder de sectie **[!UICONTROL Record Details]** het keuzerondje om te selecteren tussen een specifieke gegevensset en alle gegevenssets. Als u **[!UICONTROL Select dataset]** kiest, ga te werk om het gegevensbestandpictogram (![ het gegevensbestandpictogram ](/help/images/icons/database.png)) te selecteren om een dialoog te openen die een lijst van beschikbare datasets verstrekt. Selecteer de gewenste gegevensset in de lijst gevolgd door **[!UICONTROL Done]** .

![ de [!UICONTROL Select dataset] dialoog met een geselecteerde dataset en [!UICONTROL Done] benadrukte.](../images/ui/record-delete/select-dataset.png)

Selecteer **[!UICONTROL All datasets]** als u records uit alle gegevenssets wilt verwijderen.

![ de [!UICONTROL Select dataset] dialoog met de [!UICONTROL All datasets] geselecteerde optie.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>Als u de optie **[!UICONTROL All datasets]** selecteert, kan het verwijderen langer duren en wordt de record mogelijk niet correct verwijderd.

## Identiteiten opgeven {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Naamruimte identiteit"
>abstract="Een naamruimte voor identiteiten is een attribuut dat een record koppelt aan het profiel van een consument in Experience Platform. Het naamruimtegebied van de identiteit voor een dataset wordt bepaald door het schema dat de dataset op gebaseerd is. In deze kolom moet u het type (of de naamruimte) opgeven voor de naamruimte van de naam van de record, zoals `email` voor e-mailadressen en `ecid` voor Experience Cloud-id&#39;s. Raadpleeg de gebruikershandleiding bij de levenscyclus van gegevens voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Primaire identiteitswaarde"
>abstract="In deze kolom, moet u de waarde voor de identiteitsnamespace van het verslag verstrekken, die met het identiteitstype moet beantwoorden dat in de linkerkolom wordt verstrekt. Als het naamruimtetype van de identiteit `email` is, moet de waarde het e-mailadres van de record zijn. Raadpleeg de gebruikershandleiding bij de gegevenslevenscyclus voor meer informatie."

Wanneer het schrappen van verslagen, moet u identiteitsinformatie verstrekken zodat kan het systeem bepalen welke verslagen moeten worden geschrapt. Voor om het even welke dataset in Experience Platform, worden de verslagen geschrapt gebaseerd op het **identiteit namespace** gebied dat door het schema van de dataset wordt bepaald.

Zoals alle identiteitsgebieden in Experience Platform, wordt een identiteit namespace samengesteld uit twee dingen: a **type** (soms bedoeld als identiteit namespace) en a **waarde**. Het identiteitstype biedt context voor de manier waarop een record in het veld wordt geïdentificeerd (bijvoorbeeld een e-mailadres). De waarde vertegenwoordigt de specifieke identiteit van een record voor dat type (bijvoorbeeld `jdoe@example.com` voor het `email` identiteitstype). Veelvoorkomende velden die als identiteiten worden gebruikt, zijn accountgegevens, apparaat-id&#39;s en cookie-id&#39;s.

>[!TIP]
>
>Als u de naamruimte voor een bepaalde gegevensset niet kent, kunt u deze vinden in de gebruikersinterface van Experience Platform. Selecteer in de werkruimte **[!UICONTROL Datasets]** de desbetreffende gegevensset in de lijst. Op de detailspagina voor de dataset, houd over de naam van het schema van de dataset in het juiste spoor. De naamruimte voor identiteit wordt samen met de naam en beschrijving van het schema weergegeven.
>
>![ het dashboard van Datasets met een geselecteerde dataset, en een schemadialoog die van het paneel van de Details van de dataset wordt geopend. De primaire identiteitskaart van de dataset wordt benadrukt.](../images/ui/record-delete/dataset-primary-identity.png)

Als u verslagen van één enkele dataset schrapt, moeten alle identiteiten u verstrekt het zelfde type hebben, aangezien een dataset slechts één identiteit namespace kan hebben. Als u van alle datasets schrapt, kunt u veelvoudige identiteitstypes omvatten aangezien de verschillende datasets verschillende primaire identiteiten kunnen hebben.

Er zijn twee opties om id&#39;s op te geven wanneer u records verwijdert:

* [Een JSON-bestand uploaden](#upload-json)
* [Voer handmatig primaire identiteitswaarden in](#manual-identity)

### Een JSON-bestand uploaden {#upload-json}

Als u een JSON-bestand wilt uploaden, kunt u het bestand naar het opgegeven gebied slepen. U kunt ook **[!UICONTROL Choose files]** selecteren om in de lokale map te bladeren en een bestand te selecteren.

![ het werkschema van de verzoekverwezenlijking met de verkies dossiers en belemmering en dalingsinterface voor het uploaden van benadrukte JSON dossiers.](../images/ui/record-delete/upload-json.png)

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
| `value` | De primaire identiteitswaarde zoals die door het type wordt aangegeven. |

Zodra het dossier wordt geupload, kunt u het verzoek [ blijven voorleggen ](#submit).

### Voer identiteiten handmatig in {#manual-identity}

Selecteer **[!UICONTROL Add identity]** als u identiteiten handmatig wilt invoeren.

![ het werkschema van de verzoekverwezenlijking met de [!UICONTROL Add identity] benadrukte optie.](../images/ui/record-delete/add-identity.png)

Er worden besturingselementen weergegeven waarmee u de identiteiten een voor een kunt invoeren. Selecteer het identiteitstype in het keuzemenu onder **[!UICONTROL identity namespace]** . Geef onder **[!UICONTROL Primary Identity Value]** de naamruimtewaarde van de identiteit op voor de record.

![ het werkschema van de verzoekverwezenlijking met manueel toegevoegd identiteitsgebied.](../images/ui/record-delete/identity-added.png)

Om meer identiteiten toe te voegen, selecteer het plusteken (![ A plus pictogram.](/help/images/icons/tree-expand-all.png) ) naast een van de rijen of selecteer **[!UICONTROL Add identity]** .

![ het werkschema van de verzoekverwezenlijking met het plusteken en toevoegt benadrukte identiteitspictogram.](../images/ui/record-delete/more-identities.png)

## De aanvraag verzenden {#submit}

Nadat u de gewenste id&#39;s aan de aanvraag hebt toegevoegd, voert u onder **[!UICONTROL Request settings]** een naam en een optionele beschrijving voor de aanvraag in voordat u **[!UICONTROL Submit]** selecteert.

>[!IMPORTANT]
> 
>Er zijn verschillende limieten voor het totale aantal unieke identiteitsrecords dat elke maand kan worden verzonden. Deze limieten zijn gebaseerd op uw licentieovereenkomst. Organisaties die alle edities van Adobe Real-Time Customer Data Platform of Adobe Journey Optimizer hebben aangeschaft, kunnen maximaal 100.000 identiteitsgegevens verzenden en elke maand verwijderen. De organisaties die **het Schild van de Gezondheidszorg van Adobe** of **de Privacy &amp; het Schild van de Veiligheid van Adobe** hebben gekocht kunnen tot 600.000 identiteitsverslag voorleggen schrapt elke maand.<br> één enkel verslag schrapt verzoek door UI staat u toe om 10.000 IDs in één keer voor te leggen. De [ API methode om verslagen ](../api/workorder.md#create) te schrappen staat voor de voorlegging van 100.000 IDs toe tegelijkertijd.<br> het is beste praktijken om zoveel mogelijk IDs per verzoek, tot uw grens van identiteitskaart voor te leggen. Wanneer u een hoog volume id&#39;s wilt verwijderen, moet u een laag volume of één id per record verwijderen.

![ het verzoek plaatst [!UICONTROL Name] en [!UICONTROL Description] gebieden met [!UICONTROL Submit] benadrukt.](../images/ui/record-delete/submit.png)

Er wordt een dialoogvenster [!UICONTROL Confirm request] weergegeven waarin wordt aangegeven dat de identiteiten niet kunnen worden hersteld nadat ze zijn verwijderd. Selecteer **[!UICONTROL Submit]** om de lijst met identiteiten te bevestigen waarvan u de gegevens wilt verwijderen.

![ de [!UICONTROL Confirm request] dialoog.](../images/ui/record-delete/confirm-request.png)

Nadat de aanvraag is verzonden, wordt een werkorder gemaakt en wordt deze weergegeven op het tabblad [!UICONTROL Record] van de werkruimte van [!UICONTROL Data Lifecycle] . Van hier, kunt u de status van de het werkorde controleren aangezien het het verzoek verwerkt.

>[!NOTE]
>
>Verwijs naar de overzichtssectie op [ chronologie en transparantie ](../home.md#record-delete-transparency) voor details op hoe het verslag schrapt wordt verwerkt zodra zij worden uitgevoerd.

![ het [!UICONTROL Record] lusje van de [!UICONTROL Data Lifecycle] werkruimte met het nieuwe benadrukte verzoek.](../images/ui/record-delete/request-log.png)

## Volgende stappen

In dit document wordt beschreven hoe records in de gebruikersinterface van Experience Platform kunnen worden verwijderd. Voor informatie over hoe te om andere het beheerstaken van de gegevenslevenscyclus in UI uit te voeren, verwijs naar het [ overzicht UI van de Levenscyclus van Gegevens ](./overview.md).

Leren hoe te om verslagen te schrappen gebruikend de Hygiëne API van Gegevens, verwijs naar de [ gids van het het ordeeindpunt van het werk ](../api/workorder.md).
