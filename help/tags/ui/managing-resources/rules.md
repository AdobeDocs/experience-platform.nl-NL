---
title: Regels
description: Leer hoe tagextensies werken in Adobe Experience Platform.
exl-id: 2beca2c9-72b7-4ea0-a166-50a3b8edb9cd
source-git-commit: 85413e4a8b604dd9111ca4d47ad6a1ec49d8f547
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 0%

---

# Regels

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Tags in Adobe Experience Platform volgen een op regels gebaseerd systeem. Zij zoeken gebruikersinteractie en bijbehorende gegevens. Wanneer aan de criteria die in uw regels worden geschetst wordt voldaan, teweegbrengt de regel de uitbreiding, het manuscript, of cliënt-zijcode in werking u identificeerde.

Bouw regels om de gegevens en de functionaliteit van marketing en advertentietechnologie te integreren die ongelijksoortige producten in één enkele oplossing verenigt.

## Regelstructuur

**Gebeurtenissen (indien):** De gebeurtenis is wat u de regel wilt zoeken. Dit wordt bepaald door een gebeurtenis, om het even welke toepasselijke voorwaarden, en om het even welke uitzonderingen te kiezen.

**Handelingen (vervolgens):** Triggers vinden plaats nadat de gebeurtenissen van een regel hebben plaatsgevonden en aan alle voorwaarden is voldaan. Een labelregel kan zoveel afzonderlijke acties activeren als u wilt en u kunt de volgorde bepalen waarin deze acties plaatsvinden. Bijvoorbeeld, kan één enkele regel voor e-commerce bedankt pagina uw analysehulpmiddelen en derdetags van één enkele regel teweegbrengen. Het is niet nodig voor elke extensie of tag afzonderlijke regels te maken.

U kunt meer gebeurtenistypen toevoegen. De veelvoudige gebeurtenissen worden aangesloten bij met OF, zodat zullen de voorwaarden van de regel worden geëvalueerd als om het even welke gebeurtenissen worden voldaan aan.

>[!IMPORTANT]
>
>Wijzigingen worden pas van kracht nadat ze [gepubliceerd](../publishing/overview.md).

### Gebeurtenissen en voorwaarden (indien van toepassing)

Gebeurtenissen met alle voorwaarden zijn de *Indien* deel van een regel.

Als een opgegeven gebeurtenis plaatsvindt, worden de voorwaarden geëvalueerd, worden de opgegeven handelingen zo nodig uitgevoerd.

* **Gebeurtenissen**: Geef een of meer gebeurtenissen op die moeten plaatsvinden om de regel te activeren. Bij meerdere gebeurtenissen hoort een OR. Om het even welke gespecificeerde gebeurtenissen zullen de regel teweegbrengen.

* **Voorwaarden**: Verfijn de gebeurtenis door om het even welke voorwaarden te vormen die voor een gebeurtenis waar moeten zijn om de regel teweeg te brengen. Een uitzondering wordt gedefinieerd als een NOT-voorwaarde. De veelvoudige voorwaarden worden aangesloten bij door EN.

