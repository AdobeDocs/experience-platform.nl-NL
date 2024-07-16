---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;ABAC
title: Toegangsbeheer op basis van kenmerken maakt een rol
description: Dit document bevat informatie over het beheer van rollen via de interface voor machtigingen in Adobe Experience Cloud
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: d8f72bb5ae56daf5a41c763f821ca6306514bc48
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Rollen beheren

De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben.

## Een nieuwe rol maken

Als u een nieuwe rol wilt maken, selecteert u de tab **[!UICONTROL Roles]** in het zijpaneel en selecteert u **[!UICONTROL Create Role]** .

![ flac-new-role ](../../images/flac-ui/flac-new-role.png)

Het dialoogvenster **[!UICONTROL Create a new role]** wordt weergegeven, waarin u wordt gevraagd een naam en een optionele beschrijving in te voeren.

Selecteer **[!UICONTROL Confirm]** als u klaar bent.

![ flc-creeer-new-role ](../../images/flac-ui/flac-create-new-role.png)

Selecteer vervolgens de bronmachtigingen die u in de rol wilt opnemen via het vervolgkeuzemenu.

![ fc-toe:voegen-rol-toestemming ](../../images/flac-ui/flac-add-role-permission.png)

Als u aanvullende bronnen wilt toevoegen, selecteert u **[!UICONTROL Adobe Experience Platform]** in het navigatievenster aan de linkerkant, dat een lijst met bronnen weergeeft. U kunt ook de naam van de bron invoeren in de zoekbalk in het linkernavigatievenster.

![ flc-add-additional-resources ](../../images/flac-ui/flac-add-additional-resources.png)

Klik op de relevante bron en sleep deze naar het hoofddeelvenster.

![ fc-extra-middelen-toegevoegd ](../../images/flac-ui/flac-additional-resources-added.png)

Selecteer de bronmachtigingen die u in de rol wilt opnemen via het vervolgkeuzemenu. Herhaal dit voor alle bronnen die u voor de rol wilt opnemen. Selecteer **[!UICONTROL Save and exit]** als u klaar bent.

![ flc-sparen-middelen ](../../images/flac-ui/flac-save-resources.png)

De nieuwe rol is gemaakt en u wordt omgeleid naar de **[!UICONTROL Roles]** -pagina, waar de nieuw gemaakte rol in de lijst wordt weergegeven.

![ fc-rol-bewaarde ](../../images/flac-ui/flac-role-saved.png)

Zie de secties op [ het leiden toestemmingen voor een rol ](#manage-permissions-for-a-role) voor meer details over hoe te om roltoestemmingen te beheren zodra zij worden gecreeerd.

De volgende video is bedoeld om uw begrip van het creëren van een nieuwe rol en het leiden van gebruikers voor die rol te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## Een rol dupliceren

Als u een bestaande rol wilt dupliceren, selecteert u de rol op het tabblad **[!UICONTROL Roles]** . U kunt ook de filteroptie gebruiken om de resultaten te filteren om de rol te zoeken die u wilt dupliceren.

![ fc-dubbel-rol ](../../images/flac-ui/flac-duplicate-role.png)

Selecteer vervolgens **[!UICONTROL Duplicate]** in de rechterbovenhoek van het scherm.

![ flac-duplicate ](../../images/flac-ui/flac-duplicate.png)

Het dialoogvenster **[!UICONTROL Duplicate role]** wordt weergegeven, waarin u wordt gevraagd de duplicatie te bevestigen.

![ flc-dubbel-bevestig ](../../images/flac-ui/flac-duplicate-confirm.png)

Vervolgens gaat u naar de detailpagina van de rol waar u de naam en machtigingen voor de rol kunt wijzigen. De details, de Etiketten, en de Sandboxen worden gedupliceerd van de vorige rol. Gebruikers moeten via het tabblad Gebruikers worden toegevoegd. U kunt [ bekijken beheert toestemmingen voor een rol ](permissions.md) document om meer over het toevoegen van Details, Etiketten, Sandboxes, en Gebruikers aan een rol te leren.

Klik op de linkerpijl om terug te keren naar de tab **[!UICONTROL Roles]** .

![ fc-terugkeer-aan-rollen ](../../images/flac-ui/flac-return-to-roles.png)

De nieuwe rol wordt weergegeven in de lijst op de pagina **[!UICONTROL Roles]** .

![ fc-rol-dubbel-bewaarde ](../../images/flac-ui/flac-role-duplicate-saved.png)

## Een rol verwijderen

Selecteer de ellips (`…`) naast de naam van een rol, en een dropdown vertoningencontroles om, de rol uit te geven te schrappen of te dupliceren. Selecteer Verwijderen in het vervolgkeuzemenu.

![ fc-rol-schrapping ](../../images/flac-ui/flac-role-delete.png)

Het dialoogvenster **[!UICONTROL Delete user role]** verschijnt waarin u wordt gevraagd de verwijdering te bevestigen.

![ fc-confirm-rol-schrapping ](../../images/flac-ui/flac-confirm-role-delete.png)

U wordt teruggestuurd naar het tabblad **[!UICONTROL Roles]** .

## Volgende stappen

Met een nieuwe gecreeerde rol, kunt u aan de volgende stap te werk gaan [ toestemmingen voor een rol ](permissions.md) beheren.
