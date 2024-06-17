---
title: UI-gids voor grafieksimulatie
description: Leer hoe te om de Simulatie van de Grafiek in de Dienst UI van de Identiteit te gebruiken.
badge: Beta
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 4c49bec7974dafe18d18deded6ddc936ece47dc3
workflow-type: tm+mt
source-wordcount: '1401'
ht-degree: 0%

---

# [!DNL Graph Simulation] UI-hulplijn

>[!AVAILABILITY]
>
>Deze functie is nog niet beschikbaar. Het bètaprogramma voor koppelingsregels voor identiteitsgrafieken zal naar verwachting in juli van start gaan voor ontwikkelingssandboxen. Neem contact op met het accountteam van de Adobe voor meer informatie over de deelnemingscriteria.

[!DNL Graph Simulation] is een hulpmiddel in de Dienst UI van de Identiteit dat u kunt gebruiken om te simuleren hoe een identiteitsgrafiek zich op een bepaalde combinatie identiteiten gedraagt en hoe u vormt [algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md).

Lees dit document om te leren hoe u kunt gebruiken [!DNL Graph Simulation] om het gedrag van de identiteitsgrafiek en hoe het grafiekalgoritme beter te begrijpen.

## Krijg kennis van de [!DNL Graph Simulation] interface {#interface}

U hebt toegang tot [!DNL Graph Simulation] in de gebruikersinterface van Adobe Experience Platform. Selecteren **[!UICONTROL Identities]** van de linkernavigatie en selecteer dan **[!UICONTROL Graph Simulation]** in de bovenste koptekst.

![De interface van de Simulatie van de Grafiek in Adobe Experience Platform UI.](../images/graph-simulation/graph-simulation.png)

De [!DNL Graph Simulation] de interface kan in drie secties worden verdeeld:

>[!BEGINTABS]

>[!TAB Gebeurtenissen]

Gebeurtenissen: de optie **[!UICONTROL Events]** om identiteiten toe te voegen om een grafiek te simuleren. Een volledig gekwalificeerde identiteit moet een naamruimte voor de identiteit en de bijbehorende identiteitswaarde hebben. U moet ten minste twee identiteiten toevoegen om een grafiek te simuleren. U kunt ook **[!UICONTROL Load Example]** om een vooraf geconfigureerde gebeurtenis en algoritme-instelling in te voeren.

![Het deelvenster Gebeurtenissen van het gereedschap Grafieksimulatie.](../images/graph-simulation/events.png)

>[!TAB Algoritmeconfiguratie]

Algorithm configuration: Use the **[!UICONTROL Algorithm configuration]** om het optimalisatiealgoritme voor uw naamruimten toe te voegen en te configureren. U kunt een naamruimte slepen en neerzetten om de respectievelijke prioriteitsvolgorde te wijzigen. U kunt ook **[!UICONTROL Unique Per Graph]** om te bepalen of een naamruimte uniek is.

![De algoritmeconfiguratie van het hulpmiddel van de Simulatie van de Grafiek.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB Gesimuleerde-grafiekviewer]

Gesimuleerde grafiekviewer: de gesimuleerde grafiekviewer geeft de resulterende grafiek weer op basis van de gebeurtenissen die u hebt toegevoegd en het algoritme dat u hebt geconfigureerd. Een rechte lijn tussen twee identiteiten betekent dat er een koppeling tot stand wordt gebracht. Een stippellijn geeft aan dat een koppeling is verwijderd.

