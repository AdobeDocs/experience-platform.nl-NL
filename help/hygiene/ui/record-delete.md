---
title: Records verwijderen
description: Leer hoe u records verwijdert in de gebruikersinterface van Adobe Experience Platform.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 6e97b3a6b3830cf88802a8dd89944b6ce8791f02
workflow-type: tm+mt
source-wordcount: '1498'
ht-degree: 0%

---

# [!BADGE Beta]{type=Informative} Records verwijderen {#record-delete}

Gebruik de [[!UICONTROL Data Lifecycle] werkruimte](./overview.md) om records in Adobe Experience Platform te verwijderen op basis van hun primaire identiteit. Deze gegevens kunnen worden gekoppeld aan individuele consumenten of aan elke andere entiteit die in de identiteitsgrafiek is opgenomen.

>[!IMPORTANT]
> 
>De functie Record verwijderen bevindt zich momenteel in de bètaversie en is alleen beschikbaar in een **beperkte release**. Het is niet beschikbaar voor alle klanten. Registratie-verwijderingsverzoeken zijn alleen beschikbaar voor organisaties in de beperkte release.
> 
> 
>Recordverwijderingen moeten worden gebruikt voor het opschonen van gegevens, het verwijderen van anonieme gegevens of het minimaliseren van gegevens. Ze zijn **niet** te gebruiken voor verzoeken om rechten van betrokkenen (naleving) met betrekking tot privacyvoorschriften zoals de algemene gegevensbeschermingsverordening (GDPR). Gebruik voor alle gevallen waarin aan de eisen wordt voldaan [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) in plaats daarvan.

## Vereisten {#prerequisites}

Voor het verwijderen van records moet u goed begrijpen hoe identiteitsvelden in Experience Platform werken. Specifiek, moet u de primaire identiteitswaarden van de entiteiten kennen waarvan verslagen u wilt schrappen, afhankelijk van de dataset (of datasets) u hen van schrapt.

Raadpleeg de volgende documentatie voor meer informatie over identiteiten in Platform:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Bruggen identiteiten over apparaten en systemen, die datasets verbinden samen op de identiteitsgebieden worden gebaseerd die door de schema&#39;s XDM worden bepaald zij met in overeenstemming zijn.
* [Identiteitsnaamruimten](../../identity-service/namespaces.md): Naamruimten voor identiteiten definiëren de verschillende typen identiteitsgegevens die betrekking kunnen hebben op één persoon en die een vereiste component zijn voor elk identiteitsveld.
* [Klantprofiel in realtime](../../profile/home.md): Hiermee gebruikt u identiteitsgrafieken om uniforme consumentenprofielen te bieden op basis van geaggregeerde gegevens van meerdere bronnen, die in vrijwel realtime zijn bijgewerkt.
* [Experience Data Model (XDM)](../../xdm/home.md): Verstrekt standaarddefinities en structuren voor de gegevens van het Platform door het gebruik van schema&#39;s. Alle datasets van het Platform zijn in overeenstemming met een specifiek schema XDM, en het schema bepaalt welke gebieden identiteiten zijn.
* [Identiteitsvelden](../../xdm/ui/fields/identity.md): Leer hoe een identiteitsveld wordt gedefinieerd in een XDM-schema.

## Een aanvraag maken {#create-request}

Selecteer **[!UICONTROL Data Lifecycle]** in de linkernavigatie van Platform UI. De [!UICONTROL Data lifecycle requests] wordt weergegeven. Selecteer vervolgens **[!UICONTROL Create request]** van de hoofdpagina in de werkruimte.

![De [!UICONTROL Data lifecycle requests] werkruimte met [!UICONTROL Create request] geselecteerd.](../images/ui/record-delete/create-request-button.png)

De workflow voor het maken van aanvragen wordt weergegeven. Standaard worden de **[!UICONTROL Delete record]** optie is geselecteerd onder de optie **[!UICONTROL Requested Action]** sectie. Laat deze optie ingeschakeld.

