---
solution: Experience Platform
title: Navigeren naar Hoofdletters gebruiken
description: Leer hoe u door een galerie met afspeelboeken kunt navigeren en aan de slag kunt gaan met een inspirerende sandbox.
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: 703c84e61af105bc3933e4750a3cb27df8ac19fe
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# Navigeren naar Hoofdletters gebruiken

Afspeelboeken met hoofdletters en kleine letters zijn zonder extra kosten beschikbaar voor alle Adobe Experience Platform-klanten. Als u een uitgebreide galerie met gebruikscase-afspeelboeken wilt openen in de gebruikersinterface van het Experience Platform, selecteert u **[!UICONTROL Playbooks]** in de linkernavigatie.

![ de galerij van het gebruiks case playbook.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![ Directe toegang om case playbooks in de linkernavigatiebar te gebruiken.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Selecteer een afspeelboek om naar de detailpagina te gaan en selecteer vervolgens **[!UICONTROL Go to an inspirational sandbox]** . Er wordt een bevestigingsmodaal weergegeven. Selecteer **bevestigen** om naar de inspirerende zandbak te gaan waar u met de verschillende gebruiksgevallen kunt onderzoeken en experimenteren.

Als u geen machtiging hebt om sandboxen te maken, neemt u contact op met uw beheerder voor hulp bij het maken van een inspirerende sandbox.

>[!TIP]
>
>Een inspirerende sandbox is een ontwikkelingssandbox in Adobe Experience Platform waar u verschillende gebruiksgevallen kunt maken, testen en experimenteren voordat u deze implementeert in een live productieomgeving.

![ ga naar inspirerende zandbak.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Selecteer **[!UICONTROL Create an inspirational Sandbox]** als u nog geen inspirerende sandboxen hebt ingesteld. Er wordt een modaal weergegeven. Ga de **Naam** in en **Titel** op de vereiste gebiedsvakjes en uitgezocht **creeer**. Zodra u de inspirerende zandbak creeert, zorg ervoor om [ toestemmingen ](/help/access-control/home.md) te bepalen alvorens u terug naar de de detailpagina van de gebruikscase playbooks navigeert om een instantie tot stand te brengen.

![ creeer een inspirerende zandbak.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![ ga naam en titel in om een inspirerende zandbak tot stand te brengen.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Als u een afspeelboek met een gebruikscase selecteert van buiten een inspirerende sandbox, kunt u geen instantie maken. Voor de detailspagina, uitgezochte **ga naar inspirerende zandbak** om naar een bestaande inspirerende zandbak te gaan en dan **[!UICONTROL Create instance]** te selecteren.

Als u geen machtiging hebt om sandboxen te maken, neemt u contact op met uw beheerder voor hulp bij het maken van een inspirerende sandbox.

![ Geen toestemmingen om zandbak tot stand te brengen.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Als u de limiet voor het aantal sandboxen hebt bereikt dat aan u is toegewezen, verschijnt er een bericht waarin u wordt gevraagd contact op te nemen met uw systeembeheerder om de limiet te verhogen of actieve sandboxen te deactiveren of te verwijderen. Nadat de sandboxlimiet is aangepast of het aantal actieve sandboxen is verminderd, kunt u doorgaan met het maken van de inspirerende sandbox.

![ Gevonden grens van Sandbox.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Wanneer u een inspirerende sandbox maakt, worden kanaaloppervlakken voor e-mail-, push- en SMS-berichten niet automatisch ingesteld. Neem contact op met uw IT-beheerder om deze handmatig te configureren of het maken van de instantie kan mislukken.

![ vorm kanaalvoorinstellingen.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Sandbox- en kanaaloppervlakken configureren in Journey Optimizer {#configure-channel-surfaces}

Als uw organisatie voor [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) vergunning wordt gegeven, en u wilt playbooks gebruiken die voor Journey Optimizer worden ontworpen, zult u het kanaal moeten vormen vooraf instelt in uw zandbak, die de technische parameters bepaalt die voor uw berichten worden vereist. [ Leer hoe te de oppervlakten van het opstellingskanaal in Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Als u instanties van afspeelboeken wilt maken in Journey Optimizer, moet u kanaaloppervlakken configureren voor e-mail-, push- en SMS-berichten.

### Oppervlak e-mailkanaal

Ga naar `Channels` in de Journey Optimizer-interface. Vorm afzonderlijke subdomeinen en IP pools voor marketing e-mail en transactioneel overseinen, als niet reeds gevormd. Dit zijn beste praktijken om ervoor te zorgen dat de transactieberichten zoals de bevestigingse-mail van de orde, door aan uw klanten krijgen. Voer namen, e-mailadressen en aanvullende instellingen in. Selecteer **voorleggen** bij het hoogste recht van de pagina om de oppervlakte van het marketing kanaal tot stand te brengen. Lees de documentatie op [ hoe te opstellings e-mailkanaaloppervlakken ](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-kanaal

Om een het kanaaloppervlakte van SMS tot stand te brengen, creeer eerst een referentie van SMS API, en selecteer de aangewezen verkoper (bijvoorbeeld, Sinch). Geef het oppervlak van het SMS-kanaal een naam (bijvoorbeeld SMS Marketing), selecteer de configuratie en voer een nummer voor de afzender in. Selecteer **voorleggen** bij het hoogste recht van de pagina om de het kanaaloppervlakte van SMS te bewaren. Lees de documentatie op [ hoe te de het kanaaloppervlakten van opstellingsSMS ](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=en#message-preset-sms).

Configureer ook kanalen voor afspeelboeken die transactieberichten bevatten, zoals orderbevestigingen.

### Push-kanaaloppervlak

Bevestig dat de kanaalconfiguraties of van het Experience Platform of de interface van de Inzamelingen van Gegevens worden gevormd. Zo zien kanaalconfiguraties er uit in de omgeving van gegevensverzamelingen.

## Volgende stappen {#next-steps}

Nu u dit document hebt gelezen, zou u moeten weten hoe te opstelling een inspirerende zandbak en vertrouwd met verschillende manieren om tot gebruikscaseplaybooks binnen Platform toegang te hebben. Als volgende stap, lees over hoe te [ ](/help/use-case-playbooks/playbooks/choose.md) het juiste playbook kiezen.
