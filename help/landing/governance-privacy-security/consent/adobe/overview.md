---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Verwerking van toestemming in Adobe Experience Platform
topic: aan de slag
description: Leer hoe u in Adobe Experience Platform goedkeuringssignalen voor klanten verwerkt met de Adobe 2.0-standaard.
translation-type: tm+mt
source-git-commit: f7fde2cb6828ebdd1763171008858fdd7242c784
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 0%

---


# Goedkeuring in Adobe Experience Platform

Adobe Experience Platform staat u toe om de toestemmingsgegevens te verwerken u van uw klanten hebt verzameld en het te integreren in uw opgeslagen klantenprofielen. Deze gegevens kunnen dan door stroomafwaartse processen worden gebruikt om te bepalen of de gegevensinzameling voor een specifieke klant voorkomt, of of hun profielen voor specifieke doeleinden worden gebruikt. De gegevens over machtigingen voor een bepaald profiel kunnen bijvoorbeeld bepalen of het profiel kan worden opgenomen in een geëxporteerd publiekssegment of dat het kan deelnemen aan specifieke marketingkanalen zoals e-mail, tekstberichten of pushberichten.

Dit document biedt een overzicht van hoe u de gegevensbewerkingen van uw Platform kunt configureren om gegevens over toestemming van de klant die zijn gegenereerd door een platform voor beheer van toestemming (CMP), in te voeren en deze gegevens te integreren in klantprofielen voor gevallen van downstreamgebruik.

>[!NOTE]
>
>Dit document richt zich op het verwerken van toestemmingsgegevens die de norm Adobe gebruiken. Als u toestemmingsgegevens in overeenstemming met IAB Transparantie en het Kader van de Toestemming (TCF) 2.0 verwerkt, zie de gids over [TCF 2.0 steun in het Platform van Gegevens van de Klant in real time](../iab/overview.md).

## Vereisten

Deze handleiding vereist een goed begrip van de verschillende diensten van de Experience Platform die betrokken zijn bij de verwerking van gegevens over de toestemming:

* [XDM (Experience Data Model)](../../../../xdm/home.md): Het gestandaardiseerde kader waardoor het Experience Platform gegevens van de klantenervaring organiseert.
* [Adobe Experience Platform Identity Service](../../../../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel](../../../../profile/home.md) in realtime: Gebruikt  [!DNL Identity Service] mogelijkheden om gedetailleerde klantenprofielen van uw datasets in echt tot stand te brengen - tijd. Het profiel van de Klant in real time trekt gegevens van het meer van Gegevens en handhaaft klantenprofielen in zijn eigen afzonderlijke gegevensopslag.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Een JavaScript-bibliotheek aan de clientzijde waarmee u verschillende services voor Platforms kunt integreren in uw klantgerichte website.
   * [Opdrachten](../../../../edge/consent/supporting-consent.md) voor SDK-toestemming: Een gebruiksscenario-overzicht van de toestemmingsgerelateerde bevelen van SDK in deze gids wordt getoond die.
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md): Staat u toe om gegevens van het Profiel van de Klant in real time in groepen individuen te verdelen die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.

## Samenvatting van de verwerkingsstroom van de toestemming {#summary}

Hieronder wordt beschreven hoe toestemmingsgegevens worden verwerkt nadat het systeem correct is geconfigureerd:

1. Een klant geeft via een dialoogvenster op uw website zijn voorkeuren voor het verzamelen van gegevens weer.
1. Bij elke pagina die wordt geladen (of wanneer uw CMP een wijziging in de voorkeuren voor toestemming detecteert), wijst een aangepast script op uw site de huidige voorkeuren toe aan een standaard XDM-object. Dit voorwerp wordt dan overgegaan tot het Platform Web SDK `setConsent` bevel.
1. Wanneer `setConsent` wordt geroepen, controleert het Web SDK van het Platform of de toestemmingswaarden van die verschillend zijn het laatst ontving. Als de waarden verschillend zijn (of er geen vorige waarde is), worden de gestructureerde toestemmings/voorkeursgegevens verzonden naar Adobe Experience Platform.
1. De toestemmings/voorkeursgegevens worden opgenomen in een [!DNL Profile]-Toegelaten dataset het waarvan schema toestemmings/voorkeur gebieden bevat.

Naast SDK-opdrachten die worden geactiveerd door de haken voor wijziging van de toestemming van CMP, kunnen toestemmingsgegevens ook in het Experience Platform stromen via door de klant gegenereerde XDM-gegevens die rechtstreeks naar een [!DNL Profile]-compatibele dataset worden geüpload.

