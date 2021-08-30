---
keywords: activeer profielbestemmingen;activeer bestemmingen;activeer gegevens; e-mailmarketingbestemmingen activeren; cloudopslagdoelen activeren
title: Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken
type: Tutorial
seo-title: Activate audience data to batch profile export destinations
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten naar batchbestemmingen te verzenden.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to batch profile-based destinations.
source-git-commit: 99835d0b3d8ab64422be7f878cf556ac8890b123
workflow-type: tm+mt
source-wordcount: '1895'
ht-degree: 0%

---


# Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist om publieksgegevens te activeren in op Adobe Experience Platform-batchprofielen gebaseerde bestemmingen, zoals cloudopslag en marketingdoelen voor e-mail.

## Vereisten {#prerequisites}

Om gegevens aan bestemmingen te activeren, moet u [met succes hebben verbonden met een bestemming](./connect-destination.md). Als u dit niet reeds hebt gedaan, ga naar [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteer het tabblad **[!UICONTROL Catalog]**.

   ![Tabblad Doelcatalogus](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Selecteer **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knop Segmenten activeren](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Ga naar de volgende sectie naar [selecteer uw segmenten](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de controledozen links van de segmentnamen om de segmenten te selecteren die u aan de bestemming wilt activeren, dan uitgezocht **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Segmentexport plannen {#scheduling}

[!DNL Adobe Experience Platform] Hiermee exporteert u gegevens voor e-mailmarketing en cloudopslagbestemmingen in de vorm van  [!DNL CSV] bestanden. Op de **[!UICONTROL Scheduling]** pagina, kunt u het programma en de dossiernamen voor elk segment vormen u uitvoert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] Hiermee worden de exportbestanden automatisch gesplitst op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel.
>
>Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking, als zodanig: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Selecteer **[!UICONTROL Create schedule]** knoop die aan het segment beantwoordt dat u naar uw bestemming wilt verzenden.

![De knop Planning maken](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Volledige bestanden exporteren {#export-full-files}

Selecteer **[!UICONTROL Export full files]** om de uitvoer van een dossier te teweegbrengen dat een volledige momentopname van alle profielkwalificaties voor het geselecteerde segment bevat.

![Volledige bestanden exporteren](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Gebruik de selector **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Once]**: U kunt een eenmalige volledige bestandsexport plannen.
   * **[!UICONTROL Daily]**: Plan de volledige bestandsuitvoer eenmaal per dag, elke dag, op het door u opgegeven tijdstip.

1. Gebruik de kiezer **[!UICONTROL Time]** om het tijdstip van de dag in [!DNL UTC]-indeling te kiezen wanneer het exporteren moet plaatsvinden.

   >[!IMPORTANT]
   >
   >Wegens de manier de interne processen van het Experience Platform worden gevormd, kan de eerste stijgende of volledige dossieruitvoer niet alle backfill gegevens bevatten. <br> <br> Om ervoor te zorgen dat er volledige en meest recente back-upgegevens worden geëxporteerd voor zowel volledige als incrementele bestanden, raadt Adobe aan de eerste exporttijd voor bestanden in te stellen na 12.00 uur GMT van de volgende dag. Deze beperking zal in toekomstige versies worden aangepakt.

1. Gebruik de kiezer **[!UICONTROL Date]** om de dag of het interval te kiezen waarop het exporteren moet plaatsvinden.
   >[!TIP]
   >
   > Voor dagelijkse exportbewerkingen stelt u de begin- en einddatum in zodat deze overeenkomen met de duur van uw campagnes op de downstreamplatforms.
1. Selecteer **[!UICONTROL Create]** om het schema op te slaan.


### Incrementele bestanden exporteren {#export-incremental-files}

Selecteer **[!UICONTROL Export incremental files]** om een export te activeren waarbij het eerste bestand een volledige momentopname is van alle profielkwalificaties voor het geselecteerde segment, en volgende bestanden zijn incrementele profielkwalificaties sinds de vorige export.

>[!IMPORTANT]
>
>Het eerste geëxporteerde incrementele bestand bevat alle profielen die in aanmerking komen voor een segment en die als backfill werken.

![Incrementele bestanden exporteren](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Gebruik de selector **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: plant de incrementele bestandsuitvoer eenmaal per dag, elke dag, op het door u opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: schema incrementele het dossieruitvoer om de 3, 6, 8, of 12 uur.

1. Gebruik de kiezer **[!UICONTROL Time]** om het tijdstip van de dag in [!DNL UTC]-indeling te kiezen wanneer het exporteren moet plaatsvinden.

   >[!IMPORTANT]
   >
   >Wegens de manier de interne processen van het Experience Platform worden gevormd, kan de eerste stijgende of volledige dossieruitvoer niet alle backfill gegevens bevatten. <br> <br> Om ervoor te zorgen dat er volledige en meest recente back-upgegevens worden geëxporteerd voor zowel volledige als incrementele bestanden, raadt Adobe aan de eerste exporttijd voor bestanden in te stellen na 12.00 uur GMT van de volgende dag. Deze beperking zal in toekomstige versies worden aangepakt.

1. Gebruik de kiezer **[!UICONTROL Date]** om de dag of het interval te kiezen waarop het exporteren moet plaatsvinden.
   >[!TIP]
   >
   >Stel de begin- en einddatum in zodat deze overeenkomen met de duur van uw campagnes op de downstreamplatforms.
1. Selecteer **[!UICONTROL Create]** om het schema op te slaan.

### Bestandsnamen configureren {#file-names}

De standaardbestandsnamen bestaan uit een doelnaam, segment-id en een datum- en tijdindicator. U kunt bijvoorbeeld uw geëxporteerde bestandsnamen bewerken om onderscheid te maken tussen verschillende campagnes of om de exporttijd van de gegevens aan de bestanden toe te voegen.

Selecteer het potloodpictogram om een modaal venster te openen en de bestandsnamen te bewerken. Bestandsnamen mogen maximaal 255 tekens bevatten.

![bestandsnaam configureren](../assets/ui/activate-batch-profile-destinations/configure-name.png)

In de bestandsnaameditor kunt u verschillende componenten selecteren om aan de bestandsnaam toe te voegen.

![Bestandsnaamopties bewerken](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

De doelnaam en segment-id kunnen niet uit bestandsnamen worden verwijderd. Naast deze, kunt u het volgende toevoegen:

* **[!UICONTROL Segment name]**: U kunt de segmentnaam aan de bestandsnaam toevoegen.
* **[!UICONTROL Date and time]**: U kunt kiezen tussen het toevoegen van een  `MMDDYYYY_HHMMSS` indeling of een Unix 10-cijferige tijdstempel van het tijdstip waarop de bestanden worden gegenereerd. Kies een van deze opties als u voor de bestanden een dynamische bestandsnaam wilt genereren bij elke incrementele exportbewerking.
* **[!UICONTROL Custom text]**: Voeg aangepaste tekst toe aan de bestandsnamen.

Selecteer **[!UICONTROL Apply changes]** om uw selectie te bevestigen.

>[!IMPORTANT]
> 
>Als u de component **[!UICONTROL Date and Time]** niet selecteert, zijn de bestandsnamen statisch en overschrijft het nieuwe geëxporteerde bestand het vorige bestand op uw opslaglocatie met elke exportbewerking. Als u een terugkerende importtaak uitvoert vanaf een opslaglocatie naar een e-mailmarketingplatform, is dit de aanbevolen optie.

Nadat u alle segmenten hebt geconfigureerd, selecteert u **[!UICONTROL Next]** om door te gaan.

## Profielkenmerken selecteren {#select-attributes}

Voor op profiel gebaseerde bestemmingen, moet u de profielattributen selecteren die u naar de doelbestemming wilt verzenden.


1. Selecteer **[!UICONTROL Add new field]** op de pagina **[!UICONTROL Select attributes]**.

   ![Nieuwe toewijzing toevoegen](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Selecteer de pijl rechts van de **[!UICONTROL Schema field]** ingang.

   ![Bronveld selecteren](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. Selecteer op de pagina **[!UICONTROL Select field]** de XDM-kenmerken die u naar de bestemming wilt verzenden en kies **[!UICONTROL Select]**.

   ![Bronveldpagina selecteren](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Herhaal stap 1 tot en met 3 om meer toewijzingen toe te voegen.

>[!NOTE]
>
> Adobe Experience Platform vult uw selectie voor met vier aanbevolen, veelgebruikte kenmerken uit uw schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Het exporteren van bestanden kan op de volgende manieren variëren, afhankelijk van het feit of `segmentMembership.status` is geselecteerd:
* Als het veld `segmentMembership.status` is geselecteerd, bevatten geëxporteerde bestanden **[!UICONTROL Active]** leden in de eerste volledige momentopname en **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in volgende incrementele exportbewerkingen.
* Als het veld `segmentMembership.status` niet is geselecteerd, nemen geëxporteerde bestanden alleen **[!UICONTROL Active]** leden op in de eerste volledige momentopname en in volgende incrementele exportbewerkingen.

![aanbevolen kenmerken](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Verplichte kenmerken {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Verplichte kenmerken"
>abstract="Selecteer de XDM-schemakenmerken die alle geëxporteerde profielen moeten bevatten. Profielen zonder de verplichte sleutel worden niet naar de bestemming geëxporteerd. Als u geen verplichte sleutel selecteert, worden alle gekwalificeerde profielen geëxporteerd, ongeacht hun kenmerken."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="Meer informatie in documentatie"

Een verplicht kenmerk is een selectievakje dat door de gebruiker is ingeschakeld en dat ervoor zorgt dat alle profielrecords het geselecteerde kenmerk bevatten. Bijvoorbeeld: alle geëxporteerde profielen bevatten een e-mailadres. &#x200B;

U kunt kenmerken als verplicht markeren om ervoor te zorgen dat [!DNL Platform] alleen de profielen exporteert die het specifieke kenmerk bevatten. Het resultaat is dat het kan worden gebruikt als extra filtermethode. Het markeren van een kenmerk als verplicht is **niet** vereist.

Als u geen verplicht kenmerk selecteert, worden alle gekwalificeerde profielen geëxporteerd, ongeacht de kenmerken ervan.

Men adviseert dat één van de attributen een [unieke herkenningsteken](../../destinations/catalog/email-marketing/overview.md#identity) van uw schema is. Raadpleeg de identiteitssectie in de documentatie [E-mailmarketingdoelen](../../destinations/catalog/email-marketing/overview.md#identity) voor meer informatie over verplichte kenmerken.

### Deduplicatietoetsen {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Deduplicatietoetsen"
>abstract="U kunt meerdere records van hetzelfde profiel uit de exportbestanden verwijderen door een deduplicatietoets te selecteren. Selecteer één naamruimte of maximaal twee XDM-schemakenmerken als een deduplicatietoets. Als u geen deduplicatietoets selecteert, kan dit leiden tot dubbele profielvermeldingen in de exportbestanden."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="Meer informatie in documentatie"

Een deduplicatiesleutel is een door de gebruiker gedefinieerde primaire sleutel waarmee de identiteit wordt bepaald waarmee gebruikers hun profielen willen dedupliceren. &#x200B;

Deduplicatietoetsen maken het onmogelijk meerdere records van hetzelfde profiel in één exportbestand te hebben.

Er zijn drie manieren u deduplicatietoetsen in [!DNL Platform] kunt gebruiken:

* Eén naamruimte voor identiteit gebruiken als een [!UICONTROL deduplication key]
* Eén profielkenmerk van een [!DNL XDM]-profiel gebruiken als [!UICONTROL deduplication key]
* Een combinatie gebruiken van twee profielkenmerken van een [!DNL XDM] profiel als samengestelde sleutel

>[!IMPORTANT]
>
> U kunt één naamruimte voor identiteit exporteren naar een doel en de naamruimte wordt automatisch ingesteld als deduplicatietoets. Het verzenden van meerdere naamruimten naar een doel wordt niet ondersteund.
> 
> U kunt geen combinatie van naamruimten en profielkenmerken gebruiken als deduplicatietoetsen.

### Voorbeeld van deduplicatie {#deduplication-example}

Dit voorbeeld illustreert hoe deduplicatie werkt, afhankelijk van de geselecteerde deduplicatietoetsen.

Laten we eens kijken naar de volgende twee profielen.

**Profiel A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Profiel B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "existing",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Gebruiksscenario voor deduplicatie 1: geen deduplicatie {#deduplication-use-case-1}

Als u geen deduplicatie gebruikt, bevat het exportbestand de volgende items.

| PersonalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Gebruiksscenario 2 van deduplicatie: deduplicatie op basis van naamruimte van identiteit {#deduplication-use-case-2}

Als deduplicatie wordt verondersteld door de naamruimte [!DNL Email], bevat het exportbestand de volgende items. Profiel B is het meest recente profiel dat in aanmerking komt voor het segment. Het is dus de enige die wordt geëxporteerd.

| Email* | PersonalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Gebruiksscenario voor deduplicatie 3: deduplicatie op basis van één profielkenmerk {#deduplication-use-case-3}

Ervan uitgaande dat het kenmerk `personal Email` deduplicatie bevat, bevat het exportbestand de volgende vermelding. Profiel B is het meest recente profiel dat in aanmerking komt voor het segment. Het is dus de enige die wordt geëxporteerd.

| PersonalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Gebruiksscenario voor deduplicatie 4: deduplicatie op basis van twee profielkenmerken {#deduplication-use-case-4}

Als deduplicatie wordt verondersteld met de samengestelde sleutel `personalEmail + lastName`, bevat het exportbestand de volgende items.

| PersonalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe raadt u aan een naamruimte voor identiteiten, zoals een [!DNL CRM ID]- of e-mailadres, te selecteren als deduplicatietoets om ervoor te zorgen dat alle profielrecords op unieke wijze worden geïdentificeerd.

>[!NOTE]
> 
>Als er labels voor gegevensgebruik zijn toegepast op bepaalde velden in een gegevensset (in plaats van op de gehele gegevensset), wordt de toepassing van die labels op veldniveau bij activering uitgevoerd onder de volgende voorwaarden:
>
>* De velden worden gebruikt in de segmentdefinitie.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.

>
> Bijvoorbeeld, als het gebied `person.name.firstName` bepaalde etiketten van het gegevensgebruik heeft die met de marketing van de bestemming actie in conflict brengen, zou u een schending van het beleid van het gegevensgebruik in de overzichtsstap worden getoond. Zie [Gegevensbeheer in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations) voor meer informatie.

## Controleren {#review}

Op de **[!UICONTROL Review]** pagina, kunt u een samenvatting van uw selectie zien. Selecteer **[!UICONTROL Cancel]** om de stroom te verbreken, **[!UICONTROL Back]** om uw montages te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe te om beleidsschendingen op te lossen, zie [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie van de documentatie van het gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-batch-profile-destinations/review.png)

## Segmentactivering verifiëren {#verify}


Voor marketingdoelen en opslagdoelen voor de cloud maakt Adobe Experience Platform een door tabs gescheiden `.csv`-bestand op de opslaglocatie die u hebt opgegeven. Verwacht dat er elke dag een nieuw bestand op uw opslaglocatie wordt gemaakt. De standaardbestandsindeling is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

De bestanden die u op drie opeenvolgende dagen ontvangt, kunnen er als volgt uitzien:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt. Als u wilt weten hoe de geëxporteerde bestanden zijn gestructureerd, kunt u [een voorbeeld-CSV-bestand](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv) downloaden. Dit voorbeeldbestand bevat de profielkenmerken `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` en `personalEmail.address`.
