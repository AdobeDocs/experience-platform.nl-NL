---
keywords: Experience Platform;huis;populaire onderwerpen;PSQL;psqlconnect met de vraagdienst;de dienst van de vraag;de vraagdienst;
solution: Experience Platform
title: PSQL verbinden met Query Service
topic-legacy: connect
description: PSQL is een opdrachtregelinterface die wordt weergegeven wanneer u PostgreSQL op uw computer installeert. U kunt het installeren door deze instructies te volgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# PSQL verbinden met Query Service

PSQL is een opdrachtregelinterface die wordt geïnstalleerd wanneer u [!DNL PostgreSQL] op uw computer installeert. In dit document worden de stappen beschreven voor het verbinden van PSQL met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze gids veronderstelt u reeds toegang tot [!DNL PSQL] hebt en vertrouwd met hoe te om het te gebruiken. Meer informatie over [!DNL PSQL] vindt u in de [officiële [!DNL PSQL] documentatie] (https://www.postgresql.org/docs/current/app-psql.html.

Na het installeren van PSQL op uw computer, bent u klaar om PSQL met de Dienst van de Vraag te verbinden. Ga terug naar [!DNL Platform] UI, dan uitgezocht **[!UICONTROL Queries]**, die door **[!UICONTROL Credentials]** wordt gevolgd.

![Image](../images/clients/psql/connect-bi.png)

Selecteer het pictogram om de sectie te kopiëren geëtiketteerd **[!UICONTROL PSQL Command]**, dan kleef het bevelkoord in een terminal of bevel-lijn venster alvorens te drukken gaat binnen.

>[!IMPORTANT]
>
>Als u op PC bent, gebruik een tekstredacteur om de lijnonderbrekingen in het bevelkoord te verwijderen, dan kopieer het koord. Bovendien, als u versie 12.0 of groter gebruikt, zult u `PGGSSENCMODE=disable` aan uw verbindingskoord moeten toevoegen.

U zou een resultaat als dit moeten zien:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Als u versie 10.5 of hoger niet ziet, moet u die versie of nieuwer downloaden.

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u PSQL gebruiken om vragen te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de gids op [lopende vragen](../best-practices/writing-queries.md).
