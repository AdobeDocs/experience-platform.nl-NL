---
title: Pakketten delen in de hele organisatie met behulp van Sandbox-tools
description: Leer hoe u Sandbox Tooling in Adobe Experience Platform gebruikt om pakketten te delen tussen verschillende organisaties.
source-git-commit: 77994c1cdd185cc8a2963c5aa2eb345c8702fe02
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Pakketten delen tussen organisaties met behulp van sandboxgereedschappen

Verbeter de configuratienauwkeurigheid over zandbakken en voer naadloos zandbakconfiguraties tussen zandbakken over verschillende organisaties uit met de zandbaktoolingeigenschap. In dit document wordt beschreven hoe u gereedschappen voor sandboxen in Adobe Experience Platform kunt gebruiken om pakketten te delen tussen verschillende organisaties. Er zijn twee typen gedeelde pakketten:

- **Privé pakket**

[ Privé pakketten ](#private-packages) kunnen slechts met organisaties worden gedeeld die het het delen verzoek van de bronorganisatie hebben goedgekeurd.

- **Openbaar pakket**

[ Openbare pakketten ](#public-packages) zijn beschikbaar om zonder enige extra goedkeuring in te voeren. Deze pakketten kunnen worden gedeeld op de website, de blog of het platform van een partner. Met de pakketlading kunnen pakketten van deze kanalen naar de doelorganisatie worden gekopieerd en geplakt.

## Privépakketten {#private-packages}

>[!NOTE]
>
>Om een het delen verzoek in werking te stellen en goed te keuren en pakketten over organisaties te delen, zult u **pakket-aandeel** op rol-gebaseerde toegangsbeheertoestemming moeten hebben.

Gebruik de functie Sandbox Tooling om partnerschappen te maken, de status van partnerschapsverzoeken bij te houden, bestaande partnerschappen te beheren en pakketten met partnerorganisaties te delen.

### Een aanvraag voor een partnerschap voor organisaties maken

Navigeer naar het tabblad **[!UICONTROL Sandboxes]** **[!UICONTROL Partner orgs]** als u een verzoek voor samenwerking met organisaties wilt maken. Selecteer vervolgens **[!UICONTROL Manage partner orgs]** .

![ de zandbakken UI, met het lusje van de Organisaties van de Partner en leidt benadrukte partnerorganisaties.](../images/ui/sandbox-tooling/private-manage-partner-orgs.png)

Voer in het dialoogvenster [!UICONTROL Package partner management] de organisatie-id in **[!UICONTROL Enter Org ID]** in en druk op Enter (Windows) of Return (Mac). De organisatie-id wordt weergegeven in de onderstaande sectie **[!UICONTROL Selected Org IDs]** . Selecteer **[!UICONTROL Confirm]** nadat u de id&#39;s hebt toegevoegd.

>[!TIP]
>
>U kunt meerdere organisatie-id&#39;s tegelijk invoeren met behulp van door komma&#39;s gescheiden lijsten of door elke organisatie-id in te voeren, gevolgd door Enter.

![ het de orgasdialoog van de Partner van het Pakket met ingaat Org identiteitskaart, Geselecteerde Org IDs, en bevestigt benadrukte Bevestiging.](../images/ui/sandbox-tooling/private-enter-org-id.png)

De aanvraag voor delen wordt naar de partnerorganisatie verzonden en u gaat terug naar het tabblad [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** , dat de **[!UICONTROL Outgoing request]** weergeeft.

![ de organisatie van de Partner lusje met Uitgaand benadrukte verzoek.](../images/ui/sandbox-tooling/private-outgoing-request.png)

### Een partnerschapverzoek toestaan {#authorize-request}

Navigeer naar het tabblad [!UICONTROL Sandboxes] **[!UICONTROL Partner orgs]** als u een aanvraag voor een partnership voor organisatie wilt autoriseren. Selecteer vervolgens **[!UICONTROL Incoming request]** .

![ de zandbakken UI met het lusje van de Organisaties van de Partner en het Binnenkomende benadrukte verzoek.](../images/ui/sandbox-tooling/private-authorise-partner-org.png)

Huidige **[!UICONTROL Status]** voor het verzoek, in dit stadium, is **In afwachting**. Als u de aanvraag wilt goedkeuren, selecteert u de ellips (`...`) naast de geselecteerde aanvraag en selecteert u vervolgens **[!UICONTROL Approve]** in de vervolgkeuzelijst.

![ Lijst van inkomende verzoeken die het drop-down menu tonen met benadrukte Goedkeuren.](../images/ui/sandbox-tooling/private-approve-partner-org.png)

Het dialoogvenster **[!UICONTROL Review partner org request]** bevat informatie over het partnerschapverzoek voor de organisatie. Voer een [!UICONTROL Reason] in voor goedkeuring en selecteer vervolgens **[!UICONTROL Approve]** .

![ de dialoog van het de partnerorganisatieverzoek van het overzicht met Reden en benadrukte Goedkeuren.](../images/ui/sandbox-tooling/private-approval-partner-org.png)

U keert terug naar de [!UICONTROL Incoming request] -pagina en de status van de aanvraag is bijgewerkt naar **[!UICONTROL Approved]** .

![ Lijst van inkomende verzoeken met Goedgekeurd benadrukte.](../images/ui/sandbox-tooling/private-approved-partner-org.png)

Gebruik deze workflow/dit proces om pakketten te delen tussen uw organisatie en de bronorganisatie.

### Pakketten delen met partnerorganisaties {#share-package}

>[!NOTE]
>
>Slechts kunnen de pakketten met de status **Gepubliceerde** worden gedeeld.

Als u een pakket wilt delen met een erkende partnerorganisatie, navigeert u naar het tabblad [!UICONTROL Sandboxes] **[!UICONTROL Packages]** . Selecteer vervolgens de ellips (`...`) naast het pakket en selecteer **[!UICONTROL Share package]** in het vervolgkeuzemenu.

![ Lijst van pakketten die het dropdown menu met het benadrukte pakket van het Aandeel tonen.](../images/ui/sandbox-tooling/private-share-package.png)

Selecteer in het dialoogvenster **[!UICONTROL Share package]** het pakket dat u wilt delen in de vervolgkeuzelijst **[!UICONTROL Share settings]** en selecteer vervolgens **[!UICONTROL Confirm]** .

>[!TIP]
>
>U kunt meerdere organisaties selecteren. Geselecteerde organisaties worden weergegeven onder de vervolgkeuzelijst [!UICONTROL Share settings] .

![ het pakketdialoog van het Aandeel met de montages van het Aandeel en bevestigt benadrukte.](../images/ui/sandbox-tooling/private-share-package-confirm.png)

## Openbare pakketten {#public-packages}

Gebruik de functie Sandbox-gereedschappen om deelbare openbare pakketten te maken waarvoor geen extra goedkeuring nodig is en die gemakkelijk kunnen worden geïmporteerd met de lading van het pakket.

### Pakketbeschikbaarheid bijwerken naar openbaar {#update-package}

Als u het beschikbaarheidstype van een pakket wilt bijwerken, navigeert u naar de tab [!UICONTROL Sandboxes] **[!UICONTROL Packages]** . Selecteer vervolgens de ellips (`...`) naast het pakket en selecteer **[!UICONTROL Update to public package]** in het vervolgkeuzemenu.

![ Sandboxen UI met het pakketlusje en dropdown optiemenu met Update aan openbaar benadrukt pakket.](../images/ui/sandbox-tooling/update-to-public.png)

Controleer in het dialoogvenster **[!UICONTROL Change package availability to public]** of de pakketnaam correct is en selecteer **[!UICONTROL Confirm]** .

>[!IMPORTANT]
>
> Zodra een pakket openbaar is gemaakt, kan het niet meer worden gewijzigd in een privé-pakket.

![ het pakketbeschikbaarheid van de Verandering aan openbare dialoog met Bevestig benadrukte.](../images/ui/sandbox-tooling/change-package-availability.png)

### Pakketten delen met de pakketlading

Als u het openbare pakket wilt delen, selecteert u de ovalen (`...`) naast het pakket en selecteert u vervolgens **[!UICONTROL Copy package payload]** .

![ Sandboxes UI die een individueel die pakketdrop menu met het benadrukt pakketlading van het Exemplaar toont.](../images/ui/sandbox-tooling/copy-package-payload.png)

In het dialoogvenster **[!UICONTROL Copy package payload]** worden de pakketnaam en de lading weergegeven. Selecteer **[!UICONTROL Copy package payload]** om de lading te kopiëren verbonden aan het pakket.

![ het dialoogvakje van de het pakketlading van het Exemplaar dat JSON nuttige lading met benadrukte het pakketlading van het Exemplaar toont.](../images/ui/sandbox-tooling/confirm-payload-copy.png)

### Een nieuw pakket maken met een pakketlading

Als u een pakket wilt maken met een pakketlading, navigeert u naar de tab [!UICONTROL Sandboxes] **[!UICONTROL Packages]** . Selecteer vervolgens **[!UICONTROL Create package]** .

![ Sandboxs UI die toont Create benadrukt pakket.](../images/ui/sandbox-tooling/create-package.png)

Selecteer in het dialoogvenster **[!UICONTROL Create package]** de optie die u wilt **[!UICONTROL Paste package payload]** en selecteer vervolgens **[!UICONTROL Select]** .

![ creeer pakketdialoog met de geselecteerde lading van het deegpakket en Uitgezochte benadrukt.](../images/ui/sandbox-tooling/create-package-options.png)

Plak de gekopieerde pakketlading in het tekstgebied en selecteer **[!UICONTROL Create]**.

![ creeer pakketdialoog met het lege tekstgebied en creeer benadrukte.](../images/ui/sandbox-tooling/paste-payload.png)

Navigeer naar **[!UICONTROL Sharing status]** om de huidige status van uw aanvraag voor delen weer te geven. De huidige status van de aanvraag wordt weergegeven in de kolom **[!UICONTROL Sharing status]** .

![ het het Delen statuslusje dat een handig ladingsverzoek toont.](../images/ui/sandbox-tooling/sharing-status.png)

## Volgende stappen {#next-steps}

In dit document wordt uitgelegd hoe u de functie Sandbox-gereedschappen kunt gebruiken om pakketten te delen tussen verschillende organisaties. Voor extra informatie, verwijs naar de [ zandbak tooling gids ](../ui/sandbox-tooling.md).

Leren hoe te om verschillende handelingen uit te voeren gebruikend Sandbox API, zie de [ gids van de zandbakontwikkelaar ](../api/getting-started.md). Voor een overzicht op hoog niveau van sandboxen in Experience Platform, verwijs naar de [ overzichtsdocumentatie ](../home.md).
