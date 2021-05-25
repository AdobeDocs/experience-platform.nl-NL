---
keywords: Experience Platform;profiel;realtime klantprofiel;samenvoegbeleid;UI;gebruikersinterface;geordende tijdstempel;prioriteit gegevensset
title: Overzicht van beleid samenvoegen
type: Documentation
description: Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om de verenigde mening tot stand te brengen.
source-git-commit: c2cc1428e3a70cf987adab583e9f9fb5d5140c74
workflow-type: tm+mt
source-wordcount: '1467'
ht-degree: 0%

---


# Overzicht van beleid samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het samenbrengen van deze gegevens, zijn het fusiebeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een verenigde mening tot stand te brengen.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Dit document biedt een overzicht van het samenvoegbeleid en de rol die deze spelen in Experience Platform.

## Aan de slag

Deze gids vereist een werkend inzicht van verscheidene belangrijke [!DNL Experience Platform] eigenschappen. Lees de documentatie voor de volgende services voordat u deze handleiding volgt en samenvoegt met het beleid voor samenvoegen:

* [Klantprofiel](../home.md) in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Laat het Profiel van de Klant in real time toe door identiteiten van ongelijke gegevensbronnen te overbruggen die in worden opgenomen  [!DNL Platform].
* [XDM (Experience Data Model)](../../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Platform] klantenervaring worden georganiseerd.

## Samenvoegingsbeleid

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren, zodat u een volledige, uniforme weergave van elk van uw individuele klanten kunt zien. Wanneer het brengen van deze gegevens samen, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Wanneer de gegevens van veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl de andere klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het fusiebeleid welke informatie om in het profiel voor het individu te omvatten.

