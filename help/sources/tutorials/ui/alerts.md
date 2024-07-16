---
keywords: Experience Platform;home;populaire onderwerpen; waarschuwingen
description: U kunt op alarm intekenen wanneer het creëren van een gegevensstroom, om waakzame berichten betreffende de status, het succes, of het mislukken van uw stroom te ontvangen in werking stellen.
title: Abonneren op in-context-waarschuwingen in de gebruikersinterface
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: 9120377f5f2048579d7e2a4740cfcbc56d49d61a
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Abonneren op waarschuwingen voor brongegevens in de gebruikersinterface

>[!NOTE]
>
>Waarschuwingen worden niet ondersteund in niet-productiesandboxen. Als u zich wilt abonneren op waarschuwingen, moet u ervoor zorgen dat u een productiesandbox gebruikt.

Met Adobe Experience Platform kunt u zich abonneren op waarschuwingen voor gebeurtenissen met betrekking tot Adobe Experience Platform-activiteiten. Het alarm vermindert of elimineert de behoefte om [[!DNL Observability Insights]  API ](../../../observability/api/overview.md) te peilen om te controleren als een baan heeft voltooid, als een bepaalde mijlpaal binnen een werkschema is bereikt, of als om het even welke fouten zijn voorgekomen.

U kunt zich op alarm abonneren wanneer het creëren van een gegevensstroom om waakzame berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen.

In dit document worden de stappen beschreven voor het ontvangen van berichten met waarschuwingen voor uw brongegevens.

## Aan de slag

