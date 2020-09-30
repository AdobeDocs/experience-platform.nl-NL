---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Verbinding maken met RStudio
topic: connect
description: Dit document loopt door de stappen voor het verbinden van R Studio met de Dienst van de Vraag van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---


# Verbinden met [!DNL RStudio]

Dit document loopt door de stappen voor het verbinden van R Studio met Adobe Experience Platform [!DNL Query Service].

Na installatie [!DNL RStudio], op het scherm van de *Console* dat verschijnt, zult u eerst uw manuscript van R aan gebruik moeten voorbereiden [!DNL PostgreSQL].

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Nadat u het R-script hebt voorbereid voor gebruik, kunt u nu verbinding maken [!DNL PostgreSQL]met [!DNL RStudio] het [!DNL Query Service] [!DNL PostgreSQL] stuurprogramma.

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{DATABASE_NAME}` | De naam van de database die wordt gebruikt. |
| `{HOST_NUMBER` en `{PORT_NUMBER}` | Het gastheereindpunt en zijn haven voor de Dienst van de Vraag. |
| `{USERNAME}` en `{PASSWORD}` | De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Ga naar de pagina met [referenties op het Platform](https://platform.adobe.com/query/configuration)voor meer informatie over het zoeken naar uw databasenaam, host, poort en aanmeldingsgegevens. Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform], klikt u op **[!UICONTROL Vragen]** en vervolgens op **[!UICONTROL Referenties]**.

## Volgende stappen

Nu u met hebt verbonden, kunt u vragen schrijven om SQL verklaringen uit te voeren en uit te geven. [!DNL Query Service] U kunt bijvoorbeeld query&#39;s uitvoeren `dbGetQuery(con, sql)` om query&#39;s uit te voeren, waarbij `sql` de SQL-query is die u wilt uitvoeren.

De volgende vraag gebruikt een dataset die [ExperienceEvents](../creating-queries/experience-event-queries.md) bevat en leidt tot een histogram van paginameningen van een website, gezien de het schermhoogte van het apparaat.

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

Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [lopende vraaggids](../creating-queries/creating-queries.md).