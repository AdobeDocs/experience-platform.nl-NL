---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Verwerking van toestemming in Adobe Experience Platform
description: Leer hoe u in Adobe Experience Platform goedkeuringssignalen kunt verwerken met de Adobe 2.0-standaard.
role: Developer
feature: Consent
exl-id: cd76a3f6-ae55-4d75-9b30-900fadb4664f
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 0%

---

# Goedkeuring in Adobe Experience Platform

Adobe Experience Platform staat u toe om de toestemmingsgegevens te verwerken u van uw klanten hebt verzameld en het te integreren in uw opgeslagen klantenprofielen. Deze gegevens kunnen dan door stroomafwaartse processen worden gebruikt om te bepalen of de gegevensinzameling voor een specifieke klant voorkomt, of of hun profielen voor specifieke doeleinden worden gebruikt. De gegevens over machtigingen voor een bepaald profiel kunnen bijvoorbeeld bepalen of het profiel kan worden opgenomen in een geëxporteerd publiekssegment of dat het kan deelnemen aan specifieke marketingkanalen zoals e-mail, tekstberichten of pushberichten.

Dit document biedt een overzicht van hoe u uw Experience Platform-gegevensbewerkingen kunt configureren om gegevens over toestemming van klanten die zijn gegenereerd door een platform voor beheer van toestemming (CMP), in te voeren en deze gegevens te integreren in klantprofielen voor downstreamgebruik.

