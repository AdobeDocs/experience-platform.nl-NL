---
title: Beheer voorspellende leads en accountscoring in Real-Time CDP B2B
type: Documentation
description: Dit document bevat informatie over het beheer van de functie voor het voorspellen van leads en accounts in Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B Edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 2%

---

# Beheer voorspellende leads en accountscoring in Adobe Real-time Customer Data Platform, B2B Edition

>[!NOTE]
>
>Alleen gebruikers met de machtiging B2B AI beheren kunnen muziekdoelen maken, wijzigen en verwijderen.

Dit leerprogramma begeleidt u door de stappen om scoredoelstellingen van de voorspellende lood en rekening het scoren dienst te beheren. Score-doelen kunnen worden gesteld voor het profiel van een persoon of account

## Een nieuwe score maken

Als u een nieuwe score wilt maken, selecteert u de **[!UICONTROL Services]** in de zijbalk en selecteer **[!UICONTROL Create score]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

De **[!UICONTROL Basic information]** wordt weergegeven en u wordt gevraagd een profieltype te selecteren, een naam en een optionele beschrijving in te voeren. Selecteer **[!UICONTROL Next]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

De **[!UICONTROL Define your goal]** wordt weergegeven. Selecteer de vervolgkeuzepijl en selecteer vervolgens een doeltype in het vervolgkeuzevenster dat wordt weergegeven.

