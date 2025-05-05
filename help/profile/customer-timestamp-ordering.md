---
title: Volgorde tijdstempel van klant
description: Leer hoe u tijdstempelvolgorde van klanten toevoegt aan uw gegevenssets om consistentie in uw profielgegevens te verzekeren.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1cd9f0b5-6334-4815-860a-78596a9cea1a
source-git-commit: 57d42d88ec9a93744450a2a352590ab57d9e5bb7
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Tijdstempel van klant bestellen

In Adobe Experience Platform wordt de gegevensvolgorde niet standaard gegarandeerd wanneer gegevens via streaming worden ingevoerd in de profielopslag. Met de tijdstempelbestelling van de klant kunt u garanderen dat het laatste bericht, volgens de opgegeven tijdstempel van de klant, behouden blijft in de profielopslag. Alle stapelberichten zullen dan worden gelaten vallen, en zullen **niet** voor gebruik in de stroomafwaartse diensten beschikbaar zijn die profielgegevens zoals segmentatie en bestemmingen gebruiken. Hierdoor kunnen uw profielgegevens consistent zijn en blijven uw profielgegevens synchroon met uw bronsystemen.

Om klanten timestamp het opdracht geven tot, gebruik het `extSourceSystemAudit.lastUpdatedDate` gebied binnen de [ Externe het gebiedsgroep van de Attributen van de Controle van het Systeem van Source ](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/shared/external-source-system-audit-details.schema.md) en contacteer uw Adobe Technische Manager van de Rekening of de Zorg van de Klant van de Adobe met uw zandbak en datasetinformatie.

## Restricties

Tijdens deze persoonlijke bètaversie zijn de volgende beperkingen van toepassing wanneer u tijdstempelbestellingen van klanten gebruikt:

- U kunt klant timestamp slechts gebruiken die met **profielattributen** opdracht geven die met **worden ingebed het stromen ingestie** op de opslag van het Profiel.
   - Er zijn **geen** opdracht gevend tot garanties die voor gegevens in het gegevens meer of de Dienst van de Identiteit worden verstrekt.
- U kunt klant timestamp slechts gebruiken die op **opdracht geeft tot niet productie** zandbakken.
- U kunt klant timestamp die tot **slechts toepassen 5** datasets per zandbak opdracht geeft.
- U **kunt niet** het stromen upserts gebruiken om gedeeltelijke rijupdates in een dataset te verzenden die klant timestamp het opdracht geven tot toegelaten heeft.
- Het `extSourceSystemAudit.lastUpdatedDate` gebied **moet** in het [ formaat van ISO 8601 ](https://www.iso.org/iso-8601-date-and-time-format.html) zijn. Wanneer het gebruiken van ISO 8601 formaat, moet het **&#x200B;**&#x200B;als volledige datetime in het formaat `yyyy-MM-ddTHH:mm:ss.sssZ` (bijvoorbeeld, `2028-11-13T15:06:49.001Z`) zijn.
- Alle rijen van gegevens die **worden opgenomen moeten** het `extSourceSystemAudit.lastUpdatedDate` gebied als top level gebiedsgroep bevatten. Dit betekent dat dit gebied **&#x200B;**&#x200B;niet binnen het schema XDM moet worden genest. Als dit gebied ontbreekt of in een onjuist formaat is, zal het misvormde verslag **niet** worden opgenomen, en een overeenkomstig foutenbericht zal worden verzonden.
- Om het even welke dataset die voor klant timestamp opdracht geven tot **wordt toegelaten moet** een nieuwe dataset zonder om het even welke eerder opgenomen gegevens zijn.
- Voor een bepaald profielfragment worden alleen rijen met een recentere `extSourceSystemAudit.lastUpdatedDate` opgenomen. Rijen die een `extSourceSystemAudit.lastUpdatedDate` bevatten die ouder of even oud is, worden genegeerd.

## Aanbevelingen

Houd rekening met het volgende wanneer u tijdstempelbestellingen voor klanten implementeert:

- U bent verantwoordelijk voor het synchroniseren van de klokken op alle interne systemen die gegevens verzenden naar het archief met profielen.
- De tijdstempels in de indeling ISO 8061 moeten een precisie op millisecondenniveau hebben.
