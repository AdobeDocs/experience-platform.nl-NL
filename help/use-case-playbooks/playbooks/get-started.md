---
solution: Experience Platform
title: Ga aan de slag met Hoofdletters gebruiken
description: Leer hoe u aan de slag gaat met de functie Hoofdletters gebruiken.
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 0%

---


# Aan de slag

Leer hoe u uw account instelt voor Use Case Playbooks, die zijn ontworpen voor Real-time Customer Data Platform en Adobe Journey Optimizer als dit niet automatisch is ingesteld. De drie belangrijkste configuratiestappen zijn:

* Een sandbox maken
* Gebruikersmachtigingen configureren
* Journey Optimizer-kanaaloppervlakken configureren voor e-mail-, push- en SMS-berichten (als u Journey Optimizer-afspeelboeken wilt gebruiken)

## Configureer Use Case Playbooks - Video Walthrough {#video}

Bekijk deze video voor meer informatie over de stappen die nodig zijn om uw sandbox te maken, machtigingen te configureren en kanaaloppervlakken te configureren voor e-mail-, push- en SMS-berichten in Journey Optimizer.

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## Een ontwikkelingssandbox maken {#create-development-sandbox}

In Use Case Playbooks is een speciaal type ontwikkelingssandbox gebruikt. Om begonnen te worden en toegang tot de [[!UICONTROL Use Case Playbooks]](/help/use-case-playbooks/playbooks/overview.md) functionaliteit te krijgen, [ creeer een nieuwe ontwikkelingszandbak ](/help/sandboxes/ui/user-guide.md#create) (zorg ervoor u geen productiesandbox) met de naam (niet de titel) die of `-ucp` of `-UCP` in het achtervoegsel, zoals hieronder getoond bevat.

>[!IMPORTANT]
>
>Wanneer u een nieuwe ontwikkelingssandbox maakt, moet u ervoor zorgen dat de naam `-ucp` of `-UCP` bevat in het achtervoegsel.


![ creeer een ontwikkelingszandbak voor gebruikscase playbooks ](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

U moet nu [!UICONTROL Playbooks] in de linkerrail onder [!UICONTROL Use Case Playbooks] zien.

![ Playbooks van het Geval van het Gebruik in UI na het creëren van zandbak.](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

Als u [!UICONTROL Playbooks] niet ziet in de linkertrack, zoals hierboven is weergegeven, gebruikt u deze koppeling `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` om er rechtstreeks naartoe te navigeren. In de koppeling is `<YOUR_ORG>` de naam van uw organisatie en is `<YOUR_SANDBOX_NAME>` de naam van de ontwikkelingssandbox die u hebt gemaakt.

## Geef uw team de vereiste toegangsrechten {#grant-access-permissions}

Om met [!UICONTROL Use Case Playbooks] te beginnen, hebben de leden van uw marketing team de juiste toestemmingen nodig zodat zij de lijst van gecreeerde playbooks kunnen bekijken of playbooks zelf tot stand brengen.

**Vereiste toestemmingen**

Om de vereiste toestemmingen, in de Toestemmingen UI toe te voegen, omvat de nieuwe zandbak van het gebruiksgeval playbook in [ rollen die u reeds ](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role) hebt gevormd, met inbegrip van die gebruikt voor andere ontwikkelingszandbakken.

![ zandbak van het Playbook voor rollen reeds gevormd ](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**opstelling een rol voor Playbooks:**

Alternatief, kon u ook overwegen toevoegend nieuwe rollen met [ de vereiste toestemmingen ](/help/access-control/home.md#sandboxes-and-permissions).

[ opstelling een nieuwe rol ](/help/access-control/abac/ui/permissions.md) met de noodzakelijke toestemmingen voor essentiële playbook taken. Maak een rol en voeg de nieuwe sandbox eraan toe, zoals hieronder wordt weergegeven.

![ creeer een rol en voeg het aan Sandbox ](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png) toe

**Toestemmingen voor playbook instanties**

Als onderdeel van Use Case Playbooks, zult u diverse activa zoals schema&#39;s, publiek, bestemmingen, reizen tot stand brengen. U en andere gebruikers hebben de juiste machtigingen nodig om deze objecten te maken.

**Toestemmingen voor schema&#39;s**

Als u schema&#39;s wilt maken en beheren, gebruikt u de machtigingen voor gegevensmodellering; **[!UICONTROL Manage Schemas]**, **[!UICONTROL View Schemas]**, **[!UICONTROL Manage Relationships]**, **[!UICONTROL Manage Identity Metadata]**

**Toestemmingen voor bestemmingen**

Gebruik de machtigingen Doelen om doelen te maken en te beheren. **[!UICONTROL Manage]**, **[!UICONTROL Destinations]**, **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL Manage and Activate Dataset Destination]**, **[!UICONTROL Destination Authoring]** .

**Toestemmingen voor reizen**

Als u ritten wilt maken en beheren, gebruikt u de machtigingen voor reizen; **[!UICONTROL Manage Journeys]**, **[!UICONTROL View Journeys]**, **[!UICONTROL View Journeys Report]**, **[!UICONTROL Manage Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions]**, **[!UICONTROL View Journeys]**, **[!UICONTROL Events]**, **[!UICONTROL Data Sources and Actions, Publish Journeys]**.

In de onderstaande afbeelding ziet u een momentopname van de aanbevolen rechten voor gebruikers om afspeelboeken en de elementen die door afspeelboeken zijn gegenereerd, weer te geven, te maken en te beheren.

![ Momentopname van alle toestemmingspunten nodig om alle instanties van playbooks tot stand te brengen ](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**voeg gebruikers aan de rol** toe

Zodra u [ een nieuwe rol ](/help/access-control/abac/ui/permissions.md#managing-users-for-role) zoals hierboven van verwijzingen voorzien hebt gecreeerd, voeg me als gebruiker aan het toe. Als u een rol met beperkte toegang voor een andere reeks gebruikers met mening-slechts toegang creeert, omvat slechts de noodzakelijke meningspunten verbonden aan deze toestemmingen.

## Sandbox- en kanaaloppervlakken configureren in Journey Optimizer {#configure-channel-surfaces}

Als uw organisatie voor [ Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) vergunning wordt gegeven, en u wilt playbooks gebruiken die voor Journey Optimizer worden ontworpen, zult u het kanaal moeten vormen vooraf instelt in uw zandbak, die de technische parameters bepaalt die voor uw berichten worden vereist. [ Leer hoe te de oppervlakten van het opstellingskanaal in Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html).

Als u instanties van afspeelboeken wilt maken in Journey Optimizer, moet u kanaaloppervlakken configureren voor e-mail-, push- en SMS-berichten.

### Oppervlak e-mailkanaal

Ga naar `Channels` in de Journey Optimizer-interface. Vorm afzonderlijke subdomeinen en IP pools voor marketing e-mail en transactioneel overseinen, als niet reeds gevormd. Dit zijn beste praktijken om ervoor te zorgen dat de transactieberichten zoals de bevestigingse-mail van de orde, door aan uw klanten krijgen. Voer namen, e-mailadressen en aanvullende instellingen in. Selecteer **voorleggen** bij het hoogste recht van de pagina om de oppervlakte van het marketing kanaal tot stand te brengen. Lees de documentatie op [ hoe te opstellings e-mailkanaaloppervlakken ](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### SMS-kanaal

Om een het kanaaloppervlakte van SMS tot stand te brengen, creeer eerst een referentie van SMS API, en selecteer de aangewezen verkoper (bijvoorbeeld, Sinch). Geef het oppervlak van het SMS-kanaal een naam (bijvoorbeeld SMS Marketing), selecteer de configuratie en voer een nummer voor de afzender in. Selecteer **voorleggen** bij het hoogste recht van de pagina om de het kanaaloppervlakte van SMS te bewaren. Lees de documentatie op [ hoe te de het kanaaloppervlakten van opstellingsSMS ](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=en#message-preset-sms).

Configureer ook kanalen voor afspeelboeken die transactieberichten bevatten, zoals orderbevestigingen.

### Push-kanaaloppervlak

Controleer of de toepassingsoppervlakken zijn geconfigureerd via het Experience Platform of de interface Gegevensverzamelingen. Zo zien toepassingsoppervlakken er uit in de gegevensverzamelingsomgeving.

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

Selecteer vervolgens het kanaal, de platforms en de apps die u hebt bekeken in de configuraties van het oppervlak van de app. Selecteer **voorleggen** om de oppervlakte van het drukkanaal tot stand te brengen.

Lees de documentatie op [ hoe te opstellings de oppervlakken van het drukkanaal ](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## Volgende stappen {#next-steps}

Nu u alle stappen in dit document hebt gevolgd, had u een ontwikkelingssandbox moeten maken met Use Case Playbooks die beschikbaar is in de linkernavigatie. U weet nu ook hoe u uw teamleden de vereiste machtigingen kunt geven om afspeelboeken te bekijken en te beheren en elementen te genereren. Als volgende stap, lees hoe te [ het juiste playbook ](/help/use-case-playbooks/playbooks/choose.md) voor u te kiezen en [ dan tot instanties van het ](/help/use-case-playbooks/playbooks/create-share-reuse.md) leiden.
