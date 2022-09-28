---
keywords: Experience Platform;thuis;populaire onderwerpen; waarschuwingen
description: U kunt op alarm intekenen wanneer het creëren van een gegevensstroom, om waakzame berichten betreffende de status, het succes, of het mislukken van uw stroom te ontvangen in werking stellen.
title: Abonneren op in-context-waarschuwingen in de gebruikersinterface
exl-id: 5d51edaa-ecba-4ac0-8d3c-49010466b9a5
source-git-commit: d450dc7b0dc0303c9d33c3e8e003659e3140cf5b
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# Abonneren op waarschuwingen voor brongegevens in de gebruikersinterface

Met Adobe Experience Platform kunt u zich abonneren op waarschuwingen voor gebeurtenissen met betrekking tot Adobe Experience Platform-activiteiten. Waarschuwingen verminderen of elimineren de noodzaak om de [[!DNL Observability Insights] API](../../../observability/api/overview.md) om na te gaan of een baan heeft voltooid, of een bepaalde mijlpaal in een werkstroom is bereikt of of er fouten zijn opgetreden.

U kunt zich op alarm abonneren wanneer het creëren van een gegevensstroom om waakzame berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen.

In dit document worden de stappen beschreven voor het ontvangen van berichten met waarschuwingen voor uw brongegevens.

## Aan de slag

Voor dit document is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Waarneming](../../../observability/home.md): [!DNL Observability Insights] kunt u de activiteiten van Platforms volgen door statistische gegevens en gebeurtenismeldingen te gebruiken.
   * [Waarschuwingen](../../../observability/alerts/overview.md): Wanneer een bepaalde reeks voorwaarden in uw verrichtingen van het Platform wordt bereikt (zoals een potentieel probleem wanneer het systeem een drempel) schendt, kan het Platform waakzame berichten aan om het even welke gebruikers in uw organisatie leveren die aan hen hebben ingetekend.

## Abonneren op waarschuwingen in de gebruikersinterface {#subscribe-sources-alerts}

>[!CONTEXTUALHELP]
>id="platform_sources_alerts_subscribe"
>title="Abonneren op waarschuwingen voor bronnen"
>abstract="Met waarschuwingen kunt u meldingen ontvangen op basis van de status van de gegevensstromen van uw bronnen. U kunt waarschuwingsmeldingen instellen om updates op te halen als uw gegevensstroom is gestart, is gelukt, is mislukt of geen gegevens heeft ingevoerd."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>U moet directe meldingen van e-mails voor uw Platform-account inschakelen om e-mailmeldingen voor uw gegevensstromen te ontvangen.

U kunt waarschuwingen inschakelen voor uw gegevensstromen tijdens de [!UICONTROL Dataflow detail] stap van de bronworkflow in de werkruimte Bronnen.

![dataFlow-detail](../../images/tutorials/alerts/dataflow-detail.png)

De beschikbare alarm voor bronnen dataflows zijn:

| Waarschuwingen | Beschrijving |
| --- | --- |
| Bronnen DataAfter Run Start | Deze waarschuwing stuurt u een bericht wanneer uw brongegevensstroom is begonnen. |
| Bronnen DataAfterFlow voltooid | Deze waarschuwing stuurt u een bericht wanneer gegevens van uw bron met succes aan Platform worden opgenomen. |
| Bronnen DataAfterFlow-fout | Deze waarschuwing stuurt u een bericht als er een fout optreedt in uw gegevensstroom. |
| ~~Bronnen Gegevensstroom Gebrek aan Ingestie~~ | ~~Deze waarschuwing stuurt u een bericht als de inname meer dan zeven uur wordt vertraagd en er geen gegevens aan het Platform worden gegeven.~~ <br>**Opmerking:** Je ontvangt geen waarschuwingen meer omdat deze waarschuwing is afgekeurd. |

Selecteer de waarschuwingen waarop u zich wilt abonneren en selecteer **[!UICONTROL Next]** om uw gegevensstroom te bekijken en te voltooien.

![waarschuwingen selecteren](../../images/tutorials/alerts/select-alerts.png)

