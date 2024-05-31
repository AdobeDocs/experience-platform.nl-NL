---
title: Volgorde tijdstempel van klant
description: Leer hoe u tijdstempelvolgorde van klanten toevoegt aan uw gegevenssets om consistentie in uw profielgegevens te verzekeren.
badgePrivateBeta: label="Private Bèta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: f73b7ac38c681ec5161e2b5e7075f31946a6563e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Tijdstempel van klant bestellen

In Adobe Experience Platform wordt de gegevensvolgorde niet standaard gegarandeerd wanneer gegevens via streaming worden ingevoerd in de profielopslag. Met de tijdstempelbestelling van de klant kunt u garanderen dat het laatste bericht, volgens de opgegeven tijdstempel van de klant, behouden blijft in de profielopslag. Alle berichten van de waliteit zullen dan worden gelaten vallen, en zullen **niet** beschikbaar zijn voor gebruik in de stroomafwaartse diensten die profielgegevens zoals segmentatie en bestemmingen gebruiken. Hierdoor kunnen uw profielgegevens consistent zijn en blijven uw profielgegevens synchroon met uw bronsystemen.

Als u tijdstempelvolgorde van klanten wilt inschakelen, gebruikt u de optie `extSourceSystemAudit.lastUpdatedDate` in het veld [Gegevenstype Kenmerken externe bronsysteemcontrole](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/shared/external-source-system-audit-details.schema.md) en neem contact op met de technische accountmanager van de Adobe of de klantenservice van de Adobe met uw sandbox- en datasetgegevens.

## Restricties

Tijdens deze persoonlijke bètaversie zijn de volgende beperkingen van toepassing wanneer u tijdstempelbestellingen van klanten gebruikt:

- U kunt de tijdstempelvolgorde van klanten alleen gebruiken met **profielkenmerken** ingesloten met **streaming opname** in de profielenwinkel.
   - Er zijn **nee** het bestellen van garanties die zijn verstrekt voor gegevens in het datumpigment of de Identity Service.
- U kunt de tijdstempelvolgorde van de klant alleen gebruiken op **niet-productie** sandboxen.
- U kunt de tijdstempelvolgorde van klanten alleen toepassen op **5** datasets per sandbox.
- U **kan** gebruik het stromen upserts om gedeeltelijke rijupdates in een dataset te verzenden die klant toegelaten timestamp orde heeft.
- De `extSourceSystemAudit.lastUpdatedDate` field **moet** in de [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) gebruiken. Wanneer u de ISO 8601-indeling gebruikt, wordt **moet** zijn als volledige datetime in het formaat `yyyy-MM-ddTHH:mm:ss.sssZ` (bijvoorbeeld `2028-11-13T15:06:49.001Z`).
- Alle rijen met gegevens die worden ingevoerd **moet** bevatten `extSourceSystemAudit.lastUpdatedDate` veld als veldgroep op hoofdniveau. Dit betekent dat dit veld **moet** niet genest zijn binnen het XDM-schema. Als dit veld ontbreekt of een onjuiste indeling heeft, wordt de onjuiste record **niet** worden opgenomen en er wordt een overeenkomstig foutbericht verzonden.
- Om het even welke dataset die voor klant timestamp het opdracht geven wordt toegelaten **moet** zijn een nieuwe dataset zonder om het even welke eerder opgenomen gegevens.
- Voor een bepaald profielfragment alleen rijen die een recentere versie bevatten `extSourceSystemAudit.lastUpdatedDate` wordt opgenomen. Rijen die een `extSourceSystemAudit.lastUpdatedDate` ouder is of dezelfde leeftijd wordt weggegooid.

## Recommendations

Houd rekening met het volgende wanneer u tijdstempelbestellingen voor klanten implementeert:

- U bent verantwoordelijk voor het synchroniseren van de klokken op alle interne systemen die gegevens verzenden naar het archief met profielen.
- De tijdstempels in de indeling ISO 8061 moeten een precisie op millisecondenniveau hebben.