>[!NOTE]
>
>Dit document richt zich op het verwerken van toestemmingsgegevens gebruikend de norm van Adobe. Als u toestemmingsgegevens in overeenstemming met IAB Transparantie en het Kader van de Toestemming (TCF) 2.0 verwerkt, zie de gids op [&#x200B; TCF 2.0 steun in Adobe Real-Time Customer Data Platform &#x200B;](../iab/overview.md).

## Vereisten

Deze handleiding vereist een goed begrip van de verschillende Experience Platform-diensten die betrokken zijn bij de verwerking van toestemmingsgegevens:

* [&#x200B; Model van de Gegevens van de Ervaring (XDM) &#x200B;](/help/xdm/home.md): Het gestandaardiseerde kader waardoor Experience Platform gegevens van de klantenervaring organiseert.
* [&#x200B; de Dienst van de Identiteit van Adobe Experience Platform &#x200B;](/help/identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [&#x200B; Real-Time het Profiel van de Klant &#x200B;](/help/profile/home.md): Gebruikt [!DNL Identity Service] mogelijkheden om gedetailleerde klantenprofielen van uw datasets in real time tot stand te brengen. Het profiel van de Klant in real time trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [&#x200B; Adobe Experience Platform Web SDK &#x200B;](/help/collection/js/js-overview.md): Een cliënt-kant bibliotheek van JavaScript die u toestaat om diverse diensten van Experience Platform in uw klant-onder ogen ziet website te integreren.
   * [&#x200B; de toestemmingsbevelen van SDK &#x200B;](/help/collection/js/commands/setconsent.md): Een gebruik-geval overzicht van de toestemming-verwante bevelen van SDK die in deze gids worden getoond.
* [&#x200B; de Dienst van de Segmentatie van Adobe Experience Platform &#x200B;](/help/segmentation/home.md): Staat u toe om gegevens van het Profiel van de Klant in real time in groepen individuen te verdelen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.

## Samenvatting van de verwerkingsstroom van de toestemming {#summary}

Hieronder wordt beschreven hoe toestemmingsgegevens worden verwerkt nadat het systeem correct is geconfigureerd:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Bij elke pagina die wordt geladen (of wanneer uw CMP een wijziging in de voorkeuren voor toestemming detecteert), wijst een aangepast script op uw site de huidige voorkeuren toe aan een standaard XDM-object. Dit object wordt vervolgens doorgegeven aan de Experience Platform Web SDK `setConsent` -opdracht.
1. Wanneer `setConsent` wordt aangeroepen, controleert de Experience Platform Web SDK of de toestemmingswaarden verschillen van de waarden die het het laatst heeft ontvangen. Als de waarden verschillend zijn (of er geen vorige waarde is), worden de gestructureerde toestemmings/voorkeursgegevens verzonden naar Adobe Experience Platform.
1. De toestemmings-/voorkeursgegevens worden opgenomen in een gegevensset waarvoor [!DNL Profile] is ingeschakeld en waarvan het schema toestemmings-/voorkeursvelden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van de toestemming van CMP, kunnen toestemmingsgegevens ook naar Experience Platform stromen via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile] -gegevensset worden geüpload.

### Goedkeuring

In de huidige versie van de steun van de toestemmingsverwerking in Experience Platform, slechts wordt de toestemming van de gegevensinzameling (`collect.val`) automatisch afgedwongen door het Web SDK van Experience Platform. Terwijl meer korrelige toestemmingen en voorkeur in klantenprofielen kunnen worden verzameld en worden voortgeduurd, moeten deze extra signalen manueel in uw eigen stroomafwaartse processen worden afgedwongen.

>[!NOTE]
>
>Raadpleeg de handleiding over het [[!UICONTROL Consents and Preferences] gegevenstype &#x200B;](/help/xdm/data-types/consents.md) voor meer informatie over de structuur van de bovenstaande XDM-toestemmingsvelden.

Zodra het systeem is gevormd, interpreteert het Web SDK van Experience Platform de waarde van de gegevensinzamelingstoestemming voor de huidige gebruiker om te bepalen als de gegevens naar Adobe Experience Platform Edge Network zouden moeten worden verzonden, van de cliënt zouden moeten worden gelaten vallen, of tot de toestemming van de gegevensinzameling aan of ja of nr wordt geplaatst.

## Bepalen hoe gegevens over klanttoestemming binnen uw CMP worden gegenereerd {#consent-data}

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een algemene manier om dit te bereiken is door gebruik te maken van een dialoogvenster voor cookie-toestemming, vergelijkbaar met het volgende voorbeeld:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

In dit dialoogvenster kan de klant kiezen of hij of zij voor zijn of haar gegevens gebruikmaakt van specifieke gevallen voor marketing en personalisatie. Deze toestemmingen en voorkeur zouden aan het gegevensmodel moeten in overeenstemming zijn dat u voor [!DNL Profile] - toegelaten dataset in de volgende stap bepaalt.

## Standaardtoestemmingsvelden toevoegen aan een gegevensset met [!DNL Profile] mogelijkheden {#dataset}

De gegevens van de toestemming van de klant moeten naar een [!DNL Profile]-Toegelaten dataset worden verzonden het waarvan schema toestemmingsgebieden bevat. Deze gebieden moeten in het zelfde schema en de dataset worden omvat die u gebruikt om attributeninformatie over individuele klanten te vangen.

Verwijs naar het leerprogramma op [&#x200B; vormend een dataset voor het vangen van toestemmingsgegevens &#x200B;](./dataset.md) voor gedetailleerde stappen op hoe te om deze vereiste gebieden aan a [!DNL Profile]-Toegelaten dataset toe te voegen alvorens met deze gids verder te gaan.

## Beleid voor samenvoegen van [!DNL Profile] bijwerken en gegevens over toestemming opnemen {#merge-policies}

Zodra u een [!DNL Profile]-Toegelaten dataset voor de gegevens van de verwerkingstoestemming hebt gecreeerd, moet u ervoor zorgen dat uw samenvoegbeleid is gevormd om toestemmingsgebieden in elk klantenprofiel altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

>[!NOTE]
>
>Als u geen conflicterende datasets hebt, zou u timestamp belangrijkheid voor uw samenvoegbeleid in plaats daarvan moeten plaatsen. Dit helpt ervoor te zorgen dat de recentste toestemming die door een klant wordt gespecificeerd de toestemmingsinstelling is die wordt gebruikt.

Voor meer informatie over hoe te met fusiebeleid te werken, begin door het [&#x200B; overzicht van het samenvoegingsbeleid &#x200B;](../../../../profile/merge-policies/overview.md) te lezen. Wanneer vestiging moet uw samenvoegbeleid, u ervoor zorgen dat uw profielen alle vereiste toestemmingsattributen omvatten die door de [!UICONTROL Consents and Preferences] groep van het schemagebied worden verstrekt, zoals die in de gids over [&#x200B; wordt geschetst datasetvoorbereiding &#x200B;](./dataset.md).

## Goedkeuringsgegevens in Experience Platform plaatsen

Zodra u uw datasets en samenvoegbeleid hebt om de vereiste toestemmingsgebieden in uw klantenprofielen te vertegenwoordigen, is de volgende stap de toestemmingsgegevens zelf in Experience Platform te brengen.

In de eerste plaats moet u de Adobe Experience Platform Web SDK gebruiken om toestemmingsgegevens naar Experience Platform te verzenden wanneer de CMP gebeurtenissen voor het wijzigen van de instemming detecteert. Als u toestemmingsgegevens op een mobiel platform verzamelt, zou u Adobe Experience Platform Mobile SDK moeten gebruiken. U kunt er ook voor kiezen om de verzamelde toestemmingsgegevens rechtstreeks in te voeren door deze toe te wijzen aan het XDM-schema van uw toestemmingsdataset en deze via batch-opname naar Experience Platform te verzenden.

Nadere bijzonderheden over elk van deze methoden zijn te vinden in de onderstaande punten.

### Experience Platform Web SDK configureren om toestemmingsgegevens te verwerken {#web-sdk}

Nadat u uw CMP hebt geconfigureerd om te luisteren naar gebeurtenissen voor het wijzigen van de toestemming op uw website, kunt u de Experience Platform Web SDK integreren om de bijgewerkte toestemmingsinstellingen te ontvangen en deze naar Experience Platform te verzenden bij elke laadpagina en telkens wanneer gebeurtenissen voor het wijzigen van de toestemming plaatsvinden. Zie de gids bij [&#x200B; vormend het Web SDK om de gegevens van de klantentoestemming &#x200B;](../sdk.md) voor meer informatie te verwerken.

### Experience Platform Mobile SDK configureren voor het verwerken van toestemmingsgegevens {#mobile-sdk}

Als in uw mobiele toepassing de voorkeursinstellingen voor toestemming van de klant zijn vereist, kunt u de Experience Platform Mobile SDK integreren om toestemmingsinstellingen op te halen en bij te werken en deze naar Experience Platform te verzenden telkens wanneer de API voor toestemming wordt aangeroepen.

Zie de Mobiele documentatie van SDK voor [&#x200B; het vormen van de Mobiele uitbreiding van de Toestemming &#x200B;](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) en [&#x200B; gebruikend toestemmings API &#x200B;](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/api-reference/). Voor meer details op hoe te om privacyzorgen te behandelen die Mobiele SDK gebruiken, gelieve te verwijzen naar de sectie [&#x200B; Privacy en GDPR &#x200B;](https://developer.adobe.com/client-sdks/resources/privacy-and-gdpr/).

### Gegevens met XDM-compatibele machtigingen direct invoeren {#batch}

U kunt XDM-Volgzame toestemmingsgegevens van een Csv- dossier door batch-opname in te voeren. Dit kan nuttig zijn als u een achterstand van eerder verzamelde toestemmingsgegevens hebt die nog in uw klantenprofielen moet worden geïntegreerd.

Volg het leerprogramma op [&#x200B; in kaart brengen een Csv- dossier aan XDM &#x200B;](../../../../ingestion/tutorials/map-csv/overview.md) om te leren hoe te om uw gegevensgebieden in XDM om te zetten en hen in Experience Platform in te voeren. Wanneer u [!UICONTROL Destination] selecteert voor de toewijzing, moet u de optie **[!UICONTROL Use existing dataset]** selecteren en de gegevensset met [!DNL Profile] ingeschakelde toestemming kiezen die u eerder hebt gemaakt.

## Implementatie testen {#test-implementation}

Nadat u gegevens over klanttoestemming in uw [!DNL Profile]-Toegelaten dataset hebt opgenomen, kunt u uw bijgewerkte profielen controleren om te zien of zij toestemmingsattributen bevatten.

>[!IMPORTANT]
>
>Als u de kenmerken van een bestaand profiel in de gebruikersinterface wilt weergeven, moet u ten minste één identiteitswaarde (en de bijbehorende naamruimte) weten die aan dat profiel is gekoppeld.
>
>Als u geen toegang hebt tot deze informatie, kunt u ervoor kiezen om uw eigen gegevens over de testtoestemming in te voeren en deze te koppelen aan een identiteitswaarde/naamruimte die u bekend is.

Zie de sectie over [&#x200B; het doorbladeren profielen door identiteit &#x200B;](../../../../profile/ui/user-guide.md#browse) in de [!DNL Profile] gids UI voor specifieke stappen op hoe te omhoog de details van een profiel te kijken.

De nieuwe toestemmingsattributen zullen niet op het dashboard van een profiel door gebrek verschijnen. Daarom moet u naar het tabblad **[!UICONTROL Attributes]** op de detailpagina van een profiel navigeren om te bevestigen dat de gegevens zijn ingevoerd zoals u had verwacht. Zie de gids op het [&#x200B; profieldashboard &#x200B;](../../../../profile/ui/profile-dashboard.md) leren hoe te om het dashboard aan uw behoeften aan te passen.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Experience Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Experience Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Experience Platform and the appropriate profile attributes are updated accordingly.
-->

## Volgende stappen

In deze handleiding wordt beschreven hoe u uw Experience Platform-bewerkingen kunt configureren voor het verwerken van gegevens met toestemming van klanten aan de hand van de Adobe-standaard en hoe u deze kenmerken kunt laten weergeven in klantprofielen. U kunt de voorkeur van de klantentoestemming nu als bepalende factor in segmentkwalificatie en andere downstreamgebruiksgevallen integreren.

Voor meer informatie over Experience Platform op privacy betrekking hebbende mogelijkheden, zie het overzicht over [&#x200B; bestuur, privacy, en veiligheid in Experience Platform &#x200B;](../../overview.md).
