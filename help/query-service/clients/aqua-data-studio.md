---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Verbinding maken met Aqua Data Studio
topic: connect
description: Dit document doorloopt de stappen voor het verbinden van de Studio van Gegevens Aqua met de Dienst van de Vraag van Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Verbinden met [!DNL Aqua Data Studio]

Dit document doorloopt de stappen voor het verbinden van [!DNL Aqua Data Studio] met Adobe Experience Platform [!DNL Query Service].

Nadat u [!DNL Aqua Data Studio] hebt geïnstalleerd, moet u de server eerst registreren. Klik in het hoofdmenu op **[!UICONTROL Server]** en klik vervolgens op **[!UICONTROL Server registreren]**.

![](../images/clients/aqua-data-studio/register-server.png)

Het dialoogvenster **[!UICONTROL Server registreren]** wordt weergegeven. Selecteer **[!UICONTROL PostgreSQL]** in de lijst aan de linkerkant onder het tabblad **[!UICONTROL Algemeen]**. Geef in het dialoogvenster dat wordt weergegeven de volgende gegevens op voor de serverinstellingen.

- **[!UICONTROL Naam]**: De naam van de verbinding.
- **[!UICONTROL Aanmeldnaam en wachtwoord]**: De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host en poort]**: Het gastheereindpunt en zijn haven voor  [!DNL Query Service]. U moet poort 80 gebruiken om verbinding te maken met [!DNL Query Service].
- **[!UICONTROL Database]:** de database die wordt gebruikt.

>[!NOTE]
>
>Voor meer informatie bij het vinden van uw login geloofsbrieven, gastheer, haven, en gegevensbestandnaam, bezoek de [geloofsbrieven pagina op Platform](https://platform.adobe.com/query/configuration). Om uw geloofsbrieven te vinden, login aan [!DNL Platform], klik **[!UICONTROL Vragen]**, dan klik **[!UICONTROL Referenties]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selecteer het tabblad **[!UICONTROL Stuurprogramma]**. Stel onder **[!UICONTROL Parameters]** de waarde in als `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Na het invoeren van uw verbindingsdetails, klik **[!UICONTROL Verbinding van de Test]** om uw geloofsbrieven te verzekeren behoorlijk werkt. Als uw verbinding succesvol is, klik **[!UICONTROL sparen]** om uw server te registreren. De verbinding verschijnt op **Dashboard** na succesvolle registratie, bevestigend dat u nu met de server kunt verbinden en zijn schemavoorwerpen bekijken.

## Volgende stappen

Nu u met [!DNL Query Service] hebt verbonden, kunt u **[!UICONTROL de Analysator van de Vraag]** binnen [!DNL Aqua Data Studio] gebruiken om SQL verklaringen uit te voeren en uit te geven. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen [lopende vraaggids](../best-practices/writing-queries.md).