---
solution: Experience Platform
title: Afspeelboeken ontdekken
description: Leer hoe u een galerie met afspeelboeken ontdekt en aan de slag gaat met een inspirerende sandbox.
role: User
source-git-commit: ad3f746580f85e77cba390208d147b35b6854e10
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Afspeelboeken ontdekken

Afspeelboeken met hoofdletters en kleine letters zijn zonder extra kosten beschikbaar voor alle Adobe Experience Platform-klanten. Om tot een rijke galerij van gebruiksgeval te toegang te hebben playbooks in Experience Platform UI, selecteer **[!UICONTROL Playbooks]** in de linkernavigatie.

![Galerie met afspeelboeken gebruiken.](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![Directe toegang tot het gebruik van afspeelboeken met hoofdletters en kleine letters op de linkernavigatiebalk.](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

Selecteer een afspeelboek om naar de detailpagina te gaan en selecteer **[!UICONTROL Go to an inspirational sandbox]**. Er wordt een bevestigingsmodaal weergegeven. Selecteren **Bevestigen** om naar de inspirerende zandbak te gaan waar u met de verschillende gebruiksgevallen kunt onderzoeken en experimenteren.

Als u geen machtiging hebt om sandboxen te maken, neemt u contact op met uw beheerder voor hulp bij het maken van een inspirerende sandbox.

>[!TIP]
>
>Een inspirerende sandbox is een ontwikkelingssandbox in Adobe Experience Platform waar u verschillende gebruiksgevallen kunt maken, testen en experimenteren voordat u deze implementeert in een live productieomgeving.

![Ga naar inspirerende sandbox.](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

Als u nog geen inspirerende sandboxes hebt ingesteld, selecteert u **[!UICONTROL Create an inspirational Sandbox]**. Er wordt een modaal weergegeven. Voer de **Naam** en **Titel** in de vereiste vakjes en selecteer **Maken**. Wanneer u de inspirerende sandbox hebt gemaakt, moet u ervoor zorgen dat [machtigingen definiëren](/help/access-control/home.md) voordat u teruggaat naar de pagina met details over afspeelboeken gebruiken om een instantie te maken.

![Maak een inspirerende sandbox.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![Voer een naam en titel in om een inspirerende sandbox te maken.](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

Als u een afspeelboek met een gebruikscase selecteert van buiten een inspirerende sandbox, kunt u geen instantie maken. Selecteer op de pagina Details de optie **Naar inspirerende sandbox** om naar een bestaande inspirerende sandbox te gaan en vervolgens **[!UICONTROL Create instance]**.

Als u geen machtiging hebt om sandboxen te maken, neemt u contact op met uw beheerder voor hulp bij het maken van een inspirerende sandbox.

![Geen machtigingen om sandbox te maken.](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

Als u de limiet voor het aantal sandboxen hebt bereikt dat aan u is toegewezen, verschijnt er een bericht waarin u wordt gevraagd contact op te nemen met uw systeembeheerder om de limiet te verhogen of actieve sandboxen te deactiveren of te verwijderen. Nadat de sandboxlimiet is aangepast of het aantal actieve sandboxen is verminderd, kunt u doorgaan met het maken van de inspirerende sandbox.

![Sandboxlimiet bereikt.](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

Wanneer u een inspirerende sandbox maakt, worden kanaaloppervlakken voor e-mail-, push- en SMS-berichten niet automatisch ingesteld. Neem contact op met uw IT-beheerder om deze handmatig te configureren of het maken van de instantie kan mislukken.

![Kanaalvoorinstellingen configureren.](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## Sandbox- en kanaaloppervlakken configureren in Journey Optimizer {#configure-channel-surfaces}

Als uw organisatie een licentie heeft voor [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)En u wilt de voor Journey Optimizer ontworpen afspeelboeken gebruiken, dan moet u de kanaalvoorinstellingen in uw sandbox configureren, die de technische parameters definiëren die vereist zijn voor uw berichten. [Leer hoe u kanaaloppervlakken instelt in Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Als u instanties van afspeelboeken wilt maken in Journey Optimizer, moet u kanaaloppervlakken configureren voor e-mail-, push- en SMS-berichten.

### Oppervlak e-mailkanaal

Ga naar `Channels` in de Journey Optimizer-interface. Vorm afzonderlijke subdomeinen en IP pools voor marketing e-mail en transactioneel overseinen, als niet reeds gevormd. Dit zijn beste praktijken om ervoor te zorgen dat de transactieberichten zoals de bevestigingse-mail van de orde, door aan uw klanten krijgen. Voer namen, e-mailadressen en aanvullende instellingen in. Selecteren **Verzenden** rechtsboven op de pagina om het oppervlak van het marketingkanaal te maken. Lees de documentatie op [hoe u de oppervlakken van e-mailkanalen instelt](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-kanaal

Om een het kanaaloppervlakte van SMS tot stand te brengen, creeer eerst een referentie van SMS API, en selecteer de aangewezen verkoper (bijvoorbeeld, Sinch). Geef het oppervlak van het SMS-kanaal een naam (bijvoorbeeld SMS Marketing), selecteer de configuratie en voer een nummer voor de afzender in. Selecteren **Verzenden** rechts boven aan de pagina om het oppervlak van het SMS-kanaal op te slaan. Lees de documentatie op [hoe u de oppervlakken van SMS-kanalen instelt](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=en#message-preset-sms).

Configureer ook kanalen voor afspeelboeken die transactieberichten bevatten, zoals orderbevestigingen.

### Push-kanaaloppervlak

Controleer of de toepassingsoppervlakken zijn geconfigureerd via het Experience Platform of de interface Gegevensverzamelingen. Zo zien toepassingsoppervlakken er uit in de gegevensverzamelingsomgeving.

## Volgende stappen {#next-steps}

Nu u dit document hebt gelezen, zou u moeten weten hoe te opstelling een inspirerende zandbak en vertrouwd met verschillende manieren om tot gebruikscaseplaybooks binnen Platform toegang te hebben. Lees als volgende stap hoe u [zoeken](/help/use-case-playbooks/playbooks/find.md) het juiste afspeelboek.

