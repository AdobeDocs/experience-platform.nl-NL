---
keywords: Experience Platform;huis;populaire onderwerpen;PSQL;psqlconnect met de vraagdienst;de dienst van de vraag;de vraagdienst;
solution: Experience Platform
title: PSQL verbinden met Query Service
description: PSQL is een opdrachtregelinterface die wordt weergegeven wanneer u PostgreSQL op uw computer installeert. U kunt het installeren door deze instructies te volgen.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# PSQL verbinden met Query Service

PSQL is een opdrachtregelinterface die wordt geïnstalleerd wanneer u [!DNL PostgreSQL] op uw computer installeert. In dit document worden de stappen beschreven voor het verbinden van PSQL met Adobe Experience Platform [!DNL Query Service] .

>[!NOTE]
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL PSQL] en vertrouwd bent met het gebruik ervan. Meer informatie over [!DNL PSQL] kan in de [ officiële  [!DNL PSQL]  documentatie ](https://www.postgresql.org/docs/current/app-psql.html) worden gevonden.

Na het installeren van PSQL op uw computer, bent u klaar om PSQL met de Dienst van de Vraag te verbinden. Ga terug naar de gebruikersinterface van [!DNL Platform] en selecteer vervolgens **[!UICONTROL Queries]** , gevolgd door **[!UICONTROL Credentials]** .

Onder de **[!UICONTROL PSQL Command]** sectie, selecteer het **[!UICONTROL Copy to clipboard]** pictogram (![ Pictogram van het Exemplaar ](/help/images/icons/copy.png)) om het bevelkoord te kopiëren.

![ het lusje van Referenties van het dashboard van Vragen met het benadrukte exemplaarpictogram.](../images/clients/psql/connect-bi.png)

Plak het bevelkoord in een terminal of bevel-lijn venster en druk **binnengaan** op uw toetsenbord.

>[!IMPORTANT]
>
>Als u op PC bent, gebruik een tekstredacteur om de lijnonderbrekingen in het bevelkoord te verwijderen, dan kopieer het koord. Als u versie 12.0 of hoger gebruikt, moet u `PGGSSENCMODE=disable` aan uw verbindingstekenreeks toevoegen. Bovendien, als u niet-vervallende geloofsbrieven gebruikt, zorg ervoor u het wachtwoordgebied met het niet-vervallende credentiewachtwoord vervangt. Om meer over niet-vervallende geloofsbrieven te leren, te lezen gelieve de [ geloofsbrieven gids ](../ui/credentials.md).

U zou een resultaat als dit moeten zien:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Als u versie 10.5 of hoger niet ziet, moet u die versie of nieuwer downloaden.

## Volgende stappen

Nu u verbinding hebt met [!DNL Query Service], kunt u PSQL gebruiken om query&#39;s te schrijven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de gids op [ lopende vragen ](../best-practices/writing-queries.md).