Zie de volgende handleidingen voor gedetailleerde stappen bij het maken van een gegevensstroom voor bronnen in de gebruikersinterface:

* [Reclame](./dataflow/advertising.md)
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

Waarschuwingen worden in de gebruikersinterface vertegenwoordigd door een meldingspictogram in de bovenste koptekst van de gebruikersinterface van het Platform. Selecteer het berichtpictogram om specifieke waakzame berichten betreffende uw gegevens te zien.

![melding](../../images/tutorials/alerts/notification.png)

Het deelvenster met meldingen wordt weergegeven met een lijst met statusupdates in de gegevensstroom die u hebt gemaakt.

![waakzaam venster](../../images/tutorials/alerts/alert-window.png)

U kunt de muisaanwijzer op een waarschuwingsbericht plaatsen om deze als gelezen te markeren of u kunt het klokpictogram selecteren om toekomstige herinneringen op de status van uw gegevensstroom in te stellen.

![herinnering](../../images/tutorials/alerts/remind-me.png)

Selecteer het waakzame bericht om specifieke informatie op uw gegevensstroom te zien.

![select-alert-message](../../images/tutorials/alerts/select-alert-message.png)

De [!UICONTROL Dataflow run overview] wordt weergegeven. In de bovenste helft van het scherm wordt een overzicht van uw gegevensstroom weergegeven, inclusief informatie over de kenmerken, de bijbehorende id voor de uitvoering van de gegevensstroom en het overzicht van de fouten op hoog niveau.

![dataFlow-overzicht](../../images/tutorials/alerts/dataflow-overview.png)

In de onderste helft van de pagina worden alle [!UICONTROL Dataflow run errors] die zijn uitgevoerd tijdens het werkgebied voor gegevensstroom. Hier kunt u een voorvertoning van de foutdiagnostiek bekijken of de [[!DNL Data Access] API](https://www.adobe.io/experience-platform-apis/references/data-access/) om foutdiagnostiek te downloaden of het bestandmanifest die overeenkomt met uw gegevensstroom.

![dataflow-run-fouten](../../images/tutorials/alerts/dataflow-run-error.png)

Zie de handleiding voor meer informatie over het verwerken van dataflow-fouten [gegevens van bronnen controleren in de UI](../../../dataflows/ui/monitor-sources.md).

### Per e-mail

Waarschuwingen voor uw gegevensstromen worden ook via e-mail aan u verzonden. Selecteer de naam van de gegevensstroom in de hoofdtekst van de e-mail om meer informatie over uw gegevensstroom te zien.

![email](../../images/tutorials/alerts/email.png)

Net als de gebruikersinterface-waarschuwing worden de [!UICONTROL Dataflow run overview] wordt weergegeven, zodat u een interface hebt waarmee u eventuele fouten kunt onderzoeken die aan uw gegevensstroom zijn gekoppeld.

![dataFlow-overzicht](../../images/tutorials/alerts/dataflow-overview.png)

## Abonneren op waarschuwingen en je abonnement opzeggen

U kunt zich abonneren op meer waarschuwingen of uw abonnement opzeggen voor bestaande waarschuwingen in de [!UICONTROL Dataflows] pagina. Zoek de gegevensstroom die u maakt in de lijst en selecteer vervolgens de ovalen (`...`) om een vervolgkeuzemenu met opties weer te geven. Selecteer vervolgens **[!UICONTROL Subscribe alerts]** om de waakzame montages van uw gegevensstroom te wijzigen.

![opties](../../images/tutorials/alerts/options.png)

Er wordt een pop-upvenster weergegeven met een lijst met waarschuwingen voor bronnen. Selecteer de waarschuwingen waarvan u zich wilt abonneren of hef de selectie van waarschuwingen op. Als u klaar bent, selecteert u **[!UICONTROL Save]**.

![opslaan](../../images/tutorials/alerts/save.png)

## Volgende stappen

Dit document verstrekte een geleidelijke gids over hoe te om aan in-context alarm voor uw brongegevens in te tekenen. Zie voor meer informatie de [UI-hulplijn voor waarschuwingen](../../../observability/alerts/ui.md).