---
solution: Experience Platform
title: Ga aan de slag met Hoofdletters gebruiken
description: Leer hoe u aan de slag gaat met de functie Hoofdletters gebruiken.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: fe87b8cdeaca5e4e852a8819534f4a5c4023ca52
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---


# Aan de slag

Leer hoe u uw account instelt voor Use Case Playbooks, speciaal ontworpen voor Real-time Customer Data Platform en Adobe Journey Optimizer. De drie belangrijkste configuratiestappen zijn:

* Een sandbox maken
* Gebruikersmachtigingen configureren
* Journey Optimizer-kanaaloppervlakken configureren voor e-mail-, push- en SMS-berichten (als u Journey Optimizer-afspeelboeken wilt gebruiken)

## Configureer Use Case Playbooks - Video Walthrough {#video}

Bekijk deze video voor meer informatie over de stappen die nodig zijn om uw sandbox te maken, machtigingen te configureren en kanaaloppervlakken te configureren voor e-mail-, push- en SMS-berichten in Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Een ontwikkelingssandbox maken {#create-development-sandbox}

In Use Case Playbooks is een speciaal type ontwikkelingssandbox gebruikt. Om aan de slag te gaan en toegang te krijgen tot [[!UICONTROL Use Case Playbooks]](/help/use-case-playbooks/playbooks/overview.md) functionaliteit, [een nieuwe ontwikkelingssandbox maken](/help/sandboxes/ui/user-guide.md#create) (zorg ervoor dat u geen productiesandbox selecteert) met de naam (niet de titel) die of `-ucp` of `-UCP` in het achtervoegsel, zoals hieronder getoond.

>[!IMPORTANT]
>
>Wanneer u een nieuwe ontwikkelingssandbox maakt, moet u ervoor zorgen dat de naam `-ucp` of `-UCP` in het achtervoegsel.


![Een ontwikkelingssandbox maken voor gebruik van afspeelboeken met hoofdletters en kleine letters](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

U moet nu [!UICONTROL Playbooks] in het linkerspoor onder [!UICONTROL Use Case Playbooks].

![Gebruik Hoofdletters en kleine letters in de gebruikersinterface nadat u een sandbox hebt gemaakt.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Als u niet ziet [!UICONTROL Playbooks] in het linker spoor zoals hierboven getoond, gebruik deze verbinding `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` om daar direct te navigeren. Op de koppeling `<YOUR_ORG>` is de naam van uw organisatie en `<YOUR_SANDBOX_NAME>` Dit is de naam van de ontwikkelingssandbox die u hebt gemaakt.

## Geef uw team de vereiste toegangsrechten {#grant-access-permissions}

Aan de slag met [!UICONTROL Use Case Playbooks]hebben leden van uw marketingteam de juiste machtigingen nodig, zodat zij de lijst met gemaakte afspeelboeken kunnen bekijken of zelf afspeelboeken kunnen maken.

**Vereiste machtigingen**

Als u de vereiste machtigingen wilt toevoegen, neemt u in de interface voor machtigingen de nieuwe afspeelgoedsandbox met gebruikscase op in [rollen die u reeds hebt gevormd](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role), met inbegrip van die welke worden gebruikt voor andere ontwikkelingssandboxen.

![Sandbox voor afspelen van rollen die al zijn geconfigureerd](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**Een rol instellen voor afspeelboeken:**

U kunt ook overwegen nieuwe rollen toe te voegen met [de vereiste machtigingen](/help/access-control/home.md#sandboxes-and-permissions).

[Een nieuwe rol instellen](/help/access-control/abac/ui/permissions.md) met de benodigde machtigingen voor essentiële taken voor de afspeelboeken. Maak een rol en voeg de nieuwe sandbox eraan toe, zoals hieronder wordt weergegeven.

![Een rol maken en toevoegen aan de sandbox](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Machtigingen voor afspeelboekinstanties**

Als onderdeel van Use Case Playbooks, zult u diverse activa zoals schema&#39;s, publiek, bestemmingen, reizen tot stand brengen. U en andere gebruikers hebben de juiste machtigingen nodig om deze objecten te maken.

**Machtigingen voor schema&#39;s**

Om schema&#39;s tot stand te brengen en te beheren, gebruik de gegevens modelleringstoestemmingen; **[!UICONTROL Manage Schemas]**, **[!UICONTROL View Schemas]**, **[!UICONTROL Manage Relationships]**, **[!UICONTROL Manage Identity Metadata]**

**Machtigingen voor bestemmingen**

Om bestemmingen tot stand te brengen en te leiden, gebruik de toestemmingen van Doelen; **[!UICONTROL Manage]**, **[!UICONTROL Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL Manage and Activate Dataset Destination]**, **[!UICONTROL Destination Authoring]**.

**Vergunningen voor reizen**

Voor het maken en beheren van reizen gebruikt u de Reismachtigingen. **[!UICONTROL Manage Journeys]**, **[!UICONTROL View Journeys]**, **[!UICONTROL View Journeys Report]**, **[!UICONTROL Manage Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions]**, **[!UICONTROL View Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions, Publish Journeys]**.

In de onderstaande afbeelding ziet u een momentopname van de aanbevolen rechten voor gebruikers om afspeelboeken en de elementen die door afspeelboeken zijn gegenereerd, weer te geven, te maken en te beheren.

![Momentopname van alle machtigingsitems die nodig zijn om alle instanties van de afspeelboeken te maken](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**Gebruikers aan de rol toevoegen**

Eenmaal [een nieuwe rol gecreëerd](/help/access-control/abac/ui/permissions.md#managing-users-for-role) zoals hierboven vermeld, voeg uzelf toe als gebruiker. Als u een rol met beperkte toegang voor een andere reeks gebruikers met mening-slechts toegang creeert, omvat slechts de noodzakelijke meningspunten verbonden aan deze toestemmingen.

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

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Selecteer vervolgens het kanaal, de platforms en de apps die u hebt bekeken in de configuraties van het oppervlak van de app. Selecteren **Verzenden** om het oppervlak van het drukkanaal te maken.

Lees de documentatie op [hoe u oppervlakken van drukkanalen instelt](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Volgende stappen {#next-steps}

Nu u alle stappen in dit document hebt gevolgd, had u een ontwikkelingssandbox moeten maken met Use Case Playbooks die beschikbaar is in de linkernavigatie. U weet nu ook hoe u uw teamleden de vereiste machtigingen kunt geven om afspeelboeken te bekijken en te beheren en elementen te genereren. Lees als volgende stap hoe u [de juiste afspeellijst ontdekken](/help/use-case-playbooks/playbooks/discover.md) voor u en dan [hiervan instanties maken](/help/use-case-playbooks/playbooks/create-share-reuse.md).
