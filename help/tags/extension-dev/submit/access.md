---
title: Gebruikerstoegang verlenen
description: Stel de gebruikersaccounts en machtigingen voor tags van uw teamleden in Adobe Experience Platform in.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 2%

---

# Gebruikerstoegang verlenen

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Voordat u aan de slag gaat met uw extension_package, moet u uw teamleden instellen met gebruikersaccounts en machtigingen.  Dit wordt verwezenlijkt in [Adobe Admin Console](https://adminconsole.adobe.com/).

Dit document bevat stappen voor het verlenen van toegang tot tags in Adobe Experience Platform via Admin Console.

## Vereisten

In deze handleiding wordt ervan uitgegaan dat u een beheerder van een organisatie bent, zoals aangegeven door de Admin Console. Als u extra informatie over de Admin Console en het toewijzen van rollen vereist, verwijs naar de volgende middelen:

* [Gebruikershandleiding](https://helpx.adobe.com/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js) voor beheer: Informatie over alle zaken in de Admin Console
* [Rollen](https://helpx.adobe.com/au/enterprise/using/admin-roles.html) voor bedrijfsbeheer: Meer over de verschillende soorten beleidsrollen. Voor de onderstaande gids gaan we ervan uit dat u een Org Admin bent.

## Kies uw organisatie

Uw Adobe Experience Cloud-organisatiebeheerder moet zich aanmelden bij de [Admin Console](https://adminconsole.adobe.com/). Het eerste scherm is het overzicht.

![Overzicht van beheerconsole, tabblad](../images/getting-started/admin-console-overview.png)

Sommigen van u hebben toegang tot meer dan één organisatie (Org). Als u de mogelijkheid tot het toevoegen van codes aan de juiste organisatie wilt toevoegen, selecteert u de naam van de organisatie die u in de rechterbovenhoek van het scherm ziet. Kies vervolgens de organisatie waar u tags wilt gebruiken in de vervolgkeuzelijst.

![Admin Console Org selection dropdown](../images/getting-started/admin-console-choose-org.png)

## Een productprofiel maken

Een productprofiel is een groep. De individuele rechten worden toegewezen aan productprofielen en om het even welke gebruikers in het profiel zullen die rechten erven.

Kies de **[!UICONTROL Products]** verbinding bij de bovenkant, en **[!UICONTROL Experience Cloud]** op de linkerzijde. Als u Adobe Experience Platform Launch niet hebt vermeld, moeten klanten contact opnemen met hun accountteam en moeten partners <ExchangeTechEC@adobe.com> per e-mail verzenden.

![Tabblad Producten voor beheerconsole](../images/getting-started/admin-console-products-launch.png)

In de bovenstaande schermafbeelding ziet u een voorbeeldprofiel. Wellicht hebt u nog geen profiel. Selecteer **[!UICONTROL New Profile]** om een sjabloon te maken. Voeg op het scherm **Een nieuw profiel maken** alleen een **Profielnaam** (bijvoorbeeld het testen van gegevensverzameling) en een optionele **Beschrijving** toe en selecteer **[!UICONTROL Save]**:

![Nieuwe profielweergave maken](../images/getting-started/admin-console-create-a-new-profile.png)

Het productprofiel is nu toegevoegd aan de organisatie. Voeg vervolgens gebruikers toe aan het productprofiel.

## Gebruikers toewijzen aan het productprofiel

Het productprofiel toont nul voor **GEENTILEERDE GEBRUIKERS** en **ADMINISTRAS**. Selecteer de naam van het productprofiel dat u hebt gemaakt (testen op gegevensverzameling in ons voorbeeld).

![Weergave productprofielen](../images/getting-started/admin-console-profiles-add-user.png)

Selecteer het tabblad **[!UICONTROL Users]**. Hier kunt u zoeken naar bestaande Adobe ID-gebruikers via e-mail of nieuwe gebruikers toevoegen aan dit productprofiel. Selecteer **[!UICONTROL Add User link]**.

![Tabblad Gebruikers productprofielen](../images/getting-started/admin-console-add-launch-user.png)

Voer een naam, gebruikersgroep of e-mailadres in het desbetreffende tekstveld in. Het wordt aanbevolen waar mogelijk een voornaam en een achternaam op te nemen. Selecteer **[!UICONTROL Save]** om de gebruiker toe te voegen.

![Gebruiker toevoegen aan profielweergave](../images/getting-started/admin-console-add-user.png)

Wanneer u alle gebruikers hebt u in dit productprofiel nodig hebt, voegen wij toestemmingen voor hen toe. Selecteer het tabblad **[!UICONTROL Permissions]**. Op het scherm van toestemmingen zult u **[!UICONTROL Properties]**, **[!UICONTROL Company Rights]**, en **[!UICONTROL Property Rights]** zien. Selecteer **[!UICONTROL Edit]**.

![Het tabblad Machtigingen voor productprofielen](../images/getting-started/admin-console-profile-permissions.png)

Uw team moet over minimaal de volgende machtigingen beschikken om extensies te kunnen schrijven:

* &quot;Eigenschappen beheren&quot; vanuit de bedrijfsgroep.
* &quot;Extensies beheren&quot;, &quot;Omgevingen beheren&quot; en &quot;Ontwikkelen&quot; in de groep met eigenschappen.

U kunt later aanvullende productprofielen met meer beperkte rechten maken, maar selecteer nu gewoon **[!UICONTROL + Add all]** voor zowel **Bedrijfsrechten** als **Eigenschappenrechten**. Zorg ervoor om **[!UICONTROL Save]** op elk te selecteren.

![Eigenschappenrechten beheren](../images/getting-started/admin-console-add-all-property-rights.png)

![Bedrijfsrechten beheren](../images/getting-started/admin-console-add-all-company-rights.png)

Tot nu toe hebben we de juiste organisatie gekozen, een productprofiel gemaakt, gebruikers toegevoegd aan het productprofiel en machtigingen toegewezen.

Dit voltooit de vereiste opstelling in Admin Console. U en uw teamleden die zijn ingesteld als gebruikers kunnen zich nu aanmelden bij [de gebruikersinterface voor gegevensverzameling](https://launch.adobe.com/).

## Levering bevestigen

Nadat uw bedrijf van toegang tot markeringen wordt voorzien en uw gebruikers opstelling zoals hierboven beschreven zijn, zou u tot het productiemilieu van [de Inzameling UI van Gegevens](https://launch.adobe.com/) moeten kunnen toegang hebben. Als u voor markeringen provisioned bent en de stappen hierboven van de Admin Console hebt voltooid, maar nog niet aan kan login aan de UI van de Inzameling van Gegevens, gelieve uw de steunvertegenwoordigers van de Adobe te contacteren.
