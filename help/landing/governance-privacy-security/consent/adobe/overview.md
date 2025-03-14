---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Verwerking van toestemming in Adobe Experience Platform
description: Leer hoe u in Adobe Experience Platform goedkeuringssignalen voor klanten verwerkt met de Adobe 2.0-standaard.
role: Developer
feature: Consent
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '1546'
ht-degree: 0%

---

# Goedkeuring in Adobe Experience Platform

Adobe Experience Platform staat u toe om de toestemmingsgegevens te verwerken u van uw klanten hebt verzameld en het te integreren in uw opgeslagen klantenprofielen. Deze gegevens kunnen dan door stroomafwaartse processen worden gebruikt om te bepalen of de gegevensinzameling voor een specifieke klant voorkomt, of of hun profielen voor specifieke doeleinden worden gebruikt. De gegevens over machtigingen voor een bepaald profiel kunnen bijvoorbeeld bepalen of het profiel kan worden opgenomen in een geëxporteerd publiekssegment of dat het kan deelnemen aan specifieke marketingkanalen zoals e-mail, tekstberichten of pushberichten.

Dit document biedt een overzicht van hoe u de gegevensbewerkingen van uw platform configureert om gegevens van uw toestemming van de klant in te voeren die door een toestemmings-beheer platform (CMP) worden geproduceerd en die gegevens in klantenprofielen voor downstreamgebruiksgevallen te integreren.

>[!NOTE]
>
>Dit document richt zich op het verwerken van toestemmingsgegevens die de norm van de Adobe gebruiken. Als u toestemmingsgegevens in overeenstemming met IAB Transparantie en het Kader van de Toestemming (TCF) 2.0 verwerkt, zie de gids op [ TCF 2.0 steun in Adobe Real-time Customer Data Platform ](../iab/overview.md).

## Vereisten

Deze handleiding vereist een goed begrip van de verschillende diensten van de Experience Platform die betrokken zijn bij de verwerking van gegevens over de toestemming:

