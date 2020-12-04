---
keywords: Experience Platform;home;popular topics;data governance;data usage policy user guide
solution: Experience Platform
title: Gebruikershandleiding voor gegevensgebruiksbeleid
topic: policies
description: Adobe Experience Platform Data Governance biedt een gebruikersinterface waarmee u beleid voor gegevensgebruik kunt maken en beheren. Dit document biedt een overzicht van de acties die u kunt uitvoeren in de werkruimte Beleid in de gebruikersinterface van het Experience Platform.
translation-type: tm+mt
source-git-commit: a362b67cec1e760687abb0c22dc8c46f47e766b7
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Gebruikershandleiding voor gegevensgebruiksbeleid

Adobe Experience Platform [!DNL Data Governance] biedt een gebruikersinterface waarmee u beleid voor gegevensgebruik kunt maken en beheren. Dit document biedt een overzicht van de acties die u kunt uitvoeren in de werkruimte **Beleid** in de [!DNL Experience Platform] gebruikersinterface.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten. Zie de sectie over het [toelaten van beleid](#enable) voor stappen op hoe te om dit in UI te doen.

## Vereisten

Deze gids vereist een werkend begrip van de volgende [!DNL Experience Platform] concepten:

- [[!DNL Data Governance]](../home.md)
- [Beleid voor gegevensgebruik](./overview.md)

## Beleid voor gegevensgebruik weergeven {#view-policies}

Klik in de [!DNL Experience Platform] gebruikersinterface op **[!UICONTROL Beleid]** om de werkruimte **[!UICONTROL Beleid]** te openen. Op het tabblad **[!UICONTROL Bladeren]** ziet u een lijst met beschikbare beleidsregels, inclusief de bijbehorende labels, marketingacties en status.

![](../images/policies/browse-policies.png)

Klik op een vermeld beleid om de beschrijving en het type ervan weer te geven. Als een douanebeleid wordt geselecteerd, worden de extra controles getoond om uit te geven, te schrappen, of [toe te laten/onbruikbaar te maken het beleid](#enable).

![](../images/policies/policy-details.png)

## Een aangepast beleid voor gegevensgebruik maken {#create-policy}

Als u een nieuw beleid voor het gebruik van aangepaste gegevens wilt maken, klikt u op **[!UICONTROL Beleid]** maken in de rechterbovenhoek van het tabblad **[!UICONTROL Bladeren]** in de werkruimte **[!UICONTROL Beleid]** .

![](../images/policies/create-policy-button.png)

De **[!UICONTROL workflow Beleid]** maken wordt weergegeven. Begin door een naam en een beschrijving voor het nieuwe beleid te verstrekken.

![](../images/policies/create-policy-description.png)

Selecteer vervolgens de labels voor gegevensgebruik waarop het beleid wordt gebaseerd. Als u meerdere labels selecteert, kunt u kiezen of de gegevens alle labels moeten bevatten of slechts één label, zodat het beleid van toepassing is. Klik op **[!UICONTROL Volgende]** als u klaar bent.

![](../images/policies/add-labels.png)

De stap **[!UICONTROL Marketingacties]** selecteren wordt weergegeven. Kies de gewenste marketingacties in de lijst en klik op **[!UICONTROL Volgende]** om door te gaan.

>[!NOTE]
>
>Wanneer het selecteren van veelvoudige marketing acties, interpreteert het beleid hen als &quot;OF&quot;regel. Met andere woorden, het beleid is van toepassing als **om het even welke** geselecteerde marketing acties worden uitgevoerd.

![](../images/policies/add-marketing-actions.png)

De stap **[!UICONTROL Revisie]** wordt weergegeven, zodat u de details van het nieuwe beleid kunt bekijken voordat u het maakt. Als u tevreden bent, klikt u op **[!UICONTROL Voltooien]** om het beleid te maken.

![](../images/policies/policy-review.png)

Het tabblad **[!UICONTROL Bladeren]** wordt opnieuw weergegeven. Hierin wordt nu het nieuwe beleid in de status &quot;Concept&quot; weergegeven. Zie de volgende sectie om het beleid in te schakelen.

![](../images/policies/created-policy.png)

## Een beleid voor gegevensgebruik in- of uitschakelen {#enable}

Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten door API of UI.

U kunt beleid van het **[!UICONTROL Browse]** lusje in of onbruikbaar maken in de werkruimte van **[!UICONTROL Beleid]** . Selecteer een aangepast beleid in de lijst om de details aan de rechterkant weer te geven. Selecteer onder **[!UICONTROL Status]** de schakelknop om het beleid in of uit te schakelen.

![](../images/policies/enable-policy.png)

## Marketingacties weergeven {#view-marketing-actions}

In de werkruimte **[!UICONTROL Beleid]** , selecteer het lusje van de Acties **[!UICONTROL van de]** Marketing om een lijst van beschikbare marketing acties te bekijken die door Adobe en uw eigen organisatie worden bepaald.

![](../images/policies/marketing-actions.png)

## Een marketingactie maken {#create-marketing-action}

Als u een nieuwe aangepaste marketingactie wilt maken, klikt u op **[!UICONTROL Marketing-actie]** maken in de rechterbovenhoek van het tabblad **[!UICONTROL Handelingen]** voor marketing in de werkruimte **[!UICONTROL Beleid]** .

![](../images/policies/create-marketing-action.png)

Het dialoogvenster **[!UICONTROL Handeling]** voor marketingacties maken wordt weergegeven. Voer een naam en beschrijving in voor de marketingactie en klik op **[!UICONTROL Maken]**.

![](../images/policies/create-marketing-action-details.png)

De nieuwe actie wordt weergegeven op het tabblad **[!UICONTROL Handelingen]** voor marketingdoeleinden. U kunt de marketingactie nu gebruiken bij het [maken van nieuw beleid](#create-policy)voor gegevensgebruik.

![](../images/policies/created-marketing-action.png)

## Een marketingactie bewerken of verwijderen {#edit-delete-marketing-action}

>[!NOTE]
>
>Alleen aangepaste marketingacties die door uw organisatie zijn gedefinieerd, kunnen worden bewerkt. Marketingacties die door Adobe worden gedefinieerd, kunnen niet worden gewijzigd of verwijderd.

In de werkruimte **[!UICONTROL Beleid]** , selecteer het lusje van de Acties **[!UICONTROL van de]** Marketing om een lijst van beschikbare marketing acties te bekijken die door Adobe en uw eigen organisatie worden bepaald. Selecteer een aangepaste marketingactie in de lijst en gebruik vervolgens de beschikbare velden in de rechtersectie om de details van de marketingactie te bewerken.

![](../images/policies/edit-marketing-action.png)

Als de marketingactie niet wordt gebruikt door een bestaand gebruiksbeleid, kunt u deze verwijderen door te klikken op **[!UICONTROL Marketing-actie]** verwijderen.

>[!NOTE]
>
>Als u probeert een marketingactie te verwijderen die door een bestaand beleid wordt gebruikt, wordt een foutbericht weergegeven dat aangeeft dat de verwijderpoging is mislukt.

![](../images/policies/delete-marketing-action.png)

## Volgende stappen

In dit document wordt een overzicht gegeven van de manier waarop beleidsregels voor gegevensgebruik in de [!DNL Experience Platform] gebruikersinterface kunnen worden beheerd. Raadpleeg de handleiding voor [!DNL Policy Service API]ontwikkelaars voor informatie over het beheren van beleidsregels met behulp van [de handleiding](../api/getting-started.md). Voor informatie over hoe te om het beleid van het gegevensgebruik af te dwingen, zie het [beleidshandhavingsoverzicht](../enforcement/overview.md).

De volgende video biedt een demonstratie van hoe u met gebruiksbeleid kunt werken in de [!DNL Experience Platform] gebruikersinterface:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)