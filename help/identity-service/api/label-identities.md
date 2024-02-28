---
keywords: Experience Platform;home;populaire onderwerpen;label-id's
solution: Experience Platform
title: Een veld als identiteit labelen
description: Velden met PII-gegevens (Persoonlijk identificeerbaar) kunnen als identiteitsvelden worden gemarkeerd. Een waarde die in een identiteitsveld wordt opgegeven, wordt geïnterpreteerd als een identiteit van de identiteitsdienst. De naamruimte van de identiteit wordt opgegeven als onderdeel van het labelen van het veld.
role: Developer
exl-id: f0b3f18b-7302-4a0b-b444-2d4b59787681
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 1%

---

# Een veld labelen als identiteit

Velden met PII-gegevens (Persoonlijk identificeerbaar) kunnen als identiteitsvelden worden gemarkeerd. Een waarde die in een identiteitsveld wordt opgegeven, wordt door [!DNL Identity Service]. De naamruimte van de identiteit wordt opgegeven als onderdeel van het labelen van het veld.

Een veld met het opschrift identity mag alleen aan de volgende criteria voldoen:

- Alleen tekenreekstype velden kunnen voor identiteit worden gebruikt
- Identificaties worden alleen opgenomen in gegevens uit records- en tijdreeksen
- Alleen PII-velden moeten als identiteit worden gemarkeerd. Als u een veld met meer generieke gegevens kiest, worden relaties minder nauwkeurig en kunnen er fouten optreden bij de toegang tot verwante identiteiten in de identiteitsgrafiek

Ga voor instructies over het gebruik van de API voor het registreren van het schema om een veld als identiteit te labelen naar [eindhulplijn descriptorpunt](../../xdm/api/descriptors.md#create).

## Volgende stappen

Ga naar de volgende zelfstudie om [lijst met clusteridentiteiten](./list-cluster-identites.md)
