---
title: Beheer voorspellende leads en accountscoring in Real-Time CDP B2B
type: Documentation
description: Dit document bevat informatie over het beheer van de functie voor het voorspellen van leads en accounts in Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=nl-NL#rtcdp-editions" newtab=true
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 2%

---

# Beheer voorspellende leads en accountscoring in Adobe Real-Time Customer Data Platform, B2B edition

>[!NOTE]
>
>Alleen gebruikers met de machtiging B2B AI beheren kunnen muziekdoelen maken, wijzigen en verwijderen.

Dit leerprogramma begeleidt u door de stappen om scoredoelstellingen van de voorspellende lood en rekening het scoren dienst te beheren. Score-doelen kunnen worden gesteld voor het profiel van een persoon of account

## Een nieuwe score maken

Als u een nieuwe score wilt maken, selecteert u **[!UICONTROL Services]** in het zijpaneel en selecteert u **[!UICONTROL Create score]** .

![&#x200B; plas-new-score &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

Het scherm **[!UICONTROL Basic information]** wordt weergegeven en u wordt gevraagd een profieltype te selecteren, een naam en een optionele beschrijving in te voeren. Selecteer **[!UICONTROL Next]** als u klaar bent.

![&#x200B; plas-enter-basis-informatie &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

Het scherm **[!UICONTROL Define your goal]** wordt weergegeven. Selecteer de vervolgkeuzepijl en selecteer vervolgens een doeltype in het vervolgkeuzevenster dat wordt weergegeven.

![&#x200B; plas-selecteren-a-doel &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

Het dialoogvenster **[!UICONTROL Goal specifics]** wordt geopend. Selecteer de vervolgkeuzepijl en selecteer vervolgens de naam van het doelveld in het vervolgkeuzevenster dat wordt weergegeven.

![&#x200B; plas-uitgezochte-a-doel-gebied-naam &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

De selectie van **[!UICONTROL Goal conditions]** wordt weergegeven. Selecteer de vervolgkeuzepijl en selecteer vervolgens de voorwaarde in het vervolgkeuzevenster dat wordt weergegeven.

![&#x200B; plas-doel-specificatie-voorwaarde &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

Het veld **[!UICONTROL Goal value]** wordt weergegeven. Configureer vervolgens de [!UICONTROL Goal specifics] . Selecteer het deelvenster [!UICONTROL Enter Field Value] en voer de waarde van uw doel in.

>[!NOTE]
>
>U kunt meerdere doelwaarden toevoegen.

![&#x200B; plas-doel-specifiek-gebied-waarde &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Selecteer **[!UICONTROL Add field]** als u aanvullende velden wilt toevoegen.

![&#x200B; plas-doel-specifiek-toe:voegen-gebeurtenis &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Selecteer de vervolgkeuzepijl en selecteer vervolgens het gewenste tijdframe om de voorspelling te configureren.

![&#x200B; plas-voorspelling-timeframe &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

Het geselecteerde samenvoegbeleid bepaalt hoe de veldwaarden van een personenprofiel worden geselecteerd. Selecteer met de vervolgkeuzepijl het gewenste samenvoegbeleid en selecteer vervolgens **[!UICONTROL Finish]** .

Het dialoogvenster **[!UICONTROL Scoring setup is complete]** wordt weergegeven met de bevestiging dat de nieuwe score is gemaakt. Selecteer **[!UICONTROL OK]**.

![&#x200B; plas-score-volledige &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Het kan tot 24 uur duren voor elk scoringsproces wordt voltooid.

U keert terug naar het tabblad **[!UICONTROL Services]** waar u de nieuwe score kunt zien die is gemaakt in de lijst met scores.

![&#x200B; plas-score-gecreeerde &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Selecteer de score om details en aanvullende informatie over de details van de laatste uitvoering weer te geven.

![&#x200B; plas-score-extra-informatie &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Voor meer gedetailleerde informatie over de foutencodes die onder de laatste looppasdetails kunnen worden gezien, gelieve naar de sectie op [&#x200B; te verwijzen leidt AI de codes van de pijpleidingsfout &#x200B;](#leads-ai-pipeline-error-codes) in dit document.

## Een score bewerken

Als u een score wilt bewerken, selecteert u een score op de tab **[!UICONTROL Services]** en selecteert u **[!UICONTROL Edit]** in het deelvenster Extra details aan de rechterkant van het scherm.

![&#x200B; plas-geef-score &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png) uit

Het dialoogvenster **[!UICONTROL Edit instance]** wordt weergegeven. Hier kunt u de beschrijving van de score bewerken. Breng de gewenste wijzigingen aan en selecteer **[!UICONTROL Save]** .

![&#x200B; plas-geef-sparen &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>De scoreconfiguratie kan niet worden gewijzigd omdat dit modelomscholing en re-scoring teweegbrengt. Het equivalent hiervan is het verwijderen van de score en het maken van een nieuwe score. Als u de configuratie van de score wilt bewerken, moet u deze score klonen of een nieuwe score maken.

U wordt teruggestuurd naar het tabblad **[!UICONTROL Services]** . Selecteer de score om de bijgewerkte beschrijvingsdetails in het extra detailpaneel op de rechterkant van het scherm te bekijken.

## Een score klonen

Als u een score wilt klonen, selecteert u een score op de tab **[!UICONTROL Services]** en selecteert u **[!UICONTROL Clone]** in het deelvenster Extra details aan de rechterkant van het scherm.

![&#x200B; plas-klone-score &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

Het scherm **[!UICONTROL Basic information]** wordt weergegeven. Het profieltype, de naam en de beschrijving worden gekloond op basis van de oorspronkelijke score. Wijzig deze details en selecteer **[!UICONTROL Next]** .

![&#x200B; plas-clone-basic-info &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

Het scherm **[!UICONTROL Define your goal]** wordt weergegeven. Voltooi de doelsectie zoals u zou toen het creëren van een nieuwe score en selecteer **[!UICONTROL Finish]**.

U keert terug naar het tabblad **[!UICONTROL Services]** waar u de zojuist gekloonde score in de lijst kunt zien.

>[!NOTE]
>
>De sectie **[!UICONTROL Define your goal]** wordt niet gekloond op basis van de oorspronkelijke score.

## Muziek verwijderen

Als u een score wilt verwijderen, selecteert u een score op de tab **[!UICONTROL Services]** en selecteert u **[!UICONTROL Delete]** in het deelvenster Extra details aan de rechterkant van het scherm.

![&#x200B; plas-schrapping-score &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

Het bevestigingsvenster van **[!UICONTROL Delete documentation]** wordt weergegeven. Selecteer **[!UICONTROL Delete]**.

![&#x200B; plas-schrapping-score-bevestiging &#x200B;](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>Als u de muziekdefinitie verwijdert, worden ook alle voorspelde scores in het profiel van de persoon of het account verwijderd, maar niet de veldgroep die voor de muziekdefinitie is gemaakt. De veldgroep wordt in het gegevensmodel &#39;wees&#39; gelaten.

U keert terug naar het tabblad **[!UICONTROL Services]** waar u de score niet meer kunt zien in de lijst.

## Voorloopfoutcodes voor AI-pijpleidingen

| Foutcode | Foutbericht |
| --- | --- |
| 401 | FOUT 401. De AI-pijpleiding voor leads is gestopt: onvoldoende geldige accounts voor accountscoring. Aantal accounts: {}. |
| 402 | FOUT 402. Leidt AI pijpleiding tegengehouden: niet genoeg geldige contacten voor contactscore. Aantal contactpersonen: {}. |
| 403 | FOUT 403. De AI-pijplijn van leads is gestopt: onvoldoende activiteitenvolume voor modeltraining. Aantal gebeurtenissen: {}. |
| 404 | FOUT 404. De AI-pijplijn van leads is gestopt: onvoldoende conversies voor modeltraining. Aantal conversies: {}. |
| 405 | FOUT 405. De AI-pijplijn van leads is gestopt: de activiteit is te beperkt voor een geldige modeltraining. Slechts {} procent van de accounts heeft activiteit. |
| 406 | FOUT 406. De AI-pijplijn van leads is gestopt: de activiteit is te beperkt voor een geldige modeltraining. Slechts {} percent van contacten heeft activiteit. |
| 407 | FOUT 407. De AI-pijplijn van leads is gestopt: de gegevenstypen van de scoring komen niet overeen met de trainingsgegevens. |
| 408 | FOUT 408. AI-pijpleiding gestopt: ontbrekende snelheid is te hoog voor activiteitsfuncties. Ontbrekende snelheid: {}. |
| 409 | FOUT 409. De AI-pijplijn van leads is gestopt: de auc van de test is te laag. Testauc: {}. |
| 410 | FOUT 410. De AI-pijplijn wordt gestopt: de auc van de test is te laag na het instellen van de parameter. Testauc: {}. |
| 411 | FOUT 411 De AI-pijplijn van leads is gestopt: de trainingsgegevens hebben onvoldoende conversies om een betrouwbaar model te produceren. Conversies: {}. |
| 412 | FOUT 412. AI-pijpleiding gestopt: testgegevens hebben geen conversie om AUC-ROC te berekenen. |

| Waarschuwing/informatiecode | Bericht |
| --- | --- |
| 100 | INFO 100. Leidt AI-kwaliteitscontrole: het aantal accounts is: {} . |
| 101 | INFO 101. Leidt AI-kwaliteitscontrole: het aantal contactpersonen is: {} . |
| 102 | INFO 102. Leidt AI-kwaliteitscontrole: het aantal kansen is: {} . |
| 103 | INFO 103. Leidt de AI-kwaliteitscontrole: de testauc is laag. Start parameterinstelling. Testauc: {}. |
| 200 | Waarschuwing 200. Leidt AI-kwaliteitscontrole: de ontbrekende snelheid van eerste grafische functies is: {} . |
| 201 | Waarschuwing 201. Leidt AI-kwaliteitscontrole: de ontbrekende activiteitsfuncties zijn: {} . |

## Volgende stappen

Met deze zelfstudie kunt u nu scores maken en beheren. Raadpleeg de volgende documenten voor meer informatie:

* [Voorspelend lood en account scoring](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Voorspelende functies en taken voor accountscoring bewaken](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
