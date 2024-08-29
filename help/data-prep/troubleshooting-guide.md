---
keywords: Experience Platform;thuis;populaire onderwerpen;
title: Handleiding voor het oplossen van problemen met Data Prep
description: Dit document geeft antwoorden op veelgestelde vragen over Adobe Experience Platform Data Prep.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# [!DNL Data Prep] gids voor probleemoplossing

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform [!DNL Data Prep] en een gids voor probleemoplossing voor algemene fouten. Voor vragen en het oplossen van problemeninformatie betreffende Platform APIs in het algemeen, zie de [ het oplossen van problemengids van Adobe Experience Platform API ](../landing/troubleshooting.md).

## Veelgestelde vragen

Hieronder volgt een lijst met veelgestelde vragen over [!DNL Data Prep] en de bijbehorende antwoorden.

### Hoe worden transformatiefouten opgelost?

[!DNL Data Prep] lokaliseert alle transformatiefouten naar de kolom waarin zij voorkwamen. Dientengevolge, wordt die kolom nietig verklaard en de rest van de rij zal verder worden verwerkt. Deze transformatiekwesties worden geregistreerd als **Waarschuwingen**. U wordt aangeraden de waarschuwingen regelmatig te controleren en de transformatielogica aan te passen om rekening te houden met de transformatieproblemen. Dit zal de kwaliteit van de gegevens verhogen die in Experience Platform worden opgenomen.

Als de kolommen die als **worden gemerkt Vereist** wegens transformatiekwesties ongeldig worden gemaakt, dan zal de rij niet worden opgenomen. Wanneer gedeeltelijke gegevensopname wordt toegelaten, kunt u de drempel van dergelijke verwerpingen plaatsen alvorens de volledige stroom ontbreekt. Als het ongeldig gemaakte attribuut geen bevestigingen van het schemaniveau beïnvloedde, zal de rij blijven worden opgenomen.

Alle rijen die ongeldig zijn, zelfs zonder transformatiefouten, worden eveneens afgewezen. Een gegevensinvoerstroom kan bijvoorbeeld een doorvoertoewijzing (geen transformatielogica) naar een vereist veld hebben en er is geen binnenkomende waarde voor dat kenmerk. Deze rij wordt afgewezen.

### Hoe kan ik aan speciale tekens in een veld ontsnappen?

