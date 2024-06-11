---
title: Grafieksimulatie
description: Leer hoe te om de Simulatie van de Grafiek in de Dienst UI van de Identiteit te gebruiken.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 2afdfd54b420bcf59423ea64048d928422ea61c9
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 1%

---

# Grafieksimulatie

De Simulatie van de grafiek is een hulpmiddel in de Dienst UI van de Identiteit die u kunt gebruiken om te simuleren hoe een identiteitsgrafiek zich op een bepaalde combinatie identiteiten gedraagt en hoe u vormt [algoritme voor identiteitsoptimalisatie](./identity-optimization-algorithm.md).

Lees dit document om te leren hoe u de Simulatie van de Grafiek kunt gebruiken om het gedrag van de identiteitsgrafiek en hoe het grafiekalgoritme beter te begrijpen.

## Krijg om de interface van de Simulatie van de Grafiek te kennen

U kunt tot de Simulatie van de Grafiek in Adobe Experience Platform UI toegang hebben. Selecteren **[!UICONTROL Identities]** van de linkernavigatie en selecteer dan **[!UICONTROL Graph Simulation]** in de bovenste koptekst.

![De interface van de Simulatie van de Grafiek in Adobe Experience Platform UI.](../images/graph-simulation/graph-simulation.png)

De interface van de Simulatie van de Grafiek kan in drie secties worden verdeeld:

* Gebeurtenissen: de optie **[!UICONTROL Events]** om identiteiten toe te voegen om een grafiek te simuleren. Een volledig gekwalificeerde identiteit moet een naamruimte voor de identiteit en de bijbehorende identiteitswaarde hebben. U moet ten minste twee identiteiten toevoegen om een grafiek te simuleren. U kunt ook **[!UICONTROL Load Example]** om een vooraf geconfigureerde gebeurtenis en algoritme-instelling in te voeren.

![Het deelvenster Gebeurtenissen van het gereedschap Grafieksimulatie.](../images/graph-simulation/events.png)

* Algorithm Configuration: Use the **[!UICONTROL Algorithm Configuration]** om het optimalisatiealgoritme voor uw naamruimten toe te voegen en te configureren. U kunt een naamruimte slepen en neerzetten om de respectievelijke prioriteitsvolgorde te wijzigen. U kunt ook **[!UICONTROL Unique Per Graph]** om te bepalen of een naamruimte uniek is.

![De algoritmeconfiguratie van het hulpmiddel van de Simulatie van de Grafiek.](../images/graph-simulation/algorithm-configuration.png)

* Gesimuleerde grafiekviewer: de gesimuleerde grafiekviewer geeft de resulterende grafiek weer op basis van de gebeurtenissen die u hebt toegevoegd en het algoritme dat u hebt geconfigureerd. Een rechte lijn tussen twee knopen betekent dat een verbinding wordt gevestigd. Een stippellijn geeft aan dat een koppeling is verwijderd.


![Het gesimuleerde deelvenster van de grafiekviewer, met een voorbeeld van een gesimuleerde grafiek.](../images/graph-simulation/simulated-graph.png)

## Gebeurtenissen toevoegen

Selecteer **[!UICONTROL Add Events]**.

![De knop Gebeurtenissen toevoegen is geselecteerd.](../images/graph-simulation/add-events.png)

