---
title: Secreten configureren bij doorsturen van gebeurtenissen
description: Leer hoe te om geheimen in UI te vormen voor authentiek te verklaren aan eindpunten die in gebeurtenis worden gebruikt door:sturen eigenschappen.
exl-id: eefd87d7-457f-422a-b159-5b428da54189
source-git-commit: a863d65c3e6e330254a58aa822383c0847b0e5f5
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 0%

---

# Het vormen geheimen in gebeurtenis door:sturen

In gebeurtenis door:sturen, is een geheim een middel dat een authentificatiereferentie voor een ander systeem vertegenwoordigt, dat voor de veilige uitwisseling van gegevens toestaat. De geheimen kunnen slechts binnen gebeurtenis worden gecreeerd die eigenschappen door:sturen.

De volgende geheime types worden momenteel gesteund:

| Geheim type | Beschrijving |
| --- | --- |
| [!UICONTROL Google OAuth 2] | Bevat diverse kenmerken die de [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) verificatiespecificatie voor gebruik in de [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview) en [Pub/Sub-API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview). Het systeem vraagt u om de vereiste informatie, dan behandelt de vernieuwing van deze tokens voor u op een gespecificeerd interval. |
| [!UICONTROL HTTP] | Bevat respectievelijk twee tekenreekskenmerken voor een gebruikersnaam en wachtwoord. |
| [!UICONTROL OAuth 2] | Bevat diverse kenmerken die de [type clientverificatietype](https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.4) voor de [OAuth 2.0](https://datatracker.ietf.org/doc/html/rfc6749) verificatiespecificatie. Het systeem vraagt u om de vereiste informatie, dan behandelt de vernieuwing van deze tokens voor u op een gespecificeerd interval. |
| [!UICONTROL OAuth 2 JWT] | Bevat diverse kenmerken die JSON Web Token (JWT)-profiel ondersteunen voor [OAuth 2.0 Autorisatie](https://datatracker.ietf.org/doc/html/rfc7523#section-2.1) subsidies. Het systeem vraagt u om de vereiste informatie, dan behandelt de vernieuwing van deze tokens voor u op een gespecificeerd interval. |
| [!UICONTROL Token] | Een enkele tekenreeks met tekens die een verificatietoken-waarde vertegenwoordigt die door beide systemen bekend en begrepen is. |

{style="table-layout:auto"}

Deze gids verstrekt een overzicht op hoog niveau van hoe te om geheimen voor een gebeurtenis te vormen door:sturen ([!UICONTROL Edge]) in de gebruikersinterface van het Experience Platform of de gebruikersinterface van de gegevensverzameling.

>[!NOTE]
>
>Raadpleeg voor gedetailleerde informatie over het beheren van geheimen in de Reactor-API, zoals bijvoorbeeld JSON van de structuur van een geheim [geheimen-API](../../api/guides/secrets.md).

## Vereisten

Deze gids veronderstelt dat u reeds vertrouwd met bent hoe te om middelen voor markeringen en gebeurtenis te beheren door:sturen in UI, met inbegrip van hoe te om een gegevenselement en een gebeurtenis tot stand te brengen door:sturen regel. Zie de handleiding op [resources beheren](../managing-resources/overview.md) als u een inleiding nodig hebt.

U hebt ook een goed inzicht in de publicatiestroom voor tags en het doorsturen van gebeurtenissen, inclusief hoe u bronnen aan een bibliotheek kunt toevoegen en een build op uw website kunt installeren om deze te testen. Zie de [publicatieoverzicht](../publishing/overview.md) voor meer informatie .

## Een geheim maken {#create}

>[!CONTEXTUALHELP]
>id="platform_eventforwarding_secrets_environments"
>title="Omgevingen voor geheimen"
>abstract="Opdat een geheim door gebeurtenis te gebruiken door:sturen, moet het aan een bestaand milieu worden toegewezen. Als u geen milieu&#39;s hebt die voor uw gebeurtenis door:sturen bezit worden gecreeerd, moet u hen vormen alvorens verder te gaan."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" text="Overzicht van omgevingen"

Als u een geheim wilt maken, selecteert u **[!UICONTROL Event Forwarding]** in de linkernavigatie, dan open de gebeurtenis die bezit door:sturen u het geheim onder wilt toevoegen. Selecteer vervolgens **[!UICONTROL Secrets]** in de linkernavigatie, gevolgd door **[!UICONTROL Create New Secret]**.

![Nieuw geheim maken](../../images/ui/event-forwarding/secrets/create-new-secret.png)

Het volgende scherm staat u toe om de details van het geheim te vormen. Opdat een geheim door gebeurtenis te gebruiken door:sturen, moet het aan een bestaand milieu worden toegewezen. Als u geen milieu&#39;s hebt die voor uw gebeurtenis door:sturen bezit worden gecreeerd, zie de gids op [omgevingen](../publishing/environments.md) voor begeleiding op hoe te om hen te vormen alvorens verder te gaan.

>[!NOTE]
>
>Als u het geheim nog wilt creëren en bewaren alvorens het aan een milieu toe te voegen, maak onbruikbaar **[!UICONTROL Attach Secret to Environments]** schakelen voordat de rest van de informatie wordt ingevuld. Let op: u moet het later toewijzen aan een omgeving als u het geheim wilt gebruiken.
>
>![Omgeving uitschakelen](../../images/ui/event-forwarding/secrets/env-disabled.png)

Onder **[!UICONTROL Target Environment]** selecteert u de omgeving waaraan u het geheim wilt toewijzen in het vervolgkeuzemenu. Onder **[!UICONTROL Secret Name]**, een naam voor het geheim in de context van het milieu verstrekken. Deze naam moet uniek over alle geheimen onder de gebeurtenis zijn die bezit door:sturen.

![Omgeving en naam](../../images/ui/event-forwarding/secrets/env-and-name.png)

Een geheim kan slechts aan één milieu tegelijkertijd worden toegewezen, maar u kunt de zelfde geloofsbrieven aan veelvoudige geheimen over verschillende milieu&#39;s toewijzen als u wenst. Selecteren **[!UICONTROL Add Environment]** om nog een rij aan de lijst toe te voegen.

![Omgeving toevoegen](../../images/ui/event-forwarding/secrets/add-env.png)

Voor elke omgeving die u toevoegt, moet u een andere unieke naam opgeven voor het bijbehorende geheim. Als u alle beschikbare omgevingen uitlaat, **[!UICONTROL Add Environment]** button is niet beschikbaar.

![Omgeving niet beschikbaar toevoegen](../../images/ui/event-forwarding/secrets/add-env-greyed.png)

Van hier, verschillen de stappen om het geheim tot stand te brengen afhankelijk van het type van geheim u creeert. Raadpleeg de onderstaande subsecties voor meer informatie:

* [[!UICONTROL Token]](#token)
* [[!UICONTROL HTTP]](#http)
* [[!UICONTROL OAuth 2]](#oauth2)
* [[!UICONTROL OAuth 2 JWT]](#oauth2jwt)
* [[!UICONTROL Google OAuth 2]](#google-oauth2)

### [!UICONTROL Token] {#token}

Selecteer **[!UICONTROL Token]** van de **[!UICONTROL Type]** vervolgkeuzelijst. In de **[!UICONTROL Token]** in het veld dat wordt weergegeven, geeft u de referentietekenreeks op die wordt herkend door het systeem waarop u de verificatie uitvoert. Selecteren **[!UICONTROL Create Secret]** om het geheim te bewaren.

![Tokengeheim](../../images/ui/event-forwarding/secrets/token-secret.png)

### [!UICONTROL HTTP] {#http}

Als u een HTTP-geheim wilt maken, selecteert u **[!UICONTROL Simple HTTP]** van de **[!UICONTROL Type]** vervolgkeuzelijst. Geef in de onderstaande velden een gebruikersnaam en wachtwoord op voor de referentie voordat u **[!UICONTROL Create Secret]** om het geheim te bewaren.

>[!NOTE]
>
>Als de referentie wordt opgeslagen, wordt deze gecodeerd met de [&quot;Basic&quot; HTTP-verificatieschema](https://www.rfc-editor.org/rfc/rfc7617.html).

![HTTP-geheim](../../images/ui/event-forwarding/secrets/http-secret.png)

### [!UICONTROL OAuth 2] {#oauth2}

Als u een OAuth 2-geheim wilt maken, selecteert u **[!UICONTROL OAuth 2]** van de **[!UICONTROL Type]** vervolgkeuzelijst. Geef in de onderstaande velden uw [[!UICONTROL Client ID] en [!UICONTROL Client Secret]](https://www.oauth.com/oauth2-servers/client-registration/client-id-secret/)en uw [[!UICONTROL Token URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) voor uw OAuth integratie. De [!UICONTROL Token URL] in UI is een aaneenschakeling tussen de gastheer van de vergunningsserver en de symbolische weg.

![OAuth 2-geheim](../../images/ui/event-forwarding/secrets/oauth-secret-1.png)

Onder **[!UICONTROL Credential Options]**, kunt u andere referentie-opties opgeven, zoals `scope` en `audience` in de vorm van sleutelwaardeparen. Als u meer sleutelwaardeparen wilt toevoegen, selecteert u **[!UICONTROL Add another]**.

![Referentieopties](../../images/ui/event-forwarding/secrets/oauth-secret-2.png)

Tot slot kunt u vormen **[!UICONTROL Refresh Offset]** waarde voor het geheim. Dit vertegenwoordigt het aantal seconden vóór de symbolische vervaldatum dat het systeem automatisch zal uitvoeren verfrist zich. De equivalente tijd in uren en minuten wordt rechts van het veld weergegeven en wordt automatisch bijgewerkt terwijl u typt.

![Verschuiving vernieuwen](../../images/ui/event-forwarding/secrets/oauth-secret-3.png)

Als de verschuiving Vernieuwen bijvoorbeeld is ingesteld op de standaardwaarde van `14400` (vier uur) en het toegangstoken heeft een `expires_in` waarde van `86400` (24 uur), vernieuwt het systeem automatisch het geheim over 20 uur.

>[!IMPORTANT]
>
>Een geheim OAuth vereist minstens vier uren tussen verfrissingen en moet ook voor een minimum van acht uur geldig zijn. Deze beperking geeft u een minimum van vier uren om in te grijpen als de problemen met het geproduceerde teken zich voordoen.
>
>Als de verschuiving bijvoorbeeld is ingesteld op `28800` (8 uur) en het toegangstoken heeft een `expires_in` van `36000` (10 uur), zou de ruil mislukken omdat het resulterende verschil minder dan vier uur bedraagt.

Als u klaar bent, selecteert u **[!UICONTROL Create Secret]** om het geheim te bewaren.

![OAuth 2-verschuiving opslaan](../../images/ui/event-forwarding/secrets/oauth-secret-4.png)

### [!UICONTROL OAuth 2 JWT] {#oauth2jwt}

Selecteer **[!UICONTROL OAuth 2 JWT]** van de **[!UICONTROL Type]** vervolgkeuzelijst.

![De [!UICONTROL Create Secret] tabblad met het geheim van OAuth 2 JWT gemarkeerd in het dialoogvenster [!UICONTROL Type] vervolgkeuzelijst.](../../images/ui/event-forwarding/secrets/oauth-jwt-secret.png)

>[!NOTE]
>
>De enige [!UICONTROL Algorithm] die momenteel voor het ondertekenen van JWT wordt gesteund is RS256.

Geef in de onderstaande velden uw [!UICONTROL Issuer], [!UICONTROL Subject], [!UICONTROL Audience], [!UICONTROL Custom Claims], [!UICONTROL TTL]Selecteer vervolgens de [!UICONTROL Algorithm] in de vervolgkeuzelijst. Voer vervolgens de [!UICONTROL Private Key Id]en uw [[!UICONTROL Token URL]](https://www.oauth.com/oauth2-servers/access-tokens/client-credentials/) voor uw OAuth integratie. De [!UICONTROL Token URL] veld is geen verplicht veld. Wanneer een waarde wordt opgegeven, wordt de JWT uitgewisseld met een toegangstoken. Het geheim wordt vernieuwd volgens de `expires_in` kenmerk van het antwoord en de [!UICONTROL Refresh Offset] waarde. Als er geen waarde wordt opgegeven, wordt de JWT gebruikt als geheim dat naar de rand wordt geduwd. De JWT wordt vernieuwd volgens de [!UICONTROL TTL] en [!UICONTROL Refresh Offset] waarden.

![De [!UICONTROL Create Secret] met een selectie van invoervelden gemarkeerd.](../../images/ui/event-forwarding/secrets/oauth-jwt-information.png)

Onder **[!UICONTROL Credential Options]**, kunt u andere referentie-opties opgeven, zoals `jwt_param` in de vorm van sleutelwaardeparen. Als u meer sleutelwaardeparen wilt toevoegen, selecteert u **[!UICONTROL Add another]**.

![De [!UICONTROL Create Secret] tabblad markeren [!UICONTROL Credential Options] velden.](../../images/ui/event-forwarding/secrets/oauth-jwt-credential-options.png)

Tot slot kunt u vormen **[!UICONTROL Refresh Offset]** waarde voor het geheim. Dit vertegenwoordigt het aantal seconden vóór de symbolische vervaldatum dat het systeem automatisch zal uitvoeren verfrist zich. De equivalente tijd in uren en minuten wordt rechts van het veld weergegeven en wordt automatisch bijgewerkt terwijl u typt.

![De [!UICONTROL Create Secret] tabblad markeren [!UICONTROL Refresh Offset] veld.](../../images/ui/event-forwarding/secrets/oauth-jwt-refresh-offset.png)

Als de verschuiving Vernieuwen bijvoorbeeld is ingesteld op de standaardwaarde van `1800` (30 minuten) en het toegangstoken heeft een `expires_in` waarde van `3600` (één uur), vernieuwt het systeem automatisch het geheim over een uur.

>[!IMPORTANT]
>
>Een OAuth 2 JWT geheim vereist minstens 30 minuten tussen verfrissingen en moet ook voor een minimum van één uur geldig zijn. Deze beperking geeft u een minimum van 30 minuten om in te grijpen als de problemen met het geproduceerde teken zich voordoen.
>
>Als de verschuiving bijvoorbeeld is ingesteld op `1800` (30 minuten) en het toegangstoken heeft een `expires_in` van `2700` (45 minuten), zou de ruil mislukken omdat het resulterende verschil minder dan 30 minuten bedraagt.

Als u klaar bent, selecteert u **[!UICONTROL Create Secret]** om het geheim te bewaren.

![De [!UICONTROL Create Secret] tabmarkering [!UICONTROL Create Secret]](../../images/ui/event-forwarding/secrets/oauth-jwt-create-secret.png)

### [!UICONTROL Google OAuth 2] {#google-oauth2}

Als u een Google OAuth 2-geheim wilt maken, selecteert u **[!UICONTROL Google OAuth 2]** van de **[!UICONTROL Type]** vervolgkeuzelijst. Onder **[!UICONTROL Scopes]**, selecteert u de Google API&#39;s die u met dit geheim toegang wilt verlenen. De volgende producten worden momenteel ondersteund:

* [Google Ads API](https://developers.google.com/google-ads/api/docs/oauth/overview)
* [Pub/Sub-API](https://cloud.google.com/pubsub/docs/reference/service_apis_overview)

Als u klaar bent, selecteert u **[!UICONTROL Create Secret]**.

![Google OAuth 2-geheim](../../images/ui/event-forwarding/secrets/google-oauth.png)

Er verschijnt een pop-up met de mededeling dat het geheim handmatig moet worden geautoriseerd via Google. Selecteren **[!UICONTROL Create & Authorize]** om door te gaan.

![Google-autorisatiepopup](../../images/ui/event-forwarding/secrets/google-authorization.png)

Er wordt een dialoogvenster weergegeven waarin u de referenties voor uw Google-account kunt invoeren. Volg de herinneringen om gebeurtenis door:sturen toegang tot uw gegevens onder het geselecteerde werkingsgebied te verlenen. Zodra het vergunningsproces volledig is, wordt het geheim gecreeerd.

>[!IMPORTANT]
>
>Als in uw organisatie een beleid voor herverificatie is ingesteld voor Google Cloud-toepassingen, worden de gemaakte geheimen niet vernieuwd nadat de verificatie is verlopen (tussen 1 en 24 uur, afhankelijk van de beleidsconfiguratie).
>
>Meld u aan bij de Google Admin-console en navigeer naar de **[!DNL App access control]** pagina zodat u de gebeurtenis kunt markeren door:sturen app (de Gebeurtenis die van Adobe Real-Time CDP door:sturen) als [!DNL Trusted]. Raadpleeg de documentatie van Google op [sessielengtes instellen voor Google Cloud-services](https://support.google.com/a/answer/9368756) voor meer informatie .

## Een geheim bewerken

Nadat u geheimen voor een eigenschap hebt gemaakt, vindt u deze in het menu **[!UICONTROL Secrets]** werkruimte. Als u de details van een bestaand geheim wilt bewerken, selecteert u de naam in de lijst.

![Selecteer geheim om te bewerken](../../images/ui/event-forwarding/secrets/edit-secret.png)

In het volgende scherm kunt u de naam en referenties voor het geheim wijzigen.

![Bewerken, geheim](../../images/ui/event-forwarding/secrets/edit-secret-config.png)

>[!NOTE]
>
>Als het geheim met een bestaand milieu wordt geassocieerd, kunt u niet het geheim aan een andere milieu opnieuw toewijzen. Als u dezelfde gegevens wilt gebruiken in een andere omgeving, moet u [een nieuw geheim maken](#create) in plaats daarvan. De enige manier om de omgeving van dit scherm opnieuw toe te wijzen is door het geheim nooit vooraf aan een omgeving toe te wijzen of door de omgeving te verwijderen waaraan het geheim was gekoppeld.

### Opnieuw een geheime uitwisseling

U kunt een geheime uitwisseling van het het uitgeven scherm opnieuw proberen of verfrissen. Dit proces is afhankelijk van het type geheim dat wordt bewerkt:

| Geheim type | Protocol opnieuw proberen |
| --- | --- |
| [!UICONTROL Token] | Selecteren **[!UICONTROL Exchange Secret]** om de geheime uitwisseling opnieuw te proberen. Deze controle is slechts beschikbaar wanneer er een milieu verbonden aan het geheim is. |
| [!UICONTROL HTTP] | Als er geen omgeving aan het geheim is gekoppeld, selecteert u **[!UICONTROL Exchange Secret]** de referentie aan base64 om te wisselen. Als een omgeving is gekoppeld, selecteert u **[!UICONTROL Exchange and Deploy Secret]** om uit te wisselen om base64 te gebruiken en het geheim op te stellen. |
| [!UICONTROL OAuth 2] | Selecteren **[!UICONTROL Generate Token]** om de geloofsbrieven uit te wisselen en een toegangstoken van de authentificatieleverancier terug te keren. |

## Een geheim verwijderen

Om een bestaand geheim in te schrappen  **[!UICONTROL Secrets]** in de werkruimte selecteert u het selectievakje naast de naam van de werkruimte voordat u **[!UICONTROL Delete]**.

![geheim verwijderen](../../images/ui/event-forwarding/secrets/delete.png)

## Het gebruiken van geheimen in gebeurtenis door:sturen

Om gebruik te maken van een geheim in gebeurtenis die door:sturen, moet u eerst tot een [gegevenselement](../managing-resources/data-elements.md) dat verwijst naar het geheim zelf. Na het bewaren van het gegevenselement, kunt u het in gebeurtenis omvatten door:sturen [regels](../managing-resources/rules.md) en voegt deze regels toe aan een [bibliotheek](../publishing/libraries.md), die op hun beurt als een [build](../publishing/builds.md).

Selecteer bij het maken van het gegevenselement de optie **[!UICONTROL Core]** extensie selecteert u vervolgens **[!UICONTROL Secret]** voor het gegevenstype data. Het juiste paneel werkt en verstrekt dropdown controles bij om tot drie geheimen aan het gegevenselement toe te wijzen: één voor [!UICONTROL Development], [!UICONTROL Staging], en [!UICONTROL Production] respectievelijk.

![Gegevenselement](../../images/ui/event-forwarding/secrets/data-element.png)

>[!NOTE]
>
>Alleen geheimen die zijn gekoppeld aan de ontwikkelings-, staging- en productieomgevingen worden weergegeven voor hun respectieve dropdowns.

Door veelvoudige geheimen aan één enkel gegevenselement toe te wijzen en het op te nemen een regel, kunt u de waarde van de verandering van het gegevenselement hebben afhankelijk van waar de bevattende bibliotheek in is [publicatiestroom](../publishing/publishing-flow.md).

![Gegevenselement met meerdere geheimen](../../images/ui/event-forwarding/secrets/multi-secret-data-element.png)

>[!NOTE]
>
>Bij het maken van het gegevenselement moet een ontwikkelomgeving worden toegewezen. Geheimen voor de het opvoeren en productiemilieu&#39;s worden niet vereist, maar bouwt die proberen om naar die milieu&#39;s over te schakelen zal ontbreken als hun geheim-type gegevenselementen geen geheim hebben dat voor het milieu in kwestie wordt geselecteerd.

## Volgende stappen

Deze gids behandelde hoe te om geheimen in UI te beheren. Voor informatie over hoe u met geheimen communiceert met de Reactor-API raadpleegt u de [punthulplijn voor geheimen](../../api/endpoints/secrets.md).
