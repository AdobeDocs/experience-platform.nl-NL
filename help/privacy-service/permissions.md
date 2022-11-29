---
title: Rechten voor Privacy Service beheren
description: Leer hoe u gebruikersmachtigingen voor Adobe Experience Platform Privacy Service beheert met Adobe Admin Console.
source-git-commit: 59dc28a84971dc8c21d633741cfe2dc1b44ea1a6
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# Machtigingen voor Privacy Service beheren

Toegang tot [Adobe Experience Platform Privacy Service](./home.md) wordt gecontroleerd door granulaire op rol-gebaseerde toestemmingen in Adobe Admin Console. Door productprofielen te creëren die toestemmingen aan groepen gebruikers toewijzen, kunt u bepalen wie toegang heeft tot welke eigenschappen in de Privacy Service [UI](./ui/overview.md) en [API](./api/overview.md).

>[!NOTE]
>
>Wanneer u een integratie maakt voor de Privacy Service-API, moet u een bestaand productprofiel selecteren om te bepalen voor welke functies of handelingen integratiemachtigingen gelden. Zie de handleiding op [aan de slag met de Privacy Service-API](./api/getting-started.md) voor meer informatie .

In deze handleiding ziet u hoe u machtigingen voor Privacy Service beheert.

## Aan de slag

Om toegangsbeheer voor Privacy Service te vormen, moet u beheerdervoorrechten voor een organisatie hebben die een productintegratie met Adobe Experience Platform Privacy Service heeft. De minimale rol die machtigingen kan verlenen of intrekken, is een **productprofielbeheerder**. Andere beheerderrollen die toestemmingen kunnen beheren zijn **productbeheerders** (kan alle profielen in een product beheren) en **systeembeheerders** (geen beperkingen). Zie het artikel over [administratieve taken](https://helpx.adobe.com/enterprise/using/admin-roles.html) in de Adobe Enterprise Administration guide voor meer informatie.

Deze gids veronderstelt u vertrouwd met basisconcepten van de Admin Console zoals productprofielen en hoe zij producttoestemmingen aan individuele gebruikers en groepen verlenen. Zie voor meer informatie de [Gebruikershandleiding voor Admin Consoles](https://helpx.adobe.com/enterprise/using/admin-console.html).

## Beschikbare machtigingen

De volgende lijst schetst de beschikbare toestemmingen voor Privacy Service met beschrijvingen van de specifieke mogelijkheden die zij toegang verlenen tot:

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Privacy Read Permission] | Bepaalt of de gebruiker bestaande toegang en schrappingsverzoeken, samen met hun details kan bekijken. |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Privacy Write Permission] | Hiermee wordt bepaald of een gebruiker nieuwe toegangs- en verwijderverzoeken kan maken. |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Read (Access) Content Delivery Permission] | Wanneer een toegangsverzoek door Privacy Service wordt verwerkt, wordt een dossier van het PIT die de gegevens van de klant bevat verzonden naar die klant. Wanneer het omhoog zoeken van de details van een toegangsverzoek, bepaalt deze toestemming of de gebruiker tot de downloadverbinding voor het dossier van het ZIP van het verzoek kan toegang hebben. |
| [!UICONTROL Opt Out of Sale Permissions] | [!UICONTROL Read Permission - Opt Out of Sale] | Bepaalt of de gebruiker bestaande opt-out-of-sales verzoeken, samen met hun details kan bekijken. |
| [!UICONTROL Opt Out of Sale Permissions] | [!UICONTROL Write Permission - Opt Out of Sale] | Bepaalt of een gebruiker nieuwe opt-out-of-verkoop verzoeken kan tot stand brengen. |

{style=&quot;table-layout:auto&quot;}

## Machtigingen beheren {#manage}

