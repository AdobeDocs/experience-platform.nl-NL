---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbinding maken met RStudio
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---


# Verbinding maken met RStudio

Dit document loopt door de stappen voor het verbinden van R Studio met de Dienst van de Vraag van het Adobe Experience Platform.

Nadat u RStudio hebt geïnstalleerd, moet u op het *consolescherm* dat wordt weergegeven eerst uw R-script voorbereiden om PostSQL te gebruiken.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Zodra u uw manuscript van R hebt voorbereid om PostSQL te gebruiken, kunt u RStudio aan de Dienst van de Vraag nu verbinden door de bestuurder te laden PostgreSQL.

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
>Ga naar de pagina met [referenties op het Platform](https://platform.adobe.com/query/configuration)voor meer informatie over het zoeken naar uw databasenaam, host, poort en aanmeldingsgegevens. Als u uw referenties wilt zoeken, meldt u zich aan bij het Platform, klikt u op **Vragen** en vervolgens op **Referenties**.

## Volgende stappen

Nu u met de Dienst van de Vraag hebt verbonden, kunt u vragen schrijven om SQL verklaringen uit te voeren en uit te geven. U kunt bijvoorbeeld query&#39;s uitvoeren `dbGetQuery(con, sql)` om query&#39;s uit te voeren, waarbij `sql` de SQL-query is die u wilt uitvoeren.

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