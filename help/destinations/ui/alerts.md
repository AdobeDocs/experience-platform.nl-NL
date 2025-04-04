---
keywords: Experience Platform;home;populaire onderwerpen; waarschuwingen;doelen
description: U kunt op alarm intekenen wanneer het creëren van een gegevensstroom, om waakzame berichten betreffende de status, het succes, of het mislukken van uw stroom te ontvangen in werking stellen.
title: Abonneren op in-context-bestemmingswaarschuwingen
exl-id: 134144a0-cdfe-49a8-bd8b-e36a4f053de5
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 3%

---

# Abonneren op in-context-bestemmingswaarschuwingen

Met Adobe Experience Platform kunt u zich abonneren op waarschuwingen voor gebeurtenissen met betrekking tot Adobe Experience Platform-activiteiten. Het alarm vermindert of elimineert de behoefte om [[!DNL Observability Insights]  API ](../../observability/api/overview.md) te peilen om te controleren als een baan heeft voltooid, als een bepaalde mijlpaal binnen een werkschema is bereikt, of als om het even welke fouten zijn voorgekomen.

U kunt zich op alarm abonneren wanneer het creëren van een gegevensstroom om waakzame berichten betreffende de status, het succes, of het mislukken van uw looppas te ontvangen.

In dit document worden de stappen beschreven voor de manier waarop u zich abonneert op waarschuwingsberichten voor uw doelgegevens.

## Aan de slag

Voor dit document is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

* [ Doelen ](../home.md): Vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.
* [ Observability ](../../observability/home.md): [!DNL Observability Insights] staat u toe om de activiteiten van Experience Platform door het gebruik van statistische metriek en gebeurtenisberichten te controleren.
   * [ Alarm ](../../observability/alerts/overview.md): Wanneer een bepaalde reeks voorwaarden in uw verrichtingen van Experience Platform wordt bereikt (zoals een potentieel probleem wanneer het systeem een drempel) schendt, kan Experience Platform waakzame berichten aan om het even welke gebruikers in uw organisatie leveren die aan hen zijn ingetekend.

## Abonneren op waarschuwingen in de gebruikersinterface {#subscribe-destination-alerts}

>[!CONTEXTUALHELP]
>id="platform_destination_alerts_subscribe"
>title="Abonneren op bestemmingswaarschuwingen"
>abstract="Met waarschuwingen kunt u meldingen ontvangen op basis van de status van uw doelgegevens. U kunt waarschuwingsberichten instellen om updates op te halen als uw gegevensstroom is gestart, is gelukt, is mislukt of geen gegevens naar uw bestemming heeft verzonden."
>text="Learn more in documentation"

>[!IMPORTANT]
>
>U moet directe meldingen van e-mails voor uw Experience Platform-account inschakelen om e-mailmeldingen voor uw gegevensstromen te ontvangen.

U kunt alarm voor uw gegevensstromen tijdens de [!UICONTROL Configure new destination] stap van het [ werkschema van de bestemmingsverbinding ](connect-destination.md) toelaten.

![ beeld UI die de sectie van het bestemmingsalarm toont.](../assets/ui/alerts/destination-alerts.png)

Selecteer de waarschuwingen waarop u zich wilt abonneren en selecteer vervolgens **[!UICONTROL Next]** om uw gegevensstroom te bekijken en af te ronden.

De waarschuwingen die beschikbaar zijn voor bestemmingsgegevensstromen worden beschreven in de onderstaande tabel.

* Voor streamingdoelen is alleen de waarschuwing [!DNL Activation Skipped Rate Exceeded] beschikbaar.
* Voor op een bestand gebaseerde doelen zijn alle waarschuwingen beschikbaar.

| Waarschuwingen | Beschrijving |
| --- | --- |
| Vertraging bij uitvoering bestemmingsworkflow | Deze waarschuwing geeft een melding wanneer een doelstroom langer dan 150 minuten duurt om een publiek te activeren. |
| Uitvoerfout bestemming | Deze waarschuwing brengt u op de hoogte wanneer een fout voorkomt terwijl het activeren van een publiek aan een bestemming. |
| Uitvoersucces bestemming | Deze waarschuwing brengt u op de hoogte wanneer een publiek met succes aan een bestemming wordt geactiveerd. |
| Start stroom bestemming | Deze waarschuwing brengt u op de hoogte wanneer een looppas van de bestemmingsstroom begint een publiek te activeren. |
| Overgeslagen activeringssnelheid overschreden | Deze waarschuwing geeft een melding wanneer de activeringsfrequentie hoger is dan 1% van de totale activeringen. De identiteiten worden overgeslagen tijdens activering wanneer ze ontbrekende kenmerken of een schending van de toestemming hebben. |

## Ontvangen van waarschuwingen {#receiving-alerts}

