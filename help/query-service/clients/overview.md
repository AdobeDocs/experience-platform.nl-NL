---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;verbind;verbind met vraagdienst;aqua gegevensstudio;Aqua Data Studio;Looker;plukker;Postico;postico;Power BI;macht bi;psql;studio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Clients verbinden met Query-service
description: In dit document wordt uitgelegd hoe u verbinding maakt met de Query-service via een groot aantal clienttoepassingen op het bureaublad en hoe u die verbindingen kunt verifiëren.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Clients verbinden met [!DNL Query Service]

In deze sectie wordt uitgelegd hoe u verbinding maakt met [!DNL Query Service] via verschillende clienttoepassingen op het bureaublad en hoe u deze verbindingen kunt verifiëren. [!DNL Query Service] gebruikt het [!DNL PostgreSQL] -protocol, dus in de instructies in deze sectie wordt uitgelegd hoe u [!DNL PostgreSQL] -gereedschappen en -stuurprogramma&#39;s gebruikt om query&#39;s te verbinden en te schrijven.

>[!IMPORTANT]
>
>De TLS/SSL-certificaten op productieomgevingen voor de API voor interactieve posters van Query Service zijn op woensdag 24 januari 2024 vernieuwd.<br> Hoewel dit een jaarlijks vereiste is, is het wortelcertificaat in de ketting ook veranderd aangezien de het certificaatleverancier van TLS/SSL van Adobe hun certificaathiërarchie heeft bijgewerkt. Dit kan gevolgen hebben voor bepaalde klanten van Postgres als hun lijst van de Autoriteiten van het Certificaat de wortelcert mist. Een PSQL CLI-client moet bijvoorbeeld de basiscertificaten toevoegen aan een expliciet bestand `~/postgresql/root.crt` , anders kan dit resulteren in een fout. Bijvoorbeeld `psql: error: SSL error: certificate verify failed` . Zie de [ officiële documentatie PostgreSQL ](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) voor meer informatie over deze kwestie.<br> het wortelcertificaat om toe te voegen kan van [ https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem ](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem) worden gedownload.

Instructies worden gegeven voor de volgende cliënten:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>Als gebruiker van Power BI en van Tableau, kunt u Customer Journey Analytics met uw hulpmiddelen van BI van de geloofsbrieven tabel van de Dienst van de Vraag verbinden. Zie de geloofsbrieven documentatie voor instructies op hoe te [ uw hulpmiddelen van BI aan Customer Journey Analytics ](../ui/credentials.md#connect-to-customer-journey-analytics) verbinden.
