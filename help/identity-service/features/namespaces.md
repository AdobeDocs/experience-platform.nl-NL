---
title: Overzicht van id-naamruimte
description: Meer informatie over naamruimten in Identity Service.
exl-id: 86cfc7ae-943d-4474-90c8-e368afa48b7c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1848'
ht-degree: 0%

---

# Overzicht naamruimte identiteit

Lees het volgende document voor meer informatie over wat u kunt doen met naamruimten in Adobe Experience Platform Identity Service.

## Aan de slag

Naamruimten vereisen inzicht in verschillende Adobe Experience Platform-services. Voordat u begint te werken met naamruimten, raadpleegt u de documentatie voor de volgende services:

* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, klantprofiel in real-time op basis van geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Identity Service]](../home.md): verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Privacy Service]](../../privacy-service/home.md): Identiteitsnaamruimten worden gebruikt in nalevingsverzoeken voor wettelijke privacyverordeningen zoals de algemene gegevensbeschermingsverordening (GDPR). Elk privacyverzoek wordt ingediend met betrekking tot een naamruimte om te bepalen welke gegevens van de consument moeten worden beïnvloed.

## Naamruimten voor identiteiten {#understanding-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Identiteitsnaamruimten"
>abstract="Een naamruimte voor identiteiten is de context van een bepaalde identiteit. Bijvoorbeeld, kon een namespace van `Email` met **naam <span>@acme.com** beantwoorden. Een naamruimte van `Phone` kan ook overeenkomen met `555-555-1234` ."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Identiteitsinstellingen"
>abstract="Een identiteitswaarde is een herkenningsteken die een uniek individu, een organisatie, of een middel vertegenwoordigt. De context of het type van identiteit die de waarde vertegenwoordigt wordt bepaald door een overeenkomstige identiteitsnaamruimte. Wanneer recordgegevens worden vergeleken met profielfragmenten, moeten de naamruimte en de identiteitswaarde overeenkomen. Wanneer recordgegevens worden vergeleken met profielfragmenten, moeten de naamruimte en de identiteitswaarde overeenkomen."
>text="Learn more in documentation"

Een volledig gekwalificeerde identiteit omvat twee componenten: een **identiteitswaarde** en een **identiteit namespace**. Als de waarde van een identiteit bijvoorbeeld `scott@acme.com` is, biedt een naamruimte context aan deze waarde door deze te onderscheiden als een e-mailadres. Op dezelfde manier kan een naamruimte `555-123-456` als een telefoonnummer herkennen en `3126ABC` als een CRMID. Hoofdzakelijk, **verstrekt a namespace context aan een bepaalde identiteit**. Bij het afstemmen van recordgegevens over profielfragmenten, zoals wanneer [!DNL Real-Time Customer Profile] profielgegevens samenvoegt, moeten zowel de identiteitswaarde als de naamruimte overeenkomen.

Twee profielfragmenten kunnen bijvoorbeeld verschillende primaire id&#39;s bevatten, maar hebben dezelfde waarde voor de naamruimte E-mail. Daarom kan Experience Platform zien dat deze fragmenten in feite dezelfde persoon zijn en de gegevens samenvoegen in de identiteitsgrafiek voor de persoon.

>[!BEGINSHADEBOX]

**Verklaarde identiteitskaart namespace**

Een andere manier om het concept van naamruimte beter te begrijpen, is het overwegen van echte wereldvoorbeelden zoals steden en hun overeenkomstige staten. Portland, Maine en Portland, Oregon zijn bijvoorbeeld twee verschillende plaatsen in de Verenigde Staten. Terwijl de steden dezelfde naam hebben, werkt de staat als naamruimte en biedt de noodzakelijke context die de twee steden van elkaar onderscheidt.

Dezelfde logica toepassen op Identity Service:

* In één oogopslag kan de identiteitswaarde van: `1-234-567-8900` er uitzien als een telefoonnummer. Nochtans, vanuit een systeemperspectief, kon deze waarde als CRMID worden gevormd. De Dienst van de identiteit zou geen manier hebben om de noodzakelijke context op deze identiteitswaarde zonder overeenkomstige namespace toe te passen.
* Een ander voorbeeld is de identiteitswaarde van: `john@gmail.com`. Hoewel deze identiteitswaarde gemakkelijk kan worden verondersteld om een E-mail te zijn, is het volledig mogelijk dat het als douane namespace CRMID wordt gevormd. Met naamruimte kunt u `Email:john@gmail.com` onderscheiden van `CRMID:john@gmail.com` .

