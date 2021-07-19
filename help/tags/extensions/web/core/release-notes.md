---
title: Opmerkingen bij de release Core Extension
description: De nieuwste release bevat informatie over de Core-extensie in Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 1%

---

# Opmerkingen bij de release Core Extension

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

## 20 mei 2021

v2.0.7

* Hiermee wordt een probleem verholpen waarbij muisinteractie op tekstinvoer niet meer correct werkte.
* Hiermee wordt het gebruik van de voorwaarden van de browser en het besturingssysteem afgekeurd.

## 4 mei 2021

v2.0.6

* Kleine update voor het corrigeren van pictogrammen die worden vervormd wanneer de schermgrootte verandert.

## 11 maart 2021

v2.0.5

* Bijgewerkte code in de runtime evaluatie voor gebeurtenissen en acties die een vertragingsoptie hebben, die nu waarden van gegevenselementen die in versie 2.0.4 worden toegevoegd, aan behoorlijk dwingen koorden aan aantallen steunen.

## 9 maart 2021

v2.0.4

* Ondersteuning voor gegevenselement toegevoegd voor verschillende velden - Ondersteuning voor gegevenselement is toegevoegd aan de volgende gebeurtenissen: &#39;Time on Page&#39;, &#39;Enters Viewport&#39;, &#39;Hover&#39; en &#39;Media Time Played&#39;. alsmede de volgende voorwaarden: &#39;Time on Site&#39; en &#39;Value Comparison&#39;
* Hiermee voegt u ondersteuning toe voor standaardgedrag voor ctrl/cmd + klikken en middenmuisklikken bij gebruik van Vertraging koppeling
* **De vertraging van de gemarkeerde koppeling bij de klikgebeurtenis wordt niet meer ondersteund.** - meer informatie is te vinden op de  [gegevensverzamelingsblog ](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/explainer-link-delay/ba-p/398403) voor Adobe Experience Platform

## 6 januari 2021

v1.9.0

