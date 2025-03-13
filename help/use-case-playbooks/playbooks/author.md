---
solution: Experience Platform
title: Leer hoe u uw eigen afspeelboeken ontwerpt en deelt met de AI Assistant.
description: Hoe te om uw eigen gebruiksdoosplaybooks te ontwerpen en te delen.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: f76db5c8d397c6c7b006c70147c054dc0a67be04
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# Auteur en deel uw eigen afspeelboeken

Met [!DNL Playbook Authoring Framework], aangedreven door AI Assistant in Adobe Experience Platform, kunt u op efficiënte wijze afspeelboeken maken, beheren en delen in Adobe Experience Platform.

Het kader volgt een driestappenproces:

1. **Meta-gegevens vangen**: De Medewerker van AI van het gebruik of [ webform ] om playbook meta-gegevens te vangen.

2. **Technische vereniging**: Voeg specifieke technische activa zoals reizen of publiek aan playbook toe. U behoudt de volledige controle over het maken van een afspeelboek in uw ontwikkelingssandbox en zorgt ervoor dat de bestanden en andere unieke gegevensstructuren op elkaar worden afgestemd.

3. **distributie van het Playbook**: De playbooks van het aandeel over verschillende organisaties. Zo kan het Martech Center of Excellence van ACME in Duitsland een &quot;gouden&quot; toneelboek maken en dit verspreiden onder regionale organisaties in Thailand, Australië, enz. om het gebruik van het geneesmiddel te helpen standaardiseren.

## Een afspeelboek maken

U kunt een afspeelboek op twee manieren maken: met de AI-assistent of handmatig. Lees de volgende secties voor meer informatie.

### Overzicht van afspeelboeken

Ga als volgt te werk om een afspeelboek te maken met de AI-assistent:

Selecteer **[!UICONTROL Playbooks]** in het navigatievenster aan de linkerkant.