>[!ENDSHADEBOX]

### Componenten van een naamruimte

Een naamruimte bestaat uit de volgende componenten:

* **naam van de Vertoning**: De gebruikersvriendelijke naam voor een bepaalde namespace.
* **symbool van de Identiteit**: Een code die intern door de Dienst van de Identiteit wordt gebruikt om een namespace te vertegenwoordigen.
* **Type van Identiteit**: De classificatie van een bepaalde namespace.
* **Beschrijving**: (Optioneel) Om het even welke aanvullende informatie die u met betrekking tot een bepaalde namespace kunt verstrekken.

### Identiteitstype {#identity-type}

>[!CONTEXTUALHELP]
>id="platform_identity_create_namespace"
>title="Identificatietype opgeven"
>abstract="Het identiteitstype bepaalt of gegevens worden opgeslagen in de identiteitsgrafiek. Identiteitsgrafieken worden niet gegenereerd voor de volgende identiteitstypen: niet-persoonlijke id&#39;s en partner-id."
>text="Learn more in documentation"

Één element van een identiteit namespace is het **identiteitstype**. Het identiteitstype bepaalt:

* Of een identiteitsgrafiek zal worden geproduceerd:
   * Identiteitsgrafieken worden niet gegenereerd voor de volgende identiteitstypen: niet-persoonlijke id&#39;s en partner-id.
   * Identiteitsgrafieken worden gegenereerd voor alle andere identiteitstypen.
* Welke identiteiten worden verwijderd uit de identiteitsgrafiek wanneer de systeemgrenzen worden bereikt. Voor meer informatie, lees de [ gidsen voor identiteitsgegevens ](../guardrails.md).

De volgende identiteitstypen zijn beschikbaar in Experience Platform:

| Identiteitstype | Beschrijving |
| --- | --- |
| Cookie-id | Cookie-id&#39;s identificeren webbrowsers. Deze identiteiten zijn essentieel voor uitbreiding en vormen het grootste deel van de identiteitsgrafiek. Maar door de natuur verval ze snel en verliezen hun waarde in de loop der tijd. |
| Apparaatoverschrijdende id | Apparaatoverschrijdende id&#39;s identificeren een individu en koppelen gewoonlijk andere id&#39;s aan elkaar. Voorbeelden zijn een aanmeldings-id, een CRMID en een loyale-id. Dit is een aanwijzing voor [!DNL Identity Service] om de waarde gevoelig af te handelen. |
| Apparaat-id | Apparaat-id&#39;s identificeren hardwareapparaten, zoals IDFA (iPhone en iPad), GAID (Android) en RIDA (Roku), en kunnen door meerdere personen in huishoudens worden gedeeld. |
| E-mailadres | E-mailadressen zijn vaak gekoppeld aan één persoon en kunnen daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. Tot dit type identiteiten behoren ook PII&#39;s (Persoonlijke identificeerbare informatie). Dit is een aanwijzing voor [!DNL Identity Service] om de waarde gevoelig af te handelen. |
| Id van niet-personen | Niet-persoonlijke id&#39;s worden gebruikt voor het opslaan van id&#39;s die naamruimten vereisen maar niet zijn verbonden met een personencluster. Bijvoorbeeld een product-SKU, gegevens met betrekking tot producten, organisaties of winkels. |
| Partner-id | <ul><li>Identiteitskaart van de partner is herkenningstekens die door gegevenspartners worden gebruikt om mensen te vertegenwoordigen. Identiteitskaart van de partner is vaak pseudoniem zodat om de ware identiteit van een persoon niet te onthullen, en kan probabilistisch zijn. In Real-Time Customer Data Platform, worden de Partner IDs gebruikt hoofdzakelijk voor uitgebreide publieksactivering en gegevensverrijking, en niet voor de verbindingen van de de grafiekgrafiek van de bouwidentiteit.</li><li>Identiteitsgrafieken worden niet geproduceerd wanneer het opnemen van een identiteit die een identiteitsnamespace omvat die als type van identiteitskaart van de Partner wordt gespecificeerd.</li><li>Het nalaten om partnergegevens op te nemen die het identiteitstype van identiteitskaart van de Partner gebruiken kon in het bereiken van de beperkingen van de systeemgrafiek op de Dienst van de Identiteit, evenals ongewenste samenvoeging van profielen resulteren.</li><ul> |
| Telefoonnummer | Telefoonnummers zijn vaak gekoppeld aan één persoon en kunnen daarom worden gebruikt om die persoon via verschillende kanalen te identificeren. Tot dit type identiteiten behoren PII. Dit is een aanwijzing voor [!DNL Identity Service] om de waarde gevoelig af te handelen. |

