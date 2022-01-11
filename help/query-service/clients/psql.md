---
keywords: Experience Platform;huis;populaire onderwerpen;PSQL;psqlconnect met de vraagdienst;de dienst van de vraag;de vraagdienst;
solution: Experience Platform
title: PSQL verbinden met Query Service
topic-legacy: connect
description: PSQL is een opdrachtregelinterface die wordt weergegeven wanneer u PostgreSQL op uw computer installeert. U kunt het installeren door deze instructies te volgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 06d3a8aa6f2f73c2d5392a76fb5b36b18691cf0d
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

---

# PSQL verbinden met Query Service

PSQL is een opdrachtregelinterface die wordt geïnstalleerd wanneer u de software installeert [!DNL PostgreSQL] op uw computer. In dit document worden de stappen beschreven voor het verbinden van PSQL met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL PSQL] en zijn vertrouwd met het gebruik ervan. Meer informatie over [!DNL PSQL] kunt u vinden in het dialoogvenster [ambtenaar [!DNL PSQL] documentatie](https://www.postgresql.org/docs/current/app-psql.html).

Na het installeren van PSQL op uw computer, bent u klaar om PSQL met de Dienst van de Vraag te verbinden. Terugkeren naar de [!DNL Platform] UI, dan selecteren **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

![Image](../images/clients/psql/connect-bi.png)

Selecteer het pictogram om de sectie met het label te kopiëren **[!UICONTROL PSQL Command]**, dan kleef het bevelkoord in een terminal of bevel-lijn venster alvorens binnen te drukken.

>[!IMPORTANT]
>
>Als u op PC bent, gebruik een tekstredacteur om de lijnonderbrekingen in het bevelkoord te verwijderen, dan kopieer het koord. Als u versie 12.0 of hoger gebruikt, moet u toevoegen `PGGSSENCMODE=disable` naar de verbindingstekenreeks. Bovendien, als u niet-vervallende geloofsbrieven gebruikt, zorg ervoor u het wachtwoordgebied met het niet-vervallende credentiewachtwoord vervangt. Als u meer wilt weten over niet-vervallende gegevens, leest u de [aanmeldingsgids](../ui/credentials.md).

U zou een resultaat als dit moeten zien:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Als u versie 10.5 of hoger niet ziet, moet u die versie of nieuwer downloaden.

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service], kunt u PSQL gebruiken om vragen te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
