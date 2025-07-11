---
solution: Experience Platform
title: Leer hoe u uw eigen afspeelboeken ontwerpt en deelt met de AI Assistant.
description: Hoe te om uw eigen gebruiksdoosplaybooks te ontwerpen en te delen.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 5cdbc160369a146da3ae8ca39d8c3095887e03b5
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 0%

---


# Auteur en deel uw eigen afspeelboeken (Beta)

Met [!DNL Playbook Authoring Framework], aangedreven door AI Assistant in Adobe Experience Platform, kunt u op efficiënte wijze afspeelboeken maken, beheren en delen in Adobe Experience Platform.

Het kader volgt een driestappenproces:

1. **Meta-gegevens vangen**: De Medewerker van AI van het gebruik of webform om playbook meta-gegevens te vangen.

2. **Technische vereniging**: Voeg specifieke technische activa zoals reizen of publiek aan playbook toe. U behoudt de volledige controle over het maken van een afspeelboek in uw ontwikkelingssandbox en zorgt ervoor dat de bestanden en andere unieke gegevensstructuren op elkaar worden afgestemd.

3. **distributie van het Playbook**: De playbooks van het aandeel over verschillende organisaties. Zo kan het Martech Center of Excellence van ACME in Duitsland een &quot;gouden&quot; toneelboek maken en dit verspreiden onder regionale organisaties in Thailand, Australië, enz. om het gebruik van het geneesmiddel te helpen standaardiseren.

## Een afspeelboek maken

U kunt een afspeelboek op twee manieren maken: met de AI-assistent of handmatig. Lees de volgende secties om te leren hoe u een afspeelboek maakt met AI Assistant.

### Overzicht van afspeelboeken

Ga als volgt te werk om een afspeelboek te maken met de AI-assistent:

Selecteer **[!UICONTROL Playbooks]** in het navigatievenster aan de linkerkant.

