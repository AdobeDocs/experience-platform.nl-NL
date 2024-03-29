---
keywords: Experience Platform;profiel;realtime klantprofiel;samenvoegbeleid;UI;gebruikersinterface;geordende tijdstempel;prioriteit gegevensset
title: Overzicht van beleid samenvoegen
type: Documentation
description: Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 0%

---

# Overzicht van beleid samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Bij het samenvoegen van deze gegevens gelden als samenvoegbeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens voorrang krijgen en welke gegevens worden gecombineerd om een verenigde mening tot stand te brengen.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Dit document biedt een overzicht van het samenvoegbeleid en de rol die deze spelen in Experience Platform.

## Aan de slag

Deze gids vereist een goed begrip van verscheidene belangrijke [!DNL Experience Platform] functies. Lees de documentatie voor de volgende services voordat u deze handleiding volgt en samenvoegt met het beleid voor samenvoegen:

* [Klantprofiel in realtime](../home.md): Biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Schakelt het Real-Time Profiel van de Klant in door identiteiten te overbruggen van verschillende gegevensbronnen die worden opgenomen in [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): Het gestandaardiseerde kader waarbinnen [!DNL Platform] organiseert de gegevens van de klantenervaring.

## Samenvoegingsbeleid

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren, zodat u een volledige, uniforme weergave van elk van uw individuele klanten kunt zien. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Wanneer de gegevens van veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl de andere klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het fusiebeleid welke informatie om in het profiel voor het individu te omvatten.

