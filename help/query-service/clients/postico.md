---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;postico;Postico;verbind met de vraagdienst;
solution: Experience Platform
title: Connect Postico aan de Dienst van de Vraag
description: Dit document bevat de koppeling voor de installatie van de back-upclient Postico for Adobe Experience Platform Query Service.
exl-id: a19abfc8-b431-4e57-b44d-c6130041af4a
source-git-commit: 9fe7e618d251867c90c88f8bee6ef5863ae78f60
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Verbinden [!DNL Postico] naar Query Service (Mac)

In dit document worden de stappen beschreven voor het verbinden [!DNL Postico] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL Postico] en zijn vertrouwd met hoe te om zijn interface te navigeren. Meer informatie over [!DNL Postico] kunt u vinden in het dialoogvenster [ambtenaar [!DNL Postico] documentatie](https://eggerapps.at/postico/docs).
> 
> Daarnaast [!DNL Postico] is **alleen** beschikbaar op macOS-apparaten.

Verbinding maken [!DNL Postico] naar Query Service, openen [!DNL Postico] en selecteert u **[!DNL New Favorite]**. Het dialoogvenster voor verbindingsinstellingen wordt weergegeven. Vanaf hier kunt u parameterwaarden invoeren om verbinding te maken met Adobe Experience Platform. Voer de hieronder vermelde verbindingsinstellingen in. Instructies over hoe [verbinding maken met een PostgreSQL-server met Postico](https://eggerapps.at/postico/docs/v1.5.21/favorite-window.html) zijn ook beschikbaar op de officiële website van Postico.

| Verbindingsparameter | Beschrijving |
|---|---|
| **[!DNL Host]:** | De hostnaam van de PostSQL-server. |
| **[!DNL Port]:** | De poort voor [!DNL Query Service]. U moet poort gebruiken **80** of **5432** om te verbinden met [!DNL Query Service]. |
| **[!DNL User]** | Maak een naam voor uw specifieke verbinding. Laat het veld leeg om uw Mac-aanmeldnaam te gebruiken. |
| **[!DNL Password]** | Deze alfanumerieke tekenreeks is uw Experience Platform **[!UICONTROL Password]** referentie. Als u niet-vervallende geloofsbrieven wilt gebruiken, is deze waarde de samengevoegde argumenten van `technicalAccountID` en de `credential` gedownload in de configuratie JSON-bestand. De wachtwoordwaarde heeft de vorm: {technicalAccountId}:{credential}. Het configuratieJSON dossier voor niet-vervallende geloofsbrieven is een eenmalig download tijdens hun initialisering die Adobe geen exemplaar van houdt. |
| **[!DNL Database]** | Uw Experience Platform gebruiken **[!UICONTROL Database]** referentie waarde: `prod:all`. |

Voor meer informatie over het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

Nadat u uw referenties hebt ingevoegd, selecteert u **[!DNL Connect]** om met de Dienst van de Vraag te verbinden.

Na het verbinden met Platform, zult u een lijst van alle relaties kunnen zien die eerder met de Dienst van de Vraag worden gemaakt.

## SQL-instructies maken

Als u een nieuwe SQL-query wilt maken, selecteert u **[!DNL SQL Query]** op de zijbalk. U kunt ook de sneltoets ( ⇧ ⌘ T) gebruiken om naar de queryweergave te navigeren en de query in te voeren die u wilt uitvoeren. Als u klaar bent, selecteert u **[!DNL Execute Statement]** om de query uit te voeren. Er wordt een tabel weergegeven met de resultaten van de voltooide query.

Zie de officiële Postico documentatie voor meer informatie over [de queryweergave gebruiken](https://eggerapps.at/postico/docs/v1.3.1/sql-query-view.html).

## Volgende stappen

Nu hebt u verbinding met [!DNL Query Service]kunt u [!DNL Postico] om query&#39;s te schrijven. Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de [gids voor uitvoeren van query&#39;s](../best-practices/writing-queries.md).
