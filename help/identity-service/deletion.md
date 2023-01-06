---
title: Verwijderen in identiteitsservice
description: Dit document biedt een overzicht van de verschillende methoden waarmee u uw identiteitsgegevens in Experience Platform kunt verwijderen en om duidelijk te maken hoe identiteitsgrafieken worden beïnvloed.
source-git-commit: 17e39f6e9d6e62e22f867de91d571593ba945c71
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---

# Verwijderen in identiteitsservice

Adobe Experience Platform Identity Service genereert identiteitsgrafieken door identiteiten op deterministische wijze te koppelen tussen apparaten en systemen voor een individuele persoon. Identiteitsgrafiekkoppelingen worden tot stand gebracht wanneer twee of meer gemarkeerde identiteiten binnen dezelfde gegevensrij worden ontvangen.

Identiteitsgrafieken worden gebruikt door het profiel van de Klant in real time om een uitvoerige en unieke mening van uw klantenattributen en gedrag tot stand te brengen, toelatend u om impactvolle, persoonlijke digitale ervaringen in real time, aan mensen, en niet apparaten te leveren.

Dit document biedt een overzicht van de verschillende methoden waarmee u uw identiteitsgegevens in Experience Platform kunt verwijderen en om duidelijk te maken hoe identiteitsgrafieken worden beïnvloed.

## Aan de slag

In het onderstaande document wordt verwezen naar de volgende kenmerken van Experience Platform:

* [Identiteitsservice](home.md): Verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
   * [Identiteitsgrafiek](./ui/identity-graph-viewer.md): Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten voor een bepaalde klant, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.
   * [Identiteitsnaamruimten](namespaces.md): Identiteitsnaamruimten zijn een onderdeel van Identiteitsdienst dat fungeert als indicator van de context waarop een identiteit betrekking heeft. Ze onderscheiden bijvoorbeeld de waarde &#39;name&#39;<span>@email.com&quot; als e-mailadres of &quot;443522&quot; als een numerieke CRM-id.
* [Catalogusservice](../catalog/home.md): Onderzoek de gegevenslijn, meta-gegevens, dossierbeschrijvingen, folders, en datasets binnen het gegevensmeer.
* [Gegevenshygiëne](../hygiene/home.md): Beheer uw opgeslagen gegevens van de consument door geautomatiseerde datasetvervaldatums te plannen of individuele verslagen van één dataset of alle datasets te schrappen.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Beheer verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, niet te verkopen of te verwijderen.
* [Klantprofiel in realtime](../profile/home.md): Verstrekt een verenigd, klantenprofiel in real time die op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Eén enkele identiteitsschrapping

Met één aanvraag voor het verwijderen van identiteiten kunt u een identiteit binnen een grafiek verwijderen. Dit leidt tot het verwijderen van koppelingen die zijn gekoppeld aan één gebruikersidentiteit die is gekoppeld aan een naamruimte voor identiteiten. U kunt [Gegevenshygiëne](../hygiene/home.md) voor gegevens het zuiveren, het verwijderen van anonieme gegevens, of gegevensminimalisering voor de gegevens die u hebt verzameld. Voor gebruiksgevallen zoals verzoeken van klanten om gegevens te verwijderen en naleving van privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR), kunt u mechanismen gebruiken die worden geboden door [Privacy Service](../privacy-service/home.md).

In de volgende secties worden de mechanismen beschreven die u kunt gebruiken voor verzoeken om één identiteit te verwijderen in Experience Platform.

### Eén identiteitsverwijdering in Privacy Service