{style="table-layout:auto"}

### Standaardnaamruimten {#standard}

Experience Platform biedt verschillende naamruimten die beschikbaar zijn voor alle organisaties. Deze worden standaardnaamruimten genoemd en zijn zichtbaar met de API van [!DNL Identity Service] of via de gebruikersinterface van Experience Platform.

De volgende standaardnaamruimten kunnen door alle organisaties in Experience Platform worden gebruikt:

| Weergavenaam | Beschrijving |
| ------------ | ----------- |
| AdCloud | Een naamruimte die staat voor Adobe AdCloud. |
| Adobe Analytics (verouderd ID) | Een naamruimte die Adobe Analytics vertegenwoordigt. Zie het volgende document op [ Adobe Analytics namespaces ](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/gdpr-namespaces.html?lang=nl-NL#namespaces) voor meer informatie. |
| Apple IDFA (ID voor adverteerders) | Een naamruimte die Apple-id voor adverteerders vertegenwoordigt. Zie het volgende document op [ op rente-gebaseerde advertenties ](https://support.apple.com/en-us/HT202074) voor meer informatie. |
| Apple Push Notification-service | Een naamruimte die identiteiten vertegenwoordigt die zijn verzameld met de Apple Push Notification-service. Zie het volgende document op [ de dienst van het Bericht van de Duw van Apple ](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html#//apple_ref/doc/uid/TP40008194-CH8-SW1) voor meer informatie. |
| ECID | Een naamruimte die ECID vertegenwoordigt. Deze naamruimte kan ook worden aangeduid met de volgende aliassen: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Zie het volgende document op [ ECID ](./ecid.md) voor meer informatie. |
| Email | Een naamruimte die een e-mailadres vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |
| E-mails (SHA256, verlaagd) | A namespace for pre-hashed email address. Waarden die in deze naamruimte worden opgegeven, worden omgezet in kleine letters voordat er een hash plaatsvindt met SHA256. De spaties aan het begin en aan het einde moeten worden bijgesneden alvorens een e-mailadres wordt genormaliseerd. Deze instelling kan niet met terugwerkende kracht worden gewijzigd. Zie het volgende document op [ SHA256 het hakken steun ](https://experienceleague.adobe.com/docs/id-service/using/reference/hashing-support.html?lang=nl-NL#hashing-support) voor meer informatie. |
| Firebase Cloud Messaging | Een naamruimte die identiteiten vertegenwoordigt die zijn verzameld met Google Firebase Cloud Messaging voor pushberichten. Zie het volgende document op [ het Overseinen van de Wolk van de Wolk van Google Firebase ](https://firebase.google.com/docs/cloud-messaging) voor meer informatie. |
| Google-advertentie-ID (GAID) | Een naamruimte die een Google Advertising-id vertegenwoordigt. Zie het volgende document op [ identiteitskaart van Google Advertising ](https://support.google.com/googleplay/android-developer/answer/6048248?hl=en) voor meer informatie. |
| Telefoon | Een naamruimte die een telefoonnummer vertegenwoordigt. Dit type naamruimte is vaak gekoppeld aan één persoon en kan daarom worden gebruikt om die persoon op verschillende kanalen te identificeren. |
| Telefoon (E.164) | A namespace that represents raw phone numbers that need to be hashed in E.164 format. De indeling E.164 omvat een plusteken (`+`), een internationale aanroepende code van het land, een lokale gebiedscode, en een telefoonaantal. Bijvoorbeeld: `(+)(country code)(area code)(phone number)` . |
| Telefoon (SHA256) | Een naamruimte die telefoonnummers vertegenwoordigt die moeten worden gehasht met behulp van SHA256. U moet symbolen, letters en voorloopnullen verwijderen. U moet ook het land toevoegen dat code als prefix roept. |
| Telefoon (SHA256_E.164) | A namespace that represents raw phone numbers that need to be hashed using both SHA256 and E.164 format. |
| TNTID | Een naamruimte die Adobe Target vertegenwoordigt. Zie het volgende document op [ Doel ](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=nl-NL) voor meer informatie. |
| Windows-ID | Een naamruimte die een Windows Advertising-id vertegenwoordigt. Zie het volgende document op [ identiteitskaart van Advertising van Vensters 1&rbrace; voor meer informatie.](https://docs.microsoft.com/en-us/uwp/api/windows.system.userprofile.advertisingmanager.advertisingid?view=winrt-19041) |

### Identiteitsnaamruimten weergeven {#view-identity-namespaces}

>[!CONTEXTUALHELP]
>id="platform_identity_view_integration_identities"
>title="Integratie-id&#39;s weergeven"
>abstract="Integratie-id&#39;s zijn naamruimten die worden gebruikt om verbinding te maken met andere systemen en die niet worden gebruikt in identiteitsresolutie of om identiteiten aan te sluiten. <br> Deze identiteiten zijn standaard verborgen. Met de schakeloptie kunt u integratienaamruimten weergeven."

Als u naamruimten in de gebruikersinterface wilt weergeven, selecteert u **[!UICONTROL Identities]** in de linkernavigatie en selecteert u vervolgens **[!UICONTROL Browse]** .

Er wordt een map met naamruimten in uw organisatie weergegeven met informatie over de namen, identiteitssymbolen, laatst bijgewerkte datums, overeenkomende identiteitstypen en beschrijving.

![ een folder van douane identiteitsnamespaces in uw organisatie.](../images/namespace/browse.png)

## Aangepaste naamruimten maken {#create-namespaces}

Afhankelijk van uw organisatorische gegevens en gebruiksgevallen hebt u mogelijk aangepaste naamruimten nodig. U kunt aangepaste naamruimten maken met de API [[!DNL Identity Service]](../api/create-custom-namespace.md) of via de gebruikersinterface.

Selecteer **[!UICONTROL Create identity namespace]** als u een aangepaste naamruimte wilt maken.

>[!TIP]
>
>Integratie-id&#39;s zijn naamruimten die worden gebruikt om verbinding te maken met andere systemen. Ze worden niet gebruikt in identiteitsresolutie en worden ook niet gebruikt om identiteiten aan te hechten. Selecteer **[!UICONTROL View integration identities]** om de lijst bij te werken en integratie-id&#39;s op te nemen. Integratie-id&#39;s zijn echter standaard verborgen omdat ze alleen-weergeven zijn en u ze niet hoeft te configureren.

![ creeer identiteit namespace knoop in de identiteitswerkruimte.](../images/namespace/create-identity-namespace.png)

Het venster [!UICONTROL Create identity namespace] wordt weergegeven. Eerst moet u een weergavenaam en een identiteitssymbool opgeven voor de aangepaste naamruimte die u wilt maken. U kunt desgewenst ook een beschrijving opgeven om meer context toe te voegen aan de aangepaste naamruimte die u maakt.

![ pop-up venster van A waar u informatie betreffende uw douanetechnische naamruimte kunt invoeren.](../images/namespace/name-and-symbol.png)

Selecteer vervolgens het identiteitstype dat u wilt toewijzen aan de aangepaste naamruimte. Selecteer **[!UICONTROL Create]** als u klaar bent.

![ een selectie van identiteitstypes die u van kunt kiezen en aan uw douaneidentiteit namespace toewijst.](../images/namespace/select-identity-type.png)

>[!IMPORTANT]
>
>* De naamruimten die u definieert, zijn persoonlijk voor uw organisatie en vereisen een uniek identiteitssymbool om te kunnen worden gemaakt.
>
>* Nadat een naamruimte is gemaakt, kan deze niet worden verwijderd en kunnen het identiteitssymbool en het type van de naamruimte niet worden gewijzigd.
>
>* Dubbele naamruimten worden niet ondersteund. U kunt een bestaande weergavenaam en identiteitssymbool niet gebruiken wanneer u een nieuwe naamruimte maakt.

## Naamruimten in identiteitsgegevens

Het leveren van de naamruimte voor een identiteit is afhankelijk van de methode die u gebruikt voor het opgeven van identiteitsgegevens. Voor details bij het verstrekken van gegevens van de gegevensidentiteit, gelieve de [[!DNL Identity Service]  implementatiegids ](../implementation.md) te lezen.

## Volgende stappen

Nu u de belangrijkste concepten identiteitsnamespaces begrijpt, kunt u beginnen te leren hoe te met uw identiteitsgrafiek te werken gebruikend de [ kijker van de identiteitsgrafiek ](../features/identity-graph-viewer.md).
