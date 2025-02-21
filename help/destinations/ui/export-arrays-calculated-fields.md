---
title: Arrays, kaarten en objecten van Real-Time CDP naar cloudopslagdoelen exporteren
type: Tutorial
description: Leer hoe u arrays, kaarten en objecten van Real-Time CDP naar cloudopslagdoelen exporteert.
exl-id: ff13d8b7-6287-4315-ba71-094e2270d039
source-git-commit: 6122ddc078101c26061e8662de3fcdcb1cb65992
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# Arrays, kaarten en objecten van Real-Time CDP naar cloudopslagdoelen exporteren {#export-arrays-cloud-storage}

>[!AVAILABILITY]
>
>De functionaliteit voor het exporteren van arrays naar cloudopslagdoelen is over het algemeen beschikbaar voor de volgende doelen: [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md), [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md), [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md), [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md), [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md), [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md),

Leer hoe te om series van Real-Time CDP naar [ wolkenopslagbestemmingen ](/help/destinations/catalog/cloud-storage/overview.md) uit te voeren. Lees dit document om inzicht te krijgen in de exportworkflow, de gebruiksgevallen die door deze functionaliteit worden ingeschakeld en de bekende beperkingen.

Bekijk deze pagina voor alles wat u wilt weten over het exporteren van arrays, kaarten en andere objecttypen uit Experience Platform.

## Onderste regel naar boven

Haal de belangrijkste informatie over de functionaliteit in deze sectie op en ga verder onder de andere secties in het document voor meer informatie.

