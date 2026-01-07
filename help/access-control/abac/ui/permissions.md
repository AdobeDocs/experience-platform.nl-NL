---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;op attributen-gebaseerd toegangsbeheer;ABAC
title: Op kenmerken gebaseerde toegangsbeheerfuncties voor rolmachtigingen beheren
description: Leer hoe te om rollen door de interface van Toestemmingen in Adobe Experience Cloud te vormen.
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 157fb27ae492971a48ad62c2d6b3eddd674167f4
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 0%

---

# Machtigingen voor een rol beheren {#manage-role-permissions}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_about"
>title="Wat zijn rollen?"
>abstract="De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. Zij categoriseren de gebruikers die met uw instantie van Experience Platform in wisselwerking staan en zijn de bouwstenen van toegangsbeheerbeleid. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/access-control/abac/permissions-ui/roles.html?lang=nl-NL" text="Rollen beheren"

>[!IMPORTANT]
>
>Het toegangsbeheer gebruikt gebruiker - identiteitskaart (een interne unieke identiteitskaart die aan een gebruiker wordt toegewezen) voor het verlenen van toestemmingen. Wanneer een organisatie van Adobe ID naar bedrijfs-id wordt gemigreerd, gaan alle machtigingen die voor de gebruikers zijn ingesteld, verloren omdat de gebruikers-id wordt gewijzigd en het toegangsbeheer de nieuwe gebruikers-id gebruikt. Als uw organisatie is gemigreerd naar bedrijfs-id, neemt u contact op met uw Adobe-vertegenwoordiger om uw gebruikersnaam te migreren van Adobe ID naar bedrijfs-id.

Machtigingen zijn het gebied van Experience Cloud waar beheerders gebruikersrollen en toegangsbeleid kunnen definiëren om toegangsmachtigingen voor functies en objecten binnen een producttoepassing te beheren.

Door Toestemmingen, kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld.