* **Nieuwe actie**  &quot;Rechtstreekse aanroep activeren&quot; - De extensie Core bevat nu een nieuw actietype met de naam  `Trigger Direct Call`.  Dit kan worden gebruikt wanneer u een directe vraagregel via een actie van een verschillende regel wilt teweegbrengen. Deze wordt rechtstreeks toegewezen aan de methode `_satellite.track()`. Hartelijk dank voor deze bijdrage.[](https://twitter.com/jexner)

## 8 december 2020

v1.8.4

* Probleem verholpen waarbij een gebruiker de instelling van het CDV niet één keer kon wissen of ongedaan maken.

## 28 juli 2020

v1.8.3

* Probleem verholpen waarbij de CSP één keer werd gelezen bij het opstarten van de extensie in plaats van vers te worden opgehaald tijdens het aanroepen van aangepaste code.

## 13 juli 2020

v1.8.2

* Probleem verholpen waarbij de aangepaste code-actie een fout genereerde voor HTML-code die tokens zonder tagnaam bevat (bijvoorbeeld opmerkingen).

## 10 juli 2020

v1.8.1

* Probleem verholpen waarbij aangepaste HTML-entiteiten in kenmerken van `script`- en `style`-tags niet correct werden gedecodeerd voordat deze naar de pagina werden geschreven.&quot;
* Probleem verholpen waarbij een fout optreedt wanneer een externe aangepaste code-actie geen inhoud bevat. Externe aangepaste code-actie is de actie die wordt geladen vanuit een ander bestand dan de bibliotheek (dit gebeurt wanneer de gebeurtenis die de regel veroorzaakt, niet libraryLoaded of pageBottom is)

## 6 juli 2020

v1.8.0

* **Beloften in Aangepaste code**  - Aangepaste codevoorwaarden en JavaScript-handelingen die niet in het algemene bereik worden uitgevoerd, kunnen nu Promises retourneren.  U kunt deze gebruiken om volgende voorwaarden en handelingen te laten wachten tot een asynchroon proces in de aangepaste code is voltooid voordat u naar het volgende item gaat.
* **Callbacks in Acties**  van de Code van de Douane van HTML - u kunt het zelfde ding in de acties van de Code van de Douane van HTML bereiken gebruikend  `onCustomCodeSuccess()` en  `onCustomCodeFailure()` callbacks.

Raadpleeg de [Referentie voor kernextensie](./overview.md) in Voorwaarden > Aangepaste code en handelingen > Aangepaste code voor meer informatie.

## 7 april 2020

v1.7.3

* **Verhoging**  van de lengte van tekstvelden - De invoervelden voor tekst zijn gewijzigd in een flex-indeling om de schermbreedte van de gebruiker beter te kunnen gebruiken en om meer ruimte te geven voor langere tekstreeksen.

## 1 november 2019

v1.7.0

* **Toegang tot  `event` Variabele binnen het Element**  van de Gegevens van de Code van de Douane - u kunt de gebeurtenis van binnen een element van de douanecodegegevens nu van verwijzingen voorzien wanneer looppas binnen de context van een regel. Het object bevat nuttige informatie over de gebeurtenis die de regel heeft geactiveerd. Hartelijk dank voor deze bijdrage.[](https://twitter.com/sdi_stewart)

## 7 oktober 2019

v1.6.2

* **Nieuw gegevenstype**  &quot;Constant&quot; gegevenselement - De extensie Core bevat nu een nieuw type gegevenselement met de naam  `Constant`.  Dit kan worden gebruikt wanneer u een constante waarde wilt opslaan waarnaar in diverse voorwaarden, handelingen of aangepaste code wordt verwezen. Hartelijk dank voor deze bijdrage.[](https://twitter.com/jexner)

## 11 september 2019

v1.6.1

* **Ondersteuning voor CSP Nonce**  - De Core-extensie heeft nu een optionele configuratieparameter. U kunt een gegevenselement toevoegen dat naar één keer verwijst. Als dit is geconfigureerd, gebruiken alle inlinescripts die door een tag aan de pagina worden toegevoegd de nonce die u hebt geconfigureerd. Deze verandering steunt het gebruik van een Beleid van de Veiligheid van de Inhoud met één keer zodat de manuscripten van de Platform launch nog in een CSP milieu kunnen laden.  U kunt meer lezen over het gebruiken van Platform launch met CSP [hier](../../../ui/client-side/content-security-policy.md).

## 18 juni 2019

v1.5.0

* **Het directe Loggen**  van de Vraag - Browser registreren voor directe vraagregels zal nu extra details verstrekken wanneer het wordt overgegaan.

## 8 mei 2019

v1.4.3

* **Invoervelden**  - Invoervelden zijn nu veel langer!
* **Aangepaste gebeurtenis**  - Aangepast gebeurtenistype kan nu worden gebruikt met gebeurtenissen die buiten het venster worden verzonden.
* **Opgeloste problemen** : hiermee is een probleem opgelost waarbij de waarde-vergelijkingsvoorwaarde geen waarde 0 bevat.
* **Opgeloste problemen**  - uitwisseling\_url is bijgewerkt, zodat u de lijst Core Extension nu kunt zien in Adobe Exchange.

## 8 januari 2019

v1.4.2

* **Voert gebeurtenis**  Viewport in - voorheen zou de gebeurtenis Enters ViewerPort slechts één keer per pagina activeren. Dit gedrag kan nu worden gevormd om telkens als het element viewport ingaat te teweegbrengen.
* **Aangepaste gebeurtenis**  - Aangepaste gebeurtenissen kunnen nu contextuele gegevens bevatten die binnen voorwaarden en handelingen kunnen worden gebruikt.
* **Klik op gebeurtenis**  - Wanneer u een koppelingsvertraging instelt voor de gebeurtenis Click, wordt dit nu correct geregistreerd voor de onderliggende elementen van het anker en niet alleen voor het anker zelf.

## 8 november 2018

* **De optie**  Cohort behouden - De optie om een cohort te behouden is toegevoegd aan de voorwaarde Monster. Dit heeft het effect dat een gebruiker in- of uitgaat van de voorbeeldcohort tijdens sessies. Als bijvoorbeeld het selectievakje &#39;persnel blijven&#39; is ingeschakeld en de voorwaarde de eerste keer true retourneert wanneer deze voor een bepaalde bezoeker wordt uitgevoerd, retourneert deze waarde true op alle volgende reeksen van de voorwaarde voor dezelfde bezoeker. Op dezelfde manier als het selectievakje &#39;persnel blijven&#39; is ingeschakeld en de voorwaarde de eerste keer dat deze voor een bepaalde bezoeker wordt uitgevoerd false retourneert, retourneert deze false op alle volgende reeksen van de voorwaarde voor dezelfde bezoeker.
* **Bug Fix**  - Probleem verholpen waarbij een regel die een gebeurtenis onder aan de pagina gebruikt en een handeling Aangepaste code op een pagina waarop tags synchroon werden geladen maar onjuist werden geïnstalleerd (geen aanroep naar  `_satellite.pageBottom()`), de inhoud van de website zou wissen.
* **Bug Fix**  - Probleem verholpen waarbij de invoerviewport niet zou functioneren als de tagbibliotheek asynchroon was geladen en volledig was geladen nadat de DOMContentLoaded-gebeurtenis van de browser was gestart.

## 24 mei 2018

* **Functie**  - Er is een voorwaarde toegevoegd voor waardetevergelijking. Deze vergelijkt twee waarden met een van de verschillende beschikbare operatoren. Dit vervangt de functionaliteit van verscheidene oudere voorwaarden die veel te specifiek waren.
* **Functie**  - Met deze voorwaarde is een Max Frequency toegevoegd en kunt u opgeven hoe vaak de voorwaarde binnen een tijdsperiode of gebeurtenis true moet retourneren. Voorbeelden: 5 keer per dag, 2 keer per bezoek.

## 11 april 2018

* **Functie**  - gegevenselementen kunnen nu verwijzen naar andere gegevenselementen.

## 20 maart 2018

* **Bugcorrectie** : aangepaste codevensters genereren  `document.write` fouten en voeren deze niet uit in asynchrone implementaties
* **Foutopsporing**  - Hoofdmodules zijn niet opgenomen in een bibliotheek
* **Foutopsporing** : er zijn problemen opgetreden met minimale en maximale waarden in het gegevenselement Willekeurig getal

## 10 januari 2018

* **Functie**  - Willekeurig gegevenselement getal
* **Functie**  - Gegevenselement pagina-informatie
* **Functie**  - Datumvoorwaarde
* **Functie**  - Bemonsteringsvoorwaarde