### Goedkeuring

In de huidige versie van de steun van de toestemmingsverwerking in Platform, slechts wordt de toestemming van de gegevensinzameling (`collect.val`) automatisch afgedwongen door het Web SDK van het Platform. Terwijl meer korrelige toestemmingen en voorkeur in klantenprofielen kunnen worden verzameld en worden voortgeduurd, moeten deze extra signalen manueel in uw eigen stroomafwaartse processen worden afgedwongen.

>[!NOTE]
>
>Voor meer informatie over de structuur van de XDM toestemmingsgebieden hierboven, verwijs naar de gids op [het gegevenstype van de Inhoud &amp; van de Voorkeur ](../../../../xdm/data-types/consents.md).

Zodra het systeem is gevormd, interpreteert het Web SDK van het Platform de waarde van de gegevensinzamelingstoestemming voor de huidige gebruiker om te bepalen als de gegevens naar het Netwerk van de Rand van Adobe Experience Platform zouden moeten worden verzonden, van de cliënt, zouden moeten worden gelaten vallen, of tot de toestemming van de gegevensinzameling aan of ja of nr wordt geplaatst.

## Bepaal hoe u gegevens over klanttoestemming binnen uw CMP {#consent-data} kunt genereren

Aangezien elk CMP-systeem uniek is, moet u de beste manier bepalen om uw klanten toestemming te geven wanneer ze met uw service communiceren. Een algemene manier om dit te bereiken is door gebruik te maken van een dialoogvenster voor cookie-toestemming, vergelijkbaar met het volgende voorbeeld:

![](../../../images/governance-privacy-security/consent/adobe/overview/consent-dialog.png)

In dit dialoogvenster kan de klant kiezen of hij of zij voor zijn of haar gegevens gebruikmaakt van specifieke gevallen voor marketing en personalisatie. Deze toestemmingen en voorkeur zouden aan het gegevensmodel moeten in overeenstemming zijn dat u voor [!DNL Profile]-Toegelaten dataset in de volgende stap bepaalt.

## Voeg gestandaardiseerde toestemmingsgebieden aan een [!DNL Profile]-Toegelaten dataset {#dataset} toe

De gegevens van de toestemming van de klant moeten naar een [!DNL Profile]-Toegelaten dataset worden verzonden het waarvan schema toestemmingsgebieden bevat. Deze gebieden moeten in het zelfde schema en de dataset worden omvat die u gebruikt om attributeninformatie over individuele klanten te vangen.

Raadpleeg de zelfstudie over [het configureren van een gegevensset voor het vastleggen van toestemmingsgegevens](./dataset.md) voor gedetailleerde stappen over het toevoegen van deze vereiste velden aan een [!DNL Profile]-compatibele gegevensset voordat u doorgaat met deze handleiding.

## [!DNL Profile] samenvoegbeleid bijwerken om gegevens over toestemming {#merge-policies} op te nemen

Zodra u een [!DNL Profile]-Toegelaten dataset voor de gegevens van de verwerkingstoestemming hebt gecreeerd, moet u ervoor zorgen dat uw samenvoegbeleid is gevormd om toestemmingsgebieden in elk klantenprofiel altijd te omvatten. Dit impliceert het plaatsen van datasetbelangrijkheid zodat uw toestemmingsdataset boven andere potentieel conflicterende datasets voorrang krijgt.

>[!NOTE]
>
>Als u geen conflicterende datasets hebt, zou u timestamp belangrijkheid voor uw samenvoegbeleid in plaats daarvan moeten plaatsen. Dit helpt ervoor te zorgen dat de recentste toestemming die door een klant wordt gespecificeerd de toestemmingsinstelling is die wordt gebruikt.

Voor meer informatie over hoe te om met fusiebeleid te werken, verwijs naar [de gebruikersgids van het samenvoegingsbeleid](../../../../profile/ui/merge-policies.md). Wanneer het opzetten van uw fusiebeleid, moet u ervoor zorgen dat uw profielen alle vereiste toestemmingsattributen omvatten die door de Consents &amp; de mengen van Voorkeur worden verstrekt, zoals die in de gids over [datasetvoorbereiding](./dataset.md) worden geschetst.

## Goedkeuringsgegevens in Platform plaatsen

Zodra u uw datasets en fusiebeleid hebt om de vereiste toestemmingsgebieden in uw klantenprofielen te vertegenwoordigen, is de volgende stap de toestemmingsgegevens zelf in Platform te brengen.

