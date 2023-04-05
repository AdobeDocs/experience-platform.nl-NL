---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;segment;segmentLidmaatschap;segmentlidmaatschap;Schemaontwerp;kaart;Kaart;
solution: Experience Platform
title: Segment Membership Details Schema Field Group
description: Dit document verstrekt een overzicht van de het schemagebiedgroep van de Details van het Lidmaatschap van het Segment.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
source-git-commit: 229dd08bc5d5dfab068db3be84ad20d10992fd31
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# [!UICONTROL Segment Membership Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../name-updates.md) voor meer informatie .

[!UICONTROL Segment Membership Details] is een standaardschemagebiedgroep voor [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md). De gebiedsgroep verstrekt één enkel kaartgebied dat informatie betreffende segmentlidmaatschap, met inbegrip van welke segmenten het individu tot, de laatste kwalificatietijd behoort, en wanneer het lidmaatschap geldig tot is.

>[!WARNING]
>
>Terwijl de `segmentMembership` moet handmatig aan uw profielschema worden toegevoegd met deze veldgroep. U moet niet handmatig proberen dit veld te vullen of bij te werken. Het systeem werkt automatisch de `segmentMembership` kaart voor elk profiel als segmentatietaken worden uitgevoerd.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `segmentMembership` | Kaart | A map object that describes the individu&#39;s segment membership. De structuur van dit object wordt hieronder in detail beschreven. |

{style="table-layout:auto"}

Hier volgt een voorbeeld `segmentMembership` kaart die het systeem voor een bepaald profiel heeft gevuld. Segmentlidmaatschappen worden gesorteerd op naamruimte, zoals aangegeven door de sleutels op hoofdniveau van het object. De afzonderlijke sleutels onder elke naamruimte vertegenwoordigen vervolgens de id&#39;s van de segmenten waarvan het profiel lid is. Elk segmentobject bevat verschillende subvelden met meer informatie over het lidmaatschap:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:version` | De versie van het segment waarvoor dit profiel in aanmerking kwam. |
| `xdm:lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `xdm:validUntil` | Een tijdstempel waarin wordt aangegeven wanneer het segmentlidmaatschap niet langer geldig is. Als dit veld niet is ingesteld voor externe doelgroepen, wordt het segmentlidmaatschap slechts 30 dagen na de datum van `lastQualificationTime`. |
| `xdm:status` | Een koordgebied dat erop wijst of het segmentlidmaatschap als deel van het huidige verzoek is gerealiseerd. De volgende waarden worden geaccepteerd: <ul><li>`realized`: Het profiel komt in aanmerking voor het segment.</li><li>`exited`: Het profiel verlaat het segment als deel van het huidige verzoek.</li></ul> |
| `xdm:payload` | Sommige segmentlidmaatschappen omvatten een lading die extra waarden beschrijft die direct met het lidmaatschap verband houden. Voor elk lidmaatschap kan slechts één lading van een bepaald type worden verstrekt. `xdm:payloadType` Hiermee wordt het type lading aangegeven (`boolean`, `number`, `propensity`, of `string`), terwijl de eigenschap sibling de waarde voor het ladingstype bevat. |

{style="table-layout:auto"}

>[!NOTE]
>
>Om het even welk segmentlidmaatschap dat in is `exited` gedurende meer dan 30 dagen, op basis van de `lastQualificationTime`, worden geschrapt.

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)