* [ Model van de Gegevens van de Ervaring (XDM) ](/help/xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [ de Dienst van de Identiteit van Adobe Experience Platform ](/help/identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [ Real-Time het Profiel van de Klant ](/help/profile/home.md): Gebruikt [!DNL Identity Service] mogelijkheden om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. Het profiel van de Klant in real time trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [ SDK van het Web van Adobe Experience Platform ](/help/web-sdk/home.md): Een cliënt-kant bibliotheek van JavaScript die u toestaat om de diverse diensten van het Platform in uw klant-onder ogen ziet website te integreren.
   * [ SDK toestemmingsbevelen ](../../../../web-sdk/commands/setconsent.md): Een gebruik-geval overzicht van de toestemming-verwante bevelen SDK die in deze gids worden getoond.
* [ de Dienst van de Segmentatie van Adobe Experience Platform ](/help/segmentation/home.md): Staat u toe om gegevens van het Profiel van de Klant in real time in groepen individuen te verdelen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.

## Samenvatting van de verwerkingsstroom van de toestemming {#summary}

Hieronder wordt beschreven hoe toestemmingsgegevens worden verwerkt nadat het systeem correct is geconfigureerd:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Bij elke pagina die wordt geladen (of wanneer uw CMP een wijziging in de voorkeuren voor toestemming detecteert), wijst een aangepast script op uw site de huidige voorkeuren toe aan een standaard XDM-object. Dit object wordt vervolgens doorgegeven aan de opdracht Platform Web SDK `setConsent` .
1. Wanneer `setConsent` wordt geroepen, controleert het Web SDK van het Platform of de toestemmingswaarden van die verschillend zijn het laatst ontving. Als de waarden verschillend zijn (of er geen vorige waarde is), worden de gestructureerde toestemmings/voorkeursgegevens verzonden naar Adobe Experience Platform.
1. De toestemmings-/voorkeursgegevens worden opgenomen in een gegevensset waarvoor [!DNL Profile] is ingeschakeld en waarvan het schema toestemmings-/voorkeursvelden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van CMP-toestemming, kunnen gegevens over toestemming ook in het Experience Platform stromen via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile] -gegevensset worden geüpload.

### Goedkeuring

In de huidige versie van de steun van de toestemmingsverwerking in Platform, slechts wordt de toestemming van de gegevensinzameling (`collect.val`) automatisch afgedwongen door het Web SDK van het Platform. Terwijl meer korrelige toestemmingen en voorkeur in klantenprofielen kunnen worden verzameld en worden voortgeduurd, moeten deze extra signalen manueel in uw eigen stroomafwaartse processen worden afgedwongen.

>[!NOTE]
>
>Raadpleeg de handleiding over het [[!UICONTROL Consents and Preferences] gegevenstype ](/help/xdm/data-types/consents.md) voor meer informatie over de structuur van de bovenstaande XDM-toestemmingsvelden.

Zodra het systeem is gevormd, interpreteert het Web SDK van het Platform de waarde van de gegevensinzamelingstoestemming voor de huidige gebruiker om te bepalen als het gegeven naar de Edge Network van Adobe Experience Platform zou moeten worden verzonden, van de cliënt, zou moeten worden gelaten vallen of tot de toestemming van de gegevensinzameling aan of ja of nr wordt geplaatst.

## Bepalen hoe gegevens over klanttoestemming binnen uw CMP worden gegenereerd {#consent-data}

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een algemene manier om dit te bereiken is door gebruik te maken van een dialoogvenster voor cookie-toestemming, vergelijkbaar met het volgende voorbeeld:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

In dit dialoogvenster kan de klant kiezen of hij of zij voor zijn of haar gegevens gebruikmaakt van specifieke gevallen voor marketing en personalisatie. Deze toestemmingen en voorkeur zouden aan het gegevensmodel moeten in overeenstemming zijn dat u voor [!DNL Profile] - toegelaten dataset in de volgende stap bepaalt.

## Standaardtoestemmingsvelden toevoegen aan een gegevensset met [!DNL Profile] mogelijkheden {#dataset}

De gegevens van de toestemming van de klant moeten naar een [!DNL Profile]-Toegelaten dataset worden verzonden het waarvan schema toestemmingsgebieden bevat. Deze gebieden moeten in het zelfde schema en de dataset worden omvat die u gebruikt om attributeninformatie over individuele klanten te vangen.

Verwijs naar het leerprogramma op [ vormend een dataset voor het vangen van toestemmingsgegevens ](./dataset.md) voor gedetailleerde stappen op hoe te om deze vereiste gebieden aan a [!DNL Profile]-Toegelaten dataset toe te voegen alvorens met deze gids verder te gaan.

## Beleid voor samenvoegen van [!DNL Profile] bijwerken en gegevens over toestemming opnemen {#merge-policies}

Zodra u een [!DNL Profile]-Toegelaten dataset voor de gegevens van de verwerkingstoestemming hebt gecreeerd, moet u ervoor zorgen dat uw samenvoegbeleid is gevormd om toestemmingsgebieden in elk klantenprofiel altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

>[!NOTE]
>
>Als u geen conflicterende datasets hebt, zou u timestamp belangrijkheid voor uw samenvoegbeleid in plaats daarvan moeten plaatsen. Dit helpt ervoor te zorgen dat de recentste toestemming die door een klant wordt gespecificeerd de toestemmingsinstelling is die wordt gebruikt.

Voor meer informatie over hoe te met fusiebeleid te werken, begin door het [ overzicht van het samenvoegingsbeleid ](../../../../profile/merge-policies/overview.md) te lezen. Wanneer vestiging moet uw samenvoegbeleid, u ervoor zorgen dat uw profielen alle vereiste toestemmingsattributen omvatten die door de [!UICONTROL Consents and Preferences] groep van het schemagebied worden verstrekt, zoals die in de gids over [ wordt geschetst datasetvoorbereiding ](./dataset.md).

## Goedkeuringsgegevens in platform plaatsen

Zodra u uw datasets en fusiebeleid hebt om de vereiste toestemmingsgebieden in uw klantenprofielen te vertegenwoordigen, is de volgende stap de toestemmingsgegevens zelf in Platform te brengen.

Hoofdzakelijk, zou u SDK van het Web van Adobe Experience Platform moeten gebruiken om toestemmingsgegevens naar Platform te verzenden wanneer de toestemming-verandering gebeurtenissen door uw CMP worden ontdekt. Als u toestemmingsgegevens op een mobiel platform verzamelt, zou u Adobe Experience Platform Mobile SDK moeten gebruiken. U kunt er ook voor kiezen om uw verzamelde toestemmingsgegevens direct in te voeren door het aan het XDM schema van uw toestemmingsdataset in kaart te brengen en het te verzenden naar Platform door batch ingestion.

Nadere bijzonderheden over elk van deze methoden zijn te vinden in de onderstaande punten.

### Vorm het Web SDK van het Experience Platform om toestemmingsgegevens te verwerken {#web-sdk}

Zodra u uw CMP hebt gevormd om op toestemmings-verandering gebeurtenissen op uw website te luisteren, kunt u het Web SDK van het Experience Platform integreren om de bijgewerkte toestemmingsmontages te ontvangen en hen te verzenden naar Platform op elke paginading en wanneer de toestemming-verandering gebeurtenissen voorkomt. Zie de gids bij [ vormend het Web SDK om de gegevens van de klantentoestemming ](../sdk.md) voor meer informatie te verwerken.

### De Experience Platform Mobile SDK configureren voor het verwerken van toestemmingsgegevens {#mobile-sdk}

Als in uw mobiele toepassing de voorkeursinstellingen voor toestemming van de klant zijn vereist, kunt u de Experience Platform Mobile SDK integreren om toestemmingsinstellingen op te halen en bij te werken en deze naar Platform te verzenden wanneer de API voor toestemming wordt aangeroepen.

Zie de Mobiele documentatie van SDK voor [ het vormen van de Mobiele uitbreiding van de Toestemming ](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) en [ gebruikend toestemmings API ](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Voor meer details op hoe te om privacyzorgen te behandelen die Mobiele SDK gebruiken, gelieve te verwijzen naar de sectie [ Privacy en GDPR ](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Gegevens met XDM-compatibele machtigingen direct invoeren {#batch}

U kunt XDM-Volgzame toestemmingsgegevens van een Csv- dossier door batch-opname in te voeren. Dit kan nuttig zijn als u een achterstand van eerder verzamelde toestemmingsgegevens hebt die nog in uw klantenprofielen moet worden geïntegreerd.

Volg het leerprogramma op [ in kaart brengen een Csv- dossier aan XDM ](../../../../ingestion/tutorials/map-csv/overview.md) om te leren hoe te om uw gegevensgebieden in XDM om te zetten en hen in Platform in te voeren. Wanneer u [!UICONTROL Destination] selecteert voor de toewijzing, moet u de optie **[!UICONTROL Use existing dataset]** selecteren en de gegevensset met [!DNL Profile] ingeschakelde toestemming kiezen die u eerder hebt gemaakt.

## Implementatie testen {#test-implementation}

Nadat u gegevens over klanttoestemming in uw [!DNL Profile]-Toegelaten dataset hebt opgenomen, kunt u uw bijgewerkte profielen controleren om te zien of zij toestemmingsattributen bevatten.

>[!IMPORTANT]
>
>Als u de kenmerken van een bestaand profiel in de gebruikersinterface wilt weergeven, moet u ten minste één identiteitswaarde (en de bijbehorende naamruimte) weten die aan dat profiel is gekoppeld.
>
>Als u geen toegang hebt tot deze informatie, kunt u ervoor kiezen om uw eigen gegevens over de testtoestemming in te voeren en deze te koppelen aan een identiteitswaarde/naamruimte die u bekend is.

Zie de sectie over [ het doorbladeren profielen door identiteit ](../../../../profile/ui/user-guide.md#browse) in de [!DNL Profile] gids UI voor specifieke stappen op hoe te omhoog de details van een profiel te kijken.

De nieuwe toestemmingsattributen zullen niet op het dashboard van een profiel door gebrek verschijnen. Daarom moet u naar het tabblad **[!UICONTROL Attributes]** op de detailpagina van een profiel navigeren om te bevestigen dat de gegevens zijn ingevoerd zoals u had verwacht. Zie de gids op het [ profieldashboard ](../../../../profile/ui/profile-dashboard.md) leren hoe te om het dashboard aan uw behoeften aan te passen.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Volgende stappen

Deze gids behandelde hoe te om uw verrichtingen van het Platform te vormen om de gegevens van de klantentoestemming te verwerken gebruikend de norm van de Adobe, en die attributen te hebben die in klantenprofielen worden vertegenwoordigd. U kunt de voorkeur van de klantentoestemming nu als bepalende factor in segmentkwalificatie en andere downstreamgebruiksgevallen integreren.

Voor meer informatie over de privacy-verwante mogelijkheden van het Experience Platform, zie het overzicht over [ bestuur, privacy, en veiligheid in Platform ](../../overview.md).