Voor dit document is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [ Bronnen ](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [ Observability ](../../../observability/home.md): [!DNL Observability Insights] staat u toe om de activiteiten van het Platform door het gebruik van statistische metriek en gebeurtenisberichten te controleren.
   * [ Alarm ](../../../observability/alerts/overview.md): Wanneer een bepaalde reeks voorwaarden in uw verrichtingen van het Platform wordt bereikt (zoals een potentieel probleem wanneer het systeem een drempel) schendt, kan het Platform waakzame berichten aan om het even welke gebruikers in uw organisatie leveren die aan hen hebben ingetekend.

## Abonneren op waarschuwingen in de gebruikersinterface {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Abonneren op waarschuwingen voor bronnen"
>abstract="Met waarschuwingen kunt u meldingen ontvangen op basis van de status van de gegevensstromen van uw bronnen. U kunt waarschuwingsmeldingen instellen om updates op te halen als uw gegevensstroom is gestart, is gelukt, is mislukt of geen gegevens heeft ingevoerd."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>U moet directe meldingen van e-mails voor uw Platform-account inschakelen om e-mailmeldingen voor uw gegevensstromen te ontvangen.

U kunt waarschuwingen voor uw gegevensstromen tijdens de [!UICONTROL Dataflow detail] stap van de bronwerkstroom in de bronwerkruimte inschakelen.

![ dataflow-detail ](../../images/tutorials/alerts/dataflow-detail.png)

De beschikbare alarm voor bronnen dataflows zijn:

>[!NOTE]
>
>Streaming bronnen worden momenteel niet ondersteund door waarschuwingen. U kunt zich alleen abonneren op waarschuwingsmeldingen voor batchbronnen.

| Waarschuwingen | Beschrijving |
| --- | --- |
| Bronnen Start Stroom | Deze waarschuwing stuurt u een bericht wanneer uw brongegevensstroom is begonnen. |
| Resources Flow Run Success | Deze waarschuwing stuurt u een bericht wanneer gegevens van uw bron met succes aan Platform worden opgenomen. |
| Fout bij uitvoeren van bronstroom | Deze waarschuwing stuurt u een bericht als er een fout optreedt in uw gegevensstroom. |

Selecteer de waarschuwingen waarop u zich wilt abonneren en selecteer vervolgens **[!UICONTROL Next]** om uw gegevensstroom te bekijken en af te ronden.

![ selecteren-alarm ](../../images/tutorials/alerts/select-alerts.png)

Zie de volgende handleidingen voor gedetailleerde stappen bij het maken van een gegevensstroom voor bronnen in de gebruikersinterface:

* [Advertising](./dataflow/advertising.md)
* [Cloud-opslag](./dataflow/batch/cloud-storage.md)
* [CRM](./dataflow/crm.md)
* [Database](./dataflow/databases.md)
* [E-handel](./dataflow/ecommerce.md)
* [Lokale bestanden](./create/local-system/local-file-upload.md)
* [Marketing automatiseren](./dataflow/marketing-automation.md)
* [Betalingen](./dataflow/payments.md)
* [Protocollen](./dataflow/protocols.md)

## Waarschuwingen ontvangen

Zodra uw gegevensstroom loopt, kunt u alarm door UI of door e-mail ontvangen.

### In de gebruikersinterface

Alarm wordt vertegenwoordigd in UI door een berichtpictogram in de hoogste kopbal van het Platform UI. Selecteer het berichtpictogram om specifieke waakzame berichten betreffende uw gegevens te zien.

![ bericht ](../../images/tutorials/alerts/notification.png)

Het deelvenster met meldingen wordt weergegeven met een lijst met statusupdates in de gegevensstroom die u hebt gemaakt.

![ alarm-venster ](../../images/tutorials/alerts/alert-window.png)

U kunt de muisaanwijzer op een waarschuwingsbericht plaatsen om deze als gelezen te markeren of u kunt het klokpictogram selecteren om toekomstige herinneringen op de status van uw gegevensstroom in te stellen.

![ herinnering-me ](../../images/tutorials/alerts/remind-me.png)

Selecteer het waakzame bericht om specifieke informatie op uw gegevensstroom te zien.

![ selecteren-waakzaam-bericht ](../../images/tutorials/alerts/select-alert-message.png)

De pagina [!UICONTROL Dataflow run overview] wordt weergegeven. In de bovenste helft van het scherm wordt een overzicht van uw gegevensstroom weergegeven, inclusief informatie over de kenmerken, de bijbehorende id voor de uitvoering van de gegevensstroom en het overzicht van de fouten op hoog niveau.

![ dataflow-overview ](../../images/tutorials/alerts/dataflow-overview.png)

In de onderste helft van de pagina worden alle [!UICONTROL Dataflow run errors] weergegeven die zijn uitgevoerd tijdens het werkgebied waarin de gegevensstroom is uitgevoerd. Van hier, kunt u foutendiagnostiek voorproef of [[!DNL Data Access]  API ](https://www.adobe.io/experience-platform-apis/references/data-access/) gebruiken om foutendiagnostiek of dossiermanifest te downloaden die aan uw dataflow beantwoordt.

![ dataflow-run-errors ](../../images/tutorials/alerts/dataflow-run-error.png)

Voor meer informatie bij de behandeling van dataflow fouten, zie de gids over [ controlemiddelen dataflows in UI ](../../../dataflows/ui/monitor-sources.md).

### Per e-mail

Waarschuwingen voor uw gegevensstromen worden ook via e-mail aan u verzonden. Selecteer de naam van de gegevensstroom in de hoofdtekst van de e-mail om meer informatie over uw gegevensstroom te zien.

![ e-mail ](../../images/tutorials/alerts/email.png)

Net als de UI-waarschuwing wordt de pagina [!UICONTROL Dataflow run overview] weergegeven, die u een interface biedt om eventuele fouten die aan uw gegevensstroom zijn gekoppeld, te onderzoeken.

![ dataflow-overview ](../../images/tutorials/alerts/dataflow-overview.png)

## Abonneren op waarschuwingen en je abonnement opzeggen

U kunt zich abonneren op meer waarschuwingen of uw abonnement op bestaande waarschuwingen opzeggen voor een bestaande gegevensstroom op de pagina [!UICONTROL Dataflows] . Zoek de gegevensstroom die u maakt in de lijst en selecteer vervolgens de ovalen (`...`) om een vervolgkeuzemenu met opties weer te geven. Selecteer vervolgens **[!UICONTROL Subscribe alerts]** om de waarschuwingsinstellingen van uw gegevensstroom te wijzigen.

![ opties ](../../images/tutorials/alerts/options.png)

Er wordt een pop-upvenster weergegeven met een lijst met waarschuwingen voor bronnen. Selecteer de waarschuwingen waarvan u zich wilt abonneren of hef de selectie van waarschuwingen op. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ sparen ](../../images/tutorials/alerts/save.png)

## Volgende stappen

Dit document verstrekte een geleidelijke gids over hoe te om aan in-context alarm voor uw brongegevens in te tekenen. Voor meer informatie, zie het [ alarm UI gids ](../../../observability/alerts/ui.md).