![ &quot;Playbooks&quot;die in de linkernavigatieruit worden benadrukt in UI.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Selecteer **[!UICONTROL New Playbook]**, en selecteer dan **playbook met AI Medewerker** produceren.

![ de playbook interface met &quot;produceer playbook met AI Medewerker&quot;geselecteerd.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Beschrijf het gebruiksgeval in het veld Vraag.

**Voorbeeld**: &quot;Neem ACME klanten in dienst die lopende schoenen doorbladeren maar niet de aankoop voltooiden.&quot;

![ de playbook interface met het benadrukte webformuliergebied.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Selecteer **[!UICONTROL Generate]** om de metagegevens voor de afspeelboek te maken.

![ het snelle gebied met &quot;produceer&quot;benadrukte playbook knoop.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Als de code eenmaal is gegenereerd, selecteert u **[!UICONTROL Edit]** om de gegenereerde titel, beschrijving en metagegevens naar wens te wijzigen.

![ geproduceerde playbook met de &quot;geef&quot;benadrukte knoop uit.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Vul de sectie **[!UICONTROL Playbook detail]** in om ervoor te zorgen dat de gegevensengineers over alle benodigde details beschikken om het geval te gebruiken. Deze velden zijn optioneel, maar helpen u belangrijke informatie vast te leggen, waardoor het makkelijker wordt om de juiste technische componenten te verbinden. Selecteer **[!UICONTROL Edit]** om waarden toe te voegen aan de volgende velden:

* **Industrie**
* **het publiek van het Doel**
* **Marketing kanaal**

![ de sectie van playbook details met &quot;geeft&quot;benadrukte knoop uit.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Nadat de metagegevens zijn gegenereerd, selecteert u **[!UICONTROL Edit journey map]** om de stappen in het reisoverzicht naar wens aan te passen.

![ geef de knoop van het reisoverzicht uit.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![ geeft de reiskaart uit zodra u de playbook meta-gegevens vangt.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Ga vervolgens verder met het koppelen van het afspeelboek aan technische elementen. Selecteer **[!UICONTROL Create playbook manually]** als u handmatig een afspeelboek wilt maken.

![ creeer manueel playbook ](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Er wordt een lege afspeelboeksjabloon weergegeven. Vul details zoals **Titel** en **Beschrijving** uit. U kunt het reisoverzicht ook bewerken om gebeurtenissen en aanraakpunten toe te voegen als dat nodig is.

## Afspeelboek koppelen aan technische middelen

Ongeacht of u handmatig een afspeelboek maakt of met de AI Assistant, moet u deze aan de vereiste technische elementen koppelen. Navigeer naar het tabblad **[!UICONTROL Technical Assets]** en selecteer het gewenste product. Selecteer **[!UICONTROL Journey Optimizer]** voor dit voorbeeld.

>[!NOTE]
>
> Ondersteuning voor Real-Time CDP wordt in een toekomstige release toegevoegd.

![ de &quot;Technische activa&quot;tabel en de &quot;Add vereiste benadrukte productknoop&quot;.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Kies **[!UICONTROL Select an Asset]** om dit afspeelboek te koppelen aan een reis zoals in de onderstaande afbeelding wordt getoond. Dan uitgezocht **publiceer playbook** om playbook te voltooien.

![ &quot;Selecteer activa&quot;knoop die op de &quot;Technische activa&quot;tabel wordt benadrukt ](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![ selecteer een reis ](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Na publicatie extraheert en koppelt het afspeelboek automatisch het schema en de publieksdetails van de reis.

![ Gepubliceerd playbook ](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Alle gecreeerde playbooks zijn beschikbaar in **Uw Playbooks** tabel.

![ &quot;Uw playbooks&quot;lusje ](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

U kunt elke gewenste afspeellijst in de catalogus selecteren om instanties te maken voor hergebruik. Verwijs naar de documentatie aan [ leren hoe te om instanties ](/help/use-case-playbooks/playbooks/create-share-reuse.md) tot stand te brengen.

![ De optie &quot;Instantie maken&quot; wordt gemarkeerd op het tabblad &quot;Overzicht van afspeelboek&quot; nadat u een afspeelboek hebt geselecteerd. ](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Nadat een afspeelboek is gepubliceerd, kan het niet worden bewerkt. Als u wijzigingen wilt aanbrengen, verwijdert u het afspeelboek en begint u opnieuw.

## Voorbeeld vragen

De AI Medewerker kan diverse snelle structuren verwerken en zeer belangrijke details halen terwijl het filtreren uit onnodige informatie. Hieronder volgen enkele voorbeelden van gebruikersvragen en hoe deze door het systeem worden geïnterpreteerd:

**Voorbeeld 1:**

&quot;Creeer een campagne getiteld &quot;Voltooi de Blik&quot;om verkoop en CLV te verhogen. De campagne moedigt klanten aan keukengerei of meubilair te kopen om een aanvullende aankoop te voltooien via gepersonaliseerde aanbevelingen en aanbiedingen met betrekking tot hun aankoop. Eerste bericht aan de klanten met productaanbevelingen. Als ze binnen 7 dagen geen aankopen doen, ontvangen ze een tweede bericht met productaanbevelingen en voorstellen. Gebruik pushberichten en e-mail om contact op te nemen met de klanten. Doelklanten die in de afgelopen 7 dagen een aankoop hebben gedaan in keukengerei of meubelcategorie en die in de afgelopen 30 dagen niet als doelgroep zijn aangemerkt. Als onderdeel van de campagne, willen wij KPIs zoals kliks (e-mail, app, sms, duw), CTR, e-Wallet CTR, de Omzetting van AOV.CLV Inkomsten, de Totale gebeurtenissen van de Aankoop (in-store, digitaal, callcenter) meten.&quot;

![ Voorbeeld 1 herinnering ](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**Voorbeeld 2:**

&quot;Projectnaam: Modenieuwsbrief
Achtergrond: (pro-actief of oplossend voor probleem): Een reis die wordt ontworpen om modebulletins naar klanten te verzenden ACME die voor nieuwsbrief mededeling hebben geabonneerd.
Doel: Stuur e-mails met nieuwsbrieven naar ACME-klanten die zich voor communicatie hebben geabonneerd.
Actiedetails: de klant ontvangt modenieuws via e-mail. De e-mail moet gepersonaliseerd zijn en de inhoud moet variëren op basis van geslacht, taal en markt.
Projectkanalen/aanraakpunten: E-mail
Doelpubliek: Klanten die zijn geabonneerd op ACME-nieuwsbrieven.
Doel-KPI&#39;s/Betrokkenheidsmetriek/ROI: 1. Verhoog de inkomsten uit producten. 2. Klantloyaliteit aansturen.&quot;

![ Voorbeeld 2 herinnering ](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**Voorbeeld 3:**

&quot;Vraag kopers om producten te kopen tijdens een doorlopende productpromotiecampagne.
Neem contact op met kopers tijdens een doorlopende promotie door geschikte communicatie via e-mail, SMS of via pushberichten te verzenden om producten te kopen. Stuur ze een herinnering per e-mail nadat ze 24 uur niet hebben deelgenomen aan de promotie.&quot;

![ Voorbeeld 3 herinnering ](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**Voorbeeld 4:**

&quot;Verkoop schoenen aan middelbare scholieren.&quot;

![ Voorbeeld 4 herinnering ](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

De AI-assistent verwijdert alle overbodige details zoals &quot;Projectnaam&quot; of &quot;Achtergrond&quot;. De code extraheert de belangrijkste elementen zoals &quot;doelpubliek&quot;, &quot;campagnedoel&quot; en &quot;marketingkanaal&quot; en werkt met elke invoerstijl.

Deze voorbeelden tonen aan hoe AI essentiële details van gebruikersherinneringen kan verfijnen en halen.

>[!NOTE]
>
> Vermijd het gebruik van PII&#39;s of expliciete woorden bij het schrijven van uw vragen.

## Richtlijnen voor inhoud en modernisering

Houd bij het maken van afspeelboeken rekening met de taal en inhoud die u inneemt. Afspeelboeken zijn in uw hele organisatie zichtbaar en alle aanstootgevende of ongeschikte inhoud kan door gebruikers worden gemarkeerd.

### Markering- en controleproces

Als een afspeelboek wordt gemarkeerd voor onjuiste of aanstootgevende inhoud, wordt het automatisch ter controle naar Adobe gerapporteerd. Adobe controleert vervolgens de gemarkeerde inhoud en als dit niet passend wordt geacht, wordt de klant op de hoogte gesteld en wordt het afspeelboek verwijderd.

## Volgende stappen

Nu u begrijpt hoe te om playbooks tot stand te brengen en te publiceren gebruikend de Medewerker AI, hoe te beginnen met de beschikbare playbooks en juiste te kiezen voor uw gebruiksgeval van [ Lijst van Playbooks ](/help/use-case-playbooks/playbooks/choose.md).
