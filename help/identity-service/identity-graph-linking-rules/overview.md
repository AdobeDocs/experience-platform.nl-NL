---
title: Overzicht van regels voor identiteitsgrafiek
description: Leer over de Regels van de Vereniging van de Grafiek van Identiteit in de Dienst van de Identiteit.
hide: true
hidefromtoc: true
badge: Alfa
source-git-commit: a6e4511c41408b78a70a22eb8038bb7a37c41ed5
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Overzicht van regels voor identiteitsgrafiek

>[!IMPORTANT]
>
>Identiteitsgrafiekkoppelingsregels zijn momenteel in Alpha. De functie en documentatie kunnen worden gewijzigd.

## Inhoudsopgave

* [Overzicht](./overview.md)
* [Voorbeeldscenario&#39;s](./example-scenarios.md)
* [Identiteitsservice en realtime klantprofiel](identity-and-profile.md)
* [Logica voor identiteitskoppeling](./identity-linking-logic.md)

Met Adobe Experience Platform Identity Service en Real-Time Customer Profile is het eenvoudig om aan te nemen dat uw gegevens perfect zijn opgenomen en dat alle samengevoegde profielen één persoon vertegenwoordigen via een personenteken, zoals een CRM-id. Er zijn echter scenario&#39;s waarin bepaalde gegevens kunnen proberen meerdere afwijkende profielen samen te voegen tot één profiel (het profiel wordt samengevouwen). Om deze ongewenste samenvoegingen te verhinderen, kunt u configuraties gebruiken die door identiteitsgrafiek worden verstrekt die regels verbindt en voor nauwkeurige verpersoonlijking voor uw gebruikers toestaan.

## Voorbeelden van scenario&#39;s waarbij het profiel kan worden samengevouwen

* **Gedeeld apparaat**: Gedeeld apparaat verwijst naar apparaten die door meer dan één individu worden gebruikt. Voorbeelden van een gedeeld apparaat zijn tablets, bibliotheekcomputers en kiosken.
* **Onjuiste e-mail- en telefoonnummers**: Onjuiste e-mail- en telefoonnummers verwijzen naar eindgebruikers die ongeldige contactgegevens registreren, zoals &quot;test<span>@test.com&quot; voor e-mail en &quot;+1-111-111-1111&quot; voor telefoonnummer.
* **Onjuiste of onjuiste identiteitswaarden**: Onjuiste of onjuiste identiteitswaarden verwijzen naar niet-unieke identiteitswaarden die CRM-id&#39;s kunnen samenvoegen. Terwijl IDFA&#39;s bijvoorbeeld 36 tekens moeten hebben (32 alfanumerieke tekens en vier afbreekstreepjes), zijn er scenario&#39;s waarin een IDFA met de identiteitswaarde &quot;user_null&quot; kan worden opgenomen. Op dezelfde manier steunen de telefoonaantallen slechts numerieke karakters, maar een telefoonnamespace met een identiteitswaarde van &quot;niet-gespecificeerd&quot;kan worden opgenomen.

Lees het document over meer informatie over gebruiksscenario&#39;s voor koppelingsregels voor identiteitsgrafieken [voorbeeldscenario&#39;s](./example-scenarios.md).

## Doelstellingen van de identiteitsgrafiek die regels met elkaar verbindt

Met de regels voor identiteitsgrafiek kunt u:

* Configureer limieten om te voorkomen dat twee verschillende personen-id&#39;s worden samengevoegd in één identiteitsgrafiek, zodat één identiteitsgrafiek slechts één persoon vertegenwoordigt.
   * De grenzen die u vormt worden dan afgedwongen door algoritme van de identiteitsoptimalisering.
* Configureer prioriteiten om onlinegebeurtenissen die door de geverifieerde persoon worden uitgevoerd, aan een bepaalde gebruiker te koppelen.

### Limieten

U kunt naamruimtegrenzen gebruiken om het maximumaantal identiteiten te definiëren dat in een grafiek kan bestaan op basis van een bepaalde naamruimte. U kunt bijvoorbeeld instellen dat de grafiek maximaal één identiteit heeft met een CRM-id-naamruimte, waardoor het samenvoegen van twee verschillende personen-id&#39;s binnen dezelfde grafiek wordt voorkomen.

* Als een limiet niet is geconfigureerd, kan dit leiden tot ongewenste samenvoegingen van grafieken, zoals twee identiteiten met een CRM-id-naamruimte in een grafiek.
* Als een limiet niet is geconfigureerd, kan de grafiek zo veel naamruimten toevoegen als nodig is zolang de grafiek zich binnen de hulplijnen bevindt (50 identiteiten/grafiek).
* Als een grens wordt gevormd, dan zal het algoritme van de identiteitsoptimalisering ervoor zorgen dat de grens wordt afgedwongen.

### Algoritme voor identiteitsoptimalisatie

Het algoritme van de identiteitsoptimalisering is een regel die ervoor zorgt dat de grenzen worden afgedwongen. Het algoritme houdt zich aan de meest recente koppelingen en verwijdert de oudste koppelingen om ervoor te zorgen dat een bepaalde grafiek binnen de grenzen blijft die u hebt gedefinieerd.

Hieronder volgt een lijst met implicaties van het algoritme voor het koppelen van anonieme gebeurtenissen aan bekende id&#39;s:

* De ECID wordt gekoppeld aan de laatst geverifieerde gebruiker als aan de volgende voorwaarden is voldaan:
   * Als CRM-id&#39;s worden samengevoegd met ECID (gedeeld apparaat).
   * Als de grenzen aan enkel één identiteitskaart van CRM worden gevormd.

### Prioriteit

>[!IMPORTANT]
>
>Naamruimteprioriteiten zijn momenteel niet beschikbaar voor alfa.

U kunt naamruimteprioriteit gebruiken om te definiëren welke naamruimten belangrijker zijn dan andere. De hiërarchie die u instelt voor de naamruimten wordt vervolgens gebruikt om de primaire identiteiten te definiëren en profielfragmenten op te slaan. Als de prioritaire montages worden gevormd, dan zal het primaire identiteit plaatsen op Web SDK niet meer worden gebruikt om te bepalen welke profielfragmenten worden opgeslagen.

* De grenzen en de prioriteit zijn onafhankelijke configuraties en doen **niet** elkaar beïnvloeden:
   * Limieten is een configuratie voor identiteitsgrafieken in Identiteitsservice.
   * Prioriteit is een profielfragmentconfiguratie op Real-Time Klantprofiel.
   * Prioriteit **niet** invloed hebben op de handleidingen van het identiteitsdiagram.

>[!BEGINSHADEBOX]

**Voorbeeld van naamruimteprioriteit**

Veronderstel dat u de volgende prioriteit voor uw namespaces hebt gevormd:

1. CRM-id: vertegenwoordigt een gebruiker.
2. IDFA: Vertegenwoordigt een Apple-hardwareapparaat, zoals een iPhone en iPad.
3. GAID: vertegenwoordigt een Google-hardwareapparaat, zoals Google Pixel.
4. ECID: vertegenwoordigt een webbrowser, zoals Firefox, Safari en Chrome.
5. AID: vertegenwoordigt een webbrowser.
Als ECID en AID gelijktijdig worden verzonden, vertegenwoordigen beide identiteiten dezelfde webbrowser (dubbel).

Als de volgende ervaringsgebeurtenissen in Experience Platform worden opgenomen, worden de profielfragmenten dan opgeslagen tegen namespace met de hogere prioriteit.

**Voor authentiek verklaarde gebeurtenissen:**

* Als de identiteitskaart een ECID, een GAID, en identiteitskaart van CRM bevat, zal de gebeurtenisinformatie tegen identiteitskaart van CRM (primaire identiteit) worden opgeslagen.
   * GAID vertegenwoordigt een Google-hardwareapparaat (bijvoorbeeld Google Pixel), ECID staat voor een webbrowser (bijvoorbeeld Google Chrome) en CRM-id staat voor een geverifieerde gebruiker.
   * Als de identiteitskaart een CRM-id, een ECID en een HULP bevat, worden de gebeurtenisgegevens opgeslagen met de CRM-id (primaire identiteit).

**Niet-geverifieerde gebeurtenissen:**

* Als de identiteitskaart een ECID, IDFA, en STEUN bevat, dan zal de gebeurtenisinformatie tegen IDFA (primaire identiteit) worden opgeslagen.
   * IDFA vertegenwoordigt een Apple-hardwareapparaat (bijvoorbeeld iPhone), ECID en AID die beide een webbrowser (Safari) vertegenwoordigen.

>[!ENDSHADEBOX]

## Volgende stappen

Lees de volgende documentatie voor meer informatie over koppelingsregels voor identiteitsgrafieken:

* [Voorbeeldscenario&#39;s voor het configureren van identiteitsgrafiek-koppelingsregels](./example-scenarios.md)
* [Identiteitsservice en realtime klantprofiel](identity-and-profile.md)
* [Logica voor identiteitskoppeling](./identity-linking-logic.md)