Met `${...}` kunt u speciale tekens in een veld verwijderen. JSON-bestanden die velden met een punt (`.`) bevatten, worden echter niet ondersteund door dit mechanisme. Wanneer het in wisselwerking staan met hiërarchieën, als een kindattribuut een periode (`.`) heeft, moet u backslash (`\`) gebruiken om speciale karakters te ontsnappen. `address` is bijvoorbeeld een object dat het kenmerk `street.name` bevat. U kunt dit vervolgens `address.street\.name` in plaats van `address.street.name` noemen.

### Wat is de maximumlengte van berekende velden?

Berekende velden mogen maximaal 4096 tekens lang zijn.

### Mijn opname is mislukt vanwege validatie voor een kenmerk, maar ik heb dat kenmerk juist in mijn bestand. Wat is er precies mis?

Zorg ervoor dat het gegevenstype voor elk veld overeenkomt met het type dat in het schema is gedefinieerd. Daarnaast moeten beperkingen zoals &quot;Required&quot;, &quot;enum&quot; en &quot;format&quot; worden nageleefd.

De gegevens die worden opgenomen moeten het schema van de Gegevens van de Ervaring (XDM) in Experience Platform worden bepaald in overeenstemming zijn. Als het kenmerk niet overeenkomt met het verwachte type of de indeling die in het schema is opgegeven, mislukt de invoer.

Als de functies van Data Prep worden gebruikt, zorg er dan voor dat de transformatie in de juiste attributen resulteert. U kunt de kenmerken controleren tijdens het installatieproces van de workflow voor bronnen. Selecteer **[!UICONTROL New field type]** tijdens de toewijzingsstap en selecteer **[!UICONTROL Add calculated field]** . Vervolgens gebruikt u de berekende veldinterface om elke functie voor te vertonen.

### Hoe kan ik slechte gegevenswaarden uit het stromen of partij ingestigeningsverslagen verwijderen?

U kunt de de kaartinterface van de Prep van Gegevens gebruiken om kolom-vlakke het filtreren uit te voeren door slechts kolommen in kaart te brengen die vereiste gegevens hebben. U kunt berekende velden ook gebruiken om de gegevens te transformeren met de ondersteuningsfuncties.

Het rij-vlakke filtreren is momenteel beschikbaar slechts voor de [ bron van Adobe Analytics schakelaar ](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Na inname kunt u de gegevens opschonen, vormgeven en manipuleren met SQL. Nochtans, zal dit proces de schrapping van de partij met de slechte verslagen vereisen, en het opnieuw opnemen van een nieuwe partij die van het resultaat van SQL wordt gecreeerd.

>[!IMPORTANT]
>
>* Gegevensmeer: u kunt alleen records verwijderen die al zijn opgenomen door de batch in de record te verwijderen en opnieuw in te voeren.
>
>* Klantprofiel in realtime: u kunt op kenmerken gebaseerde records overschrijven door nieuwe records in te voeren, maar u kunt gebeurtenisrecords niet verwijderen.
>
>* Identiteitsservice: u kunt records niet rechtstreeks verwijderen in Identiteitsservice. U moet het volledige profiel verwijderen en het profiel opnieuw uploaden met de juiste records met de API voor het verwijderen van profielen.

### Wat zijn de beste praktijken voor het gebruiken van berekende gebieden in de gegevens van het GIF?

U kunt de de kaartfuncties van de Prep van Gegevens tijdens de afbeeldingsstap van brongegevens aan XDM schema gebruiken om een nieuw berekend gebied tot stand te brengen.

### Wanneer u Adobe Analytics-gegevens als bron inbrengt, wordt het gemaakte schema automatisch ingeschakeld voor het profiel?

De analysegegevens worden niet automatisch gevormd voor Profiel. Na het vormen van de bronschakelaar, moet u in de dataset en het schema gaan en hen voor de opname van het Profiel toelaten.

Wanneer u een bron van de Analyse gegevens in een productiesandbox creeert, worden twee gegevensstromen gecreeerd:

* Een dataflow die een 13 maanden backfill van historische gegevens van de rapportreeks in gegevens meer doet. Deze gegevensstroom eindigt wanneer de backfill volledig is.
* Een gegevensstroom die levende gegevens naar gegevens meer en naar Profiel verzendt. Deze gegevensstroom wordt voortdurend uitgevoerd.

### Hoe kan ik één waarde in kleine letters binnen een kaartvoorwerp gebruikend de functies van de Prep van Gegevens?

U kunt de waarde ophalen met de functie `map_get_values` en deze vervolgens in kleine letters weergeven met de onderste functie:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

U kunt dezelfde functie gebruiken om kleine letters te gebruiken voor een object Map. U kunt echter niet een volledige kaart doorlopen en elk item in kleine letters maken.

### Kan ik functies van Data Prep op een genestelde manier gebruiken?

Ja, u kunt één functie van de Prep van Gegevens binnen een andere functie gebruiken om voor complexe mogelijkheden van de gegevensvoorbereiding tijdens gegevensopname op te lossen.

Als u bijvoorbeeld een veld wilt definiëren als null op basis van een specifieke voorwaarde, kunt u de functie &quot;if&quot; gebruiken om te controleren of het veld bestaat. Als de functie `true` retourneert, kunt u &quot;nullify()&quot; gebruiken en als `false` wordt geretourneerd, kunt u het desbetreffende veld gebruiken.

Als marketing_type het gebied was dan kunt u &quot;.equals&quot;gebruiken om de waarde in het marketing_type gebied te controleren en dit kan binnen een &quot;iif&quot;functie worden genesteld. Als het `true` retourneert, kunt u de functie &quot;nullify()&quot; gebruiken, zoals hieronder wordt getoond:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

De volgende schetsen voorbeelden van hoe u de functies van Prep van Gegevens kunt nesten gebruikend als, evenaart, en verklaart:

| Functie | Beschrijving | Parameters | Syntaxis | Uitdrukking | Voorbeelduitvoer |
| --- | --- | --- | --- | --- | --- |
| iif | Evalueert een bepaalde booleaanse expressie en retourneert de opgegeven waarde op basis van het resultaat. | <ul><li>UITDRUKKING: **Vereiste** de booleaanse uitdrukking die wordt geëvalueerd.</li><li>TRUE_VALUE: **Vereiste** de waarde die is teruggekeerd als de uitdrukking aan waar evalueert.</li><li>FALSE_VALUE: **Vereiste** de waarde die is teruggekeerd als de uitdrukking aan vals evalueert.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;Waar&quot; |
| equals | Vergelijkt twee tekenreeksen om te bevestigen of deze gelijk zijn. Deze functie is hoofdlettergevoelig. | <ul><li>STRING1: **Vereiste** het eerste koord u wilt vergelijken.</li><li>STRING2: **Vereiste** het tweede koord u wilt vergelijken. | TEKENREEKS1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| opheffen | Stelt de waarde van het kenmerk in op null. Dit zou moeten worden gebruikt wanneer u niet het gebied aan het doelschema wilt kopiëren. | | nullify() | nullify() | null |

{style="table-layout:auto"}

Hieronder ziet u een voorbeeld van hoe de functies genest kunnen worden, ervan uitgaande dat het te evalueren veld &quot;marketing_type&quot; is.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Nu hebt u de volgende drie velden:

* marketing_type: (email, phyMail, push, sms, phone)
* total_consents: number range from 4000 to 5500
* datum : van feb tot maart 2024

U kunt de drie bovenstaande functies gebruiken en nesten om de drie velden te manipuleren:

* iif(marketing_type.equals(&quot;email&quot;), nullify(), iif(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* iif(marketing_type.equals(&quot;phyMail&quot;), nullify(), iif(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type))
* iif(total_consents > 5000, if(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;sufficient-consents&quot;)
* iif(date.equals(&quot;3/21/24&quot;), if(marketing_type.equals(&quot;push&quot;), nullify(), marketing_type), &quot;not-March&quot;)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-permission-sms&quot;, marketing_type), &quot;high-consents&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_consents > 5000, nullify(), &quot;email-low-consents&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consents &lt; 4500, &quot;low-permission-push&quot;, nullify()), marketing_type)
* iif(total_consents >= 5500, if(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-consents&quot;), marketing_type)