---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;ABAC
title: Toegangsbeheer op basis van kenmerken maakt een rol
description: Dit document bevat informatie over op kenmerken gebaseerd toegangsbeheer in Adobe Experience Platform
hide: true
hidefromtoc: true
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Rollen beheren

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven.

De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben.

## Een nieuwe rol maken

Als u een nieuwe rol wilt maken, selecteert u de optie **[!UICONTROL Roles]** op de zijbalk en selecteert u **[!UICONTROL Create Role]**.

![nieuwe rol](../../images/flac-ui/flac-new-role.png)

De **[!UICONTROL Create a new role]** wordt weergegeven en u wordt gevraagd een naam en een optionele beschrijving in te voeren.

Als u klaar bent, selecteert u **[!UICONTROL Confirm]**.

![flash-create-new-role](../../images/flac-ui/flac-create-new-role.png)

Selecteer vervolgens de bronmachtigingen die u in de rol wilt opnemen via het vervolgkeuzemenu.

![flash-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

Als u aanvullende bronnen wilt toevoegen, selecteert u **[!UICONTROL Adobe Experience Platform]** in het linkernavigatievenster, dat een lijst met bronnen weergeeft. U kunt ook de naam van de bron invoeren in de zoekbalk in het linkernavigatievenster.

![flash-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

Klik op de relevante bron en sleep deze naar het hoofddeelvenster.

![toegevoegde flash-resources](../../images/flac-ui/flac-additional-resources-added.png)

Selecteer de bronmachtigingen die u in de rol wilt opnemen via het vervolgkeuzemenu. Herhaal dit voor alle bronnen die u voor de rol wilt opnemen. Als u klaar bent, selecteert u **[!UICONTROL Save and exit]**.

![flash-save-resources](../../images/flac-ui/flac-save-resources.png)

De nieuwe rol is gemaakt en u wordt omgeleid naar de **[!UICONTROL Roles]** pagina, waar u de nieuwe rol ziet verschijnen in de lijst.

![opgeslagen met een rol](../../images/flac-ui/flac-role-saved.png)

Zie de secties op [machtigingen voor een rol beheren](#manage-permissions-for-a-role) voor meer informatie over hoe te om roltoestemmingen te beheren zodra zij worden gecreeerd.

## Een rol dupliceren

Als u een bestaande rol wilt dupliceren, selecteert u de rol in het menu **[!UICONTROL Roles]** tab. U kunt ook de filteroptie gebruiken om de resultaten te filteren om de rol te zoeken die u wilt dupliceren.

![flash-duplicate-rol](../../images/flac-ui/flac-duplicate-role.png)

Selecteer vervolgens **[!UICONTROL Duplicate]** vanaf de rechterbovenhoek van het scherm.

![flac-duplicaat](../../images/flac-ui/flac-duplicate.png)

De **[!UICONTROL Duplicate role]** wordt weergegeven, waarin u wordt gevraagd de duplicatie te bevestigen.

![flash-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Vervolgens gaat u naar de detailpagina van de rol waar u de naam en machtigingen voor de rol kunt wijzigen. De details, de Etiketten, en de Sandboxen worden gedupliceerd van de vorige rol. Gebruikers moeten via het tabblad Gebruikers worden toegevoegd. U kunt de [machtigingen voor een rol beheren](permissions.md) voor meer informatie over het toevoegen van Details, Labels, Sandboxen en Gebruikers aan een rol.

Klik op de linkerpijl om terug te keren naar de knop **[!UICONTROL Roles]** tab.

![flac-return-to-rollen](../../images/flac-ui/flac-return-to-roles.png)

De nieuwe rol wordt weergegeven in de lijst op de **[!UICONTROL Roles]** pagina.

![flash-rol-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Een rol verwijderen

De ovaal selecteren (`…`) naast de naam van een rol en een vervolgkeuzelijst bevat besturingselementen voor het bewerken, verwijderen of dupliceren van de rol. Selecteer Verwijderen in het vervolgkeuzemenu.

![flash-rol-delete](../../images/flac-ui/flac-role-delete.png)

De **[!UICONTROL Delete user role]** wordt weergegeven en u wordt gevraagd de verwijdering te bevestigen.

![flash-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

U wordt teruggestuurd naar de **[!UICONTROL Roles]** tab.

## Volgende stappen

Als er een nieuwe rol is gemaakt, kunt u verdergaan met de volgende stap naar [machtigingen voor een rol beheren](permissions.md).
