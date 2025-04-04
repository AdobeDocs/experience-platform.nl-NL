---
keywords: Experience Platform;profiel;realtime klantprofiel;samenvoegbeleid;UI;gebruikersinterface;geordende tijdstempel;prioriteit gegevensset
title: Overzicht van beleid samenvoegen
type: Documentation
description: Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die Experience Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 0%

---

# Overzicht van beleid samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer u deze gegevens samenbrengt, zijn samenvoegbeleidsregels de regels die [!DNL Experience Platform] gebruikt om te bepalen hoe de prioriteit van gegevens wordt bepaald en welke gegevens worden gecombineerd om een uniforme weergave te maken.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Dit document biedt een overzicht van het samenvoegbeleid en de rol die deze spelen in Experience Platform.

## Aan de slag

Deze handleiding vereist een goed begrip van verschillende belangrijke functies van [!DNL Experience Platform] . Lees de documentatie voor de volgende services voordat u deze handleiding volgt en samenvoegt met het beleid voor samenvoegen:

* [ Real-Time Profiel van de Klant ](../home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op samengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [ de Dienst van de Identiteit van Adobe Experience Platform ](../../identity-service/home.md): Laat Real-Time het Profiel van de Klant toe door identiteiten van ongelijke gegevensbronnen te overbruggen die in [!DNL Experience Platform] worden opgenomen.
* [ Model van de Gegevens van de Ervaring (XDM) ](../../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] gegevens van de klantenervaring organiseert.

## Samenvoegingsbeleid

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren, zodat u een volledige, uniforme weergave van elk van uw individuele klanten kunt zien. Wanneer het samenbrengen van deze gegevens, is het fusiebeleid de regels die Experience Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Experience Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Wanneer de gegevens van veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl de andere klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het fusiebeleid welke informatie om in het profiel voor het individu te omvatten.

Het beleid van de fusie is privé aan uw organisatie, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manieren samen te voegen die u nodig hebt. U kunt ook een standaardsamenvoegbeleid opgeven dat wordt gebruikt als er niet expliciet een wordt opgegeven. Zie de sectie op [ standaardsamenvoegingsbeleid ](#default-merge-policy) later in dit document om meer te leren. Houd er rekening mee dat per organisatie maximaal vijf samenvoegbeleidsregels zijn toegestaan.

## Methoden samenvoegen {#merge-methods}

Elk profielfragment bevat informatie voor slechts één identiteit van het totale aantal identiteiten dat voor een individu zou kunnen bestaan. Wanneer het samenvoegen van die gegevens om een klantenprofiel te vormen, is er het potentieel voor die informatie aan conflict en de prioriteit moet worden gespecificeerd.

Het selecteren van een fusiemethode staat u toe om te specificeren welke datasetattributen om voorrang te geven als een fusieconflict tussen datasets voorkomt.

Er zijn twee mogelijke samenvoegmethoden beschikbaar voor het samenvoegbeleid. Elk van deze methoden wordt hieronder samengevat met aanvullende informatie in de volgende secties:

* **[!UICONTROL Dataset precedence]:** in het geval van een conflict, geef prioriteit aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Wanneer het selecteren van deze optie, moet u de verwante datasets en hun orde van prioriteit kiezen. Leer meer over de [ belangrijkheid van de dataset ](#dataset-precedence) fusiemethode.
* **[!UICONTROL Timestamp ordered]:** In het geval van een conflict, wordt de prioriteit gegeven aan het profielfragment dat onlangs werd bijgewerkt. Leer meer over de [ timestamp geordende ](#timestamp-ordered) fusiemethode.

### Dataset-prioriteit {#dataset-precedence}

Wanneer **[!UICONTROL Dataset precedence]** als fusiemethode voor een fusiebeleid wordt geselecteerd, kunt u prioriteit aan profielfragmenten geven die op de dataset worden gebaseerd waaruit zij kwamen. Een geval van het voorbeeldgebruik zou zijn als uw organisatie informatie aanwezig in één dataset had die over gegevens in een andere dataset voorkeur of vertrouwd is.

Als u een samenvoegbeleid wilt maken met **[!UICONTROL Dataset precedence]** , moet u de profiel- en ExperienceEvent-gegevenssets selecteren die worden opgenomen en kunt u de profielgegevenssets handmatig ordenen op prioriteit. Zodra de datasets zijn geselecteerd en bevolen, zal de hoogste dataset hoogste prioriteit worden gegeven, zal de tweede dataset tweede-hoogste zijn, etc.

### Tijdstempel geordend {#timestamp-ordered}

Aangezien profielverslagen in Experience Platform worden opgenomen, wordt een systeemtimestamp verkregen op het tijdstip van opneming en toegevoegd aan het verslag. Wanneer **[!UICONTROL Timestamp ordered]** is geselecteerd als samenvoegmethode voor een samenvoegbeleid, worden profielen samengevoegd op basis van de tijdstempel van het systeem. Met andere woorden, het samenvoegen wordt uitgevoerd op basis van de tijdstempel voor het tijdstip waarop de record in Experience Platform is opgenomen.

## Identiteitsstitatie {#id-stitching}

Identiteitsstitching ([!UICONTROL ID stitching]) is het proces om gegevensfragmenten te identificeren en hen te combineren om een volledig profielverslag te vormen. Om het verschillende stitching gedrag te illustreren, overweeg één enkele klant die met een merk gebruikend twee verschillende e-mailadressen interactie aangaat.

* **[!UICONTROL None]:** Als deze optie is geselecteerd, worden id&#39;s niet aan elkaar gekoppeld. Wanneer segmentatie voorkomt, zullen de identiteiten die tot de zelfde persoon kunnen behoren niet samen worden vastgemaakt en de segmentatie zal slechts de attributen in overweging nemen verbonden aan elke individuele identiteitskaart wanneer het bepalen als een klant voor publiekslidmaatschap in aanmerking komt. Dit kan ertoe leiden dat één enkele klant veelvoudige profielen heeft en elk profiel voor verschillende soorten publiek in aanmerking zou kunnen komen, resulterend in veelvoudige marketing berichten die naar de zelfde klant worden verzonden.
* **[!UICONTROL Private graph]:** wanneer de privégrafiek wordt geselecteerd, worden meerdere identiteiten die betrekking hebben op dezelfde persoon samengevoegd. Dit resulteert in de klant die één enkel profiel heeft en staat segmentatie toe om veelvoudige attributen van veelvoudige verwante identiteiten te overwegen wanneer het bepalen van segmentkwalificatie. In dit scenario zal de klant waarschijnlijk één profiel hebben, in aanmerking komen voor één publiek op basis van de combinatie van kenmerken tussen identiteiten en slechts één marketingbericht ontvangen.

Meer over identiteiten en hun rol in het produceren van profielen en publiek leren, gelieve te beginnen door het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md) te lezen.

## Standaardsamenvoegbeleid {#default-merge-policy}

Een organisatie kan een standaardsamenvoegbeleid maken dat door haar organisatie kan worden gebruikt bij het samenvoegen van profielfragmenten. Op deze manier kunnen gebruikers het standaardbeleid eenvoudig selecteren wanneer ze handelingen uitvoeren in Experience Platform, zoals het bekijken van klantprofielen of het maken van soorten publiek. In de meeste gevallen, tenzij een ander fusiebeleid wordt gespecificeerd, zal het standaardfusiebeleid worden gebruikt.

Elke organisatie kan veelvoudige fusiebeleid met betrekking tot één enkele XDM schemaklasse tot stand brengen, nochtans kunnen zij slechts één standaardsamenvoegbeleid hebben dat voor elke klasse wordt gedeclareerd. Uw organisatie zou bijvoorbeeld een standaardsamenvoegbeleid kunnen hebben met betrekking tot de [!DNL XDM Individual Profile] -klasse en een ander standaardsamenvoegbeleid voor een aangepaste productinventarisatie.

Als u een nieuw samenvoegbeleid creeert en het plaatst als gebrek, zal het vorige standaardfusiebeleid automatisch door het systeem worden bijgewerkt om niet meer het gebrek te zijn. Om het even welk publiek dat na dit punt in tijd wordt gecreeerd zal dit nieuwe standaardsamenvoegbeleid gebruiken.

>[!WARNING]
>
>De tellingen en het publiek van het profiel met een bestaand bijbehorend standaard samenvoegbeleid kunnen worden beïnvloed. Bovendien, zal het publiek **niet** automatisch worden bijgewerkt om het nieuwe standaardsamenvoegbeleid te gebruiken, en zal het vorige fusiebeleid blijven gebruiken.

## Volgende stappen

Na het lezen van deze handleiding weet u nu wat het samenvoegingsbeleid is en welke rol ze spelen in Experience Platform. Beginnen met het samenvoegen van beleid in Experience Platform UI, gelieve te verwijzen naar de [ gids UI van het samenvoegingsbeleid ](ui-guide.md). Om met samenvoegbeleid te werken gebruikend API, bezoek de [ gids van het beleid API van de samenvoegen ](../api/merge-policies.md).
