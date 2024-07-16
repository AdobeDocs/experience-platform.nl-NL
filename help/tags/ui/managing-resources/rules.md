---
title: Regels
description: Leer hoe tagextensies werken in Adobe Experience Platform.
exl-id: 2beca2c9-72b7-4ea0-a166-50a3b8edb9cd
source-git-commit: 77190e4acf7aad448bbfdebd8ada4dbe9a55f8e0
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 0%

---

# Regels

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Tags in Adobe Experience Platform worden gebaseerd op een systeem dat is gebaseerd op regels. Ze zoeken naar gebruikersinteractie en bijbehorende gegevens. Wanneer wordt voldaan aan de criteria in uw regels, wordt de door u geïdentificeerde extensie-, script- of client-side code geactiveerd.

Stel regels samen voor de integratie van de gegevens en functionaliteit van marketing- en advertentietechnologie waarmee de afzonderlijke producten in één oplossing worden samengevoegd.

## Regelstructuur

**Gebeurtenissen (als):** de gebeurtenis is wat u de regel wilt zoeken. Dit wordt bepaald door een gebeurtenis, om het even welke toepasselijke voorwaarden, en om het even welke uitzonderingen te kiezen.

**Acties (toen):** de Trekkers komen voor nadat de gebeurtenissen van een regel plaatsvinden en alle voorwaarden worden voldaan. Een labelregel kan zoveel afzonderlijke acties activeren als u wilt en u kunt de volgorde bepalen waarin deze acties plaatsvinden. Bijvoorbeeld, kan één enkele regel voor e-commerce bedankt pagina uw analysehulpmiddelen en derdetags van één enkele regel teweegbrengen. Het is niet nodig voor elke extensie of tag afzonderlijke regels te maken.

U kunt meer gebeurtenistypen toevoegen. De veelvoudige gebeurtenissen worden aangesloten bij met OF, zodat zullen de voorwaarden van de regel worden geëvalueerd als om het even welke gebeurtenissen worden voldaan aan.

>[!IMPORTANT]
>
>De veranderingen treden niet van kracht tot zij [ worden gepubliceerd ](../publishing/overview.md).

### Gebeurtenissen en voorwaarden (indien van toepassing)

Gebeurtenissen met om het even welke voorwaarden zijn *als* gedeelte van een regel.

Als een opgegeven gebeurtenis plaatsvindt, worden de voorwaarden geëvalueerd en vinden de opgegeven handelingen plaats, indien nodig.

* **Gebeurtenissen**: specificeer één of meerdere gebeurtenissen die moeten plaatsvinden om de regel teweeg te brengen. Bij meerdere gebeurtenissen hoort een OR. Om het even welke gespecificeerde gebeurtenissen zullen de regel teweegbrengen.

* **Voorwaarden**: Verklein de gebeurtenis door om het even welke voorwaarden te vormen die voor een gebeurtenis waar moeten zijn om de regel teweeg te brengen. Een uitzondering wordt gedefinieerd als een NIET-voorwaarde. Meerdere voorwaarden worden samengevoegd door een AND.