* De capaciteit om series, kaarten, en voorwerpen uit te voeren hangt van uw selectie van de **series van de Uitvoer af, kaarten, voorwerpen** knevel. Lees meer over het [ verder neer op de pagina ](#export-arrays-maps-objects-toggle).
* U kunt arrays, toewijzingen en objecten alleen exporteren naar cloudopslagdoelen, in `JSON` - en `Parquet` -bestanden. Personen en potentiële doelgroepen worden ondersteund, accountpubliek niet.
* U *kunt* series, kaarten, en voorwerpen naar Csv- dossiers uitvoeren, maar slechts door de berekende gebiedsfunctionaliteit te gebruiken en hen in een koord door te schakelen te gebruiken `array_to_string` functie.

## Arrays en andere objecttypen in Platform {#arrays-strings-other-objects}

In Experience Platform, kunt u [ schema&#39;s XDM ](/help/xdm/home.md) gebruiken om verschillende gebiedstypes te beheren. Voordat ondersteuning voor het exporteren van arrays werd toegevoegd, kon u eenvoudige sleutelwaardepaartypevelden, zoals tekenreeksen, uit Experience Platform exporteren naar de gewenste doelen. Een voorbeeld van zulk een gebied dat voor de uitvoer eerder werd gesteund is `personalEmail.address`:`johndoe@acme.org`.

Andere veldtypen in Experience Platform zijn arrayvelden. Lees meer over [ het beheren van seriegebieden in Experience Platform UI ](/help/xdm/ui/fields/array.md). U kunt nu matrixobjecten exporteren, zoals het onderstaande voorbeeld.

```
organizations = [{
  id: 123,
  orgName: "Acme Inc",
  founded: 1990,
  latestInteraction: "2024-02-16"
}, {
  id: 456,
  orgName: "Superstar Inc",
  founded: 2004,
  latestInteraction: "2023-08-25"
}, {
  id: 789,
  orgName: 'Energy Corp',
  founded: 2021,
  latestInteraction: "2024-09-08"
}]
```

Zie verder onder [ uitgebreide voorbeelden ](#examples) van hoe u diverse functies kunt gebruiken om tot elementen van series, transformatie en filterseries toegang te hebben, arrayelementen in een koord, en meer aansluiten.

Naast arrays kunt u ook kaarten en objecten van Experience Platform naar de gewenste bestemming voor cloudopslag exporteren. Lees meer over [ kaarten ](/help/xdm/ui/fields/map.md) en [ voorwerpen ](/help/xdm/ui/fields/object.md) in Experience Platform.

## Vereisten {#prerequisites}

[ verbindt ](/help/destinations/ui/connect-destination.md) met een gewenste bestemming van de wolkenopslag, vooruitgang door de [ activeringsstappen voor de bestemmingen van de wolkenopslag ](/help/destinations/ui/activate-batch-profile-destinations.md) en krijgt aan de [ in kaart brengende ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) stap. Wanneer u verbinding maakt met de gewenste wolkenbestemming, moet u de schakeloptie **[!UICONTROL Export arrays, maps, objects]** inschakelen. Meer informatie vindt u in de onderstaande sectie.

## Arrays, kaarten, objecten in-/uitschakelen {#export-arrays-maps-objects-toggle}

>[!CONTEXTUALHELP]
>id="platform_destinations_export_arrays_maps_objects"
>title="Arrays, kaarten en objecten exporteren"
>abstract="<p> Wissel dit het plaatsen <b> op </b> om de uitvoer van series, kaarten, en voorwerpen aan JSON of de dossiers van het Parket toe te laten. U kunt deze objecttypen selecteren in de weergave Bronveld van de toewijzingsstap. Als de schakeloptie is ingeschakeld, kunt u de optie Berekende velden niet gebruiken in de toewijzingsstap.</p><p>Met deze knevel <b> weg </b>, kunt u de berekende gebiedsoptie gebruiken en diverse functies van de gegevenstransformatie toepassen wanneer het activeren van publiek. Nochtans, kunt u <i> niet </i> uitvoeren series, kaarten, en voorwerpen aan JSON of de dossiers van het Pakket en moet een afzonderlijke bestemming voor dat doel vormen.</p>"

Wanneer u verbinding maakt met een locatie voor cloudopslag, kunt u de schakeloptie **[!UICONTROL Export arrays, maps, objects]** in- of uitschakelen.

![ de series van de Uitvoer, kaarten, voorwerpen knevel getoond met aan of van het plaatsen, evenals het benadrukken van popover.](/help/destinations/assets/ui/export-arrays-calculated-fields/export-objects-toggle.gif)

Wissel dit het plaatsen **op** om de uitvoer van series, kaarten, en voorwerpen aan JSON of de dossiers van het Parket toe te laten. U kunt deze objecten types in de brongebiedmening van de [ toewijzingsstap ](/help/destinations/ui/activate-batch-profile-destinations.md#mapping) selecteren wanneer het activeren van publiek aan de bestemmingen van de wolkenopslag. Als deze instelling is ingeschakeld, kunt u de optie Berekende velden echter niet gebruiken om gegevens bij activering te transformeren.

Met deze knevel **weg**, kunt u de berekende gebiedsoptie gebruiken en diverse functies van de gegevenstransformatie toepassen wanneer het activeren van publiek. U kunt echter geen arrays, kaarten en objecten exporteren naar JSON- of Parquet-bestanden en moet daarvoor een aparte bestemming configureren.

## De series van de uitvoer, kaarten, voorwerpen schakelen *op* {#export-arrays-maps-objects-toggle-on}

Als deze instelling is ingeschakeld, kunt u volledige objecten (bijvoorbeeld `person.name` ) en arrays exporteren door deze via de bronveldkiezer te selecteren in de toewijzingsstap van de activeringsworkflow.

![ Uitgezochte voorwerpen via de selecteur van het brongebied in de afbeeldingsstap van het activeringswerkschema.](/help/destinations/assets/ui/export-arrays-calculated-fields/select-object.gif)

Als deze optie is geselecteerd, voorkomt de gebruikersinterface dat gebruikers berekende velden gebruiken en is het besturingselement **[!UICONTROL Add calculated fields]** uitgeschakeld, zoals hieronder wordt weergegeven. Als u berekende velden wilt gebruiken voor gegevenstransformaties, stelt u een doelverbinding in met de schakeloptie uit.

![ Berekende gehandicapte gebiedscontrole.](/help/destinations/assets/ui/export-arrays-calculated-fields/calculated-fields-disabled.png)

## De series van de uitvoer, kaarten, voorwerpen schakelen *weg* {#export-arrays-maps-objects-toggle-off}

Met deze optie die aan *wordt geplaatst weg*, kunt u de berekende gebiedsoptie gebruiken en diverse functies van de gegevenstransformatie toepassen wanneer het activeren van publiek. U kunt echter geen arrays, kaarten en objecten exporteren naar JSON- of Parquet-bestanden en moet daarvoor een aparte bestemming configureren.

U *kunt* series, kaarten, en voorwerpen naar Csv- dossiers uitvoeren door de berekende gebiedsfunctionaliteit te gebruiken en hen in een koord aaneenschakelen door de `array_to_string` functie te gebruiken. [ las meer ](#array-to-string-function-export-arrays) over het gebruiken van die functie.

Lees meer over het werken met berekende gebieden om [ transformaties op gegevens uit te voeren die naar de bestemmingen van de wolkenopslag ](/help/destinations/ui/data-transformations-calculated-fields.md) worden uitgevoerd.

## Voorbeeld van geëxporteerde bestanden {#sample-exported-files}

Met deze functie kunt u Parquet- en JSON-bestanden exporteren waarin de structuur van Experience Platform behouden blijft. Onder een voorbeeld van een geëxporteerd JSON-bestand weergeven.

+++ Selecteer deze optie om het geëxporteerde JSON-bestand weer te geven.

```json
{
  "person_name_firstName": "John",
  "person_name_lastName": "Smith",
  "_acmeinc_customer_hs_main_address_scalar": "Oak Avenue No 12",
  "_acmeinc_customer_hs_locations_array": [
    "home address 12",
    "office address 12"
  ],
  "_acmeinc_customer_hs_date_array": [
    "2024-11-14",
    "2024-11-15"
  ],
  "_acmeinc_customer_hs_customer_obj_emails_array0": "john.smith@example.com",
  "_acmeinc_customer_hs_customer_obj": {
    "emails_array": [
      "john.smith@example.com",
      "j.smith@example.com"
    ],
    "name_scalar": "John Smith"
  },
  "_acmeinc_customer_hs_addresses_array_obj": [
    {
      "is_primary": true,
      "streetName_scalar": "Maple Street",
      "streetNo_int": 12
    },
    {
      "is_primary": false,
      "streetName_scalar": "Pine Road",
      "streetNo_int": 45
    }
  ],
  "_acmeinc_customer_hs_addresses_array_obj0": {
    "is_primary": true,
    "streetName_scalar": "Maple Street",
    "streetNo_int": 12
  }
}
```

+++