Onmiddellijk nadat [&#x200B; creërend een nieuwe rol &#x200B;](#create-a-new-role), bent u teruggekeerd aan het **[!UICONTROL Roles]** lusje. Als u machtigingen voor een bestaande rol bewerkt, selecteert u de rol op het tabblad **[!UICONTROL Roles]** . U kunt ook de filteroptie gebruiken om de resultaten te filteren om een rol te zoeken.

## Filterrollen

Selecteer het pictogram van funnel (![&#x200B; pictogram van de Filter &#x200B;](/help/images/icons/filter.png)) om een lijst van filtercontroles te tonen om smalle resultaten te helpen.

![&#x200B; het dashboard van Rollen in Toestemmingen UI met de benadrukte sectie van filterrollen.](../../images/flac-ui/flac-filters.png)

De volgende filters zijn beschikbaar voor rollen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Created between] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |
| [!UICONTROL Created by] | Filteren op de maker van de rol door een gebruiker te selecteren in het vervolgkeuzemenu. |
| [!UICONTROL Modified between] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |
| [!UICONTROL Modified by] | Filter op rolbepaling door een gebruiker van dropdown te selecteren. |

Als u een filter wilt verwijderen, selecteert u de &quot;X&quot; op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** om alle filters te verwijderen.

![&#x200B; het dashboard van Rollen in Toestemmingen UI met X en ontruim alle selecties die op de gekozen filters worden benadrukt.](../../images/flac-ui/flac-clear-filters.png)

## Roldetails {#role-details}

>[!CONTEXTUALHELP]
>id="platform_permissions_roles_details"
>title="Roloverzicht"
>abstract="In het dialoogvenster Roloverzicht worden de details van de rol weergegeven, inclusief de bronnen en sandboxen waartoe een bepaalde rol toegang heeft. U kunt labels, gebruikers, gebruikersgroepen en API-referenties voor de rol beheren door naar het bijbehorende tabblad te navigeren in de werkruimte van de rol."
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-labels-for-a-role" text="Labels voor een rol beheren"
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/abac/permissions-ui/permissions#manage-users-for-a-role" text="Gebruikers voor een rol beheren"

Selecteer de rol op het tabblad **[!UICONTROL Roles]** , waarop het [!UICONTROL Details] -dashboard van de rol wordt geopend.

![&#x200B; De werkruimte van Details voor de geselecteerde rol wordt getoond met de benadrukte overzichtsinformatie.](../../images/flac-ui/flac-details.png)

Het dashboard van [!UICONTROL Details] biedt een overzicht van de rol. In het overzicht worden de naam van de rol, de beschrijving, de maker en de laatste modifier weergegeven, samen met de datum waarop de rol is gemaakt en gewijzigd. Ook worden de machtigingen weergegeven die zijn gekoppeld aan de rol en de lijst met toegewezen sandboxen. De rolnaam en beschrijving kunnen, indien nodig, worden gewijzigd.

## Labels voor een rol beheren

Selecteer het tabblad **[!UICONTROL Labels]** om de werkruimte voor rollabels te openen en selecteer vervolgens **[!UICONTROL Add labels]** om labels aan de rol toe te wijzen.

![&#x200B; de werkruimte van de Etiketten van de rol wordt getoond met het lusje van Etiketten en voegt Gemarkeerde knoop van Etiketten toe.](../../images/flac-ui/flac-labels.png)

Het dialoogvenster **[!UICONTROL Apply Access and Data Governance Labels]** wordt weergegeven en geeft een lijst met labels weer. In de lijst staan de labelnaam, de vriendelijke naam, de categorie en de beschrijving.

Selecteer de labels in de lijst die u aan de rol wilt toevoegen en selecteer vervolgens **[!UICONTROL Save]**

![&#x200B; toepassen de dialoog van de Etiketten van de Toegang en van het Beleid van Gegevens met een geselecteerd etiket.](../../images/flac-ui/flac-add-labels.png)

Toegevoegde labels worden weergegeven onder **[!UICONTROL Labels]** tab.

![&#x200B; de werkruimte van de Etiketten van de rol met het toegevoegde benadrukte etiket.](../../images/flac-ui/flac-added-labels.png)

Als u een label uit een rol wilt verwijderen, selecteert u het label en vervolgens **[!UICONTROL Remove Labels]** .

![&#x200B; de werkruimte van de Etiketten van de rol met een geselecteerde rol en de Remove benadrukte etiketten optie.](../../images/flac-ui/flac-delete-labels.png)

## Sandboxen beheren voor een rol

Selecteer de tab **[!UICONTROL Details]** en navigeer naar de sectie **[!UICONTROL Sandboxes]** . Selecteer **[!UICONTROL View All]** om de volledige lijst met sandboxen weer te geven die aan de rol zijn toegevoegd.

![&#x200B; de werkruimte van Details van de rol met de benadrukte sectie Sandboxes.](../../images/flac-ui/flac-sandboxes.png)

Als u meer sandboxen aan een rol wilt toevoegen, selecteert u **[!UICONTROL Edit]** rechtsboven in de gebruikersinterface.

![&#x200B; de werkruimte van Details van de rol met de Edit benadrukte optie.](../../images/flac-ui/flac-add-sandboxes.png)

In het volgende scherm wordt u gevraagd welke sandboxbronnen u in de rol wilt opnemen via het vervolgkeuzemenu. Als u klaar bent, selecteert u **[!UICONTROL Save]** en vervolgens **[!UICONTROL Close]** .

![&#x200B; het dashboard van Middelen van de rol met het benadrukt drop-down menu van zandbakmiddelen.](../../images/flac-ui/flac-add-role-permission.png)

## Gebruikers voor een rol beheren

Selecteer het tabblad **[!UICONTROL Users]** om de rollen [!UICONTROL Users] -werkruimte te openen en selecteer vervolgens **[!UICONTROL Add Users]** om gebruikers aan de rol toe te wijzen.

![&#x200B; de werkruimte van de Gebruikers van de rol wordt getoond met het lusje van Gebruikers en de Add benadrukte optie van Gebruikers.](../../images/flac-ui/flac-users.png)

Het dialoogvenster **[!UICONTROL Add Users]** wordt weergegeven. Selecteer de gebruikers in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruiker te zoeken door de naam of het e-mailadres in te voeren en vervolgens **[!UICONTROL Save]** te selecteren.

![&#x200B; Add de dialoog van Gebruikers met een geselecteerde gebruiker en de onderzoeksbar en sparen benadrukte optie.](../../images/flac-ui/flac-add-users.png)

Toegevoegde gebruikers worden weergegeven onder **[!UICONTROL Users]** tab.

![&#x200B; de werkruimte van de Gebruikers van de rol die de gebruikers tonen aan de rol worden toegevoegd.](../../images/flac-ui/flac-added-users.png)

Om een gebruiker uit een rol te verwijderen, selecteer het **X** pictogram naast de naam van de gebruiker.

![&#x200B; de werkruimte van de Gebruikers van de rol die een gebruiker met de benadrukte optie van X toont.](../../images/flac-ui/flac-remove-users.png)

De volgende video is bedoeld om uw begrip van het creëren van een nieuwe rol en het leiden van gebruikers voor die rol te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## API-referenties voor een rol beheren {#manage-api-credentials-for-role}

>[!CONTEXTUALHELP]
>id="platform_permissions_apicredentials_about"
>title="Wat zijn API-referenties?"
>abstract="API-referenties worden toegewezen aan rollen om gebruikers en ontwikkelaars toegang te verlenen tot Experience Platform API&#39;s. Met Experience Platform API&#39;s kunt u via programmacode elementaire CRUD-bewerkingen (Maken, Lezen, Bijwerken, Verwijderen) uitvoeren op gegevens, zoals het configureren van berekende kenmerken, het openen van gegevens/entiteiten, het exporteren van gegevens, het verwijderen van overbodige gegevens of batches, enzovoort."
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/landing/platform-apis/api-guide" text="Experience Platform API-handleiding"

>[!IMPORTANT]
>
> Gebruikers moeten over beheerdersrechten voor het systeem beschikken om API-referenties te kunnen gebruiken en beheren in [!UICONTROL Permissions] .

Om Experience Platform APIs als gebruiker of ontwikkelaar te gebruiken, moet een systeembeheerder API geloofsbrieven toevoegen naast een rol gegeven reeks toestemmingen. Voor een volledige gids bij het creëren van en het toewijzen van API geloofsbrieven, evenals de toestemmingen nodig, verwijs naar het geleidelijke leerprogramma in [&#x200B; voor authentiek verklaren en toegang Experience Platform APIs &#x200B;](../../../landing/api-authentication.md#generate-credentials).

Selecteer het tabblad **[!UICONTROL API credentials]** om de werkruimte met API-referenties voor rollen te openen en selecteer vervolgens **[!UICONTROL Add API credentials]** om API-referenties aan de rol toe te wijzen.

![&#x200B; de geloofsbrieven van de rol API met de Add benadrukte geloofsbrieven optie.](../../images/flac-ui/flac-api-credentials.png)

Het dialoogvenster **[!UICONTROL Add API credentials]** wordt weergegeven. Selecteer API-referenties in de lijst om aan de rol toe te voegen en selecteer vervolgens **[!UICONTROL Save]**

![&#x200B; Add API geloofsdialoog met geselecteerde referentie en sparen benadrukte optie.](../../images/flac-ui/flac-add-api-credentials.png)

Toegevoegde API-referenties worden weergegeven onder **[!UICONTROL API credentials]** tab.

![&#x200B; de geloofsbrieven van de rol API met de toegevoegde getoonde geloofsbrieven.](../../images/flac-ui/flac-added-api-credentials.png)

Om een API referentie uit een rol te verwijderen, selecteer het **X** pictogram naast de API referentie naam.

![&#x200B; de geloofsbrieven van de rol API met de optie van X om een benadrukt referentie te verwijderen.](../../images/flac-ui/flac-remove-api-credentials.png)

Het dialoogvenster **[!UICONTROL Remove API credentials]** verschijnt waarin u wordt gevraagd het verwijderen te bevestigen. Selecteer **[!UICONTROL Confirm]** om het verwijderen van de geselecteerde referentie te voltooien.

![&#x200B; verwijdert Credentials pop-over ertoe aanzettend u om het verwijderen van de referentie te bevestigen wordt benadrukt.](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

U wordt teruggestuurd naar het tabblad **[!UICONTROL API credentials]** .

## Gebruikersgroepen beheren voor een rol {#manage-user-groups}

>[!CONTEXTUALHELP]
>id="platform_permissions_usergroups_about"
>title="Wat zijn gebruikersgroepen?"
>abstract="Gebruikersgroepen zijn verzamelingen van meerdere gebruikers die toegang tot dezelfde functies delen. De toegang tot middelen binnen een organisatie wordt beheerd door rollen die aan gebruikersgroepen worden toegewezen."
>additional-url="https://experienceleague.adobe.com/nl/docs/experience-platform/access-control/abac/permissions-ui/roles" text="Rollen beheren"

Gebruikersgroepen zijn meerdere gebruikers die zijn gegroepeerd en die toegang hebben om dezelfde functies uit te voeren.

Selecteer het tabblad **[!UICONTROL User groups]** om de werkruimte van de gebruikersgroepen voor de rol te openen en selecteer vervolgens **[!UICONTROL Add Groups]** om gebruikersgroepen aan de rol toe te wijzen.

![&#x200B; De de groepenwerkruimte van de Gebruiker van de rol met de Add optie van Groepen &#x200B;](../../images/flac-ui/flac-user-groups.png)

Het dialoogvenster **[!UICONTROL Add Groups]** wordt weergegeven. Selecteer de gebruikersgroepen in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruikersgroep te zoeken door de naam van de groep in te voeren en vervolgens **[!UICONTROL Save]** te selecteren

![&#x200B; het Add dialoog van Groepen met een geselecteerde gebruikersgroep en het onderzoek en sparen optie benadrukte.](../../images/flac-ui/flac-add-user-groups.png)

Toegevoegde gebruikersgroepen worden weergegeven onder **[!UICONTROL User groups]** tab.

![&#x200B; de de groepenwerkruimte van de Gebruiker van de rol tonend de lijst van toegevoegde gebruikersgroepen.](../../images/flac-ui/flac-added-user-groups.png)

Om een gebruikersgroep uit een rol te verwijderen, selecteer het **X** pictogram naast de naam van de gebruikersgroep.

![&#x200B; de groepswerkruimte van de Gebruiker van de rol met de optie van X om een specifieke benadrukte gebruikersgroep te verwijderen.](../../images/flac-ui/flac-remove-user-groups.png)

Het dialoogvenster **[!UICONTROL Remove user group]** verschijnt waarin u wordt gevraagd het verwijderen te bevestigen. Selecteer **[!UICONTROL Confirm]** om de geselecteerde gebruikersgroep te verwijderen.

![&#x200B; popover voor het verwijderen van een gebruikersgroep wordt getoond en benadrukt.](../../images/flac-ui/flac-confirm-user-groups-delete.png)

U wordt teruggestuurd naar het tabblad **[!UICONTROL User groups]** .

## Gebruikers aan Experience Platform toevoegen

Als systeembeheerder, kunt u ontwikkelaartoegang tot een gebruiker verlenen zodat kunnen zij [&#x200B; tot integratie &#x200B;](../../../landing/api-authentication.md#generate-credentials) in Adobe Developer Console leiden.

Om een gebruiker Experience Platform toe te voegen, login aan [&#x200B; Admin Console &#x200B;](https://adminconsole.adobe.com) en selecteer **[!UICONTROL Add users]**.

![&#x200B; het dashboard van Adobe Admin Console met de Add benadrukte gebruikersoptie.](../../images/flac-ui/product-profile-add-users.png)

Het dialoogvenster **[!UICONTROL Add users to your team]** wordt weergegeven. Voer het e-mailadres, de voornaam (optioneel) en de achternaam (optioneel) van de gebruiker in. Selecteer vervolgens **[!UICONTROL Products]** .

![&#x200B; Add gebruikers aan uw teamdialoog met de benadrukte gebruikersgebieden en optie van Producten.](../../images/flac-ui/product-profile-add-users-to-your-team.png)

Het dialoogvenster **[!UICONTROL Select products]** wordt weergegeven. Selecteer **[!UICONTROL Adobe Experience Platform]**.

![&#x200B; de uitgezochte dialoog van producten met Adobe Experience Platform benadrukte.](../../images/flac-ui/product-profile-select-product.png)

Het dialoogvenster **[!UICONTROL Select product profiles]** wordt weergegeven. Selecteer **[!UICONTROL AEP-Default-All-Users]** en selecteer vervolgens **[!UICONTROL Save]** .

![&#x200B; de Uitgezochte dialoog van productprofielen met AEP-gebrek-Alle-Gebruikers selecteerde en van toepassing benadrukt.](../../images/flac-ui/product-profile-select-product-profiles.png)

Controleer de gegevens en selecteer vervolgens **[!UICONTROL Save]** om de gebruiker toe te voegen.

![&#x200B; Add gebruikers aan uw teamdialoog met de gebruikersinformatie en gekozen geselecteerde geselecteerde geselecteerde geselecteerde selecties en sparen benadrukte optie, &#x200B;](../../images/flac-ui/product-profile-save-user.png)

## Volgende stappen

Met gevestigde toestemmingen, kunt u aan de volgende stap te werk gaan [&#x200B; gebruikers &#x200B;](users.md) beheren.
