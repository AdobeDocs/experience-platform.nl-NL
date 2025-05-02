---
keywords: Experience Platform;home;populaire onderwerpen;PSQL;psqlconnect met de vraagdienst;de dienst van de vraag;de vraagdienst;
solution: Experience Platform
title: PSQL verbinden met Query Service
description: Leer hoe u de PSQL-client aansluit op de Adobe Experience Platform Query Service, inclusief ondersteunde PostSQL-versies en installatie-instructies.
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: f75ea97e8631984dcd1d4a7f8aff3c10cba7b11f
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# PSQL verbinden met Query Service

PSQL is een bevel-lijn interface die naast PostgreSQL op uw machine wordt geïnstalleerd. In dit document worden de stappen beschreven voor het verbinden van PSQL met Adobe Experience Platform Query Service.

>[!IMPORTANT]
>
>De Dienst van de vraag steunt het verbinden met versie PSQL 14.x slechts. Versies die ouder zijn dan 14.x (zoals 10.x tot en met 13.x) en latere versies (15.x en hoger) worden niet officieel ondersteund. Controleer of u een compatibele clientversie hebt geïnstalleerd. Voor verwijzing, zie [ PostSQL Dates van het Eind van het Leven ](https://endoflife.date/postgresql).

Voordat u begint, moet u ervoor zorgen dat u toegang hebt tot PSQL en dat u vertrouwd bent met het gebruik van de client. Meer informatie over PSQL kan in de [ officiële documentatie PSQL ](https://www.postgresql.org/docs/current/app-psql.html) worden gevonden.

>[!IMPORTANT]
>
>Selecteer bij het downloaden van PostSQL versie 14.x. Standaard biedt de PostgreSQL-website de nieuwste versie aan, die mogelijk niet compatibel is met Query Service.

Zodra PSQL wordt geïnstalleerd, kunt u het met de Dienst van de Vraag verbinden. Ga terug naar de gebruikersinterface van Experience Platform en selecteer vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]** .

Onder de **[!UICONTROL PSQL Command]** sectie, selecteer het **[!UICONTROL Copy to clipboard]** pictogram (![ Pictogram van het Exemplaar ](/help/images/icons/copy.png)) om het bevelkoord te kopiëren.

![ het lusje van Referenties van het dashboard van Vragen met het benadrukte exemplaarpictogram.](../images/clients/psql/copy-credentials.png)

Plak het bevelkoord in uw terminal en druk **binnengaan** op uw toetsenbord.

>[!IMPORTANT]
>
>Als u op PC bent, gebruik een tekstredacteur om de lijnonderbrekingen in het bevelkoord te verwijderen, dan kopieer het koord. Als u versie 12.0 of hoger gebruikt, moet u `PGGSSENCMODE=disable` aan uw verbindingstekenreeks toevoegen. Met deze instelling wordt GSSAPI-codering uitgeschakeld. Dit is niet nodig voor verbindingen met Query Service en kan verbindingsfouten veroorzaken.<br> bovendien, als u niet-vervallende geloofsbrieven gebruikt, zorg ervoor u het wachtwoordgebied met het niet-vervallende credentiewachtwoord vervangt. Om meer over niet-vervallende geloofsbrieven te leren, te lezen gelieve de [ geloofsbrieven gids ](../ui/credentials.md).

U zou een resultaat als dit moeten zien:

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Als u versie 14.x niet ziet, download en installeer een gesteunde versie 14.x van PSQL van de [ officiële downloadt PostSQL pagina ](https://www.postgresql.org/download/).

>[!NOTE]
>
>Volg de installatie-instructies voor uw besturingssysteem en controleer de geïnstalleerde PSQL-versie door `psql --version` in uw terminal uit te voeren.

## Volgende stappen

Nu u met de Dienst van de Vraag hebt verbonden, kunt u PSQL gebruiken om vragen te schrijven. Zie de gids op [ lopende vragen ](../best-practices/writing-queries.md) voor meer informatie.
