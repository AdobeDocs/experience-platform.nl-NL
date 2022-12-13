---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;ABAC
title: Beleid voor toegangsbeheer beheren
description: Dit document biedt informatie over het beheer van het beleid voor toegangsbeheer via de interface voor machtigingen in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Beleid voor toegangsbeheer beheren

Het beleid van de toegangscontrole is verklaringen die attributen samenbrengen om toelaatbare en ontoelaatbare acties te vestigen. Het toegangsbeleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden.

>[!IMPORTANT]
>
>Het beleid van de toegang moet niet met het beleid van het gegevensgebruik worden verward, dat controleert hoe het gegeven in Adobe Experience Platform wordt gebruikt in plaats van welke gebruikers in uw organisatie toegang tot het hebben. Zie de handleiding bij het maken van [beleid voor gegevensgebruik](../../../data-governance/policies/create.md) voor meer informatie .

## Nieuw beleid maken

Als u een nieuw beleid wilt maken, selecteert u de optie **[!UICONTROL Policies]** op de zijbalk en selecteert u **[!UICONTROL Create Policy]**.

![nieuw beleid](../../images/flac-ui/flac-new-policy.png)

De **[!UICONTROL Create a new policy]** wordt weergegeven en u wordt gevraagd een naam en een optionele beschrijving in te voeren. Als u klaar bent, selecteert u **[!UICONTROL Confirm]**.

![flash-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Selecteer met de vervolgkeuzepijl of u **Toegang tot** (![toegang tot](../../images/flac-ui/flac-permit-access-to.png)een bron of **Toegang weigeren tot** (![flc-ontkennen-toegang-aan](../../images/flac-ui/flac-deny-access-to.png)) een resource.

Selecteer vervolgens de bron die u in het beleid wilt opnemen met behulp van het vervolgkeuzemenu en het type zoektoegang, lezen of schrijven.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Selecteer vervolgens met de vervolgkeuzepijl de voorwaarde die u op dit beleid wilt toepassen, **Het volgende is waar** (![politiek-correct](../../images/flac-ui/flac-policy-true.png)) of **De volgende fout is onwaar** (![fc-policy-false](../../images/flac-ui/flac-policy-false.png)).

Selecteer het plusteken om **Overeenkomstexpressie toevoegen** of **Expressiegroep toevoegen** voor de bron.

![Fc-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Selecteer in het vervolgkeuzemenu de optie **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Selecteer vervolgens in het vervolgkeuzemenu de optie **Overeenkomsten**.

![flash-policy-match-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Selecteer vervolgens met het vervolgkeuzemenu het type label (**[!UICONTROL Core label]** of **[!UICONTROL Custom label]**) om het label aan te passen dat is toegewezen aan de gebruiker in rollen.

![fc-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Tot slot selecteert u **Sandbox** waarop u de beleidsvoorwaarden wilt toepassen via het vervolgkeuzemenu.

![fc-policy-sandboxen-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Selecteren **Bron toevoegen** om meer bronnen toe te voegen. Als u klaar bent, selecteert u **[!UICONTROL Save and exit]**.

![flash-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Het nieuwe beleid is gemaakt en u wordt omgeleid naar de **[!UICONTROL Policies]** , waarin het nieuwe beleid in de lijst wordt weergegeven.

![opgeslagen in een beleid](../../images/flac-ui/flac-policy-saved.png)

## Een beleid bewerken

Als u een bestaand beleid wilt bewerken, selecteert u het beleid in het menu **[!UICONTROL Policies]** tab. U kunt ook de filteroptie gebruiken om de resultaten te filteren en het beleid te zoeken dat u wilt bewerken.

![fc-policy-select](../../images/flac-ui/flac-policy-select.png)

Selecteer vervolgens de ellips (`…`) naast de naam van het beleid en een vervolgkeuzelijst bevat besturingselementen voor het bewerken, deactiveren, verwijderen of dupliceren van de rol. Selecteer Bewerken in het vervolgkeuzemenu.

![flash-policy-edit](../../images/flac-ui/flac-policy-edit.png)

Het scherm Beleidsmachtigingen wordt weergegeven. Breng de updates aan en selecteer **[!UICONTROL Save and exit]**.

![flash-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

Het beleid is bijgewerkt en u wordt omgeleid naar de **[!UICONTROL Policies]** tab.

## Een beleid dupliceren

Als u een bestaand beleid wilt dupliceren, selecteert u het beleid in het menu **[!UICONTROL Policies]** tab. U kunt ook de filteroptie gebruiken om de resultaten te filteren en het beleid te zoeken dat u wilt bewerken.

![fc-policy-select](../../images/flac-ui/flac-policy-select.png)

Selecteer vervolgens de ellips (`…`) naast de naam van een beleid en een vervolgkeuzelijst bevat besturingselementen voor het bewerken, deactiveren, verwijderen of dupliceren van de rol. Selecteer dupliceren in het vervolgkeuzemenu.

![flash-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

De **[!UICONTROL Duplicate policy]** wordt weergegeven, waarin u wordt gevraagd de duplicatie te bevestigen.

![flash-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

Het nieuwe beleid wordt in de lijst weergegeven als een kopie van het origineel in het dialoogvenster **[!UICONTROL Policies]** tab.

![flash-rol-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Een beleid verwijderen

Als u een bestaand beleid wilt verwijderen, selecteert u het beleid in het menu **[!UICONTROL Policies]** tab. U kunt ook de filteroptie gebruiken om de resultaten te filteren om het beleid te zoeken dat u wilt verwijderen.

![fc-policy-select](../../images/flac-ui/flac-policy-select.png)

Selecteer vervolgens de ellips (`…`) naast de naam van een beleid en een vervolgkeuzelijst bevat besturingselementen voor het bewerken, deactiveren, verwijderen of dupliceren van de rol. Selecteer Verwijderen in het vervolgkeuzemenu.

![flash-policy-delete](../../images/flac-ui/flac-policy-delete.png)

De **[!UICONTROL Delete user policy]** wordt weergegeven en u wordt gevraagd de verwijdering te bevestigen.

![flash-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

U bent teruggekeerd aan **[!UICONTROL policies]** wordt weergegeven en verschijnt er een bevestigingspop-up.

![flash-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirmation.png)

## Een beleid activeren

Als u een bestaand beleid wilt activeren, selecteert u het beleid in het menu **[!UICONTROL Policies]** tab. U kunt ook de filteroptie gebruiken om de resultaten te filteren om het beleid te zoeken dat u wilt verwijderen.

![fc-policy-select](../../images/flac-ui/flac-policy-select.png)

Selecteer vervolgens de ellips (`…`) naast de naam van een beleid en een vervolgkeuzelijst bevat besturingselementen voor het bewerken, activeren, verwijderen of dupliceren van de rol. Selecteer activeren in het vervolgkeuzemenu.

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

De **[!UICONTROL Activate user policy]** wordt weergegeven en u wordt gevraagd de activering te bevestigen.

![flash-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

U bent teruggekeerd aan **[!UICONTROL policies]** en verschijnt er een bevestiging van de activeringspop. De beleidsstatus wordt als actief weergegeven.

![geactiveerd door het beleid van de flac](../../images/flac-ui/flac-policy-activated.png)

## Volgende stappen

Als er een nieuw beleid is gemaakt, kunt u verdergaan met de volgende stap naar [machtigingen voor een rol beheren](permissions.md).