Welke gebeurtenissen beschikbaar zijn, is afhankelijk van de extensies die zijn geïnstalleerd. Voor informatie over de gebeurtenissen in de extensie Core raadpleegt u [Gebeurtenistypen van de kernextensie](../../extensions/web/core/overview.md#core-extension-event-types).

### Handelingen (dan)

Acties zijn *Vervolgens* deel van een regel. Zij bepalen wat u wilt gebeuren wanneer de regel loopt. Wanneer een gebeurtenis in werking wordt gesteld, als de voorwaarden aan waar evalueren en de uitzonderingen aan vals evalueren, worden de acties uitgevoerd. U kunt acties slepen en neerzetten om ze naar wens te bestellen.

## Een regel maken

Maak een regel door op te geven welke handelingen worden uitgevoerd als aan een voorwaarde wordt voldaan.

1. Open de [!UICONTROL Rules] tab, dan selecteren **[!UICONTROL Create New Rule]**.

   ![](../../images/launch-rule-builder.jpg)

1. Geef de regel een naam.
1. Gebeurtenissen selecteren **[!UICONTROL Add]** pictogram.
1. Kies uw extensie en een van de gebeurtenistypen die beschikbaar zijn voor die extensie en configureer vervolgens de instellingen voor de gebeurtenis.

   ![](../../images/rule-event-config.png)

   Welke gebeurtenistypen beschikbaar zijn, is afhankelijk van de extensie die u hebt geselecteerd. Gebeurtenisinstellingen verschillen afhankelijk van het gebeurtenistype. Sommige gebeurtenissen hebben geen instellingen die moeten worden geconfigureerd.

   >[!IMPORTANT]
   >
   >In een client-side regel worden gegevenselementen samengevoegd met een `%` aan het begin en einde van de naam van het gegevenselement. Bijvoorbeeld, `%viewportHeight%`. In een gebeurtenis-door:sturen regel, worden de gegevenselementen samengevoegd met `{{` aan het begin en `}}` aan het einde van de naam van het gegevenselement. Bijvoorbeeld, `{{viewportHeight}}`.

   Als u wilt verwijzen naar gegevens van het Edge-netwerk, moet het pad naar het gegevenselement `arc.event._<element>_`.

   `arc` staat voor Adobe Response Context.

   Bijvoorbeeld: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Als dit pad onjuist is opgegeven, worden geen gegevens verzameld.

1. Stel de parameter Volgorde in en selecteer vervolgens **[!UICONTROL Keep Changes]**.

   De standaardvolgorde voor alle regelcomponenten is 50. Als u wilt dat er een sneller verloop is, geef dan een getal van minder dan 50.

   * Volgorde van uitvoering is volgorde van getallen. 1 komt voor 3. 3 komt voor 10. 10 komt vóór 100, enz.
   * Regels die dezelfde volgorde hebben, worden in geen enkele volgorde uitgevoerd.
   * Regels worden op volgorde afgegaan, maar hoeven niet noodzakelijkerwijs in dezelfde volgorde af te lopen. Als Regel A en Regel B een gebeurtenis delen, en u orde toewijst zodat Regel A eerst komt, dan als Regel A iets asynchroon doet, is er geen garantie dat Regel A eindigt alvorens Regel B begint.

      Als u het later wilt uitvoeren, geef het een aantal hoger dan 50. Voor meer informatie over het opdracht geven tot, zie [Regelvolgorde](rules.md#rule-ordering).

1. Selecteer de voorwaarden **[!UICONTROL Add]** en kiest u vervolgens een logicatype, extensie, type voorwaarde en configureert u de instellingen voor uw voorwaarde. Selecteer vervolgens **[!UICONTROL Keep Changes]**.

   ![](../../images/condition-settings.png)

   De beschikbare voorwaardetypen hangen van de uitbreiding af u hebt geselecteerd. Voorwaarde-instellingen verschillen afhankelijk van het type voorwaarde.

   Type logica:

   * Met het gewone logische type kunnen handelingen worden uitgevoerd als aan de voorwaarde is voldaan
   * Het type van de logica van de uitzondering verhindert acties worden uitgevoerd als aan de voorwaarde wordt voldaan

   (Geavanceerd) Time-out: Deze optie is beschikbaar wanneer het rangschikken van de regelcomponent op uw bezit wordt toegelaten. Dit kenmerk definieert de maximale hoeveelheid tijd die de voorwaarde mag uitvoeren. Als de onderbreking wordt bereikt, ontbreekt de voorwaarde en de rest voorwaarden en de acties van de regel zullen uit de verwerkingsrij worden verwijderd. De standaardwaarde is 2000 ms.

   U kunt zoveel voorwaarden toevoegen als u wilt. De veelvoudige voorwaarden binnen de zelfde regel worden aangesloten bij EN.

1. Handelingen selecteren **[!UICONTROL Add]** het pictogram, dan kies uw uitbreiding en één van de actietypes beschikbaar voor die uitbreiding, vorm de montages voor de actie, dan selecteren **[!UICONTROL Keep Changes]**.

   ![](../../images/action-settings.png)

   Welke handelingstypen beschikbaar zijn, is afhankelijk van de extensie die u hebt geselecteerd. De instellingen voor handelingen verschillen afhankelijk van het type handeling.

   (Geavanceerd) Wacht tot volgende handeling wordt uitgevoerd: Deze optie is beschikbaar wanneer het rangschikken van de regelcomponent op uw bezit wordt toegelaten. Als deze optie is ingeschakeld, worden de volgende handelingen pas door de labels aangeroepen wanneer deze zijn voltooid. Als deze optie is uitgeschakeld, wordt de volgende actie direct uitgevoerd. De standaardwaarde is **[!UICONTROL Checked]**.

   (Geavanceerd) Time-out: Deze optie is beschikbaar wanneer het rangschikken van de regelcomponent op uw bezit wordt toegelaten. Hiermee wordt de maximale hoeveelheid tijd gedefinieerd die de handeling mag voltooien. Als de onderbreking wordt bereikt, ontbreekt de actie en om het even welke verdere acties voor deze regel zullen worden verwijderd uit de verwerkingsrij. De standaardwaarde is 2000 ms.


1. Controleer uw regel en selecteer **[!UICONTROL Save Rule]**.

   Later, wanneer u [publish](../publishing/overview.md), zult u deze regel aan een bibliotheek toevoegen en het opstellen.

Wanneer u regels maakt of bewerkt, kunt u deze opslaan en samenstellen op uw [actieve bibliotheek](../publishing/libraries.md#active-library). Hiermee slaat u de wijziging onmiddellijk op in uw bibliotheek en wordt een build uitgevoerd. De status van de build wordt weergegeven.

## Regelvolgorde {#rule-ordering}

De orde die van de regel toestaat u om de orde van uitvoering voor regels te controleren die een gebeurtenis delen. Elke regel bevat een geheel dat zijn ordeprioriteit bepaalt (de standaardwaarde is 50). Regels die lagere waarden voor hun volgorde bevatten, worden uitgevoerd vóór regels met hogere waarden.

Overweeg een reeks van vijf regels die allen een gebeurtenis delen en allen standaardprioriteit hebben:

* Als er een regel is die u als laatste wilt uitvoeren, kunt u die ene regelcomponent bewerken en er een getal hoger dan 50 (bijvoorbeeld 60) aan geven.
* Als er een regel is die u het eerst wilt uitvoeren, kunt u die ene regelcomponent bewerken en er een getal lager dan 50 (bijvoorbeeld 40) aan geven.

>[!NOTE]
>
>Uiteindelijk ligt de verantwoordelijkheid voor het uitvoeren van handelingen in volgorde bij de extensieontwikkelaar van het gebeurtenistype dat u gebruikt. Adobe-extensieontwikkelaars zorgen ervoor dat hun extensies werken zoals u wilt. Adobe biedt ontwikkelaars van extensies van derden aanwijzingen om dit naar behoren te doen, maar kan niet garanderen hoe deze richtlijnen worden gevolgd.

Het wordt ten zeerste aanbevolen om uw regels te bestellen met positieve getallen tussen 1 en 100 (de standaardwaarde is 50). Aangezien de regelorde manueel moet worden gehandhaafd, is het beste praktijken om uw het bestel zo eenvoudig mogelijk te houden. Als er randgevallen zijn waarin deze beperking te beperkt is, ondersteunen de labels volgordenummers +/- 2,147,483,648.

### Regelafhandeling op de client

De ladingsorde voor regels hangt af van of de regelactie met JavaScript, HTML, of andere cliënt-zijcode wordt gevormd, en of de regels een pagina bodem of hoogste gebeurtenis, of een verschillend type van gebeurtenis gebruiken.

U kunt `document.write` binnen uw douanescripts ongeacht de gebeurtenissen die voor de regel worden gevormd.

U kunt verschillende aangepaste codetypen onder elkaar bestellen. U kunt nu bijvoorbeeld een aangepaste JavaScript-codehandeling hebben, vervolgens een aangepaste code-actie HTML en vervolgens een aangepaste code-actie JavaScript. Tags zorgen ervoor dat ze in die volgorde worden uitgevoerd.

## Regelbundeling

Regelgebeurtenissen en -voorwaarden worden altijd gebundeld in de hoofdtagbibliotheek. Acties kunnen in de hoofdbibliotheek worden gebundeld of te laat worden geladen als subbronnen. Of de acties gebundeld zijn of niet wordt bepaald door het gebeurtenistype van de regel.

### Regels met gebeurtenissen &quot;Core - Library Loaded&quot; of &quot;Core - Page Top&quot;

Deze gebeurtenissen moeten bijna altijd worden uitgevoerd (tenzij de omstandigheden false opleveren). Voor efficiëntie worden ze gebundeld in de hoofdbibliotheek, het bestand waarnaar wordt verwezen door uw insluitcode.

* **JavaScript:** Het JavaScript is ingesloten in de bibliotheek met hoofdtags. Het aangepaste script wordt ondergebracht in een scripttag en naar het document geschreven met behulp van `document.write`. Als de regel meerdere aangepaste scripts heeft, worden deze op volgorde geschreven.

* **HTML:** De HTML wordt ingesloten in de hoofdtagbibliotheek. `document.write` wordt gebruikt om de HTML naar het document te schrijven. Als de regel meerdere aangepaste scripts heeft, worden deze op volgorde geschreven.

### Regels met andere gebeurtenissen

Adobe kan niet garanderen dat andere regels daadwerkelijk in werking zullen treden en dat hun actiecode nodig zal zijn. Daarom worden de acties voor alle gebeurtenistypen die hierboven niet worden vermeld, niet in de hoofdbibliotheek verpakt. In plaats daarvan worden ze opgeslagen als subbronnen en wordt zo nodig verwezen door de hoofdbibliotheek.

* **JavaScript:** Het JavaScript wordt vanaf de server als normale tekst geladen, in een scripttag opgenomen en met Postscript aan het document toegevoegd. Als de regel meerdere aangepaste JavaScript-scripts heeft, worden deze parallel van de server geladen, maar in dezelfde volgorde uitgevoerd als in de regel.
* **HTML:** De HTML wordt vanaf de server geladen en met Postscript aan het document toegevoegd. Als de regel veelvoudige manuscripten van douaneHTML heeft, worden zij geladen parallel van de server, maar in de zelfde orde uitgevoerd die in de regel werd gevormd.

## Reeksen van componenten van de regel {#sequencing}

Het gedrag van de runtimeomgeving hangt af van het feit of **[!UICONTROL Run rule components in sequence]** is aan of uit voor uw eigenschap. Dit het plaatsen bepaalt of de componenten van een regel parallel (asynchroon) kunnen worden geëvalueerd of of zij in opeenvolging moeten worden geëvalueerd.

>[!IMPORTANT]
>
>Dit het plaatsen bepaalt slechts hoe de voorwaarden en de acties binnen elke regel worden geëvalueerd, en beïnvloedt niet de opeenvolging waarin de regels zelf op uw bezit worden uitgevoerd. Zie de vorige sectie over [regelvolgorde](#rule-ordering) voor meer informatie over hoe te om de uitvoeringsorde voor veelvoudige regels te bepalen.
>
>In [gebeurtenis doorsturen](../event-forwarding/overview.md) eigenschappen, worden regelhandelingen altijd opeenvolgend uitgevoerd en deze instelling is niet beschikbaar. Zorg ervoor de orde correct is wanneer u de regel creeert.

### Ingeschakeld

Als het plaatsen wordt toegelaten wanneer een gebeurtenis bij runtime wordt teweeggebracht, worden de de voorwaarden en de acties van de regel toegevoegd aan een verwerkingsrij (die op de orde wordt gebaseerd u) hebt bepaald en verwerkt één voor één op een &quot;eerste binnen, eerste uit&quot;basis (FIFO). De regel wacht tot de component is voltooid voordat naar de volgende wordt gegaan.

Als een voorwaarde als vals evalueert of zijn bepaalde onderbreking bereikt, worden de verdere voorwaarden en de acties van die regel verwijderd uit de rij.

Als een actie ontbreekt of zijn bepaalde onderbreking bereikt, worden de verdere acties van die regel verwijderd uit de rij.

### Uitgeschakeld

Als deze optie is uitgeschakeld en een gebeurtenis wordt geactiveerd tijdens uitvoering, worden de voorwaarden van de regel direct geëvalueerd. Meerdere omstandigheden worden parallel geëvalueerd.

Wanneer alle voorwaarden true retourneren (en uitzonderingen false retourneren), worden de handelingen van de regel onmiddellijk uitgevoerd. De handelingen worden op volgorde aangeroepen, maar de tags wachten niet tot de ene handeling is voltooid voordat de volgende wordt aangeroepen. Als uw acties synchroon zijn, worden ze nog steeds op volgorde uitgevoerd. Als een of meer acties asynchroon zijn, worden sommige acties parallel uitgevoerd.