Er wordt een pop-upvenster weergegeven voor [!UICONTROL Event #1]. Voer van hieruit de naamruimte en de combinatie van identiteitswaarden in. U kunt het vervolgkeuzemenu gebruiken om een naamruimte voor identiteit te selecteren. U kunt ook in de eerste paar letters van een naamruimte typen en vervolgens de opties selecteren die in het vervolgkeuzemenu zijn opgegeven. Nadat u de naamruimte hebt geselecteerd, geeft u een identiteitswaarde op die overeenkomt met de naamruimte.

![](../images/graph-simulation/event-one.png)

>[!TIP]
>
>De identiteitswaarde die u tijdens oefeningen van de Simulatie van de Grafiek invoert moet geen echte identiteitswaarden zijn en kan eenvoudige placeholders zijn.

Wanneer uw eerste identiteit is voltooid, selecteert u het pictogram Toevoegen (**`+`**) om een tweede identiteit toe te voegen.

![De eerste volledig gekwalificeerde identiteit van {Email: tom@acme.com} wordt ingevoerd in het deelvenster Gebeurtenissen van Grafieksimulatie.](../images/graph-simulation/event-one-added.png)

Herhaal vervolgens dezelfde stappen en voeg een tweede identiteit toe. Twee volledig gekwalificeerde identiteiten zijn vereist om een identiteitsgrafiek te produceren. In het onderstaande voorbeeld wordt een ECID toegevoegd als een naamruimte en krijgt een waarde van `111`. Selecteer **[!UICONTROL Save]**.

![Een tweede identiteit van {ECID: 111} wordt toegevoegd aan gebeurtenis nr. 1.](../images/graph-simulation/first-event.png)

De [!UICONTROL Events] interface werkt bij om uw eerste gebeurtenis weer te geven, die in dit geval: `{Email: tom@acme.com, ECID: 111}`.

![De bijgewerkte gebeurtenisinterface met {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Herhaal vervolgens dezelfde stappen om een tweede gebeurtenis toe te voegen. Voor gebeurtenis nr. 2 voegt u `{Email: summer@acme.com}` als uw eerste identiteit en voeg vervolgens hetzelfde toe `{ECID: 111}` als tweede identiteit, waardoor een tweede gebeurtenis wordt gecreëerd van: `{Email: summer@acme.com}, {ECID: 111}`. Als u klaar bent, hebt u twee gebeurtenissen nodig, één voor `{Email: tom@acme.com, ECID: 111}` en één voor `{Email: summer@acme.com}, {ECID: 111}`.

![De bijgewerkte gebeurtenisinterface met twee gebeurtenissen.](../images/graph-simulation/two-events.png)

### Voorbeeld laden

+++Selecteren om stappen weer te geven voor het gebruik van vooraf geladen grafiekvoorbeelden

Als u een voorbeeldgrafiek wilt instellen met een vooraf geconfigureerd algoritme, selecteert u **[!UICONTROL Load example]**. Er verschijnt een pop-upvenster met beschikbare grafiekscenario&#39;s waaruit u kunt kiezen:

| Voorbeeldgrafiek | Beschrijving | Voorbeeld |
| --- | --- | --- |
| Gedeeld apparaat | Het gedeelde apparaat verwijst naar scenario&#39;s waar twee verschillende gebruikers login aan het zelfde enige apparaat. | Een man en vrouw delen een iPad voor internetsurfen en e-commerce. |
| Ongeldige (niet-unieke) telefoon | Ongeldige of niet-unieke telefoon verwijst naar scenario&#39;s waar twee verschillende gebruikers het zelfde telefoonaantal gebruiken om een rekening tot stand te brengen. | Een moeder en haar dochter gebruiken hun gedeelde huistelefoonnummer om zich aan te melden voor e-commerceaccounts. |
| Ongeldige identiteitswaarden | De &quot;slechte&quot;identiteitswaarden verwijzen naar scenario&#39;s waar de Dienst van de Identiteit niet-unieke IDFAs wegens onjuiste implementatie produceert. | WebSDK verzendt ten onrechte een `user_null` waarde voor elke gebeurtenis vanwege problemen met de implementatie van code. |

Selecteer om het even welke opties om de Simulatie van de Grafiek met pre-gevormde gebeurtenissen en algoritme te laden. U kunt nog verdere configuraties aan om het even welke vooraf geladen voorbeelden van grafiekscenario&#39;s maken.

Selecteer **[!UICONTROL Simulate]**.

+++

### Tekstversie gebruiken

+++Selecteren om stappen weer te geven voor het gebruik van tekstversie

U kunt de tekstmodus ook gebruiken om gebeurtenissen te configureren. Als u de tekstmodus wilt gebruiken, selecteert u het tandwiel (?) en selecteer vervolgens **[!UICONTROL Text (Advanced users)]**.

U kunt uw identiteiten handmatig invoeren in de tekstmodus. Een dubbele punt gebruiken (`:`) om de identiteitswaarde te onderscheiden die overeenkomt met de naamruimte die u invoert en vervolgens een komma (`,`) om uw identiteiten te scheiden. Als u verschillende gebeurtenissen van elkaar wilt onderscheiden, gebruikt u een nieuwe regel voor elke gebeurtenis.

+++

### Gebeurtenis Edit

Als u een gebeurtenis wilt bewerken, selecteert u de ovalen (`...`) naast een bepaalde gebeurtenis en selecteer vervolgens **[!UICONTROL Edit]**.

### Gebeurtenis delete

Als u een gebeurtenis wilt verwijderen, selecteert u de ovalen (`...`) naast een bepaalde gebeurtenis en selecteer vervolgens **[!UICONTROL Delete]**.

## Algoritme configureren

Het algoritme dat u vormt zal dicteren hoe de Dienst van de Identiteit de namespaces behandelt die u in uw gebeurtenissen invoerde. Om het even welke configuratie die u in UI opstelde van de Simulatie van de Grafiek wordt niet bewaard in identiteitsmontages.

Selecteer eerst Toevoegen (`+`) in de onderhoek van het configuratievenster voor algoritmen.



Er wordt een lege configuratieregel weergegeven. Voer eerst dezelfde naamruimte in als u hebt gebruikt voor uw gebeurtenissen. In dit geval begint u met het invoeren van de CRM-id. Nadat u de naamruimte hebt ingevoerd, worden de kolommen voor [!UICONTROL Identity Symbol] en [!UICONTROL Identity Type] automatisch vullen.



Herhaal vervolgens dezelfde stappen en voeg uw tweede naamruimte toe, in dit geval de ECID. Zodra al uw namespaces zijn ingegaan, kunt u beginnen hun prioriteiten en uniciteit te vormen.

* **Prioriteit naamruimte**: De prioriteit van een naamruimte bepaalt het relatieve belang ten opzichte van de andere naamruimten in een bepaalde identiteitsgrafiek. Als uw identiteitsgrafiek bijvoorbeeld vier verschillende naamruimten heeft: CRM ID, ECID, Email en Apple IDFA, kunt u prioriteiten configureren om een volgorde van belang voor de vier naamruimten te bepalen. (WAAROM TOEVOEGEN)
* **Unieke naamruimte**: Als een naamruimte als uniek is aangewezen, genereert Identity Service grafieken met het voorbehoud dat slechts één identiteit met een bepaalde unieke naamruimte kan bestaan. Bijvoorbeeld, als identiteitskaart van CRM als unieke namespace wordt aangewezen, dan kan een grafiek één identiteit met identiteitskaart van CRM slechts hebben. Als er meer dan één identiteit met identiteitskaart van CRM namespace is, dan zal de oudste verbinding worden verwijderd.

Om namespace prioriteit te vormen, selecteer en sleep de namespace rijen aan de prioritaire orde die u wilt, met de hoogste rij die hogere prioriteit vertegenwoordigt en de onderste rij die lagere prioriteit vertegenwoordigt. Als u een naamruimte als uniek wilt aanwijzen, selecteert u de optie **[!UICONTROL Unique Per Graph]** selectievakje.



Selecteer **[!UICONTROL Simulate]**.

## Gesimuleerde grafiek weergeven

De [!UICONTROL Simulated Graph] geeft de gegenereerde identiteitsgrafiek(en) weer op basis van de gebeurtenissen die u hebt toegevoegd en het algoritme dat u hebt geconfigureerd.

| Grafiekpictogrammen | Beschrijving |
| --- | --- |
| Effen lijn | Een solide lijn vormt een vaststaand verband tussen twee identiteiten. |
| Stippellijn | Een stippellijn vertegenwoordigt een verwijderde koppeling tussen twee identiteiten. |
| Aantal op regel | Een getal op een regel geeft de tijdstempel aan van wanneer die bepaalde koppeling is gegenereerd. Het laagste getal (1) geeft de oudste ingestelde koppeling aan. |

In de onderstaande voorbeeldgrafiek bestaat een stippellijn tussen `{CRM ID: Tom}` en `{ECID: 111}` om de volgende redenen:

* CRM ID werd aangewezen als uniek tijdens de stap van de algoritmeconfiguratie. Daarom kan slechts één identiteit met een identiteitskaart van CRM namespace in een grafiek bestaan.
* Het verband tussen `{CRM ID: Tom}` en `{ECID: 111}` was de eerste vastgestelde identiteit (gebeurtenis nr. 1). Het is de oudste schakel en wordt daarom verwijderd.

## Voorbeeldgrafiekscenario&#39;s

>[!NOTE]
>
>&#39;CRM ID&#39; is een aangepaste naamruimte. Daarom vereisen de voorbeelden hieronder u om een douanenamespace met een vertoningsnaam en identiteitssymbool van &quot;identiteitskaart van CRM te creëren.

De volgende sectievoorbeelden van grafiekscenario&#39;s u met de Simulatie van de Grafiek zou kunnen ontmoeten.

### Alleen CRM-id

Gebeurtenissen:

* CRM-ID: Tom, ECID: 111

Algoritmconfiguratie:

| Prioriteit | Weergavenaam | Identiteitssymbool | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- | --- |
| 1 | CRM-id | CRM-id | CROSS_DEVICE | Ja |
| 2 | ECID | ECID | COOKIE | NEE |

+++Selecteren om gesimuleerde grafiek weer te geven

+++

### CRM-id met gehashte e-mail

In dit scenario wordt een CRM-id opgenomen die zowel online (ervaringsgebeurtenis) als offline (profielrecord) gegevens vertegenwoordigt. Dit scenario impliceert ook de opname van een gehakt e-mail, die een andere namespace vertegenwoordigt die in de het recorddataset van CRM samen met identiteitskaart van CRM wordt verzonden.

Gebeurtenissen:

* CRM-id: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRM-ID: Tom, ECID: 111
* CRM-id: zomer, email_LC_SHA256: zomer<span>@acme.com
* CRM-ID: Summer, ECID: 222

Algoritmconfiguratie:

| Prioriteit | Weergavenaam | Identiteitssymbool | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- | --- |
| 1 | CRM-id | CRM-id | CROSS_DEVICE | Ja |
| 2 | E-mails (SHA256, verlaagd) | Email_LC_SHA256 | E-mail | NEE |
| 3 | ECID | ECID | COOKIE | NEE |

+++Selecteren om gesimuleerde grafiek weer te geven

+++

### CRM-id met hashed-e-mail, hashtelefoon, GAID en IDFA

Gebeurtenissen:

* CRM-id: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRM-ID: Tom, ECID: 111
* CRM-ID: Tom, ECID: 222, IDFA: A-A-A
* CRM-id: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM-ID: Summer, ECID: 333
* CRM-ID: Summer, ECID: 444, GAID:B-B-B

Algoritmconfiguratie:

| Prioriteit | Weergavenaam | Identiteitssymbool | Identiteitstype | Uniek per grafiek |
| ---| --- | --- | --- | --- |
| 1 | CRM-id | CRM-id | CROSS_DEVICE | Ja |
| 2 | E-mails (SHA256, verlaagd) | Email_LC_SHA256 | E-mail | NEE |
| 3 | Telefoon (SHA256) | Phone_SHA256 | Telefoon | NEE |
| 4 | Google-advertentie-ID (GAID) | GAID | APPARAAT | NEE |
| 5 | Apple IDFA (ID voor Apple) | IDFA | APPARAAT | NEE |
| 6 | ECID | ECID | COOKIE | NEE |

+++Selecteren om gesimuleerde grafiek weer te geven

+++