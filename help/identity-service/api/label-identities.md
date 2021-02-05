---
keywords: Experience Platform;home;populaire onderwerpen;label-id's
solution: Experience Platform
title: Een veld als identiteit labelen
topic: api guide
description: Velden met PII-gegevens (Persoonlijk identificeerbaar) kunnen als identiteitsvelden worden gemarkeerd. Een waarde die in een identiteitsveld wordt opgegeven, wordt geïnterpreteerd als een identiteit van de identiteitsdienst. De naamruimte van de identiteit wordt opgegeven als onderdeel van het labelen van het veld.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---


# Een veld labelen als identiteit

Velden met PII-gegevens (Persoonlijk identificeerbaar) kunnen als identiteitsvelden worden gemarkeerd. Een waarde die in een identiteitsveld wordt opgegeven, wordt door [!DNL Identity Service] als een identiteit geïnterpreteerd. De naamruimte van de identiteit wordt opgegeven als onderdeel van het labelen van het veld.

Een veld met het opschrift identity mag alleen aan de volgende criteria voldoen:

- Alleen tekenreekstype velden kunnen voor identiteit worden gebruikt
- Identificaties worden alleen opgenomen in gegevens uit records- en tijdreeksen
- Alleen PII-velden moeten als identiteit worden gemarkeerd. Als u een veld met meer generieke gegevens kiest, worden relaties minder nauwkeurig en kunnen er fouten optreden bij de toegang tot verwante identiteiten in de identiteitsgrafiek

Voor instructies over hoe te om de Registratie API van het Schema te gebruiken om een gebied als identiteit te etiketteren, bezoek [descriptoreindpuntgids](../../xdm/api/descriptors.md#create).

## Volgende stappen

Ga aan de volgende zelfstudie aan [lijst clusteridentiteiten](./list-cluster-identites.md)