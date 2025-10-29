---
keywords: integratie van het adform; adform;
title: Adform-integratie voor niet-geverifieerde herbestemming
description: Dankzij deze Adobe Experience Platform-integratie kunt u gebruikers opnieuw als doel instellen op basis van ECID.
last-substantial-update: 2025-03-26T00:00:00Z
exl-id: 37eb9453-fc3c-481e-94ea-54d9b1545631
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# [!DNL Adform] overzicht van extensies

De [[!DNL Adform] ](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) uitbreiding laat server-side gebeurtenis toe door:sturen in Adobe Experience Platform, toestaand adverteerders, media agentschappen en uitgevers om gegevens direct met het systeem van de Fusie van identiteitskaart van Adform te synchroniseren. Deze integratie stelt bedrijven in staat om het publiek op meerdere kanalen te betrekken, de campagneprestaties te verbeteren en biedt op maat gesneden oplossingen om de strategieën voor digitale reclame te verfijnen en de efficiëntie te maximaliseren en uit te geven.

In tegenstelling tot traditionele clienttracering elimineert deze extensie de noodzaak van cookies van derden door gebruik te maken van id&#39;s van eerste partijen, met name de ECID (Experience Cloud ID) die met Adform is gesynchroniseerd. Dit maakt het mogelijk om het publiek naadloos opnieuw te richten zonder dat JavaScript-implementatie op de client vereist is.

In deze handleiding wordt beschreven hoe u de extensie installeert, configureert en implementeert voor het doorsturen van gebeurtenissen van de digitale eigenschappen van een merk via Adobe Edge Network naar Adform, zodat bezoekers naadloos kunnen worden omgeleid.

## Offsite herbestemming

Door offsite retargeting kunt u potentiële klanten die uw website hebben bezocht opnieuw inschakelen, maar deze niet hebben omgezet. Met Adform bereikt u deze doelgroepen op verschillende platformen, waardoor uw merk beter zichtbaar wordt en de conversiemogelijkheden toenemen. Gebruik deze integratie om:

* Neem opnieuw contact op met onbekende bezoekers zonder gebruik te maken van cookies van derden.
* Activeer het publiek rechtstreeks op ECID&#39;s zonder gebruik te maken van cookie-alternatieve id&#39;s van derden of extra tags op uw digitale eigenschappen.

Met Adform kunt u:

* Verander eenvoudig uw eerste partijpubliek dat op ECID&#39;s wordt vermeld in adresseerbare id&#39;s voor digitale advertentiecampagnes.
* Koppel ECID&#39;s aan 40+ biddable ID-oplossingen om uw bereik, frequentie en prestaties te optimaliseren ten opzichte van uw doelpubliek.

### Serverdoelactivering met [!DNL Adform] {#server-side-activation}

In tegenstelling tot traditionele clientimplementatie vereist deze integratie niet dat u de oplossing van een leverancier van id op uw digitale eigenschappen implementeert. In plaats daarvan wordt de activering van het publiek op de server mogelijk gemaakt door gebruik te maken van ECID&#39;s die al zijn gesynchroniseerd met Adform. Belangrijkste voordelen zijn:

* **Geen cliënt-kant plaatsing van JavaScript**: U te hoeven niet om cliënt-kant de herkenningslogica van de bezoeker te beheren of cliënt-kant IDs in langlevende stabiele versies te decrypteren.
* **Naadloze publiekssynchronisatie**: ECIDs wordt in kaart gebracht aan de interne grafiek van identiteitskaart van Adform, die voor efficiënte het opnieuw richten over platforms toestaat.
* **Verbeterd bereik en deduplicatie**: De grafiek van de Fusie van identiteitskaart verbindt ECIDs met veelvoudige herkenningstekens die hoogwaardig publiek aanpassing verzekeren.

## Vereisten {#prerequisites}

Voordat u Adform integreert met Adobe, moet u controleren of aan de volgende voorwaarden is voldaan:

1. **de opstelling van SDK van het Web van Adobe**: De SDK van het Web van Adobe moet worden uitgevoerd om gegevensinzameling en gebeurtenis het door:sturen te vergemakkelijken.

