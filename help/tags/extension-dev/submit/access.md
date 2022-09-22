---
title: Gebruikerstoegang verlenen
description: Stel de gebruikersaccounts en machtigingen voor tags van uw teamleden in Adobe Experience Platform in.
exl-id: c7235e50-13b3-4487-b171-873063875621
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Gebruikerstoegang verlenen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Voordat u aan de slag gaat met uw extension_package, moet u uw teamleden instellen met gebruikersaccounts en machtigingen.  Dit wordt verwezenlijkt in [Adobe Admin Console](https://adminconsole.adobe.com/).

Dit document bevat stappen voor het verlenen van toegang tot tags in Adobe Experience Platform via Admin Console.

## Vereisten

In deze handleiding wordt ervan uitgegaan dat u een beheerder van een organisatie bent, zoals aangegeven door de Admin Console. Als u extra informatie over de Admin Console en het toewijzen van rollen vereist, verwijs naar de volgende middelen:

* [Gebruikershandleiding voor beheerders](https://helpx.adobe.com/enterprise/administering/user-guide.html?topic=/enterprise/administering/morehelp/introduction.ug.js): Informatie over alle zaken in de Admin Console
* [Beheerrollen voor ondernemingen](https://helpx.adobe.com/au/enterprise/using/admin-roles.html): Meer over de verschillende soorten beleidsrollen. Voor de onderstaande gids gaan we ervan uit dat u een Org Admin bent.

## Kies uw organisatie

Uw Adobe Experience Cloud-organisatiebeheerder moet zich aanmelden bij [Admin Console](https://adminconsole.adobe.com/). Het eerste scherm is het overzicht.

![Overzicht van beheerconsole, tabblad](../images/getting-started/admin-console-overview.png)

Sommigen van u hebben toegang tot meer dan één organisatie (Org). Als u de mogelijkheid tot het toevoegen van codes aan de juiste organisatie wilt toevoegen, selecteert u de naam van de organisatie die u in de rechterbovenhoek van het scherm ziet. Kies vervolgens de organisatie waar u tags wilt gebruiken in de vervolgkeuzelijst.

![Admin Console Org selection dropdown](../images/getting-started/admin-console-choose-org.png)

## Een productprofiel maken

Een productprofiel is een groep. De individuele rechten worden toegewezen aan productprofielen en om het even welke gebruikers in het profiel zullen die rechten erven.

Kies de optie **[!UICONTROL Products]** bovenaan, en **[!UICONTROL Experience Cloud]** links. Als u niet de vermelde UI van de Inzameling van Gegevens hebt, zouden de klanten hun accountteam en partners moeten contacteren e-mail <ExchangeTechEC@adobe.com>.

![Tabblad Producten voor beheerconsole](../images/getting-started/admin-console-products-launch.png)

In de bovenstaande schermafbeelding ziet u een voorbeeldprofiel. Wellicht hebt u nog geen profiel. Selecteer **[!UICONTROL New Profile]**. Op de **Een nieuw profiel maken** scherm, alleen een **Profielnaam** (bijvoorbeeld het testen van gegevensverzameling) en een optioneel **Beschrijving** selecteert u vervolgens **[!UICONTROL Save]**:

![Nieuwe profielweergave maken](../images/getting-started/admin-console-create-a-new-profile.png)

Het productprofiel is nu toegevoegd aan de organisatie. Voeg vervolgens gebruikers toe aan het productprofiel.

## Gebruikers toewijzen aan het productprofiel

Het productprofiel is nul voor **GEHECHTELIJKE GEBRUIKERS** en **BEHEER**. Selecteer de naam van het productprofiel dat u hebt gemaakt (testen op gegevensverzameling in ons voorbeeld).

![Weergave productprofielen](../images/getting-started/admin-console-profiles-add-user.png)

Selecteer het tabblad **[!UICONTROL Users]**. Hier kunt u zoeken naar bestaande Adobe ID-gebruikers via e-mail of nieuwe gebruikers toevoegen aan dit productprofiel. Selecteer **[!UICONTROL Add User link]**.

![Tabblad Gebruikers productprofielen](../images/getting-started/admin-console-add-launch-user.png)

Voer een naam, gebruikersgroep of e-mailadres in het desbetreffende tekstveld in. Het wordt aanbevolen waar mogelijk een voornaam en een achternaam op te nemen. Selecteren **[!UICONTROL Save]** om de gebruiker toe te voegen.

![Gebruiker toevoegen aan profielweergave](../images/getting-started/admin-console-add-user.png)

Wanneer u alle gebruikers hebt u in dit productprofiel nodig hebt, voegen wij toestemmingen voor hen toe. Selecteer het tabblad **[!UICONTROL Permissions]**. Op het toestemmingenscherm zult u zien **[!UICONTROL Properties]**, **[!UICONTROL Company Rights]**, en **[!UICONTROL Property Rights]**. Selecteer **[!UICONTROL Edit]**.

![Het tabblad Machtigingen voor productprofielen](../images/getting-started/admin-console-profile-permissions.png)

Uw team moet over minimaal de volgende machtigingen beschikken om extensies te kunnen schrijven:

* &quot;Eigenschappen beheren&quot; vanuit de bedrijfsgroep.
* &quot;Extensies beheren&quot;, &quot;Omgevingen beheren&quot; en &quot;Ontwikkelen&quot; in de groep met eigenschappen.

U kunt later desgewenst aanvullende productprofielen met meer beperkte rechten maken, maar selecteer nu gewoon **[!UICONTROL + Add all]** voor beide **Bedrijfsrechten** en **Eigendomsrechten**. Zorg ervoor dat u **[!UICONTROL Save]** op elk.

![Eigenschappenrechten beheren](../images/getting-started/admin-console-add-all-property-rights.png)

![Bedrijfsrechten beheren](../images/getting-started/admin-console-add-all-company-rights.png)

Tot nu toe hebben we de juiste organisatie gekozen, een productprofiel gemaakt, gebruikers toegevoegd aan het productprofiel en machtigingen toegewezen.

Dit voltooit de vereiste opstelling in Admin Console. U en uw teamleden die zijn ingesteld als gebruikers kunnen zich nu aanmelden bij [De interface voor gegevensverzameling](https://launch.adobe.com/).

## Levering bevestigen

Als uw bedrijf toegang heeft tot tags en uw gebruikers zijn ingesteld zoals hierboven is beschreven, kunt u de productieomgeving beter openen vanuit de [UI voor gegevensverzameling](https://launch.adobe.com/). Als u voor markeringen provisioned bent en de stappen hierboven van de Admin Console hebt voltooid, maar nog niet aan kan login aan de UI van de Inzameling van Gegevens, gelieve uw de steunvertegenwoordigers van de Adobe te contacteren.