Het beleid van de fusie is privé aan uw organisatie IMS, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manieren samen te voegen die u nodig hebt. U kunt ook een standaardsamenvoegbeleid opgeven dat wordt gebruikt als er niet expliciet een wordt opgegeven. Zie de sectie over [standaardsamenvoegbeleid](#default-merge-policy) later in dit document voor meer informatie.

## Methoden {#merge-methods} samenvoegen

Elk profielfragment bevat informatie voor slechts één identiteit van het totale aantal identiteiten dat voor een individu zou kunnen bestaan. Wanneer het samenvoegen van die gegevens om een klantenprofiel te vormen, is er het potentieel voor die informatie aan conflict en de prioriteit moet worden gespecificeerd.

Het selecteren van een fusiemethode staat u toe om te specificeren welke datasetattributen om voorrang te geven als een fusieconflict tussen datasets voorkomt.

Er zijn twee mogelijke samenvoegmethoden beschikbaar voor het samenvoegbeleid. Elk van deze methoden wordt hieronder samengevat met aanvullende informatie in de volgende secties:

* **[!UICONTROL Dataset precedence]:** In geval van een conflict, geef prioriteit aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Wanneer het selecteren van deze optie, moet u de verwante datasets en hun orde van prioriteit kiezen. Leer meer over de [datasetbelangrijkheid](#dataset-precedence) fusiemethode.
* **[!UICONTROL Timestamp ordered]:** In geval van een conflict, wordt de prioriteit gegeven aan het profielfragment dat onlangs werd bijgewerkt. Meer informatie over [geordende tijdstempel](#timestamp-ordered) samenvoegmethode.
   * **Aangepaste tijdstempels:** De methode voor geordende samenvoegingen met tijdstempels ondersteunt ook aangepaste tijdstempels die voorrang hebben op systeemtijdstempels bij het samenvoegen van gegevens binnen dezelfde gegevensset (meerdere identiteiten) of over gegevenssets heen. Zie de sectie over [aangepaste tijdstempels](#custom-timestamps) voor meer informatie.

### Datasetprioriteit {#dataset-precedence}

Wanneer **[!UICONTROL Dataset precedence]** als fusiemethode voor een fusiebeleid wordt geselecteerd, kunt u prioriteit aan profielfragmenten geven die op de dataset worden gebaseerd waaruit zij kwamen. Een geval van het voorbeeldgebruik zou zijn als uw organisatie informatie aanwezig in één dataset had die over gegevens in een andere dataset voorkeur of vertrouwd is.

Om een samenvoegbeleid tot stand te brengen gebruikend **[!UICONTROL Dataset precedence]**, moet u de datasets van het Profiel en van ExperienceEvent selecteren die inbegrepen zijn en dan kunt u de datasets van het Profiel voor belangrijkheid manueel in orde brengen. Zodra de datasets zijn geselecteerd en bevolen, zal de hoogste dataset hoogste prioriteit worden gegeven, zal de tweede dataset tweede-hoogste zijn, etc.

### Tijdstempel geordend {#timestamp-ordered}

Aangezien profielverslagen in Experience Platform worden opgenomen, wordt een systeemtimestamp verkregen op het tijdstip van opneming en toegevoegd aan het verslag. Als **[!UICONTROL Timestamp ordered]** is geselecteerd als samenvoegmethode voor een samenvoegbeleid, worden profielen samengevoegd op basis van de tijdstempel van het systeem. Met andere woorden, het samenvoegen wordt uitgevoerd op basis van de tijdstempel voor het tijdstip waarop de record in het Platform is opgenomen.

#### Aangepaste tijdstempels gebruiken {#custom-timestamps}

Soms zijn er gebruiksgevallen waarin het nodig is een aangepaste tijdstempel op te geven en het samenvoegbeleid de aangepaste tijdstempel moet gebruiken in plaats van de systeemtijdstempel. Voorbeelden hiervan zijn het terugvullen van gegevens of het garanderen van de juiste volgorde van gebeurtenissen als records buiten de bestelling worden opgenomen.

Als u een aangepaste tijdstempel wilt gebruiken, moet de schemaveldgroep **[!UICONTROL External Source System Audit Details]worden toegevoegd aan uw profielschema.** Nadat de aangepaste tijdstempel is toegevoegd, kan deze worden ingevuld met het veld `lastUpdatedDate`. Wanneer een verslag met het `lastUpdatedDate` gebied wordt opgenomen bevolkt, zal het Experience Platform dat gebied gebruiken om verslagen over datasets samen te voegen. Als `lastUpdatedDate` niet aanwezig, of niet bevolkt is, zal het Platform blijven gebruiken timestamp van het systeem.

>[!NOTE]
>
>U moet ervoor zorgen dat de tijdstempel `lastUpdatedDate` wordt gevuld wanneer u een update in dezelfde record invoegt.

In de volgende schermafbeelding worden de velden in de veldgroep [!UICONTROL External Source System Audit Details] weergegeven. Voor geleidelijke instructies bij het werken met schema&#39;s gebruikend het Platform UI, met inbegrip van hoe te om gebiedsgroepen aan schema&#39;s toe te voegen, gelieve [zelfstudie voor het creëren van een schema te bezoeken gebruikend UI](../../xdm/tutorials/create-schema-ui.md).

![](../images/merge-policies/custom-timestamp-field-group.png)

Als u met aangepaste tijdstempels wilt werken met de API, raadpleegt u de sectie [Bindpuntgids voor samenvoegbeleid bij het gebruik van aangepaste tijdstempels](../api/merge-policies.md#custom-timestamps).

## Identiteitskoppeling {#id-stitching}

Identiteitsstitching ([!UICONTROL ID stitching]) is het proces om gegevensfragmenten te identificeren en hen te combineren om een volledig profielverslag te vormen. Om het verschillende stitching gedrag te illustreren, overweeg één enkele klant die met een merk gebruikend twee verschillende e-mailadressen interactie aangaat.

* **[!UICONTROL None]:** Als deze optie is geselecteerd, worden id&#39;s niet aan elkaar gekoppeld. Wanneer segmentatie voorkomt, zullen de identiteiten die tot de zelfde persoon kunnen behoren niet samen worden vastgemaakt en de segmentatie zal slechts de attributen in aanmerking nemen verbonden aan elke individuele identiteitskaart wanneer het bepalen als een klant voor segmentlidmaatschap in aanmerking komt. Dit zou in één enkele klant kunnen resulteren die veelvoudige profielen heeft en elk profiel voor verschillende segmenten zou kunnen kwalificeren, resulterend in veelvoudige marketing berichten die naar de zelfde klant worden verzonden.
* **[!UICONTROL Private graph]:** Wanneer de privégrafiek is geselecteerd, worden meerdere identiteiten met betrekking tot dezelfde persoon samengevoegd. Dit resulteert in de klant die één enkel profiel heeft en staat segmentatie toe om veelvoudige attributen van veelvoudige verwante identiteiten te overwegen wanneer het bepalen van segmentkwalificatie. In dit scenario zal de klant waarschijnlijk één profiel hebben, in aanmerking komen voor één segment op basis van de combinatie van kenmerken tussen identiteiten en slechts één marketingbericht ontvangen.

Om meer over identiteiten en hun rol in het produceren van profielen en segmenten te leren, gelieve te beginnen door [Overzicht van de Dienst van de Identiteit](../../identity-service/home.md) te lezen.

## Standaardsamenvoegbeleid {#default-merge-policy}

Een organisatie kan een standaardsamenvoegbeleid maken dat door haar organisatie kan worden gebruikt bij het samenvoegen van profielfragmenten. Op deze manier kunnen gebruikers het standaardbeleid eenvoudig selecteren wanneer ze handelingen uitvoeren in een Experience Platform, zoals het weergeven van klantprofielen of het maken van segmenten. In de meeste gevallen, tenzij een ander fusiebeleid wordt gespecificeerd, zal het standaardfusiebeleid worden gebruikt.

Elke organisatie kan veelvoudige fusiebeleid met betrekking tot één enkele XDM schemaklasse tot stand brengen, nochtans kunnen zij slechts één standaardsamenvoegbeleid hebben dat voor elke klasse wordt gedeclareerd. Uw organisatie zou bijvoorbeeld een standaardsamenvoegbeleid kunnen hebben met betrekking tot de [!DNL XDM Individual Profile]-klasse en een ander standaardsamenvoegbeleid voor een aangepaste, samengestelde klasse Product Inventory.

Als u een nieuw samenvoegbeleid creeert en het plaatst als gebrek, zal het vorige standaardfusiebeleid automatisch door het systeem worden bijgewerkt om niet meer het gebrek te zijn.

>[!WARNING]
>
>De tellingen en de segmenten van het profiel met een bestaand bijbehorend standaardsamenvoegbeleid kunnen worden beïnvloed. Om het even welk segment dat een toegepast standaardsamenvoegingsbeleid heeft zal worden bijgewerkt aan het nieuwe standaardsamenvoegbeleid.

## Volgende stappen

Na het lezen van deze handleiding weet u nu wat het samenvoegingsbeleid is en welke rol zij binnen Experience Platform spelen. Om met samenvoegbeleid in de UI van het Experience Platform te beginnen te werken, te verwijzen gelieve [beleidsgids UI ](ui-guide.md) samenvoegen. Als u met samenvoegbeleid wilt werken met de API, gaat u naar de [eindgids voor beleid en API voor samenvoegen](../api/merge-policies.md).