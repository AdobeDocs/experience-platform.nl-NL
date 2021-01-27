---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: Verbinding maken met RStudio
topic: connect
description: Dit document loopt door de stappen voor het verbinden van R Studio met de Dienst van de Vraag van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---


# Verbinden met [!DNL RStudio]

Dit document doorloopt de stappen voor het verbinden van de Studio van R met Adobe Experience Platform [!DNL Query Service].

Na het installeren [!DNL RStudio], op het *Console* scherm dat verschijnt, zult u eerst uw manuscript van R voor gebruik [!DNL PostgreSQL] moeten voorbereiden.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Nadat u uw R-script hebt voorbereid voor gebruik van [!DNL PostgreSQL], kunt u [!DNL RStudio] nu verbinden met [!DNL Query Service] door het [!DNL PostgreSQL]-stuurprogramma te laden.

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
>Voor meer informatie bij het vinden van uw gegevensbestandnaam, gastheer, haven, en login geloofsbrieven, bezoek de [geloofsbrieven pagina op Platform](https://platform.adobe.com/query/configuration). Om uw geloofsbrieven te vinden, login aan [!DNL Platform], klik **[!UICONTROL Vragen]**, dan klik **[!UICONTROL Referenties]**.

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u vragen schrijven om SQL verklaringen uit te voeren en uit te geven. U kunt bijvoorbeeld `dbGetQuery(con, sql)` gebruiken om query&#39;s uit te voeren, waarbij `sql` de SQL-query is die u wilt uitvoeren.

De volgende query gebruikt een dataset met [ExperienceEvents](../best-practices/experience-event-queries.md) en maakt een histogram van paginaweergaven van een website, gezien de schermhoogte van het apparaat.

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

Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen [lopende vraaggids](../best-practices/writing-queries.md).