![Het gesimuleerde deelvenster van de grafiekviewer, met een voorbeeld van een gesimuleerde grafiek.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Gebeurtenissen toevoegen {#add-events}

Selecteer **[!UICONTROL Add events]**.

![De knop Gebeurtenissen toevoegen is geselecteerd.](../images/graph-simulation/add-events.png)

Er wordt een pop-upvenster weergegeven voor [!UICONTROL Event #1]. Voer van hieruit de naamruimte en de combinatie van identiteitswaarden in. U kunt het vervolgkeuzemenu gebruiken om een naamruimte voor identiteit te selecteren. U kunt ook in de eerste paar letters van een naamruimte typen en vervolgens de opties selecteren die in het vervolgkeuzemenu zijn opgegeven. Nadat u de naamruimte hebt geselecteerd, geeft u een identiteitswaarde op die overeenkomt met de naamruimte.

![Het venster Event #1 met een lege interface.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>De identiteitswaarde die u invoert tijdens [!DNL Graph Simulation] oefeningen hoeven geen echte identiteitswaarden te zijn en kunnen eenvoudige plaatsaanduidingen zijn.

Wanneer uw eerste identiteit is voltooid, selecteert u het pictogram Toevoegen (**`+`**) om een tweede identiteit toe te voegen.

![De eerste volledig gekwalificeerde identiteit van {Email: tom@acme.com} wordt ingevoerd in het deelvenster Gebeurtenissen van Grafieksimulatie.](../images/graph-simulation/event-one-added.png)

Herhaal vervolgens dezelfde stappen en voeg een tweede identiteit toe. Twee volledig gekwalificeerde identiteiten zijn vereist om een identiteitsgrafiek te produceren. In het onderstaande voorbeeld wordt een ECID toegevoegd als een naamruimte en krijgt een waarde van `111`. Selecteer **[!UICONTROL Save]**.

![Een tweede identiteit van {ECID: 111} wordt toegevoegd aan gebeurtenis nr. 1.](../images/graph-simulation/first-event.png)

De [!UICONTROL Events] interface werkt bij om uw eerste gebeurtenis weer te geven, die in dit geval: `{Email: tom@acme.com, ECID: 111}`.

![De bijgewerkte gebeurtenisinterface met {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Herhaal vervolgens dezelfde stappen om een tweede gebeurtenis toe te voegen. Voor gebeurtenis nr. 2 voegt u `{Email: summer@acme.com}` als uw eerste identiteit en voeg vervolgens hetzelfde toe `{ECID: 111}` als tweede identiteit, waardoor een tweede gebeurtenis wordt gecreëerd van: `{Email: summer@acme.com}, {ECID: 111}`. Als u klaar bent, hebt u twee gebeurtenissen nodig, één voor `{Email: tom@acme.com, ECID: 111}` en één voor `{Email: summer@acme.com}, {ECID: 111}`.

![De bijgewerkte gebeurtenisinterface met twee gebeurtenissen.](../images/graph-simulation/two-events.png)

### Voorbeeld laden {#load-example}

Selecteren **[!UICONTROL Load example]** om een voorbeeldgrafiek met een vooraf ingestelde algoritme en gebeurtenisconfiguratie op te zetten.

![De geselecteerde voorbeeldoptie van de Lading.](../images/graph-simulation/load-example.png)

Er verschijnt een pop-upvenster met beschikbare grafiekscenario&#39;s waaruit u kunt kiezen:

| Voorbeeldgrafiek | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Gedeeld apparaat | Het gedeelde apparaat verwijst naar scenario&#39;s waar twee verschillende gebruikers login aan het zelfde enige apparaat. | Een man en vrouw delen een iPad voor internetsurfen en e-commerce. |
| Ongeldige (niet-unieke) telefoon | Ongeldige of niet-unieke telefoon verwijst naar scenario&#39;s waar twee verschillende gebruikers het zelfde telefoonaantal gebruiken om een rekening tot stand te brengen. | Een moeder en haar dochter gebruiken hun gedeelde huistelefoonnummer om zich aan te melden voor e-commerceaccounts. |
| Ongeldige identiteitswaarden | De &quot;slechte&quot;identiteitswaarden verwijzen naar scenario&#39;s waar de Dienst van de Identiteit niet-unieke IDFAs wegens onjuiste implementatie produceert. | WebSDK verzendt ten onrechte een `user_null` waarde voor elke gebeurtenis vanwege problemen met de implementatie van code. |

![Een venster dat de beschikbare pre-gevormde voorbeelden toont: gedeeld apparaat, ongeldige telefoon, en slechte identiteitswaarden.](../images/graph-simulation/example-options.png)

Selecteer de gewenste opties om te laden [!DNL Graph Simulation] met vooraf geconfigureerde gebeurtenissen en algoritme. U kunt nog verdere configuraties aan om het even welke vooraf geladen voorbeelden van grafiekscenario&#39;s maken.

![De gebeurtenissen en het algoritme die voor ongeldige telefoon worden gevormd.](../images/graph-simulation/example-loaded.png)

Selecteer **[!UICONTROL Simulate]**.

![Een voorbeeldgrafiek die voor ongeldige telefoon wordt gesimuleerd.](../images/graph-simulation/example-simulated.png)

### Tekstversie gebruiken {#use-text-version}

U kunt de tekstmodus ook gebruiken om gebeurtenissen te configureren. Als u de tekstmodus wilt gebruiken, selecteert u het instellingenpictogram en selecteert u vervolgens **[!UICONTROL Text (Advanced users)]**.

![Het geselecteerde instellingenpictogram.](../images/graph-simulation/settings.png)

U kunt uw identiteiten handmatig invoeren in de tekstmodus. Een dubbele punt gebruiken (`:`) om de identiteitswaarde te onderscheiden die overeenkomt met de naamruimte die u invoert en vervolgens een komma (`,`) om uw identiteiten te scheiden. Als u verschillende gebeurtenissen van elkaar wilt onderscheiden, gebruikt u een nieuwe regel voor elke gebeurtenis.

![Het deelvenster Gebeurtenissen gebruikt de versie van de tekstmodus.](../images/graph-simulation/text-version.png)

### Gebeurtenis Edit {#edit-event}

Als u een gebeurtenis wilt bewerken, selecteert u de ovalen (`...`) naast een bepaalde gebeurtenis en selecteer vervolgens **[!UICONTROL Edit]**.

![Het pictogram van de bewerkingsgebeurtenis is geselecteerd.](../images/graph-simulation/edit.png)

### Gebeurtenis delete {#delete-event}

Als u een gebeurtenis wilt verwijderen, selecteert u de ovalen (`...`) naast een bepaalde gebeurtenis en selecteer vervolgens **[!UICONTROL Delete]**.

![Het pictogram voor de verwijdergebeurtenis is geselecteerd.](../images/graph-simulation/delete.png)

## Algoritme configureren {#configure-algorithm}

>[!IMPORTANT]
>
>Het algoritme dat u vormt bepaalt hoe de Dienst van de Identiteit de namespaces behandelt die u in uw gebeurtenissen invoerde. Om het even welke configuratie die u in [!DNL Graph Simulation UI] worden niet opgeslagen in identiteitsinstellingen.

Nadat u de gebeurtenissen hebt toegevoegd, kunt u nu het algoritme configureren dat wordt gebruikt om de grafiek te simuleren. Selecteer **[!UICONTROL Add config]**.

![Het deelvenster voor algoritmeconfiguratie.](../images/graph-simulation/add-config.png)

Er wordt een lege configuratieregel weergegeven. Voer eerst dezelfde naamruimte in als u hebt gebruikt voor uw gebeurtenissen. In dit geval voert u eerst e-mail in. Nadat u de naamruimte hebt ingevoerd, worden de kolommen voor [!UICONTROL Identity Symbol] en [!UICONTROL Identity Type] automatisch vullen.

![De eerste configuratieingang.](../images/graph-simulation/add-namespace.png)

Herhaal vervolgens dezelfde stappen en voeg uw tweede naamruimte toe, in dit geval de ECID. Zodra al uw namespaces zijn ingegaan, kunt u beginnen hun prioriteiten en uniciteit te vormen.

* **Prioriteit naamruimte**: De prioriteit van een naamruimte bepaalt het relatieve belang ten opzichte van de andere naamruimten in een bepaalde identiteitsgrafiek. Als uw identiteitsgrafiek bijvoorbeeld vier verschillende naamruimten heeft: CRM ID, ECID, Email en Apple IDFA, kunt u prioriteiten configureren om een volgorde van belang voor de vier naamruimten te bepalen.
* **Unieke naamruimte**: Als een naamruimte als uniek is aangewezen, genereert Identity Service grafieken met het voorbehoud dat slechts één identiteit met een bepaalde unieke naamruimte kan bestaan. Als de naamruimte E-mail bijvoorbeeld is aangewezen als een unieke naamruimte, kan een grafiek slechts één identiteit hebben met e-mail. Als er meer dan één identiteit is met de naamruimte E-mail, wordt de oudste koppeling verwijderd.

Om namespace prioriteit te vormen, selecteer en sleep de namespace rijen aan de prioritaire orde die u wilt, met de hoogste rij die hogere prioriteit vertegenwoordigt en de onderste rij die lagere prioriteit vertegenwoordigt. Als u een naamruimte als uniek wilt aanwijzen, selecteert u de optie **[!UICONTROL Unique Per Graph]** selectievakje.

Selecteer **[!UICONTROL Simulate]**.

![Alle geconfigureerde naamruimten.](../images/graph-simulation/all-namespaces.png)

## Gesimuleerde grafiek weergeven

De [!UICONTROL Simulated Graph] geeft de gegenereerde identiteitsgrafiek(en) weer op basis van de gebeurtenissen die u hebt toegevoegd en het algoritme dat u hebt geconfigureerd.

| Grafiekpictogrammen | Beschrijving |
| --- | --- |
| Effen lijn | Een solide lijn vormt een vaststaand verband tussen twee identiteiten. |
| Stippellijn | Een stippellijn vertegenwoordigt een verwijderde koppeling tussen twee identiteiten. |
| Aantal op regel | Een getal op een regel geeft de tijdstempel aan van wanneer die bepaalde koppeling is gegenereerd. Het laagste getal (1) geeft de oudste ingestelde koppeling aan. |

In de onderstaande voorbeeldgrafiek bestaat een stippellijn tussen `{Email: tom@acme.com}` en `{ECID: 111}` om de volgende redenen:

* De e-mail is als uniek aangewezen tijdens de stap van de algoritmeconfiguratie. Daarom kan er slechts één identiteit met een naamruimte E-mail in een grafiek bestaan.
* Het verband tussen `{Email: tom@acme.com}` en `{ECID: 111}` was de eerste vastgestelde identiteit (gebeurtenis nr. 1). Het is de oudste schakel en wordt daarom verwijderd.

![Het gesimuleerde deelvenster van de grafiekviewer, met een voorbeeld van een gesimuleerde grafiek.](../images/graph-simulation/simulated-graph.png)

## Volgende stappen

Door dit document te lezen, weet u nu hoe u de [!DNL Graph Simulation] om beter te begrijpen hoe uw identiteitsgegevens worden behandeld gegeven een bepaalde reeks regels en configuraties. Lees de volgende documenten voor meer informatie:

* [Koppelingsregels voor identiteitsgrafiek](overview.md)
* [Algoritme voor identiteitsoptimalisatie](identity-optimization-algorithm.md)
* [Prioriteit naamruimte](namespace-priority.md)