Hoofdzakelijk, zou u SDK van het Web van Adobe Experience Platform moeten gebruiken om toestemmingsgegevens naar Platform te verzenden wanneer de toestemming-verandering gebeurtenissen door uw CMP worden ontdekt. Als u reeds toestemmingsgegevens hebt die elders worden opgeslagen, echter, kunt u ook verkiezen om uw verzamelde toestemmingsgegevens direct in te voeren door het aan het XDM schema van uw toestemmingsdataset in kaart te brengen en het te verzenden naar Platform door partijopname.

Nadere bijzonderheden over elk van deze methoden zijn te vinden in de onderstaande punten.

### Integreer de SDK van het Web Experience Platform om gegevens van de klanteninstemming {#sdk} te verwerken

Zodra u uw CMP hebt gevormd om op toestemmings-verandering gebeurtenissen op uw website te luisteren, kunt u het Web SDK van het Experience Platform integreren om de bijgewerkte toestemmingsmontages te ontvangen en hen naar Platform te verzenden wanneer een toestemming-verandering gebeurtenis voorkomt. Volg de handleiding bij [het configureren van de SDK voor het verwerken van gegevens voor klanttoestemming](./sdk.md) voor meer informatie.

### Voeg XDM-compatibele toestemmingsgegevens direct {#batch} in

U kunt XDM-Volgzame toestemmingsgegevens van een Csv- dossier door batch-opname in te voeren. Dit kan nuttig zijn als u een achterstand van eerder verzamelde toestemmingsgegevens hebt die nog in uw klantenprofielen moet worden geïntegreerd.

Volg de zelfstudie over [het toewijzen van een CSV-bestand aan XDM](../../../../ingestion/tutorials/map-a-csv-file.md) om te leren hoe u uw gegevensvelden omzet in XDM en deze in Platform in te voeren. Wanneer het selecteren van [!UICONTROL Destination] voor de afbeelding, zorg ervoor dat u **[!UICONTROL Use existing dataset]** optie selecteert en [!DNL Profile]-Toegelaten toestemmingsdataset kiest u eerder creeerde.

## Implementatie {#test-implementation} testen

Nadat u de gegevens van de klantentoestemming in uw [!DNL Profile]-Toegelaten dataset hebt opgenomen, kunt u uw bijgewerkte profielen controleren om te zien of zij toestemmingsattributen bevatten.

>[!IMPORTANT]
>
>Als u de kenmerken van een bestaand profiel in de gebruikersinterface wilt weergeven, moet u ten minste één identiteitswaarde (en de bijbehorende naamruimte) weten die aan dat profiel is gekoppeld.
>
>Als u geen toegang hebt tot deze informatie, kunt u ervoor kiezen om uw eigen gegevens over de testtoestemming in te voeren en deze te koppelen aan een identiteitswaarde/naamruimte die u bekend is.

Zie de sectie over [het doorbladeren profielen door identiteit](../../../../profile/ui/user-guide.md#browse) in [!DNL Profile] UI gids voor specifieke stappen op hoe te om de details van een profiel omhoog te kijken.

De nieuwe toestemmingsattributen zullen niet op het dashboard van een profiel door gebrek verschijnen. Daarom moet u naar het **[!UICONTROL Attributes]** lusje op de detailspagina van een profiel navigeren om te bevestigen dat zij zoals verwacht zijn opgenomen. Zie de handleiding op het [profiel dashboard](../../../../profile/ui/profile-dashboard.md) voor informatie over het aanpassen van het dashboard aan uw wensen.

<!-- (To be included once CJM is GA)
## Handling consent in Customer Journey Management

If you are using Customer Journey Management, after confirming that your profiles and segments contain consent data, you can start honoring customer [marketing preferences](../../../../xdm/data-types/consents.md#marketing) when pulling segments from Platform. Specifically, profiles who have opted out of the email marketing preference should not be included in segments that are targeted for email campaigns.

Customer Journey Management can also send consent-change signals back to Platform. When a customer selects an "unsubscribe" link in an email message, the updated consent preference is sent to Platform and the appropriate profile attributes are updated accordingly.
-->

## Volgende stappen

Deze gids behandelde hoe te om uw verrichtingen van het Platform te vormen om de gegevens van de klantentoestemming te verwerken gebruikend de norm van de Adobe, en die attributen te hebben die in klantenprofielen worden vertegenwoordigd. U kunt de voorkeur van de klantentoestemming nu als bepalende factor in segmentkwalificatie en andere downstreamgebruiksgevallen integreren.

Voor meer informatie over de privacy-verwante mogelijkheden van Experience Platform, zie het overzicht over [governance, privacy, en veiligheid in Platform](../../overview.md).