![plas-select-a-target](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

De **[!UICONTROL Goal specifics]** wordt geopend. Selecteer de vervolgkeuzepijl en selecteer vervolgens de naam van het doelveld in het vervolgkeuzevenster dat wordt weergegeven.

![plas-select-a-target-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

De **[!UICONTROL Goal conditions]** wordt weergegeven. Selecteer de vervolgkeuzepijl en selecteer vervolgens de voorwaarde in het vervolgkeuzevenster dat wordt weergegeven.

![plas-target-specifics-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

De **[!UICONTROL Goal value]** wordt weergegeven. Vervolgens configureert u uw [!UICONTROL Goal specifics]. Selecteer de [!UICONTROL Enter Field Value] en voer de waarde van uw doel in.

>[!NOTE]
>
>U kunt meerdere doelwaarden toevoegen.

![plas-target-specifics-field-value](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Als u aanvullende velden wilt toevoegen, selecteert u **[!UICONTROL Add field]**.

![plas-target-specifics-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Selecteer de vervolgkeuzepijl en selecteer vervolgens het gewenste tijdframe om de voorspelling te configureren.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

Het geselecteerde samenvoegbeleid bepaalt hoe de veldwaarden van een personenprofiel worden geselecteerd. Selecteer met de vervolgkeuzepijl het gewenste samenvoegbeleid en selecteer **[!UICONTROL Finish]**.

De **[!UICONTROL Scoring setup is complete]** wordt bevestigd dat de nieuwe score is gemaakt. Selecteer **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Het kan tot 24 uur duren voor elk scoringsproces wordt voltooid.

U bent teruggekeerd aan **[!UICONTROL Services]** Hier kunt u de nieuwe score zien die in de lijst met scores is gemaakt.

![met plas-score](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Selecteer de score om details en aanvullende informatie over de details van de laatste uitvoering weer te geven.

![plas-score-extra-informatie](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Voor meer gedetailleerde informatie over de foutcodes die u kunt zien onder de laatste run-details, raadpleegt u de sectie over [leidt tot AI pijpleidingsfoutencodes](#leads-ai-pipeline-error-codes) in dit document.

## Een score bewerken

Als u een score wilt bewerken, selecteert u een score in het menu **[!UICONTROL Services]** en selecteert u **[!UICONTROL Edit]** in het deelvenster Extra details aan de rechterkant van het scherm.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

De **[!UICONTROL Edit instance]** wordt weergegeven, waar u de beschrijving van de score kunt bewerken. Breng uw wijzigingen aan en selecteer **[!UICONTROL Save]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>De scoreconfiguratie kan niet worden gewijzigd omdat dit modelomscholing en re-scoring teweegbrengt. Het equivalent hiervan is het verwijderen van de score en het maken van een nieuwe score. Als u de configuratie van de score wilt bewerken, moet u deze score klonen of een nieuwe score maken.

U bent teruggekeerd aan **[!UICONTROL Services]** tab. Selecteer de score om de bijgewerkte beschrijvingsdetails in het extra detailpaneel op de rechterkant van het scherm te bekijken.

## Een score klonen

Om een score te klonen, selecteer een score van **[!UICONTROL Services]** en selecteert u **[!UICONTROL Clone]** in het deelvenster Extra details aan de rechterkant van het scherm.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

De **[!UICONTROL Basic information]** wordt weergegeven. Het profieltype, de naam en de beschrijving worden gekloond op basis van de oorspronkelijke score. Wijzig deze details en selecteer **[!UICONTROL Next]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

De **[!UICONTROL Define your goal]** wordt weergegeven. Voltooi de sectie Doelen zoals u zou wanneer het creëren van een nieuwe score en selecteer **[!UICONTROL Finish]**.

U bent teruggekeerd aan **[!UICONTROL Services]** Hier ziet u de zojuist gekloonde score in de lijst.

>[!NOTE]
>
>De **[!UICONTROL Define your goal]** wordt niet gekloond vanaf de oorspronkelijke score.

## Muziek verwijderen

Om een score te schrappen, selecteer een score van **[!UICONTROL Services]** en selecteert u **[!UICONTROL Delete]** in het deelvenster Extra details aan de rechterkant van het scherm.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

De **[!UICONTROL Delete documentation]** bevestigingsvenster verschijnt. Selecteer **[!UICONTROL Delete]**.

![plas-delete-score-bevestiging](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Als u de muziekdefinitie verwijdert, worden ook alle voorspelde scores in het profiel van de persoon of het account verwijderd, maar niet de veldgroep die voor de muziekdefinitie is gemaakt. De veldgroep wordt in het gegevensmodel &#39;wees&#39; gelaten.

U bent teruggekeerd aan **[!UICONTROL Services]** waar u de score niet meer in de lijst kunt zien.

## Voorloopfoutcodes voor AI-pijpleidingen

| Foutcode | Foutbericht |
| --- | --- |
| 401 | FOUT 401. De AI-pijpleiding voor leads is gestopt: onvoldoende geldige accounts voor accountscoring. Aantal rekeningen: {}. |
| 402 | FOUT 402. Leidt AI pijpleiding tegengehouden: niet genoeg geldige contacten voor contactscore. Aantal contactpersonen: {}. |
| 403 | FOUT 403. De AI-pijplijn van leads is gestopt: onvoldoende activiteitenvolume voor modeltraining. Aantal gebeurtenissen: {}. |
| 404 | FOUT 404. De AI-pijplijn van leads is gestopt: onvoldoende conversies voor modeltraining. Aantal omzettingen: {}. |
| 405 | FOUT 405. De AI-pijplijn van leads is gestopt: de activiteit is te beperkt voor een geldige modeltraining. Alleen {} percent van rekeningen heeft activiteit. |
| 406 | FOUT 406. De AI-pijplijn van leads is gestopt: de activiteit is te beperkt voor een geldige modeltraining. Alleen {} percent van contacten heeft activiteit. |
| 407 | FOUT 407. De AI-pijplijn van leads is gestopt: de gegevenstypen van de scoring komen niet overeen met de trainingsgegevens. |
| 408 | FOUT 408. AI-pijpleiding gestopt: ontbrekende snelheid is te hoog voor activiteitsfuncties. Ontbrekende frequentie: {}. |
| 409 | FOUT 409. De AI-pijplijn van leads is gestopt: de auc van de test is te laag. Auc testen: {}. |
| 410 | FOUT 410. De AI-pijplijn wordt gestopt: de auc van de test is te laag na het instellen van de parameter. Auc testen: {}. |
| 411 | FOUT 411 De AI-pijplijn van leads is gestopt: de trainingsgegevens hebben onvoldoende conversies om een betrouwbaar model te produceren. conversies: {}. |
| 412 | FOUT 412. AI-pijpleiding gestopt: testgegevens hebben geen conversie om AUC-ROC te berekenen. |

| Waarschuwing/informatiecode | Bericht |
| --- | --- |
| 100 | INFO 100. Leidt AI-kwaliteitscontrole: het aantal rekeningen is: {}. |
| 101 | INFO 101. Leidt AI-kwaliteitscontrole: het aantal contactpersonen is: {}. |
| 102 | INFO 102. Leidt AI-kwaliteitscontrole: het aantal mogelijkheden is: {}. |
| 103 | INFO 103. Leidt de AI-kwaliteitscontrole: de testauc is laag. Start parameterinstelling. Testauc: {}. |
| 200 | Waarschuwing 200. Leidt de AI-kwaliteitscontrole: de ontbrekende snelheid van de firewallfuncties is: {}. |
| 201 | Waarschuwing 201. Leidt AI-kwaliteitscontrole: de ontbrekende activiteitsfuncties zijn: {}. |

## Volgende stappen

Met deze zelfstudie kunt u nu scores maken en beheren. Raadpleeg de volgende documenten voor meer informatie:

* [Voorspelend lood en account scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Voorspelende functies en taken voor accountscoring bewaken](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
