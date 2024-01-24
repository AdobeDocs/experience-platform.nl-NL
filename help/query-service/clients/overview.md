---
keywords: Experience Platform;huis;populaire onderwerpen;de dienst van de vraag;de vraagdienst;verbind;verbind met vraagdienst;aqua gegevensstudio;Aqua Data Studio;Looker;plukker;Postico;postico;Power BI;macht bi;psql;studio;PSQL;RStudio;Tableau;tableau;
solution: Experience Platform
title: Clients verbinden met Query-service
description: In dit document wordt uitgelegd hoe u verbinding maakt met de Query-service via een groot aantal clienttoepassingen op het bureaublad en hoe u die verbindingen kunt verifiëren.
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 778c65c6310ed4a627be0fd3ae076784cfc8495b
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Verbind cliënten met [!DNL Query Service]

In deze sectie wordt uitgelegd hoe u verbinding kunt maken met [!DNL Query Service] van een verscheidenheid van Desktopcliënttoepassingen en hoe te om die verbindingen te verifiëren. [!DNL Query Service] gebruikt de [!DNL PostgreSQL] protocol, zodat verklaren de instructies in deze sectie hoe te gebruiken [!DNL PostgreSQL] tools en stuurprogramma&#39;s voor het maken van verbindingen en het schrijven van query&#39;s.

>[!IMPORTANT]
>
>De TLS/SSL-certificaten op productieomgevingen voor de API voor interactieve posters van Query Service zijn op woensdag 24 januari 2024 vernieuwd.<br>Hoewel dit een jaarlijkse vereiste is, is het basiscertificaat in de keten in dit geval ook gewijzigd omdat de TLS/SSL-certificaatleverancier van de Adobe de certificaathiërarchie heeft bijgewerkt. Dit kan gevolgen hebben voor bepaalde klanten van Postgres als hun lijst van de Autoriteiten van het Certificaat de wortelcert mist. Bijvoorbeeld, kan een cliënt PSQL CLI de wortelcertificaten moeten hebben aan een expliciet dossier worden toegevoegd `~/postgresql/root.crt`anders kan dit resulteren in een fout. Bijvoorbeeld: `psql: error: SSL error: certificate verify failed`. Zie de [officiële documentatie van PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) voor meer informatie over dit onderwerp .<br>Het basiscertificaat dat moet worden toegevoegd, kan worden gedownload van [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Instructies worden gegeven voor de volgende cliënten:

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)