Welke gebeurtenissen beschikbaar zijn, zijn afhankelijk van de geïnstalleerde extensies. Voor informatie over de gebeurtenissen in de uitbreiding van de Kern, zie [ de types van de uitbreidingsgebeurtenis van de Kern ](../../extensions/client/core/overview.md#core-extension-event-types).

### Handelingen (dan)

De acties zijn het *toen* gedeelte van een regel. Zij bepalen wat u wilt gebeuren wanneer de regel loopt. Wanneer een gebeurtenis in werking wordt gesteld, als de voorwaarden aan waar evalueren en de uitzonderingen aan vals evalueren, worden de acties uitgevoerd. U kunt handelingen slepen en neerzetten om ze naar wens te orden.

## Een regel maken

Maak een regel door op te geven welke handelingen worden uitgevoerd als aan een voorwaarde wordt voldaan.

>[!TIP]
>
>U kunt extra bronnen weergeven die beschikbaar zijn voor meer informatie over deze functie door een info](../../images/ui/event-forwarding/overview/about.png) over te selecteren ![in het rechterdeelvenster.

1. Open het [!UICONTROL Rules] tabblad en selecteer **[!UICONTROL Create New Rule]** vervolgens .

   ![Het tabblad Regels waarin het naamveld wordt gemarkeerd.](../../images/launch-rule-builder.png)

1. Geef de regel een naam.
1. Selecteer het pictogram Gebeurtenissen **[!UICONTROL Add]** .
1. Selecteer uw extensie en een van de beschikbare gebeurtenistypen voor de extensie en configureer vervolgens de instellingen voor de gebeurtenis.

   ![Bepaalt de configuratiepagina voor gebeurtenissen.](../../images/rule-event-config.png)

   De beschikbare gebeurtenistypen zijn afhankelijk van de extensie die u hebt geselecteerd. De gebeurtenisinstellingen verschillen al naar gelang het type gebeurtenis. Sommige gebeurtenissen hebben geen instellingen die moeten worden geconfigureerd.

   >[!IMPORTANT]
   >
   >In een client-side regel worden gegevenselementen samengevoegd met een `%` aan het begin en einde van de naam van het gegevenselement. Bijvoorbeeld `%viewportHeight%` . In een gebeurtenis-door:sturen regel, worden de gegevenselementen samengevoegd met `{{` aan het begin en `}}` aan het eind van de naam van het gegevenselement. Bijvoorbeeld `{{viewportHeight}}` .

   Als u wilt verwijzen naar gegevens van het Edge-netwerk, moet het pad voor het gegevenselement `arc.event._<element>_` zijn.

   `arc` staat voor de context van de Reactie van de Adobe.

   Bijvoorbeeld: `arc.event.xdm.web.webPageDetails.URL`

   >[!IMPORTANT]
   >
   >Als dit pad onjuist is opgegeven, worden geen gegevens verzameld.

1. Stel de parameter Order in en selecteer vervolgens **[!UICONTROL Keep Changes]** .

   De standaardvolgorde voor alle regelcomponenten is 50. Als u wilt dat er een sneller verloop is, geef dan een getal van minder dan 50.

   * Volgorde van uitvoering is volgorde van getallen. 1 komt voor 3. 3 komt voor 10. 10 komt vóór 100, enz.
   * Regels die dezelfde volgorde hebben, worden in geen enkele volgorde uitgevoerd.
   * Regels worden op volgorde afgegaan, maar hoeven niet noodzakelijkerwijs in dezelfde volgorde af te lopen. Als Regel A en Regel B een gebeurtenis delen, en u orde toewijst zodat Regel A eerst komt, dan als Regel A iets asynchroon doet, is er geen garantie dat Regel A eindigt alvorens Regel B begint.

     Als je wilt dat het later wordt uitgevoerd, geef je het een getal dat hoger is dan 50. Zie [Regelbestelling voor meer informatie over bestellen](rules.md#rule-ordering).

1. Selecteer het pictogram Voorwaarden **[!UICONTROL Add]** en selecteer vervolgens een logicatype, extensie, type voorwaarde en configureer de instellingen voor uw voorwaarde. Selecteer vervolgens **[!UICONTROL Keep Changes]** .

   ![ de configuratiepagina van de voorwaardenconfiguratie van Regels.](../../images/condition-settings.png)

   De beschikbare voorwaardetypen hangen van de uitbreiding af u hebt geselecteerd. Voorwaarde-instellingen verschillen op basis van het type voorwaarde.

   Type logica:

   * Met het gewone logische type kunnen handelingen worden uitgevoerd als aan de voorwaarde is voldaan
   * Het type van de logica van de uitzondering verhindert acties worden uitgevoerd als aan de voorwaarde wordt voldaan

   (Geavanceerd) Onderbreking: deze optie is beschikbaar wanneer de regelcomponent het rangschikken op uw bezit wordt toegelaten. Dit kenmerk definieert de maximale hoeveelheid tijd die de voorwaarde mag uitvoeren. Als de onderbreking wordt bereikt, ontbreekt de voorwaarde en de rest voorwaarden en de acties van de regel zullen uit de verwerkingsrij worden verwijderd. De standaardwaarde is 2000 ms.

   U kunt zoveel voorwaarden toevoegen als u wilt. De veelvoudige voorwaarden binnen de zelfde regel worden aangesloten bij EN.

1. Selecteer het pictogram Handelingen **[!UICONTROL Add]** , selecteer de extensie en een van de typen handelingen die beschikbaar zijn voor die extensie, configureer de instellingen voor de handeling en selecteer **[!UICONTROL Keep Changes]** vervolgens .

   ![Bepaalt de configuratiepagina voor handelingen.](../../images/action-settings.png)

   De beschikbare typen handelingen zijn afhankelijk van de geselecteerde extensie. De instellingen voor handelingen verschillen al naar gelang het type handeling.

   (Geavanceerd) Wacht tot de volgende handeling is uitgevoerd: deze optie is beschikbaar wanneer sequentiebepaling van regelcomponenten is ingeschakeld voor uw eigenschap. Als deze optie is ingeschakeld, worden de volgende handelingen pas door de labels aangeroepen wanneer deze zijn voltooid. Als deze optie is uitgeschakeld, wordt de volgende actie direct uitgevoerd. De standaardwaarde is **[!UICONTROL Checked]** .

   (Geavanceerd) Onderbreking: deze optie is beschikbaar wanneer de regelcomponent het rangschikken op uw bezit wordt toegelaten. Hiermee wordt de maximale hoeveelheid tijd gedefinieerd die de handeling mag voltooien. Als de onderbreking wordt bereikt, ontbreekt de actie en om het even welke verdere acties voor deze regel zullen worden verwijderd uit de verwerkingsrij. De standaardwaarde is 2000 ms.


1. Controleer uw regel en selecteer vervolgens **[!UICONTROL Save Rule]** .

   Later, wanneer u [ ](../publishing/overview.md) publiceert, zult u deze regel aan een bibliotheek toevoegen en het opstellen.

Wanneer het creëren van of het uitgeven van regels, kunt u sparen en aan uw [ actieve bibliotheek ](../publishing/libraries.md#active-library) bouwen. Hiermee slaat u de wijziging onmiddellijk op in uw bibliotheek en wordt een build uitgevoerd. De status van de build wordt weergegeven.

## Regelvolgorde {#rule-ordering}

De orde die van de regel toestaat u om de orde van uitvoering voor regels te controleren die een gebeurtenis delen. Elke regel bevat een geheel dat zijn ordeprioriteit bepaalt (de standaardwaarde is 50). Regels die lagere waarden voor hun volgorde bevatten, worden uitgevoerd vóór regels met hogere waarden.

Overweeg een reeks van vijf regels die allen een gebeurtenis delen en allen standaardprioriteit hebben:

* Als u een regel als laatste wilt uitvoeren, kunt u die ene regelcomponent bewerken en deze een hoger getal dan 50 geven (bijvoorbeeld 60).
* Als u een regel als eerste wilt uitvoeren, kunt u die ene regelcomponent bewerken en deze een getal geven dat lager is dan 50 (bijvoorbeeld 40).

>[!NOTE]
>
>Uiteindelijk ligt de verantwoordelijkheid voor het uitvoeren van handelingen in volgorde bij de extensieontwikkelaar van het gebeurtenistype dat u gebruikt. Ontwikkelaars van extensies voor Adoben zorgen ervoor dat hun extensies werken zoals bedoeld. Adobe biedt ontwikkelaars van extensies van derden aanwijzingen om dit naar behoren te doen, maar kan niet garanderen hoe deze richtsnoeren worden gevolgd.

Het wordt ten zeerste aanbevolen om uw regels te bestellen met positieve getallen tussen 1 en 100 (de standaardwaarde is 50). Aangezien de regelorde manueel moet worden gehandhaafd, is het beste praktijken om uw het bestel zo eenvoudig mogelijk te houden. Als er randgevallen zijn waarin deze beperking te beperkt is, ondersteunen de labels volgordenummers +/- 2,147,483,648.

### Verwerking van regels aan clientzijde

De volgorde van het laden van regels is afhankelijk van het feit of de regelhandeling is geconfigureerd met JavaScript-, HTML- of andere client-side code en of in de regels een onderste of bovenste gebeurtenis van de pagina wordt gebruikt, of van een ander type gebeurtenis.

U kunt deze scripts in uw aangepaste scripts gebruiken `document.write` ongeacht de gebeurtenissen die voor de regel zijn geconfigureerd.

U kunt verschillende aangepaste codetypen onder elkaar bestellen. U kunt nu bijvoorbeeld een aangepaste JavaScript-codeactie gebruiken, vervolgens een aangepaste HTML-codeactie en vervolgens een aangepaste JavaScript-codeactie. Codes zorgen ervoor dat de bestanden in die volgorde worden uitgevoerd.

## Regelbundeling

Regelgebeurtenissen en -voorwaarden worden altijd gebundeld in de hoofdtagbibliotheek. Handelingen kunnen in de hoofdbibliotheek worden gebundeld of kunnen laat als subbronnen worden geladen als dat nodig is. Of de handelingen worden gebundeld, wordt bepaald door het gebeurtenistype van de regel.

### Regels met de gebeurtenissen &#39;Kern - Bibliotheek geladen&#39; of &#39;Kern - Pagina boven&#39;

Deze gebeurtenissen moeten bijna altijd worden uitgevoerd (tenzij de omstandigheden worden geëvalueerd als onwaar), dus worden ze voor efficiëntie gebundeld in de hoofdbibliotheek, het bestand waarnaar wordt verwezen door uw insluitcode.

* **Javascript:** Het JavaScript is ingesloten in de bibliotheek met hoofdtags. Het aangepaste script wordt ondergebracht in een scripttag en met `document.write` naar het document geschreven. Als de regel meerdere aangepaste scripts heeft, worden deze op volgorde geschreven.

* **HTML:** De HTML is ingesloten in de bibliotheek met hoofdtags. `document.write` wordt gebruikt om de HTML naar het document te schrijven. Als de regel meerdere aangepaste scripts heeft, worden deze in de volgorde geschreven.

### Regels met andere gebeurtenissen

Adobe kan niet garanderen dat er daadwerkelijk andere regels in werking zullen treden en dat hun actiecode nodig zal zijn. Daarom worden de acties voor alle gebeurtenistypen die hierboven niet worden vermeld, niet in de hoofdbibliotheek verpakt. In plaats daarvan worden ze opgeslagen als subbronnen en wordt zo nodig verwezen door de hoofdbibliotheek.

* **JavaScript:** Het JavaScript wordt vanaf de server geladen als gewone tekst, omsloten in een scripttag en met Behulp van Postscribe aan het document toegevoegd. Als de regel meerdere aangepaste JavaScript-scripts heeft, worden deze gelijktijdig vanaf de server geladen, maar uitgevoerd in dezelfde volgorde die in de regel is geconfigureerd.
* **HTML:** De HTML wordt vanaf de server geladen en aan het document toegevoegd met behulp van Postscribe. Als de regel meerdere aangepaste HTML-scripts heeft, worden deze gelijktijdig vanaf de server geladen, maar uitgevoerd in dezelfde volgorde die in de regel is geconfigureerd.

## Sequencing van regelcomponenten {#sequencing}

Het gedrag van de runtime-omgeving is afhankelijk van het feit of **[!UICONTROL Run rule components in sequence]** deze is ingeschakeld voor uw property. Dit het plaatsen bepaalt of de componenten van een regel parallel (asynchroon) kunnen worden geëvalueerd of of zij in opeenvolging moeten worden geëvalueerd.

>[!IMPORTANT]
>
>Dit het plaatsen bepaalt slechts hoe de voorwaarden en de acties binnen elke regel worden geëvalueerd, en beïnvloedt niet de opeenvolging waarin de regels zelf op uw bezit worden uitgevoerd. Verwijs naar de vorige sectie op [ regel die ](#rule-ordering) voor meer informatie opdracht geeft tot hoe te om de uitvoeringsorde voor veelvoudige regels te bepalen.
>
>In [ gebeurtenis die ](../event-forwarding/overview.md) eigenschappen door:sturen, worden de regelacties altijd opeenvolgend uitgevoerd en dit het plaatsen is niet beschikbaar. Controleer of de volgorde correct is wanneer u de regel maakt.

### Ingeschakeld

Als de instelling is ingeschakeld wanneer een gebeurtenis tijdens runtime wordt geactiveerd, worden de voorwaarden en handelingen van de regel toegevoegd aan een verwerkingswachtrij (op basis van de volgorde die u hebt gedefinieerd) en een voor een verwerkt op FIFO-basis (first in, first out). De regel wacht tot de component is voltooid voordat naar de volgende wordt gegaan.

Als een voorwaarde als vals evalueert of zijn bepaalde onderbreking bereikt, worden de verdere voorwaarden en de acties van die regel verwijderd uit de rij.

Als een actie ontbreekt of zijn bepaalde onderbreking bereikt, worden de verdere acties van die regel verwijderd uit de rij.

### Uitgeschakeld

Als deze optie is uitgeschakeld en een gebeurtenis wordt geactiveerd tijdens uitvoering, worden de voorwaarden van de regel direct geëvalueerd. Meerdere omstandigheden worden parallel geëvalueerd.

Wanneer alle voorwaarden true retourneren (en uitzonderingen false retourneren), worden de handelingen van de regel onmiddellijk uitgevoerd. De handelingen worden op volgorde aangeroepen, maar de tags wachten niet tot de ene handeling is voltooid voordat de volgende wordt aangeroepen. Als uw acties synchroon zijn, worden ze nog steeds op volgorde uitgevoerd. Als een of meer acties asynchroon zijn, worden sommige acties parallel uitgevoerd.