Privacy Service verwerkt verzoeken van klanten om toegang, om zich uit verkoop te laten of om hun persoonsgegevens te verwijderen, zoals die zijn omschreven in privacyregels zoals de General Data Protection Regulation (GDPR) en de California Consumer Privacy Act (CCPA). Met Privacy Service kunt u taakaanvragen verzenden via de API of de gebruikersinterface. Wanneer het Experience Platform een schrappingsverzoek van Privacy Service ontvangt, verzendt het Platform bevestiging aan Privacy Service dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De verwijdering van de individuele identiteit is gebaseerd op de opgegeven naamruimte en/of ID-waarde. Bovendien wordt de verwijdering uitgevoerd voor alle sandboxen die bij een bepaalde organisatie horen. Lees voor meer informatie de handleiding op [verwerking van privacyverzoeken in identiteitsservice](privacy.md).

### Eén identiteitsverwijdering in het dialoogvenster [!UICONTROL Data Hygiene] werkruimte

De [[!UICONTROL Data Hygiene] werkruimte](../hygiene/ui/overview.md) in de gebruikersinterface van het Platform kunt u de consumentengegevens verwijderen die deelnemen aan Identiteitsservice en Real-Time klantprofiel. Voor een uitgebreide handleiding over het gebruik van de [!UICONTROL Data Hygiene] werkruimte, raadpleeg de zelfstudie op [verwijderen van consumentengegevens](../hygiene/ui/record-delete.md).

In de onderstaande tabel wordt een overzicht gegeven van de verschillen tussen het afzonderlijk verwijderen van de identiteit in Privacy Service en gegevenshygiëne:

| Eén identiteit verwijderen | Privacy Service | Gegevenshygiëne |
| --- | --- | --- |
| Gebruikskwesties | Alleen gegevensprivacyverzoeken (GDPR, CCPA). | Beheer van in Experience Platform opgeslagen gegevens. |
| Geschatte vertraging | Dagen tot weken | Dagen |
| Betrokken services | Eén identiteitsverwijdering in Privacy Service stelt u in staat te selecteren of gegevens worden verwijderd uit Identiteitsservice, Real-Time Klantprofiel of Gegevensbestand. | De enige identiteitsschrapping in de hygiëne van Gegevens schrapt de geselecteerde gegevens over de Dienst van de Identiteit, het Profiel van de Klant in real time, en het gegevenspeer. |
| Verwijderingspatronen | Verwijder een identiteit uit Identiteitsservice. | Verwijder een identiteit uit Identiteitsservice. |

{style=&quot;table-layout:auto&quot;}

## Gegevensset verwijderen

In de volgende secties worden de mechanismen beschreven die kunnen worden gebruikt om gegevenssets en bijbehorende identiteitskoppelingen in Experience Platform te verwijderen.

### Gegevensset verwijderen in Catalog Service