Om de toestemmingen van de Privacy Service te beheren, login aan [Admin Console](https://adminconsole.adobe.com/) en selecteert u **[!UICONTROL Products]** in de bovenste navigatie. Selecteer **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![Afbeelding van de Privacy Service productkaart in Admin Console](./images/permissions/privacy-service-card.png)

### Een productprofiel selecteren of maken

In het volgende scherm ziet u een lijst met beschikbare productprofielen voor Privacy Service onder uw organisatie. Als er geen productprofielen bestaan, selecteert u **[!UICONTROL New Profile]** om er een te maken. Als u veelvoudige rollen of gebruikersgroepen in uw organisatie hebt die verschillende niveaus van toegang vereisen, zou u een afzonderlijk productprofiel voor elk van hen moeten creëren.

![Afbeelding met de productprofielen voor Privacy Service in Admin Console](./images/permissions/select-or-create-profile.png)

Nadat u een productprofiel hebt geselecteerd, kunt u de opdracht **[!UICONTROL Permissions]** te beginnen tab [bewerken, machtigingen](#edit-permissions) voor het profiel, of selecteer **[!UICONTROL Users]** te beginnen tab [gebruikers toewijzen](#assign-users) naar het profiel.

![Afbeelding met het tabblad Machtigingen voor een Admin Console met productprofielen](./images/permissions/users-permissions-tabs.png)

### Machtigingen voor het profiel bewerken {#edit-permissions}

Op de **[!UICONTROL Permissions]** selecteert u een van de weergegeven machtigingscategorieën voor toegang tot de weergave voor bewerken van machtigingen.

Wanneer u machtigingen voor een profiel bewerkt, worden in de linkerkolom de beschikbare machtigingen vermeld, terwijl de machtigingen die in het profiel zijn opgenomen in de rechterkolom worden weergegeven. Selecteer de vermelde toestemmingen om hen tussen één van beide kolom te bewegen.

![Afbeelding met de beschikbare en opgenomen machtigingskolommen](./images/permissions/edit-permissions.png)

Machtigingen zijn ingedeeld in categorieën. Als u wilt schakelen tussen categorieën, selecteert u de gewenste categorie in de linkernavigatie.

![Afbeelding die de [!UICONTROL Opt Out of Sale] sectie onder machtigingen](./images/permissions/switch-category.png)

Selecteren **[!UICONTROL Save]** zodra u klaar bent met het configureren van machtigingen.

![Afbeelding met de machtigingsconfiguratie die wordt opgeslagen voor het productprofiel](./images/permissions/save-permissions.png)

De weergave van het productprofiel wordt opnieuw weergegeven met de toegevoegde machtigingen weergegeven.

![Afbeelding met de toegevoegde machtigingen voor het productprofiel](./images/permissions/permissions-added.png)

### Gebruikers toewijzen aan het profiel {#assign-users}

Als u gebruikers wilt toewijzen aan het productprofiel (en hun de geconfigureerde machtigingen van het profiel wilt verlenen), selecteert u de optie **[!UICONTROL Users]** tab, gevolgd door **[!UICONTROL Add user]**.

![Afbeelding die het tabblad Gebruikers voor een productprofiel in Admin Console weergeeft](./images/permissions/manage-users.png)

Voor meer informatie over het beheren van gebruikers voor een productprofiel raadpleegt u de [Documentatie Admin Console](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html).

### Verouderde API-referenties migreren naar het profiel {#migrate-tech-accounts}

>[!NOTE]
>
>Deze sectie is alleen van toepassing op bestaande API-referenties die zijn gemaakt voordat Privacy Service-machtigingen in Adobe Admin Console werden geïntegreerd. Voor nieuwe referenties worden productprofielen (en hun machtigingen) toegewezen via [Adobe Developer Console-projecten](https://developer.adobe.com/developer-console/docs/guides/projects/) in plaats daarvan.<br><br>Zie de sectie over [productprofielen toewijzen aan een project](./api/getting-started.md#product-profiles) in de gids Aan de slag van de Privacy Service API voor meer informatie.

Selecteer **[!UICONTROL API Credentials]**, gevolgd door **[!UICONTROL Add API Credentials]**.

![[!UICONTROL Add API Credentials] die in Admin Console worden geselecteerd, onder [!UICONTROL API Credentials] tabblad voor een productprofiel](./images/permissions/api-credentials.png)

Kies de gewenste projecten van de Console van de Ontwikkelaar van de lijst, dan selecteer **[!UICONTROL Save]** om deze aan het productprofiel toe te voegen. Alle API vraag die de geloofsbrieven van deze projecten gebruikt zal de korrelige toestemmingen erven die door het productprofiel worden verleend.

## Volgende stappen

Deze gids behandelde de beschikbare toestemmingen voor Privacy Service en hoe te om hen door Admin Console te beheren.

Raadpleeg voor meer informatie over het maken van een nieuwe API-integratie nadat u productprofielen hebt ingesteld de [Aan de slag-handleiding voor de Privacy Service-API](./api/getting-started.md). Raadpleeg voor meer informatie over het beheren van machtigingen voor andere Adobe Experience Platform-mogelijkheden de [toegangsbeheerdocumentatie](../access-control/home.md).
