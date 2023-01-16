---
keywords: Experience Platform;huis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;Power BI;macht bi;verbindt met de vraagdienst;
solution: Experience Platform
title: Verbinding maken met Power BI-zoekservice
description: Dit document doorloopt de stappen voor het verbinden van Power BI met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 1%

---

# Verbinden [!DNL Power BI] aan de Dienst van de Vraag

In dit document worden de stappen beschreven voor het verbinden [!DNL Power BI] Desktop met Adobe Experience Platform Query Service.

## Aan de slag

Voor deze handleiding hebt u al toegang tot de [!DNL Power BI] bureaubladtoepassing en weet hoe u door de interface kunt navigeren. Downloaden [!DNL Power BI] Desktop of voor meer informatie, zie [ambtenaar [!DNL Power BI] documentatie](https://docs.microsoft.com/en-us/power-bi/).

>[!IMPORTANT]
>
> De [!DNL Power BI] bureaubladtoepassing is **alleen** beschikbaar op Windows-apparaten.

Om de vereiste geloofsbrieven te verkrijgen voor het verbinden [!DNL Power BI] aan Experience Platform, moet u toegang tot de werkruimte van Vragen in Platform UI hebben. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte met query&#39;s.

Na installatie [!DNL Power BI], moet u installeren `Npgsql`, een .NET stuurprogrammapakket voor PostgreSQL. Meer informatie over Npgsql vindt u in de [Npgsql-documentatie](https://www.npgsql.org/doc/index.html).

>[!IMPORTANT]
>
>U moet versie 4.0.10 of lager downloaden omdat nieuwere versies fouten opleveren.

Onder &quot;[!DNL Npgsql GAC Installation]&quot; in het aangepaste instellingenscherm selecteert u **[!DNL Will be installed on local hard drive]**.

Start de computer opnieuw op voordat u verdergaat met de volgende stappen om ervoor te zorgen dat Npgsql correct is geïnstalleerd.

## Verbinden [!DNL Power BI] aan de Dienst van de Vraag {#connect-power-bi}

Verbinding maken [!DNL Power BI] naar Query Service, openen [!DNL Power BI] en selecteert u **[!DNL Get Data]** in het bovenste menulint. Voer vervolgens &quot;[!DNL PostgreSQL]&quot; in de zoekbalk om de lijst met gegevensbronnen te beperken. Selecteer in de weergegeven resultaten de optie **[!DNL PostgreSQL database]**, gevolgd door **[!DNL Connect]**.

De [!DNL PostgreSQL] databasedialoogvenster wordt weergegeven waarin waarden voor uw server en database worden gevraagd. Aanvullende instructies over hoe te [Verbinding maken met een PostSQL-database vanaf Power Query Desktop](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-to-a-postgresql-database-from-power-query-desktop) is te vinden in de [!DNL PowerBI] documentatie.

Deze vereiste waarden zijn afkomstig van je Adobe Experience Platform-gebruikersgegevens. Meld u aan bij de gebruikersinterface van het Platform en selecteer **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Voor meer informatie over het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md).

![De werkruimte van de Vragen van het Experience Platform met het lusje van Referenties en het Verlopen van geloofsbrieven benadrukte.](../images/clients/power-bi/query-service-credentials-page.png)

In de **[!DNL Server]** van het [!DNL PostgreSQL database] in, voert u de waarde in voor de host die wordt gevonden in de Query Service [!UICONTROL Credentials] sectie. Voor productie, voeg haven toe `:80` tot het einde van de hosttekenreeks. Bijvoorbeeld, `made-up.platform-query.adobe.io:80`.

De **[!DNL Database]** het veld kan &quot;all&quot; of een tabelnaam van een gegevensset zijn. Bijvoorbeeld, `prod:all`.

>[!IMPORTANT]
>
>De genestelde gegevensstructuren in derdehulpmiddelen van BI kunnen worden afgevlakt om hun bruikbaarheid te verbeteren en de vereiste werkbelasting te verminderen om gegevens terug te winnen, te analyseren, om te zetten en te melden. Zie de documentatie op de[`FLATTEN` functie](../best-practices/flatten-nested-data.md) voor instructies over het activeren van deze instelling wanneer u verbinding maakt met een database.

### De modus Gegevensconnectiviteit {#data-connectivity-mode}

Vervolgens kunt u uw **[!DNL Data Connectivity mode]**. In de [!DNL PostgreSQL database] dialoogvenster, selecteren **[!DNL Import]** gevolgd door **[!DNL OK]** om een lijst van alle beschikbare lijsten te tonen, of selecteer **[!DNL DirectQuery]** om de gegevensbron te vragen direct zonder het invoeren van of het kopiëren van gegevens in [!DNL Power BI].

Meer informatie over de **[!DNL Import]** in de modus, lees de sectie op [een tabel importeren](#import). Meer informatie over **[!DNL DirectQuery]** in de modus, lees de sectie op [het vragen van een dataset zonder gegevens in te voeren](#direct-query).

Selecteren **[!DNL OK]** nadat u de databasedetails hebt bevestigd.

### Verificatie {#authentication}

Nadat u de gegevensconnectiviteitsmodus hebt bevestigd, verschijnt er een vraag om uw gebruikersnaam, wachtwoord en toepassingsinstellingen. De gebruikersnaam is in dit geval uw organisatie-id en het wachtwoord is uw verificatietoken. Beide zijn te vinden op de pagina van de geloofsbrieven van de Dienst van de Vraag.

Vul deze details in en selecteer vervolgens **[!DNL Connect]** om door te gaan met de volgende stap.

## Een tabel importeren {#import}

Als u **[!DNL Import]** [!DNL Data Connectivity mode], wordt de volledige dataset ingevoerd die u toestaat de geselecteerde lijsten en de kolommen binnen te gebruiken [!DNL Power BI] bureaubladtoepassing ongewijzigd.

>[!IMPORTANT]
>
>Als u de gegevenswijzigingen wilt zien die zijn opgetreden sinds de eerste importbewerking, moet u de gegevens vernieuwen binnen [!DNL Power BI] door de volledige dataset opnieuw in te voeren.

Als u een tabel wilt importeren, voert u de server- en databasedetails in [zoals hierboven beschreven](#connect-power-bi) en selecteert u de **[!DNL Import]** [!DNL Data Connectivity mode], gevolgd door **[!DNL OK]**. De [!DNL Navigator] wordt weergegeven, met daarin een lijst met alle beschikbare tabellen. Selecteer de tabel waarvan u een voorvertoning wilt weergeven, gevolgd door **[!DNL Load]** om de gegevensset in Power BI te brengen. De tabel wordt nu geïmporteerd in [!DNL Power BI].

[Algemene informatie over verbinding maken met gegevens op de PowerBi-desktop](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-quickstart-connect-to-data#connect-to-data) te vinden in de officiële documentatie.

### Tabellen importeren met behulp van aangepaste SQL

[!DNL Power BI] en andere hulpmiddelen van derden, zoals [!DNL Tableau] Hiermee kunnen gebruikers momenteel geen geneste objecten importeren, zoals XDM-objecten in Platform. Ter verantwoording, [!DNL Power BI] Hiermee kunt u aangepaste SQL gebruiken om toegang te krijgen tot deze geneste velden en een samengevoegde weergave van de gegevens te maken. [!DNL Power BI] laadt deze samengevoegde weergave van de eerder geneste gegevens vervolgens als een normale tabel.

Van de [!DNL PostgreSQL database] dialoogvenster, selecteren **[!DNL Advanced options]** om een aangepaste SQL-query in te voeren in het dialoogvenster **[!DNL SQL statement]** sectie. Deze aangepaste query moet worden gebruikt om de naam-waardeparen van JSON af te vlakken in een tabelindeling. De officiële documentatie bevat ook informatie over hoe [PowerBI aansluiten met behulp van een SQL-instructie in de geavanceerde opties](https://learn.microsoft.com/en-us/power-query/connectors/postgresql#connect-using-advanced-options).

Nadat u uw aangepaste vraag hebt ingegaan, uitgezocht **[!DNL OK]** om door te gaan met het verbinden van uw database. Zie de [verificatie](#authentication) Zie de bovenstaande sectie voor instructies voor het verbinden van een database vanuit dit gedeelte van de workflow.

Zodra de verificatie is voltooid, wordt een voorbeeld van de samengevoegde gegevens weergegeven in het dialoogvenster [!DNL Power BI] Bureaubladdashboard als een tabel. De server- en databasenaam worden boven in het dialoogvenster weergegeven. Selecteren **[!DNL Load]** om het importproces te voltooien.

De visualisaties kunnen nu worden bewerkt en geëxporteerd vanuit de [!DNL Power BI] Desktop-app.

## Vraag de dataset zonder gegevens in te voeren {#direct-query}

De **[!DNL DirectQuery]** [!DNL Data Connectivity mode] vraagt rechtstreeks de gegevensbron zonder het invoeren of het kopiëren gegevens in [!DNL Power BI] Desktop. Met deze verbindingsmodus kunt u alle visualisaties met de huidige gegevens vernieuwen via de gebruikersinterface. De tijd die nodig is om de visualisatie te produceren of te vernieuwen, is echter afhankelijk van de prestaties van de onderliggende gegevensbron.

Meer informatie over [het gebruik van [!DNL DirectQuery]](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-use-directquery) alsmede een uitvoerige discussie over zijn [connectiviteitsopties, gebruiksgevallen en beperkingen](https://learn.microsoft.com/en-us/power-bi/connect-data/desktop-directquery-about) is te vinden in de [!DNL PowerBI] documentatie.

Om dit te gebruiken [!DNL Data Connectivity mode], selecteert u de **[!DNL DirectQuery]** vervolgens schakelen **[!DNL Advanced options]** om een aangepaste SQL-query in te voeren in het dialoogvenster **[!DNL SQL statement]** sectie. Zorg ervoor dat **[!DNL Include relationship columns]** is geselecteerd. Als u de query hebt voltooid, selecteert u **[!DNL OK]** om door te gaan.

Er wordt een voorbeeld van de query weergegeven. Selecteren **[!DNL Load]** om de resultaten van de query weer te geven.

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe u verbinding kunt maken met de [!DNL Power BI] Desktop-app en de verschillende beschikbare gegevensverbindingsmodi. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, verwijs naar [richtlijnen voor het uitvoeren van query&#39;s](../best-practices/writing-queries.md).
