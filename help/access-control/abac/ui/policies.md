---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;op attributen-gebaseerd toegangsbeheer;ABAC
title: Beleid voor toegangsbeheer beheren
description: Het toegangsbeheerbeleid beheren via de interface voor machtigingen in Adobe Experience Cloud.
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 2a26c8786adc412dc643c8a0c94b966e439e034b
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Beleid voor toegangsbeheer beheren

Het beleid van de toegangscontrole is verklaringen die attributen samenbrengen om toelaatbare en ontoelaatbare acties te vestigen. Adobe verstrekt een standaardbeleid dat onmiddellijk kan worden geactiveerd of wanneer uw organisatie klaar is om toegang tot specifieke die voorwerpen te beginnen te controleren op [&#x200B; worden gebaseerd etiketten &#x200B;](./labels.md){target="_blank"}. Het standaardbeleid, **[!UICONTROL Default-Label-Based-Access-Control-Policy]**, leverages labels die op middelen worden toegepast om toegang te ontkennen tenzij de gebruikers in een rol met een passend etiket zijn.

>[!IMPORTANT]
>
>Het beleid van de toegangscontrole zou niet met het beleid van het gegevensgebruik moeten worden verward, dat controleert hoe de gegevens in Adobe Experience Platform worden gebruikt. Zie de gids bij het creëren van [&#x200B; beleid van het gegevensgebruik &#x200B;](../../../data-governance/policies/create.md){target="_blank"} voor meer informatie.

## Sandboxen configureren voor een beleid {#configure-policy}

Het beleid wordt toegepast op het zandbakniveau om te controleren welke zandbakken op etiket-gebaseerd toegangsbeheer afdwingen. Standaard is de functie **[!UICONTROL Auto-include]** ingeschakeld, wat betekent dat alle huidige en toekomstige sandboxen automatisch aan het beleid worden toegevoegd. Wanneer **[!UICONTROL Auto-include]** is uitgeschakeld, zijn alleen de sandboxen die u handmatig toevoegt, onderworpen aan de toegangsbeheerregels van het beleid.

>[!NOTE]
>
>Het **[!UICONTROL Default-Label-Based-Access-Control-Policy]** -beleid is momenteel het enige beleid dat beschikbaar is voor configuratie.

Beginnen vormend zandbakken van een beleid, navigeer aan **[!UICONTROL Permissions]** in [&#x200B; Adobe Experience Cloud &#x200B;](https://experience.adobe.com/){target="_blank"}. Selecteer **[!UICONTROL Policies]** in het linkerdeelvenster en selecteer vervolgens de **[!UICONTROL Default-Label-Based-Access-Control-Policy]** in de lijst.

![&#x200B; de beleidswerkruimte die een lijst van bestaand beleid tonen.](../../images/ui/policies/policies-home.png){zoomable="yes"}

De werkruimte Details van het beleid wordt weergegeven. Selecteer het tabblad **[!UICONTROL Sandboxes]** om de lijst met sandboxen weer te geven die aan het beleid zijn gekoppeld en toegang te krijgen tot de configuratieopties van de sandbox.

![&#x200B; de zandbakwerkruimte van het beleid die een lijst van bijbehorende zandbakken tonen.](../../images/ui/policies/policy-sandbox.png){zoomable="yes"}

### Automatisch opnemen beheren {#manage-auto-include}

>[!IMPORTANT]
>
>Standaard is **[!UICONTROL Auto-include]** ingeschakeld, wat betekent dat alle huidige en toekomstige sandboxen automatisch aan het beleid worden toegevoegd.

Als u wilt bepalen welke sandboxen in een beleid worden opgenomen, kunt u de functie **[!UICONTROL Auto-include]** in- of uitschakelen. Wanneer u **[!UICONTROL Auto-include]** uitschakelt, worden toekomstige sandboxen niet automatisch toegevoegd aan het beleid. Nochtans, die van de eigenschap **van een knevel voorzien zal** geen zandbakken verwijderen die reeds inbegrepen in het beleid zijn.

![&#x200B; het zandbaklusje van het beleid met auto-omvat knevel benadrukt en in de &quot;off&quot;staat.](../../images/ui/policies/policy-auto-include.png){zoomable="yes"}

Als u **[!UICONTROL Auto-include]** weer wilt inschakelen, schakelt u deze weer in. In het dialoogvenster **[!UICONTROL Enable Auto-include]** wordt u gevraagd uw selectie te bevestigen. Selecteer **[!UICONTROL Enable]** om de configuratie-instelling te voltooien.

>[!NOTE]
>
>Wanneer u **[!UICONTROL Auto-include]** weer inschakelt, worden alle sandboxen die u eerder uit het beleid hebt verwijderd, opnieuw toegevoegd.

![&#x200B; laat auto-omvat dialoog met toelaat benadrukte optie toe.](../../images/ui/policies/policy-enable-auto-include.png){zoomable="yes"}

### Sandboxen handmatig beheren {#manually-manage-sandboxes}

Wanneer **&#x200B; [!UICONTROL Auto-include] &#x200B;** wordt uitgezet, kunt u specifieke zandbakken toevoegen of manueel verwijderen uit het beleid. Dit geeft u nauwkeurige controle over welke zandbakken de toegangsbeheerregels van het beleid afdwingen.

>[!NOTE]
>
>Om zandbakken manueel toe te voegen of te verwijderen, moet **[!UICONTROL Auto-include]** knevel **&#x200B;**&#x200B;weg zijn.

**om zandbakken toe te voegen:**

Selecteer **[!UICONTROL Add Sandboxes]** in de sandboxwerkruimte van het beleid.

![&#x200B; de werkruimte van het beleid met de Add benadrukte optie van Sandboxen.](../../images/ui/policies/policy-add-sandboxes.png){zoomable="yes"}

Het dialoogvenster **[!UICONTROL Add Sandboxes]** wordt weergegeven met uw bibliotheek met beschikbare sandboxen. Selecteer de sandbox(s) die u aan het beleid wilt toevoegen en selecteer vervolgens **[!UICONTROL Save]** .

![&#x200B; voegt de Add dialoog van Sandboxen met geselecteerde zandbak en sparen benadrukte optie toe.](../../images/ui/policies/policy-add-sandboxes-select.png){zoomable="yes"}

>[!NOTE]
>
>Als alle beschikbare sandboxen al in het beleid zijn opgenomen, wordt het bericht &quot;U hebt niets in uw bibliotheek&quot; weergegeven in het dialoogvenster.

**om zandbakken te verwijderen:**

Vind zandbak u wenst om uit de lijst te verwijderen en het **X** pictogram naast zijn naam te selecteren.

![&#x200B; de zandbaklijst van het beleid met &quot;x&quot;benadrukte om een zandbak te verwijderen.](../../images/ui/policies/policy-remove-sandbox.png){zoomable="yes"}

Er wordt een bevestigingsvenster weergegeven. Selecteer **[!UICONTROL Confirm]** om het verwijderen van de sandbox uit het beleid te voltooien.

![&#x200B; de bevestigingsdialoog van een zandbak met de bevestig benadrukte optie.](../../images/ui/policies/policy-remove-sandbox-confirmation.png){zoomable="yes"}

## Een beleid activeren {#activate-policy}

>[!CONTEXTUALHELP]
>id="platform_permissions_policies_about"
>title="Wat is het beleid?"
>abstract="Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Elke organisatie wordt geleverd met een standaardbeleid dat u moet activeren om toegang tot specifieke die voorwerpen te controleren op etiketten worden gebaseerd. De etiketten die op middelen worden toegepast ontkennen toegang tenzij de gebruikers aan een rol met een passend etiket worden toegewezen. Het beleid kan niet worden uitgegeven of worden geschrapt, maar zij kunnen worden geactiveerd of worden gedeactiveerd."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-platform/access-control/abac/permissions-ui/labels" text="Labels beheren"

Als u een bestaand beleid wilt activeren, selecteert u het beleid op de tab **[!UICONTROL Policies]** in **[!UICONTROL Permissions]** . De activeringsstatus van het beleid is zichtbaar onder de sectie **[!UICONTROL Status]** .

![&#x200B; de beleidswerkruimte met de benadrukte status van een beleid.](../../images/ui/policies/policy-status.png){zoomable="yes"}

De werkruimte Details van het beleid wordt weergegeven. Selecteer **[!UICONTROL Activate]**.

![&#x200B; de het detailwerkruimte van het beleid met de Actieve benadrukte optie.](../../images/ui/policies/policy-activate.png){zoomable="yes"}

Het dialoogvenster **[!UICONTROL Activate Policy]** wordt weergegeven. Selecteer **[!UICONTROL Confirm]** om de activering van het beleid te voltooien.

![&#x200B; activeer de dialoog van het Beleid met de Bevestiging benadrukte optie.](../../images/ui/policies/policy-activate-confirm.png){zoomable="yes"}

## Volgende stappen

Met een geactiveerd beleid, kunt u aan de volgende stap te werk gaan [&#x200B; toestemmingen voor een rol &#x200B;](permissions.md) beheren.
