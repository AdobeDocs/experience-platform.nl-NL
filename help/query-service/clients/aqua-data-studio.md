---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbinding maken met Aqua Data Studio
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Verbinden met [!DNL Aqua Data Studio]

Dit document doorloopt de stappen voor het verbinden [!DNL Aqua Data Studio] met Adobe Experience Platform [!DNL Query Service].

Na de installatie [!DNL Aqua Data Studio]moet u eerst de server registreren. Klik in het hoofdmenu op **[!UICONTROL Server]** en klik vervolgens op **[!UICONTROL Server]** registreren.

![](../images/clients/aqua-data-studio/register-server.png)

Het dialoogvenster *[!UICONTROL Server]* registreren wordt geopend. Selecteer onder het tabblad *[!UICONTROL Algemeen]* de optie **[!UICONTROL PostgreSQL]** in de lijst aan de linkerkant. Geef in het dialoogvenster dat wordt weergegeven de volgende gegevens op voor de serverinstellingen.

- **[!UICONTROL Naam]**: De naam van de verbinding.
- **[!UICONTROL Aanmeldnaam en wachtwoord]**: De aanmeldingsgegevens die worden gebruikt. De gebruikersnaam heeft de vorm van `ORG_ID@AdobeOrg`.
- **[!UICONTROL Host en poort]**: Het gastheereindpunt en zijn haven voor [!DNL Query Service].
- **[!UICONTROL Database]:**De database die wordt gebruikt.

>[!NOTE]
>
>Ga naar de pagina met [referenties op het Platform](https://platform.adobe.com/query/configuration)voor meer informatie over het zoeken naar uw aanmeldingsgegevens, host, poort en databasenaam. Als u uw referenties wilt zoeken, meldt u zich aan bij [!DNL Platform], klikt u op **[!UICONTROL Vragen]** en vervolgens op **[!UICONTROL Referenties]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Selecteer het tabblad **[!UICONTROL Stuurprogramma]** . Stel onder *[!UICONTROL Parameters]* de waarde in als `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

Nadat u de verbindingsgegevens hebt ingevoerd, klikt u op Verbinding **** testen om te controleren of uw referenties naar behoren werken. Als de verbinding tot stand is gebracht, klikt u op **[!UICONTROL Opslaan]** om de server te registreren. De verbinding wordt op het *dashboard* weergegeven als de registratie is gelukt. Hierbij wordt bevestigd dat u nu verbinding kunt maken met de server en de schemaobjecten kunt bekijken.

## Volgende stappen

Nu u verbinding hebt gemaakt met [!DNL Query Service], kunt u de *[!UICONTROL Query Analyzer]* gebruiken om SQL-instructies uit [!DNL Aqua Data Studio] te voeren en te bewerken. Voor meer informatie over hoe te om vragen te schrijven en in werking te stellen, te lezen gelieve de [lopende vraaggids](../creating-queries/creating-queries.md).