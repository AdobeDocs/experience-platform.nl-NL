---
title: Overzicht van gesplitste extensie
description: Leer over de uitbreiding Splunk voor gebeurtenis door:sturen in Adobe Experience Platform.
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# Overzicht van splitsingsextensie

[Splunk](https://www.splunk.com) is een observiteitsplatform dat onderzoek, analyse, en visualisatie voor activeerbare inzichten op uw gegevens verstrekt. Splunk [gebeurtenis doorsturen](../../../ui/event-forwarding/overview.md) extensie gebruikt de [REST-API voor HTTP-gebeurtenisverzameling splitsen](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints) om gebeurtenissen vanaf Adobe Experience Platform Edge Network naar de [Splunk HTTP Event Collector](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector).

Splunk gebruikt dragertokens als authentificatiemechanisme om met de Verzameling API van de Gebeurtenis van de Splunk te communiceren.

## Gebruiksscenario’s {#use-cases}

Marketing teams kunnen de extensie voor de volgende gebruiksgevallen gebruiken:

| Gebruiksscenario | Beschrijving |
| --- | --- |
| Analyse van klantgedrag | Organisaties kunnen gegevens over klantinteractiegebeurtenissen vastleggen vanaf hun website en relevante gebeurtenissen doorsturen naar Splunk. Marketing- en analyseteams kunnen vervolgens binnen het Splunk-platform een analyse uitvoeren om inzicht te krijgen in de interactie en het gedrag van belangrijke gebruikers. Het platform Splunk kan worden gebruikt om grafieken, dashboards, of andere visualisaties te produceren om bedrijfsbelanghebbenden te informeren. |
| Schaalbaar zoeken op grote gegevenssets | Organisaties kunnen transactie- of gespreksinvoer vastleggen als gebeurtenisgegevens van de website en gebeurtenissen doorsturen naar Splunk. De teams van Analytics kunnen dan hefboomwerking Splunk&#39;s scalable indexatievermogen om grote datasets te filtreren en te verwerken om het even welke bedrijfsinzichten af te leiden en geïnformeerde besluiten te nemen. |

{style=&quot;table-layout:auto&quot;}

## Vereisten {#prerequisites}

U moet een Splunk-account hebben om deze extensie te kunnen gebruiken. U kunt zich registreren voor een Splunk-account op het tabblad [Splunk homepage](https://www.splunk.com/page/sign_up).

>[!NOTE]
>
> De uitbreiding Splunk steunt zowel de Instanties van de Cloud van de Splunk als van de Onderneming van Splunk. Deze handleiding documenteert een implementatie met [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html) als referentie. Het configuratieproces voor [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html) is gelijkaardig, maar vereist specifieke begeleiding van uw SplunkBeheerder van de Onderneming.

U moet ook de volgende technische waarden hebben om de extensie te configureren:

* An [Gebeurtenisverzamelingsteken](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). Tokens zijn doorgaans de indeling UUIDv4, zoals hieronder: `12345678-1234-1234-1234-1234567890AB`.
* Het adres en de poort van de platforminstantie Splunk voor uw organisatie. Het adres en de poort van een platforminstantie hebben doorgaans de volgende notatie: `mysplunkserver.example.com:443`.
   >[!IMPORTANT]
   >
   > Splunk endpoints die binnen gebeurtenis door:sturen worden van verwijzingen voorzien zouden haven slechts moeten gebruiken `443`. Niet-standaard havens worden momenteel niet gesteund in gebeurtenis die implementaties door:sturen.

## De extensie Splunk installeren {#install}

Als u de extensie Splunk Event Collector wilt installeren in de gebruikersinterface, navigeert u naar **Gebeurtenis doorsturen** en selecteer een eigenschap waaraan u de extensie wilt toevoegen of waarvoor u een nieuwe eigenschap wilt maken.

Wanneer u de gewenste eigenschap hebt geselecteerd of gemaakt, navigeert u naar **Extensies** > **Catalogus**. Zoeken naar &quot;[!DNL Splunk]&quot;, en selecteer dan **[!DNL Install]** op de verzonken extensie.

![Installatieknop voor de Splunk-extensie die is geselecteerd in de gebruikersinterface](../../../images/extensions/server/splunk/install.png)

## De extensie Splunk configureren {#configure_extension}

>[!IMPORTANT]
>
>Afhankelijk van uw implementatiebehoeften, kunt u een schema, gegevenselementen, en een dataset tot stand moeten brengen alvorens de uitbreiding te vormen. Controleer alle configuratiestappen voordat u begint om te bepalen welke entiteiten u moet instellen voor uw geval van gebruik.

Selecteren **Extensies** in de linkernavigatie. Onder **Geïnstalleerd**, selecteert u **Configureren** op de Splunk-extensie.

![Vorm knoop voor de uitbreiding die van het Splunk in UI wordt geselecteerd](../../../images/extensions/server/splunk/configure.png)

Voor **[!UICONTROL HTTP Event Collector URL]**, ga uw Splunk platforminstantienadres en haven in. Onder **[!UICONTROL Access Token]**, voer uw [!DNL Event Collector Token] waarde. Als u klaar bent, selecteert u **[!UICONTROL Save]**.

![Configuratieopties ingevuld in de gebruikersinterface](../../../images/extensions/server/splunk/input.png)

## Vorm een gebeurtenis door:sturen regel {#config_rule}

Begin creërend een nieuwe gebeurtenis door:sturen regel [regel](../../../ui/managing-resources/rules.md) en configureer de voorwaarden naar wens. Selecteer bij het selecteren van de handelingen voor de regel de optie [!UICONTROL Splunk] en selecteert u vervolgens de extensie [!UICONTROL Create Event] actietype. De extra controles lijken om de Gebeurtenis van de Splunk verder te vormen.

![Configuratie van handeling definiëren](../../../images/extensions/server/splunk/action-configurations.png)

De volgende stap bestaat uit het toewijzen van de Splunk-gebeurteniseigenschappen aan gegevenselementen die u eerder hebt gemaakt. De ondersteunde optionele toewijzingen op basis van de invoergebeurtenisgegevens die kunnen worden ingesteld, worden hieronder weergegeven. Zie de [Documentatie voor verzonken](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata) voor nadere bijzonderheden.

| Veldnaam | Beschrijving |
| --- | --- |
| [!UICONTROL Event]<br><br>**(VEREIST)** | Geef aan hoe u de gebeurtenisgegevens wilt opgeven. Gebeurtenisgegevens kunnen worden toegewezen aan de `event` in het JSON-object in de HTTP-aanvraag, of het kan onbewerkte tekst zijn. De `event` De sleutel is op het zelfde niveau binnen het JSON gebeurtenispakket zoals de meta-gegevenssleutels. Binnen de `event` accolades met sleutelwaarden, de gegevens kunnen elke gewenste vorm hebben (zoals een tekenreeks, een getal, een ander JSON-object, enzovoort). |
| [!UICONTROL Host] | De hostnaam van de client waarvan u gegevens verzendt. |
| [!UICONTROL Source Type] | Het brontype dat aan de gebeurtenisgegevens moet worden toegewezen. |
| [!UICONTROL Source] | De bronwaarde die aan de gebeurtenisgegevens moet worden toegewezen. Als u bijvoorbeeld gegevens verzendt vanuit een toepassing die u ontwikkelt, stelt u deze sleutel in op de naam van de app. |
| [!UICONTROL Index] | De naam van de index van de gebeurtenisgegevens. De index die u hier opgeeft, moet zich binnen de lijst met toegestane indexen bevinden als voor het token de parameter indexes is ingesteld. |
| [!UICONTROL Time] | De tijd van de gebeurtenis. De standaardtijdnotatie is UNIX-tijd (in de notatie) `<sec>.<ms>`) en is afhankelijk van uw lokale tijdzone. Bijvoorbeeld: `1433188255.500` Geeft 1433188255 seconden en 500 milliseconden na het tijdperk aan, of maandag 1 juni 2015, bij 7:50:17:00 GMT. |
| [!UICONTROL Fields] | Geef een onbewerkt JSON-object of een set sleutelwaardeparen op die expliciete aangepaste velden bevatten die tijdens de indextijd moeten worden gedefinieerd.  De `fields` key is niet van toepassing op onbewerkte gegevens.<br><br>Verzoeken met `fields` eigenschap moet naar de `/collector/event` eindpunt, of anders zullen zij niet worden geïndexeerd. Voor meer informatie, zie de documentatie van de Splunk op [geïndexeerde veldextracties](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC). |

### Gegevens valideren in Splunk {#validate}

Nadat het creëren van en het uitvoeren van de gebeurtenis door:sturen regel, bevestig of de gebeurtenis die naar Splunk API wordt verzonden zoals verwacht in Splunk UI wordt getoond. Als de gebeurtenisinzameling en de integratie van het Experience Platform succesvol waren, zult u gebeurtenissen binnen de console van de Splunk als zo zien zien:

![Gebeurtenisgegevens die tijdens de validatie in de Splunk-gebruikersinterface worden weergegeven](../../../images/extensions/server/splunk/splunk-data.png)

## Volgende stappen

Dit document behandelde om de Splunk gebeurtenis te installeren en te vormen die uitbreiding door:sturen in UI. Raadpleeg de officiële documentatie voor meer informatie over het verzamelen van gebeurtenisgegevens in Splunk:

* [De Instelling en gebruikt de Collector van de Gebeurtenis van HTTP in Splunk Web ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [Verificatie instellen met tokens](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [Problemen met HTTP Event Collector oplossen](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector) (bevat tevens een overzicht van [mogelijke foutcodes](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes))