2. **CDP of SKU van de Verbinding**: U moet of het Platform van Gegevens van de Klant van Adobe (CDP) Prime of SKU van Ultimate, of het SKU van de Verbinding hebben, om naadloze cliënt-kant en server-zijmededeling toe te laten.

3. **de configuratie van Edge Network van Adobe Experience Platform**:
   * Zorg ervoor dat de Edge Network is geconfigureerd voor ondersteuning van realtime-gebeurtenisverzending voor offsite herbestemming. Zie Adobe [ Gebeurtenis door:sturen Begonnen gids ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started) voor meer informatie.
   * Deze stap is essentieel voor het efficiënt overbrengen van gegevens naar server-zijeindpunt van Adform.

Wanneer deze voorwaarden zijn ingesteld, kunt u de extensie [!DNL Adform] blijven configureren en implementeren.

## De extensie [!DNL Adform] configureren {#configure-adform-extension}

Volg de stappen in de onderstaande secties om de extensie [!DNL Adform] te configureren.

### De extensie installeren en configureren

Navigeer naar [!DNL Adform extension] in de gebeurtenis die UI door:sturen en ga de vereiste waarden in:

| Invoer | Beschrijving |
| --- | --- |
| Instellingen bijhouden-id | De unieke id die door Adform wordt opgegeven voor het bijhouden van gebeurtenissen. |
| Wereldwijd domein | Gebruik `a1.adform.net` om de prestaties te optimaliseren en problemen met de regionale latentie te voorkomen. |

Sla de configuratie op nadat u deze gegevens hebt ingevoerd.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Parameters voor reeksspatiëring definiëren

De handeling &#39;track&#39; is de primaire gebeurtenisregel. Deze activering wordt gebaseerd op vooraf gedefinieerde handelingen. `page load.` Bevat doorgaans de volgende parameters:

**Vereiste parameters:**

| Parameters | Beschrijving |
| --- | --- |
| `Page Name` | Hiermee wordt de pagina of gebruikershandeling geïdentificeerd. |
| `User Agent` | Hiermee legt u gegevens vast voor overeenkomsten met doelgroepen. |
| `IP Address` | Cruciaal voor een nauwkeurige doelgerichtheid en heroriëntatie. |

**Geadviseerde parameters:**

| Parameters | Beschrijving |
| --- | --- |
| `Page URL` | Hiermee wordt de pagina of gebruikershandeling geïdentificeerd. |
| `Referral URL` | Hiermee legt u gegevens vast voor overeenkomsten met doelgroepen. |
| `ECID` | Cruciaal voor een nauwkeurige doelgerichtheid en heroriëntatie. |
| `Source Domain` | Cruciaal voor een nauwkeurige doelgerichtheid en heroriëntatie. |

<!-- ![Tracking parameters for Adform]() -->

### Regel koppelen

De extensie moet aan een regel zijn gekoppeld om correct te werken. Als er geen voorwaarden zijn ingesteld, maakt u een algemene regel om ervoor te zorgen dat deze altijd wordt uitgevoerd.

>[!NOTE]
>
>Als de extensie niet wordt geactiveerd, controleert u of deze is gekoppeld aan een geldige regel in Adobe Experience Platform Data Collection.

<!-- ![Attach a rule to the Adform extension]() -->

## Valideren en implementeren

Controleer of de extensie correct is geïnstalleerd en geconfigureerd en of alle vereiste gegevenselementen zijn toegewezen, inclusief:

* [ECID](/help/identity-service/features/ecid.md)
* Paginanaam
* URL verwijzing
* Gebruikersagent
* IP-adres

Zodra u alle vereiste gebieden invoert en klaar bent met testen, uitgezochte **bouwt** om de uitbreiding op te stellen.

## Volgende stappen

U moet nu begrijpen hoe Adform kan worden geïntegreerd met Adobe-serverfuncties en de haalbaarheid van de integratie in uw bestaande infrastructuur kunnen beoordelen. Voor meer informatie, verwijs naar [ officiële documentatie van Adform ](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).
