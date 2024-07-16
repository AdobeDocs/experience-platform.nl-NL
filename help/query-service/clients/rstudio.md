---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;RStudio;rstudio;verbind met de vraagdienst;
solution: Experience Platform
title: RStudio verbinden met Query Service
description: Dit document loopt door de stappen voor het verbinden van R Studio met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Verbinden [!DNL RStudio] met de Dienst van de Vraag

In dit document worden de stappen doorlopen waarmee u [!DNL RStudio] kunt verbinden met Adobe Experience Platform [!DNL Query Service] .

>[!NOTE]
>
> [!DNL RStudio] is nu herbrandd als [!DNL Posit] . De naam van [!DNL RStudio] -producten is gewijzigd in [!DNL Posit Connect] , [!DNL Posit Workbench] , [!DNL Posit Package] Manager [!DNL Posit Cloud] en [!DNL Posit Academy] .
>
> In deze handleiding wordt ervan uitgegaan dat u al toegang hebt tot [!DNL RStudio] en vertrouwd bent met het gebruik ervan. Meer informatie over [!DNL RStudio] kan in de [ officiële  [!DNL RStudio]  documentatie ](https://rstudio.com/products/rstudio/) worden gevonden.
> 
> Als u [!DNL RStudio] wilt gebruiken met Query Service, moet u bovendien het [!DNL PostgreSQL] JDBC 4.2-stuurprogramma installeren. U kunt de bestuurder JDBC van de [[!DNL PostgreSQL]  officiële plaats ](https://jdbc.postgresql.org/download/) downloaden.

## Een [!DNL Query Service] -verbinding maken in de [!DNL RStudio] -interface

Nadat u [!DNL RStudio] hebt geïnstalleerd, moet u het RJDBC-pakket installeren. De instructies op hoe te om [ een gegevensbestand door de bevellijn ](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) te verbinden kunnen in de officiële documentatie van de Positie worden gevonden.

Als u een Mac OS gebruikt, kunt u **[!UICONTROL Tools]** selecteren in de menubalk gevolgd door **[!UICONTROL Install Packages]** in het vervolgkeuzemenu. U kunt ook het tabblad **[!DNL Packages]** in de UI voor het bewerken van RStudio selecteren en **[!DNL Install]** selecteren.

Er verschijnt een pop-up met daarin het **[!DNL Install Packages]** -scherm. Zorg ervoor dat **[!DNL Repository (CRAN)]** is geselecteerd voor de sectie **[!DNL Install from]** . De waarde voor **[!DNL Packages]** moet `RJDBC` zijn. Zorg ervoor dat **[!DNL Install dependencies]** is geselecteerd. Nadat u hebt bevestigd dat alle waarden correct zijn, selecteert u **[!DNL Install]** om de pakketten te installeren. Nu het RJDBC-pakket is geïnstalleerd, start u [!DNL RStudio] opnieuw om het installatieproces te voltooien.

Nadat [!DNL RStudio] opnieuw is gestart, kunt u nu verbinding maken met Query Service. Selecteer het **[!DNL RJDBC]** -pakket in het deelvenster **[!DNL Packages]** en voer de volgende opdracht in de console in:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Waar `{PATH TO THE POSTGRESQL JDBC JAR}` het pad vertegenwoordigt naar de [!DNL PostgreSQL] JDBC JAR die op uw computer is geïnstalleerd.

Nu, kunt u uw verbinding aan de Dienst van de Vraag creëren. Ga het volgende bevel in de console in:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service]  SSL documentatie ](./ssl-modes.md) om over SSL steun voor derdeverbindingen aan de Dienst van de Vraag van Adobe Experience Platform te leren, en hoe te om het gebruiken van `verify-full` SSL wijze te verbinden.

Voor meer informatie bij het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, te lezen gelieve de [ gids van geloofsbrieven ](../ui/credentials.md). Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform] en selecteert u **[!UICONTROL Queries]** , gevolgd door **[!UICONTROL Credentials]** .

Een bericht in de consoleoutput bevestigt de verbinding aan de Dienst van de Vraag.

## Bezig met schrijven van query&#39;s

Nu u verbinding hebt gemaakt met [!DNL Query Service] , kunt u query&#39;s schrijven om SQL-instructies uit te voeren en te bewerken. U kunt `dbGetQuery(con, sql)` bijvoorbeeld gebruiken om query&#39;s uit te voeren, waarbij `sql` de SQL-query is die u wilt uitvoeren.

De volgende vraag gebruikt een dataset die [ Gebeurtenissen van de Ervaring ](../../xdm/classes/experienceevent.md) bevat en leidt tot een histogram van paginameningen van een website, gezien de het schermhoogte van het apparaat.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Een succesvol antwoord retourneert de resultaten van de query:

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

## Volgende stappen

Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de gids op [ lopende vragen ](../best-practices/writing-queries.md).
