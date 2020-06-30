---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een veld als identiteit labelen
topic: api guide
translation-type: tm+mt
source-git-commit: 6ffdcc2143914e2ab41843a52dc92344ad51bcfb
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 1%

---


# Een veld als identiteit labelen

Velden met PII-gegevens (Persoonlijk identificeerbaar) kunnen als identiteitsvelden worden gemarkeerd. Een waarde in een identiteitsveld wordt geïnterpreteerd als een identiteit door [!DNL Identity Service]. De naamruimte van de identiteit wordt opgegeven als onderdeel van het labelen van het veld.

Een veld met het opschrift identity mag alleen aan de volgende criteria voldoen:

- Alleen tekenreekstype velden kunnen voor identiteit worden gebruikt
- Identificaties worden alleen opgenomen in gegevens uit records- en tijdreeksen
- Alleen PII-velden moeten als identiteit worden gemarkeerd. Als u een veld met meer generieke gegevens kiest, worden relaties minder nauwkeurig en kunnen er fouten optreden bij de toegang tot verwante identiteiten in de identiteitsgrafiek

Voor instructies over het gebruik van de API voor het registreren van het schema om een veld als identiteit te labelen, gaat u naar [Een descriptor](../../xdm/api/descriptors.md)maken.

## Volgende stappen

Ga naar de volgende zelfstudie om clusteridentiteiten [weer te geven](./list-cluster-identites.md)