Zodra uw doelgegevensstroom loopt, kunt u alarm door UI of door e-mail ontvangen.

### Waarschuwingen ontvangen in de gebruikersinterface {#receiving-alerts-in-ui}

Waarschuwingen worden in de gebruikersinterface vertegenwoordigd door een berichtpictogram in de bovenste koptekst van de gebruikersinterface van Experience Platform. Selecteer het berichtpictogram om specifieke waakzame berichten betreffende uw gegevens te zien.

![ beeld UI die het berichtpictogram in Experience Platform toont ](../assets/ui/alerts/notification.png)

Het deelvenster met meldingen wordt weergegeven met een lijst met statusupdates in de gegevensstroom die u hebt gemaakt.

![ beeld UI die het kennisgevingspaneel ](../assets/ui/alerts/alert-window.png) tonen

U kunt de muisaanwijzer op een waarschuwingsbericht plaatsen om deze als gelezen te markeren of u kunt het klokpictogram selecteren om toekomstige herinneringen op de status van uw gegevensstroom in te stellen.

![ beeld UI die de opties van de berichtherinnering tonen ](../assets/ui/alerts/remind-me.png)

Selecteer het waakzame bericht om specifieke informatie op uw gegevensstroom te zien.

![ beeld UI die tonen hoe te om een bericht ](../assets/ui/alerts/select-alert-message.png) te selecteren

De pagina [!UICONTROL Dataflow run details] wordt weergegeven. In de bovenste helft van het scherm wordt een overzicht van uw gegevensstroom weergegeven, inclusief informatie over de kenmerken, de bijbehorende id voor de uitvoering van de gegevensstroom en het overzicht van de fouten op hoog niveau.

![ beeld UI die de dataflow looppas detailpagina toont.](../assets/ui/alerts/dataflow-overview.png)

In de onderste helft van de pagina worden alle [!UICONTROL Dataflow run errors] weergegeven die zijn uitgevoerd tijdens het werkgebied waarin de gegevensstroom is uitgevoerd. Van hier, kunt u foutendiagnostiek voorproef of [[!DNL Data Access]  API ](https://www.adobe.io/experience-platform-apis/references/data-access/) gebruiken om foutendiagnostiek of dossiermanifest te downloaden die aan uw dataflow beantwoordt.

![ beeld UI die de dataflow looppas detailpagina toont, met een hoogtepunt op de foutensectie.](../assets/ui/alerts/dataflow-run-error.png)

Voor meer informatie bij de behandeling van dataflow fouten, zie de gids over [ controlebestemmingen dataflows in UI ](../../dataflows/ui/monitor-destinations.md).

### Waarschuwingen ontvangen per e-mail {#receiving-alerts-by-email}

Waarschuwingen voor uw gegevensstromen worden ook via e-mail aan u verzonden. Selecteer de naam van de gegevensstroom in de hoofdtekst van de e-mail om meer informatie over uw gegevensstroom te zien.

![ Schermafbeelding van een waakzame e-mail ](../assets/ui/alerts/email.png)

Net als de UI-waarschuwing wordt de pagina [!UICONTROL Dataflow run overview] weergegeven, die u een interface biedt om eventuele fouten die aan uw gegevensstroom zijn gekoppeld, te onderzoeken.

![ dataflow-overview ](../assets/ui/alerts/dataflow-overview.png)

## Abonneren op waarschuwingen en je abonnement opzeggen {#subscribe-and-unsubscribe}

U kunt zich abonneren op meer waarschuwingen of uw abonnement opzeggen voor bestaande doelgegevensstroom op de pagina [!UICONTROL Browse] met doelen.

![ beeld UI die de Doelen tonen doorbladert pagina ](../assets/ui/alerts/destination-list.png)

Zoek de doelverbinding waarvoor u waarschuwingen wilt ontvangen en selecteer de ellipsen (`...`) om een vervolgkeuzemenu met opties weer te geven. Selecteer vervolgens **[!UICONTROL Subscribe to alerts]** om de waarschuwingsinstellingen van de doelgegevensstroom te wijzigen.

![ beeld UI die de bestemmingsopties tonen ](../assets/ui/alerts/destination-alerts-subscribe.png)

Er wordt een pop-upvenster weergegeven met een lijst met doelwaarschuwingen. Selecteer de waarschuwingen waarvan u zich wilt abonneren of hef de selectie van waarschuwingen op. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ beeld UI die het beeld van het bestemmingsalarm pagina toont van abonnementen ](../assets/ui/alerts/destination-alerts-list.png)

## Volgende stappen {#next-steps}

Dit document verstrekte een geleidelijke gids over hoe te om aan in-context alarm voor uw bestemmingsdataflows in te tekenen. Voor meer informatie, zie het [ alarm UI gids ](../../observability/alerts/ui.md).
