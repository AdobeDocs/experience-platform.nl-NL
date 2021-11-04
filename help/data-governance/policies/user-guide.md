---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;gebruikershandleiding voor gegevensgebruiksbeleid
solution: Experience Platform
title: Beleid voor gegevensgebruik beheren in de gebruikersinterface
topic-legacy: policies
description: Adobe Experience Platform Data Governance biedt een gebruikersinterface waarmee u beleid voor gegevensgebruik kunt maken en beheren. Dit document biedt een overzicht van de acties die u kunt uitvoeren in de werkruimte Beleid in de gebruikersinterface van het Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# Beleid voor gegevensgebruik beheren in de gebruikersinterface

Adobe Experience Platform Data Governance biedt een gebruikersinterface waarmee u beleid voor gegevensgebruik kunt maken en beheren. Dit document biedt een overzicht van de handelingen die u kunt uitvoeren in het dialoogvenster **Beleid** werkruimte in de [!DNL Experience Platform] gebruikersinterface.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten. Zie de sectie over [beleid inschakelen](#enable) voor stappen over hoe te om dit in UI te doen.

## Vereisten

Deze handleiding vereist een goed begrip van het volgende: [!DNL Experience Platform] concepten:

- [Data Governance](../home.md)
- [Beleid voor gegevensgebruik](./overview.md)

## Bestaande beleidsvormen weergeven {#view-policies}

In de [!DNL Experience Platform] UI, selecteer **[!UICONTROL Policies]** om de **[!UICONTROL Policies]** werkruimte. In de **[!UICONTROL Browse]** kunt u een lijst met beschikbare beleidsregels weergeven, inclusief de bijbehorende labels, marketingacties en status.

![](../images/policies/browse-policies.png)

Selecteer een vermeld beleid om zijn beschrijving en type te bekijken. Als een aangepast beleid is geselecteerd, worden aanvullende besturingselementen weergegeven om te bewerken, te verwijderen of [het beleid in-/uitschakelen](#enable).

![](../images/policies/policy-details.png)

## Een aangepast beleid maken {#create-policy}

Selecteer **[!UICONTROL Create policy]** in de rechterbovenhoek van het dialoogvenster **[!UICONTROL Browse]** in de **[!UICONTROL Policies]** werkruimte.

![](../images/policies/create-policy-button.png)

De **[!UICONTROL Create policy]** wordt weergegeven. Begin door een naam en een beschrijving voor het nieuwe beleid te verstrekken.

![](../images/policies/create-policy-description.png)

Selecteer vervolgens de labels voor gegevensgebruik waarop het beleid wordt gebaseerd. Als u meerdere labels selecteert, kunt u kiezen of de gegevens alle labels moeten bevatten of slechts één label, zodat het beleid van toepassing is. Selecteren **[!UICONTROL Next]** wanneer gereed.

![](../images/policies/add-labels.png)

De **[!UICONTROL Select marketing actions]** wordt weergegeven. Kies de gewenste marketingacties in de lijst en selecteer **[!UICONTROL Next]** om door te gaan.

>[!NOTE]
>
>Wanneer het selecteren van veelvoudige marketing acties, interpreteert het beleid hen als &quot;OF&quot;regel. Met andere woorden, het beleid is van toepassing als **alle** van de geselecteerde marketingacties worden uitgevoerd.

![](../images/policies/add-marketing-actions.png)

De **[!UICONTROL Review]** wordt weergegeven, zodat u de details van het nieuwe beleid kunt bekijken voordat u het maakt. Als u tevreden bent, selecteert u **[!UICONTROL Finish]** om het beleid te creëren.

![](../images/policies/policy-review.png)

De **[!UICONTROL Browse]** wordt opnieuw weergegeven. Dit betekent dat het nieuwe beleid de status &quot;Concept&quot; krijgt. Zie de volgende sectie om het beleid in te schakelen.

![](../images/policies/created-policy.png)

## Een beleid in- of uitschakelen {#enable}

Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten door API of UI.

U kunt het beleid in- of uitschakelen in het dialoogvenster **[!UICONTROL Browse]** in de **[!UICONTROL Policies]** werkruimte. Selecteer een aangepast beleid in de lijst om de details aan de rechterkant weer te geven. Onder **[!UICONTROL Status]**, selecteert u de schakelknop om het beleid in of uit te schakelen.

![](../images/policies/enable-policy.png)

## Marketingacties weergeven {#view-marketing-actions}

In de **[!UICONTROL Policies]** werkruimte, selecteert u de **[!UICONTROL Marketing actions]** tabblad om een lijst weer te geven met beschikbare marketingacties die zijn gedefinieerd door Adobe en uw eigen organisatie.

![](../images/policies/marketing-actions.png)

## Een marketingactie maken {#create-marketing-action}

Als u een nieuwe aangepaste marketingactie wilt maken, selecteert u **[!UICONTROL Create marketing action]** in de rechterbovenhoek van het dialoogvenster **[!UICONTROL Marketing actions]** in de **[!UICONTROL Policies]** werkruimte.

![](../images/policies/create-marketing-action.png)

De **[!UICONTROL Create marketing action]** wordt weergegeven. Voer een naam en beschrijving in voor de marketingactie en selecteer **[!UICONTROL Create]**.

![](../images/policies/create-marketing-action-details.png)

De nieuwe actie wordt weergegeven in het dialoogvenster **[!UICONTROL Marketing actions]** tab. U kunt nu de marketingactie gebruiken wanneer [nieuw beleid voor gegevensgebruik maken](#create-policy).

![](../images/policies/created-marketing-action.png)

## Een marketingactie bewerken of verwijderen {#edit-delete-marketing-action}

>[!NOTE]
>
>Alleen aangepaste marketingacties die door uw organisatie zijn gedefinieerd, kunnen worden bewerkt. Marketingacties die door Adobe worden gedefinieerd, kunnen niet worden gewijzigd of verwijderd.

In de **[!UICONTROL Policies]** werkruimte, selecteert u de **[!UICONTROL Marketing actions]** tabblad om een lijst weer te geven met beschikbare marketingacties die zijn gedefinieerd door Adobe en uw eigen organisatie. Selecteer een aangepaste marketingactie in de lijst en gebruik vervolgens de beschikbare velden in de rechtersectie om de details van de marketingactie te bewerken.

![](../images/policies/edit-marketing-action.png)

Als de marketingactie niet wordt gebruikt door een bestaand gebruiksbeleid, kunt u deze verwijderen door **[!UICONTROL Delete marketing action]**.

>[!NOTE]
>
>Als u probeert een marketingactie te verwijderen die door een bestaand beleid wordt gebruikt, wordt een foutbericht weergegeven dat aangeeft dat de verwijderpoging is mislukt.

![](../images/policies/delete-marketing-action.png)

## Volgende stappen

In dit document wordt een overzicht gegeven van de manier waarop u beleidsregels voor gegevensgebruik kunt beheren in [!DNL Experience Platform] UI. Voor stappen over hoe te om beleid te beheren gebruikend [!DNL Policy Service API], zie de [ontwikkelaarsgids](../api/getting-started.md). Voor informatie over hoe te om het beleid van het gegevensgebruik af te dwingen, zie [overzicht van de beleidshandhaving](../enforcement/overview.md).

In de volgende video ziet u hoe u met het gebruiksbeleid kunt werken in het dialoogvenster [!DNL Experience Platform] UI:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
