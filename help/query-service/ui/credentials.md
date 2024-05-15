---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: Handleiding Query Service Credentials
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt om query's te schrijven en uit te voeren, eerder uitgevoerde query's weer te geven en query's te openen die zijn opgeslagen door gebruikers binnen uw organisatie.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: ba4ff2715d4e3eb71377542ab2361b967cd3ac11
workflow-type: tm+mt
source-wordcount: '1759'
ht-degree: 0%

---

# Referentiegids

Met Adobe Experience Platform Query Service kunt u verbinding maken met externe clients. U kunt met deze externe cliënten verbinden door of het verlopen van geloofsbrieven of niet-vervallende geloofsbrieven te gebruiken.

>[!NOTE]
>
>Het venster Referenties is niet automatisch beschikbaar voor alle gebruikers. Neem contact op met het accountteam van uw Adobe om de [!UICONTROL Credentials] die in de werkruimte van de Dienst van de Vraag moet worden omvat als u het vereist. Indien gevraagd, is deze verandering organisatie wijd en door het technische team van Adobe geleid. Dit is geen instelling die door gebruikers wordt beheerd.

## Referenties vervallen {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="SSL-modus van client"
>abstract="SSL moet worden ingeschakeld in clients die zijn verbonden met Query Service. Zorg ervoor dat de SSL-modus is ingesteld op &#39;require&#39;."

U kunt verlopen referenties gebruiken om snel een verbinding met een externe client in te stellen.

![Het tabblad Referenties van het dashboard Vragen met de sectie Verlopende referenties gemarkeerd.](../images/ui/credentials/expiring-credentials.png)

De **[!UICONTROL Expiring credentials]** Deze sectie bevat de volgende informatie:

- **[!UICONTROL Host]**: De naam van de host waarmee de client verbinding moet maken. Dit neemt de naam van uw organisatie zoals die in het hoogste lint van het Platform UI wordt gezien op.
- **[!UICONTROL Port]**: Het poortnummer van de host waarmee verbinding moet worden gemaakt.
- **[!UICONTROL Database]**: De naam van de database waarmee een client verbinding moet maken.
- **[!UICONTROL Username]**: De gebruikersnaam die wordt gebruikt om verbinding te maken met Query Service.
- **[!UICONTROL Password]**: Het wachtwoord dat wordt gebruikt om verbinding te maken met Query Service. De wachtwoorden in UI zijn gehakt voor veiligheid. Selecteer het pictogram Kopiëren (![Het kopieerpictogram.](../images/ui/credentials/copy-icon.png)) om uw volledige, niet-gehashte gegevens naar het klembord te kopiëren.
- **[!UICONTROL PSQL command]**: Een bevel dat automatisch al relevante informatie voor u heeft opgenomen om met de Dienst van de Vraag te verbinden gebruikend PSQL op de bevellijn.
- **[!UICONTROL Expires]**: De vervaldatum en -tijd voor de verlopen referenties. De standaard geldigheidstermijn van het token is 24 uur, maar deze kan worden gewijzigd in de geavanceerde instellingen van de Admin Console.

