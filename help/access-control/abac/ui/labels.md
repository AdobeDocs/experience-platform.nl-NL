---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;op attributen-gebaseerd toegangsbeheer
title: Op kenmerken gebaseerde toegangsbeheerlabels beheren
description: Labels beheren via de machtigingsinterface in Adobe Experience Cloud.
exl-id: c790f09c-fda6-48bf-95db-3f5053cd882e
source-git-commit: 855f0a1384f658d39aa9d4fbb6bcb032933e59db
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---

# Labels beheren

U kunt etiketten gebruiken om datasets en gebieden volgens gegevensgebruik en op attribuut-gebaseerde toegangsbeheerbeleid te categoriseren. Labels kunnen op elk gewenst moment worden toegepast, zodat u op flexibele wijze gegevens kunt beheren. De beste praktijken bevorderen etiketteringsgegevens zodra het in Adobe Experience Platform wordt opgenomen, of zodra de gegevens voor gebruik beschikbaar worden. Lees dit document om te leren hoe u labels kunt beheren in de gebruikersinterface voor machtigingen.

Voor een uitvoerige lijst van etiketten en hun overeenkomstige governancebeleid, lees de gids op [&#x200B; de etiketten van het het kerngegevensgebruik &#x200B;](../../../data-governance/labels/reference.md){target="_blank"}.

>[!NOTE]
>
>Om [&#x200B; gegevens verwerkte attributen &#x200B;](../../../profile/computed-attributes/overview.md){target="_blank"} met gebieden tot stand te brengen of te bekijken die een bepaald etiket bevatten, moet u toegang tot dat etiket hebben.

## Labels verkennen {#explore-labels}

Om alle beschikbare etiketten te bekijken, navigeer aan **[!UICONTROL Permissions]** in [&#x200B; Adobe Experience Cloud &#x200B;](https://experience.adobe.com/){target="_blank"}. Selecteer **[!UICONTROL Labels]** in het linkerdeelvenster.

![&#x200B; de etikettenwerkruimte binnen Toestemmingen met Etiketten die in het linkerpaneel worden benadrukt.](../../images/ui/labels/labels-home.png){zoomable="yes"}

De etiketten worden gecategoriseerd door type en behoren tot één van de volgende categorieën:

| Type | Beschrijving |
| --- | --- |
| [&#x200B; Slinken &#x200B;](../../../data-governance/labels/reference.md#contract){target="_blank"} | Deze categorie wordt gebruikt om gegevens te categoriseren die contractuele verplichtingen hebben of die gerelateerd zijn aan het beleid van uw organisatie voor gegevensbeheer. |
| [&#x200B; Identiteit &#x200B;](../../../data-governance/labels/reference.md#identity){target="_blank"} | Deze categorie wordt gebruikt om gegevens te categoriseren die direct of indirect een persoon kunnen identificeren. |
| [&#x200B; Gevoelig &#x200B;](../../../data-governance/labels/reference.md#sensitive){target="_blank"} | Deze categorie wordt gebruikt om gegevens te categoriseren die uw organisatie als gevoelig beschouwt. |
| [&#x200B; Ecosysteem van de Partner &#x200B;](../../../data-governance/labels/reference.md#partner){target="_blank"} | Deze categorie wordt gebruikt om gegevens te categoriseren die uit bronnen buiten uw organisatie worden verkregen. |
| Verantwoordelijke betrokkenheid | Deze categorie bevat één label, **[!UICONTROL Potential for Bias]** , dat gegevens weergeeft die een afwijking kunnen veroorzaken. |
| Aangepast | Deze categorie bevat labels die door uw organisatie zijn gemaakt. |

Om etiketten te filtreren, selecteer het filterpictogram (![&#x200B; filterpictogram &#x200B;](/help/images/icons/filter.png)) en selecteer dan uw gewenste etikettype van **[!UICONTROL Type]** dropdown.

![&#x200B; de etikettenwerkruimte met de uitgevouwen filteroptie en het type onderaan lijst benadrukte.](../../images/ui/labels/label-filter.png){zoomable="yes"}

Als u een afzonderlijk label wilt weergeven, selecteert u de naam van het label in de lijst. De detailpagina van het label wordt weergegeven. Adobe kernetiketten zijn **niet** editable.

![&#x200B; de detailpagina van een individueel etiket.](../../images/ui/labels/label-details.png){zoomable="yes"}

## Een aangepast label maken {#create-custom-label}

>[!CONTEXTUALHELP]
>id="platform_abac_labelusage"
>title="Gebruik van label"
>abstract="U kunt douanelabels gebruiken om gegevensbeheer en toegangsbeheerconfiguraties op uw gegevens toe te passen."

>[!CONTEXTUALHELP]
>id="platform_permissions_labels_about_create"
>title="Nieuw label maken"
>abstract="U kunt uw eigen aangepaste labels maken die aansluiten op de behoeften van uw organisatie. De etiketten van de douane kunnen worden gebruikt om zowel gegevensbeheer als toegangsbeheerconfiguraties op uw gegevens toe te passen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-governance/labels/overview.html?lang=nl-NL#manage-labels" text="Aangepaste labels beheren"

>[!NOTE]
>
>Als u een aangepast label wilt maken, hebt u een rol nodig die de **[!UICONTROL Manage Usage Labels]** -machtigingen en de `Prod` -sandbox bevat.

Als u een nieuw label wilt maken, selecteert u **[!UICONTROL Labels]** in het linkerdeelvenster van de **[!UICONTROL Permissions]** -werkruimte en selecteert u vervolgens **[!UICONTROL Create label]** .

![&#x200B; de etikettenwerkruimte met Create benadrukte etiketoptie.](../../images/ui/labels/create-label.png){zoomable="yes"}

Het dialoogvenster **[!UICONTROL Create new label]** wordt weergegeven, waarin u wordt gevraagd een **[!UICONTROL Name]** , a **[!UICONTROL Friendly name]** en **[!UICONTROL Description]** in te voeren.

>[!IMPORTANT]
>
> Het label [!UICONTROL Name] kan niet worden gewijzigd nadat het label is gemaakt en het verwijderen van het label wordt momenteel niet ondersteund.

Selecteer **[!UICONTROL Confirm]** om het maken van het label te voltooien.

![&#x200B; creeer nieuwe etiketdialoog met de Naam, Vriendelijke naam, en Beschrijving die en de bevestig benadrukte optie wordt gevuld.](../../images/ui/labels/create-new-label.png){zoomable="yes"}

## Een aangepast label bewerken {#edit-custom-label}

U kunt de labels **[!UICONTROL Name]** van een aangepast label niet bewerken, maar wel de **[!UICONTROL Friendly name]** en **[!UICONTROL Description]** . Als u een aangepast label wilt bewerken, selecteert u het label in de lijst in de **[!UICONTROL Labels]** -werkruimte.

![&#x200B; de werkruimte van Etiketten met het benadrukte etiket.](../../images/ui/labels/select-label.png){zoomable="yes"}

Bewerk een van de velden en klik vervolgens ergens buiten het tekstvak om de wijzigingen op te slaan. Er verschijnt een bevestigingsbericht op het scherm en de datum **[!UICONTROL Modified by]** name en **[!UICONTROL Modified]** will change.

![&#x200B; de detailpagina van het etiket met een &quot;bijgewerkt met succes&quot;getoond bericht.](../../images/ui/labels/edit-label.png){zoomable="yes"}

## Volgende stappen

Nu u een dieper begrip van etiketten hebt, kunt u beginnen [&#x200B; die hen op schema&#39;s &#x200B;](../../../xdm/tutorials/labels.md) toepassen.