>[!IMPORTANT]
> 
>Als onderdeel van doorlopende wijzigingen om de efficiëntie te verbeteren en gegevenssetbewerkingen minder duur te maken, kunnen organisaties die naar de Delta-indeling zijn verplaatst, gegevens verwijderen uit de Identity Service, Real-Time Customer Profile en het data Lake. Dit type gebruiker wordt aangeduid als delta-migrated. De gebruikers van organisaties die delta-gemigreerd zijn geweest kunnen verkiezen om verslagen van of één of alle datasets te schrappen. Gebruikers van organisaties die niet zijn gemigreerd met delta, kunnen niet besluiten om records uit één gegevensset of uit alle gegevenssets te verwijderen, zoals in de onderstaande afbeelding wordt getoond. Ga in dit geval door met de [identiteiten opgeven](#provide-identities) van de handleiding.

![De workflow voor het maken van aanvragen met de [!UICONTROL Delete record] geselecteerd en gemarkeerd.](../images/ui/record-delete/delete-record.png)

## Gegevenssets selecteren {#select-dataset}

De volgende stap is te bepalen of u verslagen van één enkele dataset of alle datasets wilt schrappen. Als deze optie niet beschikbaar is, gaat u naar [identiteiten opgeven](#provide-identities) van de handleiding.

Onder de **[!UICONTROL Record Details]** gebruiken, gebruikt u het keuzerondje om te selecteren tussen een specifieke gegevensset en alle gegevenssets. Als u **[!UICONTROL Select dataset]**, selecteert u het databasepictogram (![Het databasepictogram](../images/ui/record-delete/database-icon.png)) om een dialoog te openen die een lijst van beschikbare datasets verstrekt. Selecteer de gewenste dataset in de lijst gevolgd door **[!UICONTROL Done]**.

![De [!UICONTROL Select dataset] dialoog met een geselecteerde dataset en [!UICONTROL Done] gemarkeerd.](../images/ui/record-delete/select-dataset.png)

Als u verslagen van alle datasets wilt schrappen, selecteer **[!UICONTROL All datasets]**.

![De [!UICONTROL Select dataset] met de [!UICONTROL All datasets] geselecteerd.](../images/ui/record-delete/all-datasets.png)

>[!NOTE]
>
>De **[!UICONTROL All datasets]** Deze optie kan ertoe leiden dat het verwijderen langer duurt en dat het verwijderen van records mogelijk niet correct verloopt.

## Identiteiten opgeven {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Primaire identiteit"
>abstract="Een primaire identiteit is een kenmerk dat een record koppelt aan het profiel van een consument in Experience Platform. Het primaire identiteitsgebied voor een dataset wordt bepaald door het schema dat de dataset op gebaseerd is. In deze kolom moet u het type (of de naamruimte) opgeven voor de primaire identiteit van de record, zoals `email` voor e-mailadressen en `ecid` voor Experience Cloud-id&#39;s. Raadpleeg de gebruikershandleiding bij de levenscyclus van gegevens voor meer informatie."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Identiteitswaarde"
>abstract="In deze kolom, moet u de waarde voor de primaire identiteit van het verslag verstrekken, die met het identiteitstype moet beantwoorden dat in de linkerkolom wordt verstrekt. Als het primaire identiteitstype `email`, moet de waarde het e-mailadres van de record zijn. Raadpleeg de gebruikershandleiding bij de gegevenslevenscyclus voor meer informatie."

Wanneer het schrappen van verslagen, moet u identiteitsinformatie verstrekken zodat kan het systeem bepalen welke verslagen moeten worden geschrapt. Voor om het even welke dataset in Platform, worden de verslagen geschrapt gebaseerd op **primaire identiteit** gebied dat door het schema van de dataset wordt bepaald.

Net als alle identiteitsvelden in Platform bestaat een primaire identiteit uit twee dingen: een **type** (wordt soms ook wel naamruimte voor identiteit genoemd) en een **value**. Het identiteitstype biedt context voor de manier waarop het veld een record identificeert (zoals een e-mailadres) en de waarde vertegenwoordigt de specifieke identiteit van een record voor dat type (bijvoorbeeld `jdoe@example.com` voor de `email` type identiteit). Veelvoorkomende velden die als identiteiten worden gebruikt, zijn accountgegevens, apparaat-id&#39;s en cookie-id&#39;s.

>[!TIP]
>
>Als u niet de primaire identiteit voor een bepaalde dataset kent, kunt u het in Platform UI vinden. In de **[!UICONTROL Datasets]** in de werkruimte, selecteert u de desbetreffende gegevensset in de lijst. Op de detailspagina voor de dataset, houd over de naam van het schema van de dataset in het juiste spoor. De primaire identiteit wordt samen met de schemanaam en beschrijving getoond.
>
>![Het dashboard Datasets met een geselecteerde dataset, en een schemadialoog die van het paneel van de Details van de dataset wordt geopend. De primaire id van de gegevensset wordt gemarkeerd.](../images/ui/record-delete/dataset-primary-identity.png)

Als u verslagen van één enkele dataset schrapt, moeten alle identiteiten u verstrekt het zelfde type hebben, aangezien een dataset slechts één primaire identiteit kan hebben. Als u van alle datasets schrapt, kunt u veelvoudige identiteitstypes omvatten aangezien de verschillende datasets verschillende primaire identiteiten kunnen hebben.

Er zijn twee opties om id&#39;s op te geven wanneer u records verwijdert:

* [Een JSON-bestand uploaden](#upload-json)
* [Identiteitswaarden handmatig invoeren](#manual-identity)

### Een JSON-bestand uploaden {#upload-json}

Als u een JSON-bestand wilt uploaden, kunt u het bestand naar het opgegeven gebied slepen of **[!UICONTROL Choose files]** om in uw lokale map te bladeren en te selecteren.

![De workflow voor het maken van aanvragen met de optie Bestanden kiezen en de interface voor slepen en neerzetten voor het uploaden van gemarkeerde JSON-bestanden.](../images/ui/record-delete/upload-json.png)

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

### Voer identiteiten handmatig in {#manual-identity}

Als u identiteiten handmatig wilt invoeren, selecteert u **[!UICONTROL Add identity]**.

![De workflow voor het maken van aanvragen met de [!UICONTROL Add identity] gemarkeerd.](../images/ui/record-delete/add-identity.png)

Er worden besturingselementen weergegeven waarmee u de identiteiten een voor een kunt invoeren. Onder **[!UICONTROL Primary Identity]** selecteert u het identiteitstype in het vervolgkeuzemenu. Onder **[!UICONTROL Identity Value]** geeft u de primaire identiteitswaarde voor de record op.

![De workflow voor het maken van een aanvraag waaraan handmatig een identiteitsveld is toegevoegd.](../images/ui/record-delete/identity-added.png)

Als u meer identiteiten wilt toevoegen, selecteert u het plusteken (![Een plusteken.](../images/ui/record-delete/plus-icon.png)) naast een van de rijen, of selecteer **[!UICONTROL Add identity]**.

![De workflow voor het maken van een aanvraag met het plusteken en het pictogram voor het toevoegen van een identiteit gemarkeerd.](../images/ui/record-delete/more-identities.png)

## De aanvraag verzenden {#submit}

Als u klaar bent met het toevoegen van identiteiten aan het verzoek, onder **[!UICONTROL Request settings]** Geef een naam en een optionele beschrijving voor de aanvraag op voordat u deze selecteert **[!UICONTROL Submit]**.

>[!IMPORTANT]
> 
>Er zijn verschillende limieten voor het totale aantal unieke identiteitsrecords dat elke maand kan worden verzonden. Deze limieten zijn gebaseerd op uw licentieovereenkomst. Organisaties die alle edities van Adobe Real-time Customer Data Platform en Adobe Journey Optimizer hebben aangeschaft, kunnen maximaal 100.000 identiteitsgegevens verzenden en elke maand verwijderen. Organisaties die een aankoop hebben gedaan **Adobe Gezondheidsschild** of **Privacy- en beveiligingsschild van Adobe** kan maximaal 600.000 identiteitsverslagen indienen schrapt elke maand.<br>Met één aanvraag voor het verwijderen van records via de gebruikersinterface kunt u 10.000 id&#39;s tegelijk verzenden. De [API-methode voor het verwijderen van records](../api/workorder.md#create) kan 100.000 ID&#39;s tegelijk worden ingediend.<br>Het is aan te raden zoveel mogelijk id&#39;s per aanvraag in te dienen, tot aan je ID-limiet. Wanneer u een hoog volume id&#39;s wilt verwijderen, moet u een laag volume of één id per record verwijderen.

![De instelling voor aanvragen [!UICONTROL Name] en [!UICONTROL Description] velden met [!UICONTROL Submit] gemarkeerd.](../images/ui/record-delete/submit.png)

A [!UICONTROL Confirm request] weergegeven om aan te geven dat de identiteiten niet kunnen worden hersteld wanneer ze eenmaal zijn verwijderd. Selecteren **[!UICONTROL Submit]** ter bevestiging van de lijst met identiteiten waarvan u de gegevens wilt verwijderen.

![De [!UICONTROL Confirm request] in.](../images/ui/record-delete/confirm-request.png)

Nadat het verzoek is verzonden, wordt een werkorder gemaakt en wordt deze weergegeven op het tabblad [!UICONTROL Record] tabblad van het [!UICONTROL Data Lifecycle] werkruimte. Van hier, kunt u de status van de het werkorde controleren aangezien het het verzoek verwerkt.

>[!NOTE]
>
>Zie de overzichtssectie over [tijdlijnen en transparantie](../home.md#record-delete-transparency) voor details over hoe verslagen schrapt worden verwerkt zodra zij worden uitgevoerd.

![De [!UICONTROL Record] tabblad van het [!UICONTROL Data Lifecycle] werkruimte met de nieuwe aanvraag gemarkeerd.](../images/ui/record-delete/request-log.png)

## Volgende stappen

In dit document wordt beschreven hoe records in de gebruikersinterface van het Experience Platform worden verwijderd. Voor informatie over hoe u andere taken in verband met het levenscyclusbeheer van gegevens in de gebruikersinterface uitvoert, raadpleegt u de [Overzicht van de gebruikersinterface van de gegevenslevenscyclus](./overview.md).

Raadpleeg voor meer informatie over het verwijderen van records met de API voor gegevenshygiëne [eindpuntgids voor werkorders](../api/workorder.md).