U kunt de Dienst van de Catalogus gebruiken om verzoeken om datasetschrapping voor te leggen. Voor meer informatie over hoe te om datasets met de Dienst van de Catalogus te schrappen, lees de gids op [objecten verwijderen met de API voor catalogusservice](../catalog/api/delete-object.md). Alternatief, kunt u Platform UI gebruiken om verzoeken om datasetschrapping voor te leggen. Lees voor meer informatie de [gebruikershandleiding voor gegevenssets](../catalog/datasets/user-guide.md#delete-a-dataset).

### Vervaldatum gegevensset in gegevenshygiëne

De [[!UICONTROL Data Hygiene] werkruimte](../hygiene/ui/overview.md) in Adobe Experience Platform UI staat u toe om termijnen voor datasets te plannen. Wanneer een dataset zijn vervaldatum bereikt, beginnen het gegevens meer, de Dienst van de Identiteit, en het Profiel van de Klant in real time afzonderlijke processen om de inhoud van de dataset uit hun respectieve diensten te verwijderen. Lees voor meer informatie de handleiding op [het beheren van datasettermijnen gebruikend [!UICONTROL Data Hygiene] werkruimte](../hygiene/ui/dataset-expiration.md).

De onderstaande tabel geeft een overzicht van de verschillen tussen gegevenssetverwijdering in Catalog Service en gegevenshygiëne:

| Gegevensset verwijderen | Catalogusservice | Gegevenshygiëne |
| --- | --- | --- |
| Gebruikskwesties | Schrap volledige datasets en hun bijbehorende identiteitsinformatie in Platform. | Beheer van in Experience Platform opgeslagen gegevens. |
| Geschatte vertraging | Dagen | Dagen |
| Betrokken services | De schrapping van de gegevensreeks door de Dienst van de Catalogus schrapt gegevens van de Dienst van de Identiteit, het Profiel van de Klant in real time, en het gegevenspeer. | De schrapping van de gegevensreeks door de hygiëne van Gegevens schrapt gegevens van de Dienst van de Identiteit, het Profiel van de Klant in real time, en het gegevenspeer. |
| Verwijderingspatroon | Verbonden identiteiten verwijderen uit de identiteitsdienst die door een bepaalde gegevensset is ingesteld. | Schrap verbonden identiteiten van de Dienst van de Identiteit die door een bepaalde dataset wordt gevestigd, die op vervalprogramma wordt gebaseerd. |

{style=&quot;table-layout:auto&quot;}

## Verschillende statussen van identiteitsgrafieken na verwijdering

Alle schrappingen van identiteitsgrafieken resulteren in het verwijderen van verbindingen tussen twee of meer identiteiten, zoals gespecificeerd in het verwijderingsverzoek. Voor verzoeken tot schrapping van gegevenssets worden alle identiteitskoppelingen die door de opgegeven gegevensset zijn vastgesteld, verwijderd en kunnen al dan niet identiteiten uit grafieken worden verwijderd. Voor individuele identiteitsschrappingsverzoeken worden de identiteitskoppelingen verwijderd voor de gespecificeerde identiteit, en bijgevolg wordt de identiteitswaarde zelf verwijderd uit alle identiteitsgrafieken. Identiteiten zonder één koppeling naar een andere identiteit worden niet opgeslagen in Identiteitsservice.

Hieronder ziet u een overzicht van de mogelijke effecten die verwijderingen kunnen hebben op de status van identiteitsgrafieken.

| Identiteitsgrafiekstatus | Beschrijving |
| --- | --- |
| Gedeeltelijke update | Een gedeeltelijke update van een grafiek gebeurt wanneer minstens twee identiteiten binnen een grafiek verbonden blijven nadat een schrappingsverzoek met succes wordt verwerkt. Na het verwijderen kunnen de resterende identiteitskoppelingen met elkaar verbonden blijven of worden gesplitst in twee of meer afzonderlijke grafieken, afhankelijk van de identiteiten die zijn verwijderd. |
| Volledige verwijdering | Een grafiek moet minstens twee gekoppelde identiteiten hebben om te bestaan. Daarom als een schrappingsverzoek in de verwijdering van alle bestaande verbindingen binnen een grafiek resulteert, dan zal de grafiek volledig worden verwijderd. |
| Geen wijziging | Een grafiek zal niet beïnvloed worden als een bepaald schrappingsverzoek een identiteit of dataset bevat die niet met om het even welk lid van de grafiek wordt geassocieerd. Bovendien, wordt een grafiek niet bijgewerkt zelfs als het schrappingsverzoek een verband tussen een dataset of een identiteit-datasetcombinatie verwijdert, gegeven dat de verbinding door een andere verbinding werd gevestigd die niet werd geschrapt. Dit betekent dat als een verbinding in twee verschillende datasets bestaat, de grafiek niet zal worden bijgewerkt omdat slechts één van de datasets wordt verwijderd. |

{style=&quot;table-layout:auto&quot;}

## Volgende stappen

Dit document behandelde de diverse mechanismen die u kunt gebruiken om identiteiten en datasets op Experience Platform te schrappen. In dit document wordt ook beschreven hoe het verwijderen van identiteits- en gegevenssets invloed kan hebben op identiteitsgrafieken. Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](home.md).