>[!TIP]
>
>Om het zittingsleven voor uw het verlopen geloofsbrieven verbinding aan de Dienst van de Vraag te veranderen, navigeer aan [Admin Console](https://adminconsole.adobe.com/) en selecteer de volgende opties op het scherm: **Instellingen** > **Privacy en beveiliging** > **Verificatie-instellingen** > **Geavanceerde instellingen** > **Max. sessielevensduur**.
>
>![Het lusje van de montages van de Admin Console met Privacy en Veiligheid, de montages van de Authentificatie, en het Max zittingsleven benadrukte.](../images/ui/credentials/max-session-life.png)
>
>Raadpleeg de Help bij de Adobe voor meer informatie over de [Geavanceerde instellingen](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) aangeboden door Admin Console.

### Verbinding maken met Customer Journey Analytics-gegevens binnen querysessies {#connect-to-customer-journey-analytics}

Gebruik de Customer Journey Analytics BI uitbreiding met Power BI of Tableau om tot uw Customer Journey Analytics toegang te hebben [gegevensweergaven](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) met SQL. Door de Dienst van de Vraag met de uitbreiding te integreren BI, kunt u tot uw gegevensmeningen direct binnen de zittingen van de Dienst van de Vraag toegang hebben. Deze integratie stroomlijnt functionaliteit voor hulpmiddelen BI die de Dienst van de Vraag als hun interface PostgreSQL gebruiken. Deze functionaliteit elimineert de behoefte om gegevensmeningen in hulpmiddelen van BI te dupliceren, verzekert verenigbare rapportering over platforms, en vereenvoudigt de integratie van de gegevens van de Customer Journey Analytics met andere bronnen in platforms van BI.

Raadpleeg de documentatie voor meer informatie over [Verbind de Dienst van de Vraag met een verscheidenheid van Desktopcliënttoepassingen](../clients/overview.md) zoals [Power BI](../clients/power-bi.md) of [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Voor het gebruik van deze functionaliteit zijn een Customer Journey Analytics-werkruimteproject en een gegevensweergave vereist.

Als u toegang wilt krijgen tot de gegevens van uw Customer Journey Analytics in Power BI of Tableau, selecteert u de optie [!UICONTROL Database] vervolgkeuzelijst, selecteert u vervolgens `prod:cja` uit de beschikbare opties. Kopieer vervolgens uw [!DNL Postgres] geloofsbrieven parameters (Gastheer, Haven, Gegevensbestand, Gebruikersnaam, en anderen) voor gebruik in uw Power BI of configuratie Tableau.

![Het lusje van de geloofsbrieven van de Dienst van de Vraag met benadrukt gegevensbestanddropdown.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>Wanneer u Power BI of Tableau met Customer Journey Analytics verbindt, wordt de &quot;gezamenlijke zittingen&quot;van de Dienst van de Vraag het recht verbruikt. Als extra sessies en query&#39;s vereist zijn, kan een extra add-on voor het pakket voor gebruikers van ad-hocquery&#39;s worden aangeschaft om vijf extra gelijktijdige sessies en één extra gelijktijdige query te verkrijgen.

U kunt tot uw gegevens van de Customer Journey Analytics rechtstreeks van de Redacteur van de Vraag of CLI van Postgres toegang hebben. Om dit te doen, verwijs naar `cja` database wanneer u uw query schrijft. Zie de Query-editor [queryhandleiding](./user-guide.md#query-authoring) voor meer informatie over het schrijven, uitvoeren en opslaan van vragen.

Zie de [BI-extensiegids](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension) voor volledige instructies over de toegang tot van uw de gegevensmeningen van de Customer Journey Analytics met SQL.

## Niet-verlopen referenties {#non-expiring-credentials}

U kunt niet-verlopen geloofsbrieven gebruiken aan opstelling een duurdere verbinding aan een externe cliënt.

>[!NOTE]
>
>Niet-vervallende referenties hebben de volgende beperkingen:<br><ul><li>Gebruikers dienen zich aan te melden met hun gebruikersnaam en wachtwoord, die bestaan uit `{technicalAccountId}:{credential}`. Meer informatie vindt u in de [Referenties genereren](#generate-credentials) sectie.</li><li>Op de verwezenlijking van het verlopen geloofsbrieven, wordt een nieuwe rol met een reeks basistoestemmingen gecreeerd die gebruikers toestaat om schema&#39;s en datasets te bekijken. De toestemming &quot;beheert vragen&quot;wordt ook toegewezen aan deze rol voor gebruik met de Dienst van de Vraag.</li><li>Externe clients kunnen anders presteren dan u had verwacht bij het weergeven van queryobjecten. Bijvoorbeeld, sommige derdecliënten zoals [!DNL DB Visualizer] wordt de weergavenaam niet weergegeven in het linkerdeelvenster. De weergavenaam is echter toegankelijk als deze wordt aangeroepen binnen een SELECT-query. Op dezelfde manier [!DNL PowerUI] geeft mogelijk geen lijst weer van de tijdelijke weergaven die zijn gemaakt via de SQL die moeten worden geselecteerd voor het maken van het dashboard.</li></ul>

### Vereisten

Voordat u niet-vervallende gegevens kunt genereren, moet u de volgende stappen in Adobe Admin Console uitvoeren:

1. Aanmelden [Adobe Admin Console](https://adminconsole.adobe.com/) en selecteer de relevante organisatie in de bovenste navigatiebalk.
2. [Selecteer een productprofiel.](../../access-control/ui/browse.md)
3. [Configureer beide **Sandboxen** en **De integratie van Query Service beheren** machtigingen](../../access-control/ui/permissions.md) voor het productprofiel.
4. [Een nieuwe gebruiker toevoegen aan een productprofiel](../../access-control/ui/users.md) zodat wordt hun gevormd toestemmingen verleend.
5. [De gebruiker toevoegen als beheerder van een productprofiel](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) om het maken van een account voor een actief productprofiel toe te staan.
6. [De gebruiker toevoegen als ontwikkelaar van een productprofiel](https://helpx.adobe.com/nl/enterprise/using/manage-developers.html) om een integratie tot stand te brengen.

Lees de documentatie op voor meer informatie over het toewijzen van machtigingen [toegangsbeheer](../../access-control/home.md).

Alle vereiste machtigingen zijn nu geconfigureerd in Adobe Developer Console, zodat de gebruiker de functie voor het verlopen van referenties kan gebruiken.

### Referenties genereren {#generate-credentials}

Als u een set niet-vervallende gegevens wilt maken, gaat u terug naar de interface van het platform en selecteert u **[!UICONTROL Queries]** van de linkernavigatie om tot [!UICONTROL Queries] werkruimte. Selecteer vervolgens de **[!UICONTROL Credentials]** tab gevolgd door **[!UICONTROL Generate credentials]**.

![Het dashboard van Vragen met het lusje van Referenties en Genereer geloofsbrieven benadrukte.](../images/ui/credentials/generate-credentials.png)

Er wordt een dialoogvenster weergegeven waarin u referenties kunt genereren. Als u niet-vervallende gegevens wilt maken, moet u de volgende gegevens opgeven:

- **[!UICONTROL Name]**: De naam van de referenties die u genereert.
- **[!UICONTROL Description]**: (Optioneel) Een beschrijving van de referenties die u genereert.
- **[!UICONTROL Assigned to]**: De gebruiker waaraan de geloofsbrieven zullen worden toegewezen. Deze waarde moet het e-mailadres zijn van de gebruiker die de referenties maakt.
- **[!UICONTROL Password]** (Optioneel) Een optioneel wachtwoord voor uw referenties. Als het wachtwoord niet is ingesteld, genereert de Adobe automatisch een wachtwoord voor u.

Als u alle vereiste gegevens hebt opgegeven, selecteert u **[!UICONTROL Generate credentials]** om uw referenties te genereren.

![Het dialoogvenster Referenties genereren wordt gemarkeerd.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Wanneer **[!UICONTROL Generate credentials]** is geselecteerd, wordt een JSON-configuratiebestand gedownload naar uw lokale computer. Aangezien Adobe **niet** registreert de geproduceerde geloofsbrieven, moet u het gedownloade dossier veilig opslaan en een verslag van de referentie houden.
>
>Bovendien, als de geloofsbrieven niet gedurende 90 dagen worden gebruikt, zullen de geloofsbrieven worden verklaard.

Het configuratie-JSON-bestand bevat informatie zoals de naam van de technische account, de id van de technische account en de referentie. Deze wordt in het volgende formaat verstrekt.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Nadat u de gegenereerde gegevens hebt opgeslagen, selecteert u **[!UICONTROL Close]**. U kunt nu een lijst zien van al uw niet-vervallende geloofsbrieven.

![Het tabblad Credentials van het dashboard Vragen met de sectie Niet-vervallende referenties gemarkeerd.](../images/ui/credentials/list-credentials.png)

U kunt uw niet-vervallende gegevens bewerken of verwijderen. Als u een niet-vervallende referentie wilt bewerken, selecteert u het potloodpictogram (![Een potloodpictogram.](../images/ui/credentials/edit-icon.png)). Als u een niet-verkennende referentie wilt verwijderen, selecteert u het verwijderingspictogram (![Een prullenbakpictogram.](../images/ui/credentials/delete-icon.png)).

Wanneer u een niet-verkennende referentie bewerkt, wordt een modaal veld weergegeven. U kunt de volgende gegevens opgeven om bij te werken:

- **[!UICONTROL Name]**: De naam van de referenties die u genereert.
- **[!UICONTROL Description]**: (Optioneel) Een beschrijving van de referenties die u genereert.
- **[!UICONTROL Assigned to]**: De gebruiker waaraan de geloofsbrieven zullen worden toegewezen. Deze waarde moet het e-mailadres zijn van de gebruiker die de referenties maakt.

![Het dialoogvenster Account bijwerken.](../images/ui/credentials/update-credentials.png)

Als u alle vereiste gegevens hebt opgegeven, selecteert u **[!UICONTROL Update account]** om de update van uw referenties te voltooien.

## Referenties gebruiken om verbinding te maken met externe clients {#use-credential-to-connect}

U kunt of de het verlopen of niet-verlopen geloofsbrieven gebruiken om met externe cliënten, zoals de Studio van Gegevens Aqua, Leider, of Power BI te verbinden. De invoermethode voor deze referenties is afhankelijk van de externe client. Raadpleeg de documentatie van de externe client voor specifieke instructies over het gebruik van deze referenties.

De afbeelding geeft de locatie aan van elke parameter die in de gebruikersinterface wordt gevonden, behalve het wachtwoord van de niet-vervallende gegevens. Terwijl niet-vervallende geloofsbrieven door hun JSON configuratiedossiers worden verstrekt, kunt u uw het verlopen geloofsbrieven onder bekijken **Credentials** in de gebruikersinterface.

![Het tabblad Credentials van de werkruimte Vragen met de sectie Verstrekkende referenties gemarkeerd.](../images/ui/credentials/expiring-credentials.png)

In de onderstaande tabel worden de parameters beschreven die doorgaans vereist zijn om verbinding te maken met externe clients.

>[!NOTE]
>
>Wanneer het verbinden met een gastheer die niet-vervallende geloofsbrieven gebruikt, is het nog noodzakelijk om alle parameters te gebruiken die in [!UICONTROL EXPIRING CREDENTIALS] , behalve het wachtwoord en de gebruikersnaam.
>De notatie voor het invoeren van uw gebruikersnaam en wachtwoord gebruikt door dubbele punten gescheiden waarden, zoals in dit voorbeeld wordt getoond `username:{your_username}` en `password:{password_string}`.

| Parameter | Beschrijving | Voorbeeld |
|---|---|---|
| **Server/host** | De naam van de server/host waarmee u verbinding maakt. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-vervallende geloofsbrieven en neemt de vorm van aan `server.adobe.io`. De waarde is te vinden onder **[!UICONTROL Host]** in de [!UICONTROL EXPIRING CREDENTIALS] sectie.</ul></li> | `acme.platform.adobe.io` |
| **Poort** | De poort voor de server/host waarmee u verbinding maakt. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-het verlopen geloofsbrieven en onder gevonden **[!UICONTROL Port]** in de [!UICONTROL EXPIRING CREDENTIALS] sectie.</ul></li> | `80` |
| **Database** | De database waarmee u verbinding maakt. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-het verlopen geloofsbrieven en onder gevonden **[!UICONTROL Database]** in de [!UICONTROL EXPIRING CREDENTIALS] sectie. </ul></li> | `prod:all` |
| **Gebruikersnaam** | De gebruikersnaam voor de gebruiker die verbinding maakt met de externe client. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-vervallende geloofsbrieven. De notatie heeft de vorm van een alfanumerieke tekenreeks voor `@AdobeOrg`. Deze waarde staat onder **[!UICONTROL Username]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Wachtwoord** | Het wachtwoord voor de gebruiker die verbinding maakt met de externe client. <ul><li>Als u het verlopen geloofsbrieven gebruikt, kan dit onder worden gevonden **[!UICONTROL Password]** binnen de [!UICONTROL EXPIRING CREDENTIALS] sectie.</li><li>Als u niet-vervallende geloofsbrieven gebruikt, is deze waarde de samengevoegde argumenten van technicalAccountID en de referentie die uit het configuratieJSON dossier wordt genomen. De wachtwoordwaarde heeft de vorm: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Een vervallend referentie-wachtwoord is meer dan duizend alfanumerieke tekens. Er wordt geen voorbeeld gegeven.</li><li>Een wachtwoord voor niet-vervallende gegevens ziet er als volgt uit:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Volgende stappen

Nu u begrijpt hoe zowel het verlopen als niet-het verlopen geloofsbrieven werken, kunt u deze geloofsbrieven gebruiken om met externe cliënten te verbinden. Lees voor meer informatie over externe clients de [Verbind cliënten met de gids van de Dienst van de Vraag](../clients/overview.md).
