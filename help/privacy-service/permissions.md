---
title: Rechten voor Privacy Service beheren
description: Leer hoe u gebruikersmachtigingen voor Adobe Experience Platform Privacy Service beheert met Adobe Admin Console.
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 1e164166f58540cbaaa4ad789b10cdfc40fa8a70
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 1%

---

# Machtigingen voor Privacy Service beheren

>[!IMPORTANT]
>
>De machtigingen voor Adobe Experience Platform Privacy Service zijn verbeterd om hun granulariteit te verhogen. Deze veranderingen laten organisatiebeheerders toe om meer gebruikers toegang met de gewenste rol en toestemmingsniveau te verlenen. Gebruikers van technische accounts moeten hun machtigingen voor Privacys Service bijwerken, omdat deze op handen zijnde update voor hen een baanbrekende wijziging vormt. De handhaving van deze wijziging van machtigingen vindt plaats op **13 april 2023**. Zie de documentatie op [migreren van verouderde API-gegevens](#migrate-tech-accounts) richtsnoeren voor het oplossen van dit probleem.
>
>De technische rekeningen zijn beschikbaar aan ondernemingsklanten en gecreeerd door de Console van de Ontwikkelaars van Adobe. De Adobe ID van een technische rekeninghouder eindigt in `@techacct.adobe.com`. Als u niet zeker weet of u een technische rekeninghouder bent, neemt u contact op met uw organisatiebeheerder.

Toegang tot [Adobe Experience Platform Privacy Service](./home.md) wordt gecontroleerd door granulaire op rol-gebaseerde toestemmingen in Adobe Admin Console. Door productprofielen te creëren die toestemmingen aan groepen gebruikers toewijzen, kunt u bepalen wie toegang heeft tot welke eigenschappen in de Privacy Service [UI](./ui/overview.md) en [API](./api/overview.md).

>[!NOTE]
>
>Wanneer u een integratie maakt voor de Privacy Service-API, moet u een bestaand productprofiel selecteren om te bepalen voor welke functies of handelingen integratiemachtigingen gelden. Zie de handleiding op [aan de slag met de Privacy Service-API](./api/getting-started.md) voor meer informatie .

In deze handleiding ziet u hoe u machtigingen voor Privacy Service beheert.

## Aan de slag

Om toegangsbeheer voor Privacy Service te vormen, moet u beheerdervoorrechten voor een organisatie hebben die een productintegratie met Adobe Experience Platform Privacy Service heeft. De minimale rol die machtigingen kan verlenen of intrekken, is een **productprofielbeheerder**. Andere beheerderrollen die toestemmingen kunnen beheren zijn **productbeheerders** (kan alle profielen in een product beheren) en **systeembeheerders** (geen beperkingen). Zie het artikel over [administratieve taken](https://helpx.adobe.com/enterprise/using/admin-roles.html) in de Adobe Enterprise Administration guide voor meer informatie.

Deze gids veronderstelt u vertrouwd met basisconcepten van de Admin Console zoals productprofielen en hoe zij producttoestemmingen aan individuele gebruikers en groepen verlenen. Zie voor meer informatie de [Gebruikershandleiding voor Admin Consoles](https://helpx.adobe.com/nl/enterprise/using/admin-console.html).

## Beschikbare machtigingen

De volgende lijst schetst de beschikbare toestemmingen voor Privacy Service met beschrijvingen van de specifieke mogelijkheden die zij toegang verlenen tot:

>[!NOTE]
>
>Alle Privacy Service en [!UICONTROL Opt Out of Sale] machtigingen zijn gescheiden en gescheiden van elkaar, zonder functionele overlapping. Dit is mogelijk omdat de Privacy Service-API als een epidemie wordt beschouwd.

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Privacy Read Permission] | Bepaalt of de gebruiker bestaande toegang en schrappingsverzoeken, samen met hun details kan bekijken. |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Privacy Write Permission] | Hiermee wordt bepaald of een gebruiker nieuwe toegangs- en verwijderverzoeken kan maken. |
| [!UICONTROL Privacy Service Permissions] | [!UICONTROL Read (Access) Content Delivery Permission] | Wanneer een toegangsverzoek door Privacy Service wordt verwerkt, wordt een dossier van het PIT die de gegevens van de klant bevat verzonden naar die klant. Wanneer het omhoog zoeken van de details van een toegangsverzoek, bepaalt deze toestemming of de gebruiker tot de downloadverbinding voor het dossier van het ZIP van het verzoek kan toegang hebben. |
| [!UICONTROL Opt Out of Sale Permissions] | [!UICONTROL Read Permission - Opt Out of Sale] | Bepaalt of de gebruiker bestaande opt-out-of-sales verzoeken, samen met hun details kan bekijken. |
| [!UICONTROL Opt Out of Sale Permissions] | [!UICONTROL Write Permission - Opt Out of Sale] | Bepaalt of een gebruiker nieuwe opt-out-of-verkoop verzoeken kan tot stand brengen. |

{style="table-layout:auto"}

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

Eerder hadden technische accounts geen productprofiel voor integratie en machtigingen nodig. Vanwege recente verbeteringen in de machtigingen voor Privacys Service is het nu echter nodig om oude API-gegevens te migreren naar het productprofiel. Met deze update kunnen granulaire machtigingen worden verleend aan houders van technische accounts. Volg de onderstaande stappen om technische accountmachtigingen voor Privacy Service bij te werken.

#### Technische accountmachtigingen bijwerken {#update-tech-account-permissions}

De eerste stap bij het toewijzen van een rechtenset voor uw technische account is naar de [Adobe Admin Console](https://adminconsole.adobe.com/) en maak een nieuw productprofiel voor Privacy Service.

Selecteer in de gebruikersinterface van de Admin Console de optie **Producten** vanuit de navigatiebalk, gevolgd door **[!UICONTROL Experience Cloud]** en **[!UICONTROL Adobe Experience Platform Privacy Service]** in de linkerzijbalk. De [!UICONTROL Product Profiles] wordt weergegeven. Selecteren **Nieuw profiel** om een nieuw productprofiel voor Privacy Service te maken.

![Het tabblad Productprofielen Experience Platform Privacy Service in Adobe Admin Console met Nieuw profiel gemarkeerd.](./images/permissions/create-product-profile.png)

De [!UICONTROL Create a new product profile] wordt weergegeven. Volledige instructies over het maken van een productprofiel vindt u in het gedeelte [UI-gids voor het maken van profielen](../access-control/ui/create-profile.md).

Nadat u het nieuwe productprofiel hebt opgeslagen, navigeert u naar de [Adobe Developer Console](https://developer.adobe.com/console/home) en meld u aan bij dat product of dat project. Selecteren **[!UICONTROL Projects]** vanaf de bovenste navigatie, gevolgd door de kaart voor uw project.

>[!NOTE]
>
>U moet mogelijk uw cache wissen en/of enige tijd wachten totdat het nieuwe project in uw lijst met projecten voor de Developer Console wordt weergegeven.

Nadat u zich in uw project hebt aangemeld, selecteert u **[!UICONTROL Privacy Service API]** integratie vanuit de linkerzijbalk.

![Het tabblad Projecten van de Adobe Developer Console met projecten en Privacy Service-API is gemarkeerd.](./images/permissions/login-to-dev-console-project.png)

Het Privacy Service API-integratiedashboard wordt weergegeven. Vanuit dit dashboard kunt u het productprofiel bewerken dat aan dat project is gekoppeld. Selecteren **[!UICONTROL Edit product profiles]** om het proces te starten. De [!UICONTROL Configure API] wordt weergegeven.

![Het Privacy Service API-integratiedashboard in de Adobe Developer-console met de markering Productprofielen bewerken](./images/permissions/edit-product-profiles.png)

De [!UICONTROL Configure API] toont de beschikbare productprofielen die momenteel in de dienst bestaan. Ze correleren met de productprofielen die in de beheerconsole zijn gemaakt. Selecteer in de lijst met beschikbare productprofielen het selectievakje voor het nieuwe productprofiel dat u voor de technische account in de beheerconsole hebt gemaakt. Dit associeert automatisch deze technische rekening met de toestemmingen in het geselecteerde productprofiel. Selecteren **[!UICONTROL Save configured API]** om uw instellingen te bevestigen.

>[!NOTE]
>
>Als er al een technische account is gekoppeld aan een productprofiel, wordt al een van de selectievakjes in de lijst met beschikbare productprofielen geselecteerd.

![Het dialoogvenster API configureren in Adobe Developer Console met het selectievakje Productprofiel en geconfigureerde API opslaan gemarkeerd.](./images/permissions/select-profile-for-tech-account.png)

#### Bevestig dat de instellingen zijn toegepast {#confirm-applied-settings}

Bevestig dat uw instellingen zijn toegepast op het account. Terugkeren naar de [Admin Console](https://adminconsole.adobe.com/) en navigeer naar het nieuwe productprofiel. Selecteer **[!UICONTROL API Credentials]** tabblad om een lijst met verwante projecten weer te geven. Het project dat in de Console van de Ontwikkelaar wordt gebruikt waar u het productprofiel aan de technische rekening toewees wordt getoond in de lijst van geloofsbrieven die. De naam van elke API-referentie bestaat uit de projectnaam met een willekeurig gegenereerd nummer dat aan het einde is achtervoegd. Selecteer een referentie om het dialoogvenster [!UICONTROL Details] deelvenster.

![Een productprofiel in de Admin Console met de API geloofsbrieven tabel en een rij van benadrukte projectgeloofsbrieven.](./images/permissions/confirm-credentials-in-admin-console.png)

De [!UICONTROL Details] bevat informatie over de API-referentie, waaronder de bijbehorende technische id, de API-sleutel, de datum die is gemaakt en gewijzigd, en de bijbehorende Adobe-producten.

![Het gemarkeerde deelvenster Details van een API-referentie in de Admin Console.](./images/permissions/admin-console-details-panel.png)

## Volgende stappen

Deze gids behandelde de beschikbare toestemmingen voor Privacy Service en hoe te om hen door Admin Console te beheren.

Raadpleeg voor meer informatie over het maken van een nieuwe API-integratie nadat u productprofielen hebt ingesteld de [Aan de slag-handleiding voor de Privacy Service-API](./api/getting-started.md). Raadpleeg voor meer informatie over het beheren van machtigingen voor andere Adobe Experience Platform-mogelijkheden de [toegangsbeheerdocumentatie](../access-control/home.md).
