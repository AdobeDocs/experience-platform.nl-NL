---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbinding maken met Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Verbinding maken met Aqua Data Studio

Dit document doorloopt de stappen voor het verbinden van Aqua Data Studio met de Dienst van de Vraag van het Platform van de Vraag van Adobe Experience.

Na het installeren van de Studio van Gegevens Aqua, moet u eerst de server registreren. Klik in het hoofdmenu op **Server** en klik vervolgens op **Server** registreren.

![](../images/clients/aqua-data-studio/register-server.png)

Het dialoogvenster *Server* registreren wordt geopend. Selecteer onder het tabblad *Algemeen* de optie **PostgreSQL** in de lijst aan de linkerkant. Geef in het dialoogvenster dat wordt weergegeven de volgende gegevens op voor de serverinstellingen.

- **Naam**: De naam van de verbinding.
- **Aanmeldnaam en wachtwoord**: De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.
- **Host en poort**: Het gastheereindpunt en zijn haven voor de Dienst van de Vraag.
- **Database:** De database die wordt gebruikt.

>[!NOTE] Ga voor meer informatie over het zoeken naar uw aanmeldingsgegevens, host, poort en databasenaam naar de [aanmeldingspagina op Platform](https://platform.adobe.com/query/configuration). Om uw geloofsbrieven te vinden, login aan Platform, klik **Vragen**, dan klik **Referenties**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selecteer het tabblad **Stuurprogramma** . Stel onder *Parameters* de waarde in als `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Nadat u de verbindingsgegevens hebt ingevoerd, klikt u op Verbinding **** testen om te controleren of uw referenties naar behoren werken. Als de verbinding tot stand is gebracht, klikt u op **Opslaan** om de server te registreren. De verbinding wordt op het *dashboard* weergegeven als de registratie is gelukt. Hierbij wordt bevestigd dat u nu verbinding kunt maken met de server en de schemaobjecten kunt bekijken.

## Volgende stappen

Nu u met de Dienst van de Vraag hebt verbonden, kunt u de Analysator *van de* Vraag binnen de Studio van Gegevens gebruiken Aqua om SQL verklaringen uit te voeren en uit te geven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [lopende vraaggids](../creating-queries/creating-queries.md).