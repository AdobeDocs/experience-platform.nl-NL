---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;gebruikershandleiding voor gegevensgebruiksbeleid
solution: Experience Platform
title: Beleid voor gegevensgebruik beheren in de gebruikersinterface
topic-legacy: policies
description: Adobe Experience Platform Data Governance biedt een gebruikersinterface waarmee u beleid voor gegevensgebruik kunt maken en beheren. Dit document biedt een overzicht van de acties die u kunt uitvoeren in de werkruimte Beleid in de gebruikersinterface van het Experience Platform.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Beleid voor gegevensgebruik beheren in de gebruikersinterface

Adobe Experience Platform Data Governance biedt een gebruikersinterface waarmee u beleid voor gegevensgebruik kunt maken en beheren. Dit document biedt een overzicht van de acties die u kunt uitvoeren in het dialoogvenster **Beleid** werkruimte in de [!DNL Experience Platform] gebruikersinterface.

>[!IMPORTANT]
>
>Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Om een individueel beleid voor handhaving te overwegen, moet u dat beleid manueel toelaten. Zie de sectie over [beleid inschakelen](#enable) voor stappen over hoe te om dit in UI te doen.

## Vereisten

Deze handleiding vereist een goed begrip van het volgende: [!DNL Experience Platform] concepten:

* [Data Governance](../home.md)
* [Beleid voor gegevensgebruik](./overview.md)

## Bestaande beleidsvormen weergeven {#view-policies}

In de [!DNL Experience Platform] UI, selecteer **[!UICONTROL Policies]** om de **[!UICONTROL Policies]** werkruimte. In de **[!UICONTROL Browse]** kunt u een lijst met beschikbare beleidsregels weergeven, inclusief de bijbehorende labels, marketingacties en status.

![](../images/policies/browse-policies.png)

Als u toegang hebt tot beleid voor toestemming, selecteert u de optie **[!UICONTROL Consent policies]** schakelen om ze weer te geven in het dialoogvenster [!UICONTROL Browse] tab.

![](../images/policies/consent-policy-toggle.png)

Selecteer een vermeld beleid om zijn beschrijving en type te bekijken. Als een aangepast beleid is geselecteerd, worden aanvullende besturingselementen weergegeven om te bewerken, te verwijderen of [het beleid in-/uitschakelen](#enable).

![](../images/policies/policy-details.png)

## Een aangepast beleid maken {#create-policy}

Selecteer **[!UICONTROL Create policy]** in de rechterbovenhoek van het dialoogvenster **[!UICONTROL Browse]** in de **[!UICONTROL Policies]** werkruimte.

![](../images/policies/create-policy-button.png)

Afhankelijk van of u deel uitmaakt van de bètaversie voor het toestemmingsbeleid, komt een van de volgende situaties voor:

* Als u geen deel uitmaakt van de bètaversie, wordt u onmiddellijk naar de werkstroom gebracht voor [invoering van een beleid voor gegevensbeheer](#create-governance-policy).
* Als u deel uitmaakt van de bètaversie, biedt een dialoogvenster een extra optie voor [een beleid voor instemming ontwikkelen](#consent-policy).
   ![](../images/policies/choose-policy-type.png)

### Een beleid voor gegevensbeheer maken {#create-governance-policy}

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

### Een toestemmingsbeleid maken {#consent-policy}

>[!IMPORTANT]
>
>Het beleid van de toestemming is momenteel slechts beschikbaar voor organisaties die het Schild van de Gezondheidszorg hebben gekocht.

Als u verkoos om een toestemmingsbeleid tot stand te brengen, verschijnt een nieuw scherm dat u toestaat om het nieuwe beleid te vormen.

![](../images/policies/consent-policy-dialog.png)

Als u het beleid voor toestemming wilt gebruiken, moet u toestemmingskenmerken in uw profielgegevens hebben. Zie de handleiding op [verwerking van toestemming in Experience Platform](../../landing/governance-privacy-security/consent/adobe/overview.md) voor gedetailleerde stappen op hoe te om de vereiste attributen in uw unieschema te omvatten.

Het beleid van de goedkeuring bestaat uit twee logische componenten:

* **[!UICONTROL If]**: De voorwaarde die de beleidscontrole zal teweegbrengen. Dit kan gebaseerd zijn op een bepaalde marketingactie die wordt uitgevoerd, de aanwezigheid van bepaalde labels voor gegevensgebruik of een combinatie van beide.
* **[!UICONTROL Then]**: De toestemmingskenmerken die aanwezig moeten zijn opdat een profiel wordt opgenomen in de actie die het beleid heeft geïnitieerd.

#### Voorwaarden configureren

Onder de **[!UICONTROL If]** selecteert u de marketingacties en/of labels voor gegevensgebruik die dit beleid moeten activeren. Selecteren **[!UICONTROL View all]** en **[!UICONTROL Select labels]** de volledige lijsten van de beschikbare marketingacties en etiketten te bekijken.

Nadat u ten minste één voorwaarde hebt toegevoegd, kunt u **[!UICONTROL Add condition]** om verdere voorwaarden te blijven toevoegen zoals nodig, verkies het aangewezen voorwaardetype van dropdown.

![](../images/policies/add-condition.png)

Als u meer dan één voorwaarde selecteert, kunt u het pictogram gebruiken dat tussen hen verschijnt om de voorwaardelijke verhouding tussen &quot;EN&quot;en &quot;OF&quot;te schakelen.

![](../images/policies/and-or-selection.png)

#### Goedkeuringskenmerken selecteren

Onder de **[!UICONTROL Then]** selecteert u ten minste één toestemmingskenmerk in het schema union. Dit is het kenmerk dat aanwezig moet zijn om profielen op te nemen in de actie waarop dit beleid van toepassing is. U kunt een van de beschikbare opties in de lijst kiezen of **[!UICONTROL View all]** om de attributen van het unieschema direct te kiezen.

Wanneer het selecteren van de toestemmingsattributen, kies de waarden voor de attributen die u dit beleid wilt controleren.

![](../images/policies/select-schema-field.png)

Nadat u minstens één toestemmingsattribuut hebt geselecteerd, **[!UICONTROL Policy properties]** worden bijgewerkt om het geschatte aantal profielen weer te geven dat in het kader van dit beleid is toegestaan, inclusief het percentage van de totale profielopslag. Deze schatting wordt automatisch bijgewerkt wanneer u de beleidsconfiguratie aanpast.

![](../images/policies/audience-preview.png)

Als u meer toestemmingskenmerken aan het beleid wilt toevoegen, selecteert u **[!UICONTROL Add result]**.

![](../images/policies/add-result.png)

U kunt voorwaarden en toestemmingseigenschappen aan het beleid blijven toevoegen en aanpassen zoals nodig. Als u tevreden bent met de configuratie, geeft u een naam en een optionele beschrijving voor het beleid op voordat u het beleid selecteert **[!UICONTROL Save]**.

![](../images/policies/name-and-save.png)

Het toestemmingsbeleid wordt nu tot stand gebracht en zijn status wordt geplaatst aan [!UICONTROL Disabled] standaard. Als u het beleid meteen wilt inschakelen, selecteert u de optie **[!UICONTROL Status]** schakelen in de rechterspoorstaaf.

![](../images/policies/enable-consent-policy.png)

#### Beleidshandhaving verifiëren

Nadat u een toestemmingsbeleid hebt gecreeerd en toegelaten, kunt u voorproef hoe het uw toegelaten publiek wanneer het activeren van segmenten aan bestemmingen beïnvloedt. Zie de sectie over [goedkeuring beleidsevaluatie](../enforcement/auto-enforcement.md#consent-policy-evaluation) voor meer informatie .

## Een beleid in- of uitschakelen {#enable}

Alle beleidsregels voor gegevensgebruik (inclusief kernbeleid van Adobe) zijn standaard uitgeschakeld. Voor een individueel beleid dat voor handhaving moet worden overwogen, moet u dat beleid manueel toelaten door API of UI.

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
>Wanneer wordt geprobeerd een marketingactie te verwijderen die door een bestaand beleid wordt gebruikt, verschijnt een foutbericht dat aangeeft dat de verwijderpoging is mislukt.

![](../images/policies/delete-marketing-action.png)

## Volgende stappen

In dit document wordt een overzicht gegeven van de manier waarop u beleidsregels voor gegevensgebruik kunt beheren in [!DNL Experience Platform] UI. Voor stappen over hoe te om beleid te beheren gebruikend [!DNL Policy Service API], zie de [ontwikkelaarsgids](../api/getting-started.md). Voor informatie over hoe te om het beleid van het gegevensgebruik af te dwingen, zie [overzicht van de beleidshandhaving](../enforcement/overview.md).

In de volgende video ziet u hoe u met het gebruiksbeleid kunt werken in het dialoogvenster [!DNL Experience Platform] UI:

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
