---
keywords: Experience Platform;home;populaire onderwerpen;Query-service;queryservice;connect;connect met queryservice;aqua data studio;Aqua Data Studio;Looker;looker;Postico;postico;Power BI;power bi;psql;studio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Clients verbinden met Query-service
description: In dit document wordt uitgelegd hoe u verbinding maakt met de Query-service via een groot aantal clienttoepassingen op het bureaublad en hoe u die verbindingen kunt verifiëren.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Client verbinden met Query-service

Deze sectie verklaart hoe te met de Dienst van de Vraag van een verscheidenheid van Desktopcliënttoepassingen te verbinden en hoe te om die verbindingen te verifiëren. De Dienst van de vraag gebruikt het protocol PostgreSQL, zodat verklaren de instructies in deze sectie hoe te om de hulpmiddelen en de bestuurders te gebruiken PostgreSQL om vragen te verbinden en te schrijven.

>[!IMPORTANT]
>
>De TLS/SSL-certificaten op productieomgevingen voor de API voor interactieve posters van Query Service zijn op woensdag 24 januari 2024 vernieuwd.<br> Hoewel dit een jaarlijks vereiste is, is het wortelcertificaat in de ketting ook veranderd aangezien de Adobe TLS/SSL certificaatleverancier hun certificaathiërarchie heeft bijgewerkt. Dit kan gevolgen hebben voor bepaalde klanten van Postgres als hun lijst van de Autoriteiten van het Certificaat de wortelcert mist. Een PSQL CLI-client moet bijvoorbeeld de basiscertificaten toevoegen aan een expliciet bestand `~/postgresql/root.crt` , anders kan dit resulteren in een fout, zoals `psql: error: SSL error: certificate verify failed` . Zie de [&#x200B; officiële documentatie PostgreSQL &#x200B;](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) voor meer informatie over deze kwestie.<br> het wortelcertificaat om toe te voegen kan van [&#x200B; https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem &#x200B;](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem) worden gedownload.

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
>Als Power BI- en Tableau-gebruiker kunt u Customer Journey Analytics verbinden met uw BI-hulpprogramma&#39;s aan de hand van de referenties die op het tabblad Query Service zijn vermeld. Zie de geloofsbrieven documentatie voor instructies op hoe te [&#x200B; uw hulpmiddelen van BI met Customer Journey Analytics &#x200B;](../ui/credentials.md#connect-to-customer-journey-analytics) verbinden.