![ Platform UI met de optie &quot;Playbooks&quot;die in het linkernavigatievenster wordt benadrukt.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Selecteer **[!UICONTROL New Playbook]**, en selecteer dan **playbook met AI Medewerker** produceren.

![ de interface van de playbook verwezenlijking die &quot;playbook met AI Geselecteerde optie&quot;toont.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Gebruik het snelle gebied om het gebruiksgeval te beschrijven. Bijvoorbeeld:

&quot;Neem ACME-klanten in dienst die door lopende schoenen hebben gebladerd maar de aankoop niet hebben voltooid.&quot;

![ de interface van de playboekverwezenlijking die het webvormgebied benadrukt waar de gebruikers een herinnering kunnen invoeren.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Selecteer **[!UICONTROL Generate]** om de metagegevens voor de afspeelboek te maken.

![ de playbook verwezenlijking interface die &quot;toont produceert&quot;knoop die in het snelle gebied wordt benadrukt.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Als de code eenmaal is gegenereerd, selecteert u **[!UICONTROL Edit]** om de gegenereerde titel, beschrijving en metagegevens naar wens te wijzigen.

![ A produceerde playbook met &quot;geeft&quot;benadrukte knoop uit, toestaand gebruikers om meta-gegevens te wijzigen.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Vul de sectie **[!UICONTROL Playbook detail]** in om ervoor te zorgen dat de gegevensengineers over alle benodigde details beschikken om het geval te gebruiken. Deze velden zijn optioneel, maar helpen u belangrijke informatie vast te leggen, waardoor het makkelijker wordt om de juiste technische componenten te verbinden. Selecteer **[!UICONTROL Edit]** om waarden toe te voegen aan de volgende velden:

* **Industrie**
* **het publiek van het Doel**
* **Marketing kanaal**

![ de sectie van playbook details met &quot;geeft&quot;knoop benadrukt uit zodat u details zoals industrie, doelpubliek, en marketing kanaal kunt toevoegen of wijzigen.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Nadat de metagegevens zijn gegenereerd, selecteert u **[!UICONTROL Edit journey map]** om de stappen in het reisoverzicht naar wens aan te passen.

![ &quot;geef de knoop van het reisoverzicht&quot;uit om de stappen in het reisoverzicht te wijzigen.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![ de interface van de de redacteur van het reiskaart zodat u stappen kunt aanpassen nadat u playbook meta-gegevens vangt.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Ga vervolgens verder met het koppelen van het afspeelboek aan technische elementen. Selecteer **[!UICONTROL Create playbook manually]** als u handmatig een afspeelboek wilt maken.

![ &quot;creeer playbook manueel&quot;optie om playbook van een leeg malplaatje te beginnen.](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Er wordt een lege afspeelboeksjabloon weergegeven. Vul details zoals **Titel** en **Beschrijving** uit. U kunt het reisoverzicht ook bewerken om gebeurtenissen en aanraakpunten toe te voegen als dat nodig is.

## Afspeelboek koppelen aan technische middelen

Ongeacht of u handmatig een afspeelboek maakt of met de AI Assistant, moet u deze aan de vereiste technische elementen koppelen. Navigeer naar het tabblad **[!UICONTROL Technical Assets]** en selecteer het gewenste product. Selecteer **[!UICONTROL Journey Optimizer]** voor dit voorbeeld.

>[!NOTE]
>
> Ondersteuning voor Real-Time CDP wordt in een toekomstige release toegevoegd.

![ het &quot;Technische Assets&quot;lusje met de &quot;Add vereiste benadrukte productknoop&quot;die u kunt gebruiken om technische activa met playbook te associëren.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Kies **[!UICONTROL Select an Asset]** om dit afspeelboek te koppelen aan een reis zoals in de onderstaande afbeelding wordt getoond. Dan uitgezocht **publiceer playbook** om playbook te voltooien.

![ het &quot;Technische Assets&quot;lusje met de &quot;Uitgezochte activa&quot;benadrukte knoop die u kunt gebruiken om een reis met playbook te associëren.](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![ selecteer een reis om het met playbook te associëren.](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Na publicatie extraheert en koppelt het afspeelboek automatisch het schema en de publieksdetails van de reis.

![ A gepubliceerde playbook die meta-gegevens en bijbehorende technische activa tonen.](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Alle gecreeerde playbooks zijn beschikbaar in **Uw Playbooks** tabel.

![ &quot;Uw playbooks&quot;lusje tonend een lijst van gecreeerde playbooks.](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

U kunt elke gewenste afspeellijst in de catalogus selecteren om instanties te maken voor hergebruik. Verwijs naar de documentatie aan [ leren hoe te om instanties ](/help/use-case-playbooks/playbooks/create-share-reuse.md) tot stand te brengen.

![ het lusje van het Overzicht van het Playbook met de &quot;Create instantie&quot;benadrukte optie.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Nadat een afspeelboek is gepubliceerd, kan het niet worden bewerkt. Als u wijzigingen wilt aanbrengen, verwijdert u het afspeelboek en begint u opnieuw.

## Voorbeeld vragen

De AI Medewerker kan diverse snelle structuren verwerken en zeer belangrijke details halen terwijl het filtreren uit onnodige informatie. Hieronder volgen enkele voorbeelden van gebruikersherinneringen en hoe het systeem deze interpreteert.

**Voorbeeld 1:**

&quot;Creeer een campagne getiteld &quot;Voltooi de Blik&quot;om verkoop en CLV te verhogen. De campagne moedigt klanten aan keukengerei of meubilair te kopen om een aanvullende aankoop te voltooien via gepersonaliseerde aanbevelingen en aanbiedingen met betrekking tot hun aankoop. Eerste bericht aan de klanten met productaanbevelingen. Als ze binnen 7 dagen geen aankopen doen, ontvangen ze een tweede bericht met productaanbevelingen en voorstellen. Gebruik pushberichten en e-mail om contact op te nemen met de klanten. Doelklanten die in de afgelopen 7 dagen een aankoop hebben gedaan in keukengerei of meubelcategorie en die in de afgelopen 30 dagen niet als doelgroep zijn aangemerkt. Als onderdeel van de campagne, willen wij KPIs zoals kliks (e-mail, app, sms, duw), CTR, E-Wallet CTR, de Omzetting van AOV.CLV Inkomsten, de Totale gebeurtenissen van de Aankoop (in-store, digitaal, callcenter) meten.&quot;

![ een voorbeeld van een lange herinnering ingegaan in het vakje van de tekstinput om playbook te produceren.](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Voorbeeld 2:**

&quot;Projectnaam: Modenieuwsbrief
Achtergrond: (pro-actief of oplossend voor probleem): Een reis die wordt ontworpen om modebulletins naar klanten te verzenden ACME die voor nieuwsbrief mededeling hebben geabonneerd.
Doel: Stuur e-mails met nieuwsbrieven naar ACME-klanten die zich voor communicatie hebben geabonneerd.
Actiedetails: de klant ontvangt modenieuws via e-mail. De e-mail moet gepersonaliseerd zijn en de inhoud moet variëren op basis van geslacht, taal en markt.
Projectkanalen/aanraakpunten: E-mail
Doelpubliek: Klanten die zijn geabonneerd op ACME-nieuwsbrieven.
Doel-KPI&#39;s/Betrokkenheidsmetriek/ROI: 1. Verhoog de inkomsten uit producten. 2. Klantloyaliteit aansturen.&quot;

![ een voorbeeld van een georganiseerde, lijst-stijl herinnering ingegaan in het vakje van de tekstinput om playbook te produceren.](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Voorbeeld 3:**

&quot;Vraag kopers om producten te kopen tijdens een doorlopende productpromotiecampagne.
Neem contact op met kopers tijdens een doorlopende promotie door geschikte communicatie via e-mail, SMS of via pushberichten te verzenden om producten te kopen. Stuur ze een herinnering per e-mail nadat ze 24 uur niet hebben deelgenomen aan de promotie.&quot;

![ een voorbeeld van een beknopte herinnering ingegaan in het vakje van de tekstinput om playbook te produceren.](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Voorbeeld 4:**

&quot;Verkoop schoenen aan middelbare scholieren.&quot;

![ een voorbeeld van een one-line herinnering ingegaan in het vakje van de tekstinput om playbook te produceren.](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

De AI-assistent verwijdert alle overbodige details zoals &quot;Projectnaam&quot; of &quot;Achtergrond&quot;. De code extraheert de belangrijkste elementen zoals &quot;doelpubliek&quot;, &quot;campagnedoel&quot; en &quot;marketingkanaal&quot; en werkt met elke invoerstijl.

Deze voorbeelden tonen aan hoe AI essentiële details van gebruikersherinneringen kan verfijnen en halen.

>[!NOTE]
>
> Vermijd het gebruik van PII&#39;s of expliciete woorden bij het schrijven van uw vragen.

## Richtlijnen voor inhoud en modernisering

Houd bij het maken van afspeelboeken rekening met de taal en inhoud die u inneemt. Afspeelboeken zijn zichtbaar in uw hele organisatie en alle aanstootgevende of ongepaste inhoud die gebruikers markeren.

### Markering- en controleproces

Als een afspeelboek ongeschikte of aanstootgevende inhoud bevat, ontvangt Adobe automatisch een rapport ter controle. Adobe controleert de gemarkeerde inhoud, brengt de klant op de hoogte als dit niet geschikt wordt geacht en verwijdert het afspeelboek.

## Afspeelboeken delen over sandboxen {#share-playbooks-sandboxes}

Wanneer u een afspeelboek maakt en publiceert in één sandbox, wordt dit automatisch beschikbaar in alle sandboxen binnen uw organisatie. Met deze functie is handmatig delen overbodig en kunt u naadloos instanties van het afspeelboek in andere sandboxen maken.

>[!TIP]
>
>Als de afspeelboek verwijst naar velden die niet beschikbaar zijn in het samenvoegingsschema van de doelsandbox of als u niet de vereiste machtigingen hebt, wordt een foutbericht weergegeven wanneer u de instantie probeert te maken. In het bericht worden de ontbrekende velden en/of machtigingen opgegeven.

Als er velden ontbreken in uw samenvoegingsschema, worden deze tijdens het importeren gemarkeerd in een dialoogvenster.

![ de dialoogdoos van A die gebieden van het unieschema tijdens het playbook invoerproces missen.](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Uw afspeelboeken delen tussen organisaties {#sharing-playbooks-organizations}

Het delen van afspeelboeken tussen organisaties zorgt voor consistentie en efficiëntie wanneer meerdere teams dezelfde best practices moeten volgen. Voer de volgende stappen uit om een afspeelboek van de ene organisatie naar de andere te delen:

1. **Logboek in de bronorganisatie**: Navigeer aan de organisatie die playbook bevat u creeerde en van het **[!UICONTROL Your playbooks]** lusje wilt delen.
2. **publiceer playbook**: Als playbook niet reeds wordt gepubliceerd, moet u het publiceren alvorens te delen.

   >[!NOTE]
   >
   >Er moet een partnerschap tot stand worden gebracht tussen de bron- en doelorganisaties om het delen van spelboeken mogelijk te maken. Leer hoe te [ een verzoek van het organisatiepartnerschap tot stand te brengen ](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request).

3. **stelt het aandeel** in werking: Zodra playbook wordt gepubliceerd en een partnerschap wordt gevestigd, uitgezocht **[!UICONTROL Share Playbook]**.
4. **selecteer de doelorganisatie**: Kies de organisatie u playbook wilt delen wanneer ertoe aangezet.
5. **Bevestig en deel**: Bevestig uw selectie. Je ontvangt bevestigingsberichten die aangeven dat het delen is gelukt.
6. **verifieer de doelorganisatie**: Logboek in de doelorganisatie om te verifiëren dat playbook beschikbaar is.
7. **de Invoer playbook**: Selecteer **[!UICONTROL Import]** om playbook in de doelorganisatie te brengen. U kunt het in het **Playbooks** lusje bekijken.

Als playbook niet verschijnt, zorg ervoor het wordt gepubliceerd en dat het organisatiepartnerschap actief is.

>[!IMPORTANT]
>
>Het tijdelijk delen van een afspeelboek wordt niet ondersteund. Als u een playbook van één organisatie aan een andere deelt en dan het invoert, kan het niet opnieuw van de ontvangende organisatie aan een derde organisatie worden gedeeld.

## Vereiste machtigingen {#required-permissions}

U hebt de volgende machtigingen nodig om toegang te krijgen tot de sandbox en deze functie te gebruiken:

### Sandbox-machtigingen

Deze machtigingen zijn vereist voor toegang tot de sandboxomgeving waarin de functie bestaat:

* **beheert zandbak**
* **zandbak van de Mening**

* **Pakket delend toestemmingen**:

Deze machtigingen zijn vereist voor de functionaliteit voor intern delen:

* [**Pakket beheren*](/help/sandboxes/ui/sandbox-tooling.md)
* [**Pakket delen**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Gebruik deze machtigingen om:

* De sandboxomgeving invoeren
* Toegang tot de functie in de sandbox
* Pakketten naar wens beheren en delen

Deze machtigingen bevinden zich in de sectie **[!UICONTROL Sandboxes]** van de lijst met machtigingen.

![ de toestemmingenlijst met relevante toestemmingen voor het leiden en het delen van benadrukte playbooks.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Reizen en gerelateerde objecten - machtigingen

Wanneer het bouwen van Reizen die Playbooks gebruiken, zou u andere voorwerpen, zoals **Kanalen**, **Soorten publiek**, en andere entiteiten kunnen van verwijzingen voorzien. Elk van deze objecten heeft een eigen rechtenset.

Dit zijn de belangrijkste toestemmingen voor Reisgerelateerde acties, zoals:

* **reis van de Mening**
* **beheer reis**
* Machtigingen voor objecten zoals Soorten publiek en Kanalen

U hebt ook de volgende publieksmachtigingen nodig:

* **gelezen Segment**
* **gelezen Profiel**
* **gelezen Dataset**

Aangezien de Reizen hoogst flexibel zijn en vele onderling verbonden voorwerpen kunnen impliceren, zijn hun [ volledige toestemmingen ](https://experienceleague.adobe.com/nl/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) afzonderlijk gedocumenteerd en kunnen variëren gebaseerd op uw bijzonder gebruiksgeval.

## Volgende stappen

Nu u begrijpt om, playbooks tot stand te brengen te publiceren en te delen gebruikend de Medewerker AI, leren hoe te beginnen met de beschikbare playbooks en de juiste te kiezen voor uw gebruiksgeval van [ Lijst van Playbooks ](/help/use-case-playbooks/playbooks/choose.md).