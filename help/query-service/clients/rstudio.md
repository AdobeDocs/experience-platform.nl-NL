---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;RStudio;rstudio;verbind met de vraagdienst;
solution: Experience Platform
title: RStudio verbinden met Query Service
topic-legacy: connect
description: Dit document loopt door de stappen voor het verbinden van R Studio met de Dienst van de Vraag van Adobe Experience Platform.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Verbinden [!DNL RStudio] aan de Dienst van de Vraag

Dit document doorloopt de stappen voor het verbinden [!DNL RStudio] met Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> Deze handleiding gaat ervan uit dat u al toegang hebt tot [!DNL RStudio] en zijn vertrouwd met het gebruik ervan. Meer informatie over [!DNL RStudio] kunt u vinden in het dialoogvenster [ambtenaar [!DNL RStudio] documentatie](https://rstudio.com/products/rstudio/).
> 
> Daarnaast te gebruiken [!DNL RStudio] met de Dienst van de Vraag, moet u installeren [!DNL PostgreSQL] JDBC 4.2-stuurprogramma. U kunt het JDBC-stuurprogramma downloaden van het dialoogvenster [[!DNL PostgreSQL] officiële site](https://jdbc.postgresql.org/download/).

## Een [!DNL Query Service] verbinding in de [!DNL RStudio] interface

Na installatie [!DNL RStudio]moet u het RJDBC-pakket installeren. Ga naar de **[!DNL Packages]** en selecteert u **[!DNL Install]**.

![De [!DNL RStudio] dashboard met pakketten en installatie gemarkeerd.](../images/clients/rstudio/install-package.png)

Er wordt een pop-up weergegeven met de **[!DNL Install Packages]** scherm. Zorg ervoor dat **[!DNL Repository (CRAN)]** is geselecteerd voor de **[!DNL Install from]** sectie. De waarde voor **[!DNL Packages]** moeten `RJDBC`. Zorgen **[!DNL Install dependencies]** is geselecteerd. Nadat u hebt bevestigd dat alle waarden correct zijn, selecteert u **[!DNL Install]** om de pakketten te installeren.

![Het dialoogvenster Pakketten installeren met RJDBC is in het veld Pakketten ingevoerd en is gemarkeerd.](../images/clients/rstudio/install-jrdbc.png)

Nu het RJDBC-pakket is geïnstalleerd, start u het opnieuw op [!DNL RStudio] om het installatieproces te voltooien.

Na [!DNL RStudio] opnieuw is gestart, kunt u nu verbinding maken met Query Service. Selecteer **[!DNL RJDBC]** in de **[!DNL Packages]** en voert u de volgende opdracht in de console in:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Wanneer `{PATH TO THE POSTGRESQL JDBC JAR}` staat voor het pad naar de [!DNL PostgreSQL] JDBC JAR die op uw computer is geïnstalleerd.

Nu, kunt u uw verbinding aan de Dienst van de Vraag tot stand brengen. Ga het volgende bevel in de console in:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Zie de [[!DNL Query Service] SSL-documentatie](./ssl-modes.md) voor meer informatie over SSL-ondersteuning voor verbindingen van derden met Adobe Experience Platform Query Service en over het maken van verbindingen met deze service `verify-full` SSL-modus.

Voor meer informatie over het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, gelieve te lezen [aanmeldingsgids](../ui/credentials.md). Meld u aan om uw referenties te zoeken [!DNL Platform]selecteert u vervolgens **[!UICONTROL Queries]**, gevolgd door **[!UICONTROL Credentials]**.

![De console-uitvoer in [!DNL RStudio] van de verbinding aan de Dienst van de Vraag.](../images/clients/rstudio/connection-rjdbc.png)

## Bezig met schrijven van query&#39;s

Nu hebt u verbinding met [!DNL Query Service], kunt u vragen schrijven om SQL-instructies uit te voeren en te bewerken. U kunt bijvoorbeeld `dbGetQuery(con, sql)` om query&#39;s uit te voeren, waarbij `sql` is de SQL-query die u wilt uitvoeren.

De volgende vraag gebruikt een dataset die bevat [Experience Events](../sample-queries/experience-event.md) en maakt u een histogram van paginaweergaven van een website, op basis van de schermhoogte van het apparaat.

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

Lees voor meer informatie over het schrijven en uitvoeren van query&#39;s de handleiding op [uitvoeren, query&#39;s](../best-practices/writing-queries.md).
