---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;op attributen-gebaseerd toegangsbeheer;ABAC
title: Beleid voor toegangsbeheer beheren
description: Dit document biedt informatie over het beheer van het beleid voor toegangsbeheer via de interface voor machtigingen in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: afd883c530ab1b335888e79b5f4075e774fced4b
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# Beleid voor toegangsbeheer beheren

Het beleid van de toegangscontrole is verklaringen die attributen samenbrengen om toelaatbare en ontoelaatbare acties te vestigen. Het toegangsbeleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. Adobe biedt een standaardbeleid dat direct kan worden geactiveerd of wanneer uw organisatie gereed is om de toegang tot specifieke objecten te beheren op basis van labels. Het standaardbeleid leverages etiketten die op middelen worden toegepast om toegang te ontkennen tenzij de gebruikers in een rol met een passend etiket zijn.

>[!IMPORTANT]
>
>Het beleid van de toegang moet niet met het beleid van het gegevensgebruik worden verward, dat controleert hoe het gegeven in Adobe Experience Platform wordt gebruikt in plaats van welke gebruikers in uw organisatie toegang tot het hebben. Zie de gids bij het creëren van [ beleid van het gegevensgebruik ](../../../data-governance/policies/create.md) voor meer informatie.

<!-- ## Create a new policy

To create a new policy, select the **[!UICONTROL Policies]** tab in the sidebar and select **[!UICONTROL Create Policy]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

The **[!UICONTROL Create a new policy]** dialog appears, prompting you to enter a name, and an optional description. When finished, select **[!UICONTROL Confirm]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

Using the dropdown arrow select if you would like to **Permit access to** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png)) a resource or **Deny access to** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png)) a resource.

Next, select the resource that you would like to include in the policy using the dropdown menu and search access type, read or write.

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

Next, using the dropdown arrow select the condition you would like to apply to this policy, **The following being true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png)) or **The following being false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png)).

Select the plus icon to **Add matches expression** or **Add expression group** for the resource. 

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

Using the dropdown, select the **Resource**.

![flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

Next, using the dropdown select the **Matches**.

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

Next, using the dropdown, select the type of label (**[!UICONTROL Core label]** or **[!UICONTROL Custom label]**) to match the label assigned to the User in roles.

![flac-policy-user-dropdown](../../images/flac-ui/flac-policy-user-dropdown.png)

Finally, select the **Sandbox** that you would like the policy conditions to apply to, using the dropdown menu.

![flac-policy-sandboxes-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

Select **Add resource** to add more resources. Once finished, select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The new policy is successfully created, and you are redirected to the **[!UICONTROL Policies]** tab, where you will see the newly created policy appear in the list. 

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## Edit a policy

To edit an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to the policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select edit from the dropdown.

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

The policy permissions screen appears. Make the updates then select **[!UICONTROL Save and exit]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

The policy is successfully updated, and you are redirected to the **[!UICONTROL Policies]** tab.

## Duplicate a policy

To duplicate an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to edit.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select duplicate from the dropdown.

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

The **[!UICONTROL Duplicate policy]** dialog appears, prompting you to confirm the duplication. 

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

The new policy appears in the list as a copy of the original on the **[!UICONTROL Policies]** tab.

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## Delete a policy

To delete an existing policy, select the policy from the **[!UICONTROL Policies]** tab. Alternatively, use the filter option to filter the results to find the policy you want to delete.

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

Next, select the ellipsis (`…`) next to a policies name, and a dropdown displays controls to edit, deactivate, delete, or duplicate the role. Select delete from the dropdown.

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

The **[!UICONTROL Delete user policy]** dialog appears, prompting you to confirm the deletion. 

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

You are returned to the **[!UICONTROL policies]** tab and a confirmation of deletion pop over appears.

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png) -->

## Beleid voor een sandbox configureren

>[!IMPORTANT]
>
>Standaard is de functie [!UICONTROL Auto-include] ingeschakeld voor alle klanten, wat betekent dat alle sandboxen aan het beleid worden toegevoegd.

>[!NOTE]
>
>Het **[!UICONTROL Default-Label-Based-Access-Control-Policy]** -beleid is momenteel het enige beleid dat beschikbaar is voor configuratie.

Als u sandboxen wilt weergeven die aan een beleid zijn gekoppeld, selecteert u het beleid op de tab **[!UICONTROL Policies]** .

![ de beleidspagina die een lijst van bestaand beschikbaar beleid tonen.](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Selecteer vervolgens het beleid en selecteer **[!UICONTROL Sandboxes]** tab. Er wordt een lijst weergegeven met sandboxen die aan het beleid zijn gekoppeld.

![ de beleidspagina die een lijst van bestaand beschikbaar beleid tonen.](../../images/flac-ui/abac-policies-sandboxes-tab.png)

### Beleid toevoegen aan alle sandboxen

Gebruik de schakeloptie **[!UICONTROL Auto-include]** op het tabblad **[!UICONTROL Sandboxes]** om het beleid voor alle sandboxen te activeren.

![ het [!UICONTROL Sandboxes] lusje tonen van [!UICONTROL Auto-include] knevel.](../../images/flac-ui/abac-policies-auto-include.png)

In het dialoogvenster **[!UICONTROL Enable Auto-include]** wordt u gevraagd uw selectie te bevestigen. Selecteer **[!UICONTROL Enable]** om de configuratie-instelling te voltooien.

![ de [!UICONTROL Enable Auto-include] dialoog die [!UICONTROL Enable] benadrukt.](../../images/flac-ui/abac-policies-auto-include-enable.png)

>[!SUCCESS]
>
>Het beleid wordt geactiveerd voor alle bestaande sandboxen en wordt automatisch toegevoegd aan nieuwe sandboxen wanneer deze beschikbaar komen.

### Beleid toevoegen aan geselecteerde sandboxen

>[!IMPORTANT]
>
>Toekomstige sandboxen worden niet standaard in het beleid opgenomen als de schakeloptie [!UICONTROL Auto-include] is uitgeschakeld. U moet sandboxen handmatig beheren en toevoegen aan het beleid.

Gebruik de schakeloptie **[!UICONTROL Auto-include]** op het tabblad **[!UICONTROL Sandboxes]** om het beleid voor alle sandboxen uit te schakelen.

![ het [!UICONTROL Sandboxes] lusje tonen van [!UICONTROL Auto-include] knevel.](../../images/flac-ui/abac-policies-auto-include.png)

Selecteer op het tabblad **[!UICONTROL Sandboxes]** de optie **[!UICONTROL Add Sandboxes]** om de sandboxen te selecteren waarop dit beleid van toepassing is.

![ het [!UICONTROL Sandboxes] lusje dat een lijst van zandbakken toont die aan het beleid worden toegevoegd.](../../images/flac-ui/abac-policies-sandboxes-tab-add.png)

Er wordt een lijst met sandboxen weergegeven. Selecteer in de lijst de sandbox die u wilt toevoegen. U kunt ook de zoekbalk gebruiken om te zoeken naar de sandbox. Selecteer **[!UICONTROL Save]**.

![ de [!UICONTROL Add Sandboxes] pagina die een lijst van bestaande zandbakken tonen beschikbaar om aan het beleid toe te voegen.](../../images/flac-ui/abac-policies-sandboxes-list.png)

>[!SUCCESS]
>
>De geselecteerde sandboxen zijn aan het beleid toegevoegd.

### Sandboxen verwijderen uit een beleid

Om een zandbak te verwijderen, selecteer het **X** pictogram naast de zandbaknaam.

![ het [!UICONTROL Sandboxes] lusje dat een lijst van zandbakken toont, die [!UICONTROL X] benadrukt om te schrappen.](../../images/flac-ui/abac-policies-remove-sandbox-x.png)

In het dialoogvenster **[!UICONTROL Remove]** wordt u gevraagd uw selectie te bevestigen. Selecteer **[!UICONTROL Confirm]** om het verwijderen te voltooien.

![ de [!UICONTROL Remove] dialoog die [!UICONTROL Confirm] benadrukt.](../../images/flac-ui/abac-policies-remove-sandbox.png)

>[!SUCCESS]
>
>De geselecteerde sandbox is uit het beleid verwijderd.

## Een beleid activeren {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Wat is het beleid?"
>abstract="Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Elke organisatie wordt geleverd met een standaardbeleid dat u moet activeren om toegang tot specifieke die voorwerpen te controleren op etiketten worden gebaseerd. De etiketten die op middelen worden toegepast ontkennen toegang tenzij de gebruikers aan een rol met een passend etiket worden toegewezen. Het standaardbeleid kan niet worden uitgegeven of worden geschrapt, maar zij kunnen worden geactiveerd of worden gedeactiveerd."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Labels beheren"

Als u een bestaand beleid wilt activeren, selecteert u het beleid op het tabblad **[!UICONTROL Policies]** .

![ fc-beleid-uitgezocht ](../../images/abac-end-to-end-user-guide/abac-policies-page.png)

Selecteer vervolgens de ellips (`…`) naast de naam van een beleid en een vervolgkeuzelijst met besturingselementen voor het bewerken, activeren, verwijderen of dupliceren van de rol. Selecteer activeren in het vervolgkeuzemenu.

![ fc-beleid-activeer ](../../images/abac-end-to-end-user-guide/abac-policies-activate.png)

Het dialoogvenster **[!UICONTROL Activate policy]** wordt weergegeven, waarin u wordt gevraagd de activering te bevestigen.

![ flash-policy-activate-confirm ](../../images/abac-end-to-end-user-guide/abac-activate-policies-dialog.png)


U keert terug naar het tabblad **[!UICONTROL policies]** en er verschijnt een bevestiging van de activering. De beleidsstatus wordt als actief weergegeven.

![ fc-beleid-geactiveerd ](../../images/abac-end-to-end-user-guide/abac-policies-confirm-activate.png)

## Volgende stappen

Met een geactiveerd beleid, kunt u aan de volgende stap te werk gaan [ toestemmingen voor een rol ](permissions.md) beheren.
