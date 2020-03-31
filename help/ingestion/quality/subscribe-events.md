---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Abonneren op gebeurtenissen voor gegevensinvoer
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# Meldingen voor gegevensinvoer

Het proces voor het opnemen van gegevens in het Adobe Experience Platform bestaat uit meerdere stappen. Zodra u gegevensdossiers identificeert die in Platform moeten worden opgenomen, begint het innameproces en elke stap komt achtereenvolgens tot de gegevens of met succes worden opgenomen of ontbreken. Het insluitingsproces kan worden gestart met de [Adobe Experience Platform Data Ingestie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) of via de Experience Platform-gebruikersinterface.

De gegevens die in Platform worden geladen moeten door veelvoudige stappen gaan om zijn bestemming, het meer van Gegevens of de gegevens opslag van het Profiel van de Klant in real time te bereiken. Elke stap omvat het verwerken van de gegevens, het valideren van de gegevens en het opslaan van de gegevens voordat u deze doorgeeft aan de volgende stap. Afhankelijk van de hoeveelheid gegevens die wordt opgenomen, kan dit een tijdrovend proces worden en er is altijd een kans dat het proces mislukt door validatie-, semantiek- of verwerkingsfouten. In geval van een fout moeten de gegevensproblemen worden opgelost en moet het volledige innameproces opnieuw worden gestart met de gecorrigeerde gegevensbestanden.

Om bij het controleren van het innameproces te helpen, maakt het Platform van de Ervaring het mogelijk om aan een reeks gebeurtenissen in te tekenen die door elke stap van het proces worden gepubliceerd, die u op de hoogte brengen van de status van de opgenomen gegevens en om het even welke mogelijke mislukkingen.

## Beschikbare statusmeldingsgebeurtenissen

Hieronder vindt u een lijst met beschikbare gegevensinvoerstatusmeldingen waarop u zich kunt abonneren.

>[!NOTE] Er is slechts één gebeurtenisonderwerp dat voor alle gegevens wordt verstrekt die berichten invoeren. Om onderscheid te maken tussen verschillende statussen, kan de gebeurteniscode worden gebruikt.

| Platform Service | Status | Beschrijving van gebeurtenis | Gebeurteniscode |
| ---------------- | ------ | ----------------- | ---------- |
| Gegevenslanding | succes | Opname - Batch voltooid | ing_load_success |
| Gegevenslanding | fout | Opname - Batch mislukt | ing_load_failure |
| Klantprofiel in realtime | succes | Profielservice - Gegevensladingbatch geslaagd | ps_load_success |
| Klantprofiel in realtime | fout | Profielservice - Gegevensbatch is mislukt | ps_load_failure |
| Identiteitsgrafiek | succes | Identiteitsgrafiek - Gegevensladingbatch geslaagd | ig_load_success |
| Identiteitsgrafiek | fout | Identiteitsgrafiek: batch voor laden van gegevens is mislukt | ig_load_failure |

## Payloadschema voor berichten

Het gebeurtenisschema voor gegevensinvoer is een XDM-schema (Experience Data Model) dat velden en waarden bevat die details bevatten over de status van de gegevens die worden ingevoerd. Gelieve te bezoeken de openbare reactie XDM GitHub om het recentste schema [van de](https://github.com/adobe/xdm/blob/master/schemas/common/notifications/ingestion.schema.json)berichtlading te bekijken.

## Abonneren op meldingen met de status van gegevensinsluiting

Via [Adobe I/O-gebeurtenissen](https://www.adobe.io/apis/experienceplatform/events.html)kunt u zich op meerdere berichttypen abonneren met behulp van websites. Meer informatie over websites en hoe u zich op Adobe I/O-gebeurtenissen kunt abonneren met behulp van webhaken vindt u in de [inleiding op de Adobe I/O Events Webhooks](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md) -handleiding.

### Een nieuwe integratie maken met Adobe I/O-console

Meld u aan bij de [Adobe I/O-console](https://console.adobe.io/home) en klik op het tabblad *Integraties* of klik op Integratie **** maken onder Snel starten. Wanneer het scherm *Integratie* verschijnt, klik **Nieuwe Integratie** aan het creëren van een nieuwe integratie.

![Nieuwe integratie maken](../images/quality/subscribe-events/create_integration_start.png)

Het scherm *Nieuwe integratie* maken wordt weergegeven. Selecteer Gebeurtenissen **in bijna real-** time ontvangen en klik op **Doorgaan**.

![Gebeurtenissen in bijna realtime ontvangen](../images/quality/subscribe-events/create_integration_receive_events.png)

In het volgende scherm vindt u opties waarmee u integratie kunt maken met verschillende gebeurtenissen, producten en services die beschikbaar zijn voor uw organisatie. Deze opties zijn gebaseerd op uw abonnementen, rechten en machtigingen. Selecteer voor deze integratie **Platform-meldingen** onder Experience Platform en klik op **Doorgaan**.

![Gebeurtenisprovider selecteren](../images/quality/subscribe-events/create_integration_select_provider.png)

Het formulier *Integratiedetails* wordt weergegeven. Hierin moet u een naam en beschrijving voor de integratie opgeven, evenals een certificaat met openbare sleutel.

Als u geen openbaar certificaat hebt, kunt u één in de terminal produceren door het volgende bevel te gebruiken:

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

Nadat u een certificaat hebt gegenereerd, sleept u het bestand naar het vak **Certificaten** met openbare sleutels of klikt u op Bestand **** selecteren om door de bestandsmap te bladeren en het certificaat rechtstreeks te selecteren.

Nadat u het certificaat hebt toegevoegd, wordt de optie *Gebeurtenisregistratie* weergegeven. Klik op **Gebeurtenisregistratie** toevoegen.

![integratiedetails](../images/quality/subscribe-events/create_integration_details.png)

Het dialoogvenster *Gebeurtenisregistratiegegevens* wordt uitgebreid met extra besturingselementen. Hier kunt u de gewenste gebeurtenistypen selecteren en uw webhaak registreren. Voer een naam in voor de gebeurtenisregistratie, de URL van de webhaak *(optioneel)* en een korte beschrijving. Selecteer ten slotte de gebeurtenistypen waarop u zich wilt abonneren (gegevensinvoer-melding) en klik op **Opslaan**.

![Gebeurtenissen selecteren](../images/quality/subscribe-events/create_integration_select_event.png)

## Volgende stappen

Zodra u uw I/O integratie hebt gecreeerd kunt u om het even welke ontvangen berichten voor die integratie bekijken. Raadpleeg de handleiding [OvertrekAdobe I/O-gebeurtenissen](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) voor gedetailleerde instructies over het overtrekken van gebeurtenissen.