Het beleid van de fusie is privé aan uw organisatie, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manieren samen te voegen die u nodig hebt. U kunt ook een standaardsamenvoegbeleid opgeven dat wordt gebruikt als er niet expliciet een wordt opgegeven. Zie de sectie over [standaardbeleid voor samenvoegen](#default-merge-policy) later in dit document voor meer informatie. Houd er rekening mee dat per organisatie maximaal vijf samenvoegbeleidsregels zijn toegestaan.

## Methoden samenvoegen {#merge-methods}

Elk profielfragment bevat informatie voor slechts één identiteit van het totale aantal identiteiten dat voor een individu zou kunnen bestaan. Wanneer het samenvoegen van die gegevens om een klantenprofiel te vormen, is er het potentieel voor die informatie aan conflict en de prioriteit moet worden gespecificeerd.

Het selecteren van een fusiemethode staat u toe om te specificeren welke datasetattributen om voorrang te geven als een fusieconflict tussen datasets voorkomt.

Er zijn twee mogelijke samenvoegmethoden beschikbaar voor het samenvoegbeleid. Elk van deze methoden wordt hieronder samengevat met aanvullende informatie in de volgende secties:

* **[!UICONTROL Dataset precedence]:** In geval van een conflict, geef prioriteit aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Wanneer het selecteren van deze optie, moet u de verwante datasets en hun orde van prioriteit kiezen. Meer informatie over de [gegevenssetprioriteit](#dataset-precedence) samenvoegmethode.
* **[!UICONTROL Timestamp ordered]:** In geval van een conflict wordt prioriteit gegeven aan het profielfragment dat het laatst is bijgewerkt. Meer informatie over de [timestamp geordend](#timestamp-ordered) samenvoegmethode.

### Dataset-prioriteit {#dataset-precedence}

Wanneer **[!UICONTROL Dataset precedence]** wordt geselecteerd als fusiemethode voor een fusiebeleid, kunt u prioriteit aan profielfragmenten geven die op de dataset worden gebaseerd waaruit zij kwamen. Een geval van het voorbeeldgebruik zou zijn als uw organisatie informatie aanwezig in één dataset had die over gegevens in een andere dataset voorkeur of vertrouwd is.

Om een samenvoegbeleid tot stand te brengen gebruikend **[!UICONTROL Dataset precedence]**, moet u de datasets van het Profiel en van ExperienceEvent selecteren die inbegrepen zijn en dan kunt u de datasets van het Profiel voor belangrijkheid manueel tot stand brengen. Zodra de datasets zijn geselecteerd en bevolen, zal de hoogste dataset hoogste prioriteit worden gegeven, zal de tweede dataset tweede-hoogste zijn, etc.

### Tijdstempel geordend {#timestamp-ordered}

Aangezien profielverslagen in Experience Platform worden opgenomen, wordt een systeemtimestamp verkregen op het tijdstip van opneming en toegevoegd aan het verslag. Wanneer **[!UICONTROL Timestamp ordered]** is geselecteerd als samenvoegmethode voor een samenvoegbeleid, worden profielen samengevoegd op basis van de tijdstempel van het systeem. Met andere woorden, het samenvoegen wordt uitgevoerd op basis van de tijdstempel voor het tijdstip waarop de record in Platform is opgenomen.

## Identiteitsstitatie {#id-stitching}

Identiteitsstitatie ([!UICONTROL ID stitching]) is het proces van het identificeren van gegevensfragmenten en het combineren van deze fragmenten om een volledige profielrecord te vormen. Om het verschillende stitching gedrag te illustreren, overweeg één enkele klant die met een merk gebruikend twee verschillende e-mailadressen interactie aangaat.

* **[!UICONTROL None]:** Als deze optie is geselecteerd, worden id&#39;s niet aan elkaar gekoppeld. Wanneer segmentatie voorkomt, zullen de identiteiten die tot de zelfde persoon kunnen behoren niet samen worden vastgemaakt en de segmentatie zal slechts de attributen in overweging nemen verbonden aan elke individuele identiteitskaart wanneer het bepalen als een klant voor publiekslidmaatschap in aanmerking komt. Dit kan ertoe leiden dat één enkele klant veelvoudige profielen heeft en elk profiel voor verschillende soorten publiek in aanmerking zou kunnen komen, resulterend in veelvoudige marketing berichten die naar de zelfde klant worden verzonden.
* **[!UICONTROL Private graph]:** Als de privégrafiek is geselecteerd, worden meerdere identiteiten met betrekking tot dezelfde persoon samengevoegd. Dit resulteert in de klant die één enkel profiel heeft en staat segmentatie toe om veelvoudige attributen van veelvoudige verwante identiteiten te overwegen wanneer het bepalen van segmentkwalificatie. In dit scenario zal de klant waarschijnlijk één profiel hebben, in aanmerking komen voor één publiek op basis van de combinatie van kenmerken tussen identiteiten en slechts één marketingbericht ontvangen.

Als u meer wilt weten over identiteiten en hun rol bij het genereren van profielen en publiek, leest u eerst de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Standaardsamenvoegbeleid {#default-merge-policy}

Een organisatie kan een standaardsamenvoegbeleid maken dat door haar organisatie kan worden gebruikt bij het samenvoegen van profielfragmenten. Op deze manier kunnen gebruikers het standaardbeleid eenvoudig selecteren wanneer ze handelingen in het Experience Platform uitvoeren, zoals het weergeven van klantprofielen of het maken van soorten publiek. In de meeste gevallen, tenzij een ander fusiebeleid wordt gespecificeerd, zal het standaardfusiebeleid worden gebruikt.

Elke organisatie kan veelvoudige fusiebeleid met betrekking tot één enkele XDM schemaklasse tot stand brengen, nochtans kunnen zij slechts één standaardsamenvoegbeleid hebben dat voor elke klasse wordt gedeclareerd. Uw organisatie kan bijvoorbeeld een standaardsamenvoegbeleid hebben dat betrekking heeft op de [!DNL XDM Individual Profile] en een ander standaardsamenvoegbeleid voor een aangepaste, samengestelde klasse Product Inventory.

Als u een nieuw samenvoegbeleid creeert en het plaatst als gebrek, zal het vorige standaardfusiebeleid automatisch door het systeem worden bijgewerkt om niet meer het gebrek te zijn.

>[!WARNING]
>
>De tellingen en het publiek van het profiel met een bestaand bijbehorend standaard samenvoegbeleid kunnen worden beïnvloed. Om het even welk publiek dat een standaard toegepaste samenvoegbeleid heeft zal aan het nieuwe standaardfusiebeleid worden bijgewerkt.

## Volgende stappen

Na het lezen van deze handleiding weet u nu wat het samenvoegingsbeleid is en welke rol zij binnen Experience Platform spelen. Als u wilt beginnen te werken met samenvoegbeleid in de gebruikersinterface van het Experience Platform, raadpleegt u de [UI-hulplijn voor samenvoegbeleid](ui-guide.md). Als u wilt werken met samenvoegbeleid met de API, gaat u naar de [API-eindplijn voor samenvoegbeleid](../api/merge-policies.md).
