---
keywords: activeer profielbestemmingen;activeer bestemmingen;activeer gegevens; e-mailmarketingbestemmingen activeren; cloudopslagdoelen activeren
title: Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken
type: Tutorial
seo-title: Activate audience data to batch profile export destinations
description: Leer hoe u de publieksgegevens die u in Adobe Experience Platform hebt, activeert door segmenten naar batchbestemmingen te verzenden.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to batch profile-based destinations.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 98e2076832bee8e11df8834063cc0b11c1ae3164
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken

## Overzicht {#overview}

In dit artikel wordt uitgelegd welke workflow is vereist om publieksgegevens te activeren in op Adobe Experience Platform-batchprofielen gebaseerde bestemmingen, zoals cloudopslag en marketingdoelen voor e-mail.

## Vereisten {#prerequisites}

Als u gegevens naar doelen wilt activeren, moet u [verbonden met een bestemming](./connect-destination.md). Als u dat nog niet hebt gedaan, gaat u naar de [doelcatalogus](../catalog/overview.md), doorblader de gesteunde bestemmingen, en vorm de bestemming die u wilt gebruiken.

## Kies uw bestemming {#select-destination}

1. Ga naar **[!UICONTROL Connections > Destinations]** en selecteert u de **[!UICONTROL Catalog]** tab.

   ![Tabblad Doelcatalogus](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Selecteren **[!UICONTROL Activate segments]** op de kaart die overeenkomt met de bestemming waar u de segmenten wilt activeren, zoals in de onderstaande afbeelding wordt getoond.

   ![Knop Segmenten activeren](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Selecteer de doelverbinding die u wilt gebruiken om uw segmenten te activeren en selecteer vervolgens **[!UICONTROL Next]**.

   ![Doel selecteren](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Naar de volgende sectie gaan [uw segmenten selecteren](#select-segments).

## Uw segmenten selecteren {#select-segments}

Gebruik de selectievakjes links van de segmentnamen om de segmenten te selecteren die u wilt activeren naar het doel en selecteer vervolgens **[!UICONTROL Next]**.

![Segmenten selecteren](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Segmentexport plannen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Schema"
>abstract="Gebruik het potloodpictogram om het bestandstype (volledige bestanden of incrementele bestanden) en de exportfrequentie in te stellen."
>additional-url="https://www.adobe.com/go/destinations-profile-batch-en" text="Meer informatie in documentatie"

[!DNL Adobe Experience Platform] exporteert gegevens voor e-mailmarketing en cloudopslagbestemmingen in de vorm van [!DNL CSV] bestanden. In de **[!UICONTROL Scheduling]** pagina, kunt u het programma en de dossiernamen voor elk segment vormen u uitvoert. Het is verplicht het schema te configureren, maar het configureren van de bestandsnaam is optioneel.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] Hiermee worden de exportbestanden automatisch gesplitst op 5 miljoen records (rijen) per bestand. Elke rij vertegenwoordigt één profiel.
>
>Namen van gesplitste bestanden worden toegevoegd met een getal dat aangeeft dat het bestand deel uitmaakt van een grotere exportbewerking, als zodanig: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Selecteer **[!UICONTROL Create schedule]** knoop die aan het segment beantwoordt dat u naar uw bestemming wilt verzenden.

![De knop Planning maken](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Volledige bestanden exporteren {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Exportopties voor bestanden"
>abstract="Selecteren **Volledige bestanden exporteren** om een volledige momentopname van alle profielen uit te voeren die voor het segment kwalificeren. Selecteren **Incrementele bestanden exporteren** om alleen de profielen te exporteren die voor het segment in aanmerking kwamen sinds de laatste exportbewerking. <br> Het eerste incrementele exportbestand bevat alle profielen die in aanmerking komen voor het segment en die fungeren als backfill. Toekomstige incrementele bestanden bevatten alleen de profielen die in aanmerking kwamen voor het segment sinds de eerste incrementele bestandsexport."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#export-incremental-files" text="Incrementele bestanden exporteren"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Activeren na segmentevaluatie"
>abstract="De activering wordt onmiddellijk uitgevoerd nadat de dagelijkse segmentatietaak is voltooid. Zo weet u zeker dat de meest actuele profielen worden geëxporteerd. Behoefte om deze popover naar de nieuwe activeringsketende sectie voor correcte verbinding te verplaatsen."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Geplande activering"
>abstract="De activering wordt uitgevoerd op een vast tijdstip van de dag. Behoefte om deze popover naar de nieuwe activeringsketende sectie voor correcte verbinding te verplaatsen."

Selecteren **[!UICONTROL Export full files]** om het exporteren van een bestand met een volledige opname van alle profielkwalificaties voor het geselecteerde segment te activeren.

![Volledige bestanden exporteren](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Gebruik de **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Once]**: U kunt een eenmalige volledige bestandsexport plannen.
   * **[!UICONTROL Daily]**: Plan de volledige bestandsuitvoer eenmaal per dag, elke dag, op het door u opgegeven tijdstip.

1. Gebruik de **[!UICONTROL Time]** om de tijd van de dag te kiezen, in [!DNL UTC] formaat, wanneer het exporteren moet plaatsvinden.

   >[!IMPORTANT]
   >
   >Wegens de manier de interne processen van het Experience Platform worden gevormd, kan de eerste stijgende of volledige dossieruitvoer niet alle backfill gegevens bevatten. <br> <br> Om ervoor te zorgen dat er volledige en meest recente back-upgegevens worden geëxporteerd voor zowel volledige als incrementele bestanden, raadt Adobe aan de eerste exporttijd voor bestanden in te stellen na 12.00 uur GMT van de volgende dag. Deze beperking zal in toekomstige versies worden aangepakt.

1. Gebruik de **[!UICONTROL Date]** om de dag of het interval te kiezen waarop het exporteren moet plaatsvinden. Voor dagelijkse exportbewerkingen kunt u het beste uw begin- en einddatum instellen zodat deze aansluiten op de duur van uw campagnes op de downstreamplatforms.

   >[!IMPORTANT]
   >
   > Wanneer u een exportinterval selecteert, wordt de laatste dag van het interval niet in de exportbewerking opgenomen. Als u bijvoorbeeld een interval van 4-11 januari selecteert, wordt het laatste bestand op 10 januari geëxporteerd.

1. Selecteren **[!UICONTROL Create]** om het programma op te slaan.


### Incrementele bestanden exporteren {#export-incremental-files}

Selecteren **[!UICONTROL Export incremental files]** om een exportbewerking te activeren waarbij het eerste bestand een volledige momentopname is van alle profielkwalificaties voor het geselecteerde segment, en volgende bestanden zijn incrementele profielkwalificaties sinds de vorige exportbewerking.

>[!IMPORTANT]
>
>Het eerste geëxporteerde incrementele bestand bevat alle profielen die in aanmerking komen voor een segment en die als backfill werken.

![Incrementele bestanden exporteren](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Gebruik de **[!UICONTROL Frequency]** om de exportfrequentie te selecteren:

   * **[!UICONTROL Daily]**: plant de incrementele bestandsuitvoer eenmaal per dag, elke dag, op het door u opgegeven tijdstip.
   * **[!UICONTROL Hourly]**: schema incrementele het dossieruitvoer om de 3, 6, 8, of 12 uur.

1. Gebruik de **[!UICONTROL Time]** om de tijd van de dag te kiezen, in [!DNL UTC] formaat, wanneer het exporteren moet plaatsvinden.

   >[!IMPORTANT]
   >
   >Wegens de manier de interne processen van het Experience Platform worden gevormd, kan de eerste stijgende of volledige dossieruitvoer niet alle backfill gegevens bevatten. <br> <br> Om ervoor te zorgen dat er volledige en meest recente back-upgegevens worden geëxporteerd voor zowel volledige als incrementele bestanden, raadt Adobe aan de eerste exporttijd voor bestanden in te stellen na 12.00 uur GMT van de volgende dag. Deze beperking zal in toekomstige versies worden aangepakt.

1. Gebruik de **[!UICONTROL Date]** om het interval te kiezen waarin het exporteren moet plaatsvinden. De beste manier is om uw begin- en einddatum in te stellen op de duur van uw campagnes op uw downstreamplatforms.

   >[!IMPORTANT]
   >
   >De laatste dag van het interval wordt niet in de uitvoer opgenomen. Als u bijvoorbeeld een interval van 4-11 januari selecteert, wordt het laatste bestand op 10 januari geëxporteerd.

1. Selecteren **[!UICONTROL Create]** om het programma op te slaan.

### Bestandsnamen configureren {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Bestandsnaam configureren"
>abstract="Voor op een bestand gebaseerde doelen wordt een unieke bestandsnaam per segment gegenereerd. Met de bestandsnaameditor kunt u een unieke bestandsnaam maken en bewerken of de standaardnaam behouden."

De standaardbestandsnamen bestaan uit een doelnaam, segment-id en een datum- en tijdindicator. U kunt bijvoorbeeld uw geëxporteerde bestandsnamen bewerken om onderscheid te maken tussen verschillende campagnes of om de exporttijd van de gegevens aan de bestanden toe te voegen.

Selecteer het potloodpictogram om een modaal venster te openen en de bestandsnamen te bewerken. Bestandsnamen mogen maximaal 255 tekens bevatten.

![bestandsnaam configureren](../assets/ui/activate-batch-profile-destinations/configure-name.png)

In de bestandsnaameditor kunt u verschillende componenten selecteren om aan de bestandsnaam toe te voegen.

![Bestandsnaamopties bewerken](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

De doelnaam en segment-id kunnen niet uit bestandsnamen worden verwijderd. Naast deze, kunt u het volgende toevoegen:

* **[!UICONTROL Segment name]**: U kunt de segmentnaam aan de bestandsnaam toevoegen.
* **[!UICONTROL Date and time]**: Selecteer tussen het toevoegen van een `MMDDYYYY_HHMMSS` gebruiken of een Unix 10-cijferige tijdstempel van het tijdstip waarop de bestanden worden gegenereerd. Kies een van deze opties als u voor de bestanden een dynamische bestandsnaam wilt genereren bij elke incrementele exportbewerking.
* **[!UICONTROL Custom text]**: Voeg aangepaste tekst toe aan de bestandsnamen.

Selecteren **[!UICONTROL Apply changes]** om uw selectie te bevestigen.

>[!IMPORTANT]
> 
>Als u de optie **[!UICONTROL Date and Time]** de bestandsnamen statisch zijn en het nieuwe geëxporteerde bestand overschrijft het vorige bestand in uw opslaglocatie met elke exportbewerking. Als u een terugkerende importtaak uitvoert vanaf een opslaglocatie naar een e-mailmarketingplatform, is dit de aanbevolen optie.

Nadat u alle segmenten hebt geconfigureerd, selecteert u **[!UICONTROL Next]** om door te gaan.

## Profielkenmerken selecteren {#select-attributes}

Voor op profiel gebaseerde bestemmingen, moet u de profielattributen selecteren die u naar de doelbestemming wilt verzenden.


1. In de **[!UICONTROL Select attributes]** pagina, selecteert u **[!UICONTROL Add new field]**.

   ![Nieuwe toewijzing toevoegen](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Selecteer de pijl rechts van de knop **[!UICONTROL Schema field]** vermelding.

   ![Bronveld selecteren](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. In de **[!UICONTROL Select field]** pagina, selecteert u de XDM-kenmerken die u naar het doel wilt verzenden en kiest u **[!UICONTROL Select]**.

   ![Bronveldpagina selecteren](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Herhaal stap 1 tot en met 3 om meer toewijzingen toe te voegen.

>[!NOTE]
>
> Adobe Experience Platform vult uw selectie voor met vier aanbevolen, veelgebruikte kenmerken uit uw schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Het exporteren van bestanden kan als volgt variëren, afhankelijk van of `segmentMembership.status` is geselecteerd:
* Als de `segmentMembership.status` veld is geselecteerd, geëxporteerde bestanden bevatten **[!UICONTROL Active]** leden in de eerste volledige momentopname en **[!UICONTROL Active]** en **[!UICONTROL Expired]** leden in latere incrementele uitvoer.
* Als de `segmentMembership.status` veld is niet geselecteerd, geëxporteerde bestanden bevatten alleen **[!UICONTROL Active]** leden in de eerste volledige momentopname en in de daaropvolgende incrementele uitvoer.

![aanbevolen kenmerken](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Verplichte kenmerken {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Verplichte kenmerken"
>abstract="Selecteer de XDM-schemakenmerken die alle geëxporteerde profielen moeten bevatten. Profielen zonder de verplichte sleutel worden niet naar de bestemming geëxporteerd. Als u geen verplichte sleutel selecteert, worden alle gekwalificeerde profielen geëxporteerd, ongeacht hun kenmerken."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="Meer informatie in documentatie"

Een verplicht kenmerk is een selectievakje dat door de gebruiker wordt ingeschakeld en dat ervoor zorgt dat alle profielrecords het geselecteerde kenmerk bevatten. Bijvoorbeeld: alle geëxporteerde profielen bevatten een e-mailadres. &#x200B;

U kunt kenmerken als verplicht markeren om ervoor te zorgen dat [!DNL Platform] Hiermee worden alleen de profielen geëxporteerd die het specifieke kenmerk bevatten. Het resultaat is dat het kan worden gebruikt als extra filtermethode. Een attribuut als verplicht markeren is **niet** vereist.

Als u geen verplicht kenmerk selecteert, worden alle gekwalificeerde profielen geëxporteerd, ongeacht de kenmerken ervan.

Het wordt aanbevolen een van de kenmerken [unieke id](../../destinations/catalog/email-marketing/overview.md#identity) vanuit uw schema. Zie het gedeelte Identiteit in het dialoogvenster [E-mailmarketingdoelen](../../destinations/catalog/email-marketing/overview.md#identity) documentatie.

### Deduplicatietoetsen {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Deduplicatietoetsen"
>abstract="U kunt meerdere records van hetzelfde profiel uit de exportbestanden verwijderen door een deduplicatietoets te selecteren. Selecteer één naamruimte of maximaal twee XDM-schemakenmerken als een deduplicatietoets. Als u geen deduplicatietoets selecteert, kan dit leiden tot dubbele profielvermeldingen in de exportbestanden."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="Meer informatie in documentatie"

Een deduplicatiesleutel is een door de gebruiker gedefinieerde primaire sleutel waarmee de identiteit wordt bepaald waarmee gebruikers hun profielen willen dedupliceren. &#x200B;

Deduplicatietoetsen maken het onmogelijk meerdere records van hetzelfde profiel in één exportbestand te hebben.

Er zijn drie manieren waarop u deduplicatietoetsen kunt gebruiken in [!DNL Platform]:

* Eén naamruimte voor identiteit gebruiken als een [!UICONTROL deduplication key]
* Eén profielkenmerk gebruiken vanuit een [!DNL XDM] profiel als [!UICONTROL deduplication key]
* Een combinatie van twee profielkenmerken van een [!DNL XDM] profiel als samengestelde sleutel

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

Veronderstellend deduplicatie door [!DNL Email] naamruimte, bevat het exportbestand de volgende vermeldingen. Profiel B is het meest recente profiel dat in aanmerking komt voor het segment. Het is dus de enige die wordt geëxporteerd.

| Email* | PersonalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Gebruiksscenario voor deduplicatie 3: deduplicatie op basis van één profielkenmerk {#deduplication-use-case-3}

Veronderstellend deduplicatie door `personal Email` -kenmerk, bevat het exportbestand de volgende vermelding. Profiel B is het meest recente profiel dat in aanmerking komt voor het segment. Het is dus de enige die wordt geëxporteerd.

| PersonalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Gebruiksscenario voor deduplicatie 4: deduplicatie op basis van twee profielkenmerken {#deduplication-use-case-4}

Veronderstellend deduplicatie door de samengestelde sleutel `personalEmail + lastName`bevat het exportbestand de volgende vermeldingen.

| PersonalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe raadt u aan een naamruimte voor identiteiten te selecteren, zoals een [!DNL CRM ID] of e-mailadres als deduplicatietoets, om ervoor te zorgen dat alle profielrecords uniek worden geïdentificeerd.

>[!NOTE]
> 
>Als er labels voor gegevensgebruik zijn toegepast op bepaalde velden in een gegevensset (in plaats van op de gehele gegevensset), wordt de toepassing van die labels op veldniveau bij activering uitgevoerd onder de volgende voorwaarden:
>
>* De velden worden gebruikt in de segmentdefinitie.
>* De velden worden geconfigureerd als geprojecteerde kenmerken voor de doelbestemming.
>
> Als het veld `person.name.firstName` heeft bepaalde etiketten van het gegevensgebruik die met de het op de markt brengen van de bestemming in conflict zijn, zou u een schending van het beleid van het gegevensgebruik in de overzichtsstap worden getoond. Zie voor meer informatie [Beheer van gegevens in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Controleren {#review}

Op de **[!UICONTROL Review]** , kunt u een overzicht van uw selectie zien. Selecteren **[!UICONTROL Cancel]** om de stroom op te delen, **[!UICONTROL Back]** om uw instellingen te wijzigen, of **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

>[!IMPORTANT]
>
>In deze stap controleert Adobe Experience Platform op overtredingen van het gegevensgebruiksbeleid. Hieronder ziet u een voorbeeld waarin een beleid wordt overtreden. U kunt de workflow voor segmentactivering pas voltooien nadat u de schending hebt opgelost. Voor informatie over hoe u beleidsovertredingen kunt oplossen, raadpleegt u [Beleidshandhaving](../../rtcdp/privacy/data-governance-overview.md#enforcement) in de sectie Documentatie inzake gegevensbeheer.

![schending van gegevensbeleid](../assets/common/data-policy-violation.png)

Als er geen beleidsovertredingen zijn vastgesteld, selecteert u **[!UICONTROL Finish]** om uw selectie te bevestigen en te beginnen gegevens naar de bestemming te verzenden.

![Controleren](../assets/ui/activate-batch-profile-destinations/review.png)

## Segmentactivering verifiëren {#verify}


Voor marketingdoelen en opslagdoelen voor de cloud maakt Adobe Experience Platform een `.csv` in de opslaglocatie die u hebt opgegeven. Verwacht dat er elke dag een nieuw bestand op uw opslaglocatie wordt gemaakt. De standaardbestandsindeling is:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

De bestanden die u op drie opeenvolgende dagen ontvangt, kunnen er als volgt uitzien:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

De aanwezigheid van deze bestanden op de opslaglocatie bevestigt dat de activering is gelukt. Als u wilt weten hoe de geëxporteerde bestanden zijn gestructureerd, kunt u [een voorbeeld van een CSV-bestand downloaden](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Dit voorbeeldbestand bevat de profielkenmerken `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`, en `personalEmail.address`.
