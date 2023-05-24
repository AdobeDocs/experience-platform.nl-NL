---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: Handleiding Query Service Credentials
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt om query's te schrijven en uit te voeren, eerder uitgevoerde query's weer te geven en query's te openen die zijn opgeslagen door gebruikers binnen uw organisatie.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1291'
ht-degree: 1%

---

# Referentiegids

Met Adobe Experience Platform Query Service kunt u verbinding maken met externe clients. U kunt met deze externe cliënten verbinden door of het verlopen van geloofsbrieven of niet-vervallende geloofsbrieven te gebruiken.

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
- **[!UICONTROL Password]**: Het wachtwoord dat wordt gebruikt om met de Dienst van de Vraag te verbinden. De wachtwoorden in UI zijn gehakt voor veiligheid. Selecteer het pictogram Kopiëren (![Het kopieerpictogram.](../images/ui/credentials/copy-icon.png)) om uw volledige, niet-gehashte gegevens naar het klembord te kopiëren.
- **[!UICONTROL PSQL command]**: Een bevel dat automatisch alle relevante informatie voor u heeft opgenomen om met de Dienst van de Vraag te verbinden gebruikend PSQL op de bevellijn.
- **[!UICONTROL Expires]**: De vervaldatum en tijd voor de verloopgeloofsbrieven. De standaard geldigheidstermijn van het token is 24 uur, maar deze kan worden gewijzigd in de geavanceerde instellingen van de Admin Console.

>[!TIP]
>
>Om het zittingsleven voor uw het verlopen geloofsbrieven verbinding aan de Dienst van de Vraag te veranderen, navigeer aan [Admin Console](https://adminconsole.adobe.com/) en selecteer de volgende opties op het scherm: **Instellingen** > **Privacy en beveiliging** > **Verificatie-instellingen** > **Geavanceerde instellingen** > **Max. sessielevensduur**.
>
>![Het lusje van de montages van de Admin Console met Privacy en Veiligheid, de montages van de Authentificatie, en het Max zittingsleven benadrukte.](../images/ui/credentials/max-session-life.png)
>
>Zie de documentatie van de Hulp van de Adobe voor meer informatie over [Geavanceerde instellingen](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) aangeboden door Admin Console.

## Niet-verlopen referenties {#non-expiring-credentials}

U kunt niet-verlopen geloofsbrieven gebruiken aan opstelling een duurdere verbinding aan een externe cliënt.

### Vereisten

Voordat u niet-vervallende gegevens kunt genereren, moet u de volgende stappen in Adobe Admin Console uitvoeren:

1. Aanmelden [Adobe Admin Console](https://adminconsole.adobe.com/) en selecteer de relevante organisatie in de bovenste navigatiebalk.
2. [Selecteer een productprofiel.](../../access-control/ui/browse.md)
3. [Vorm beide **Sandboxen** en **De integratie van Query Service beheren** machtigingen](../../access-control/ui/permissions.md) voor het productprofiel.
4. [Een nieuwe gebruiker toevoegen aan een productprofiel](../../access-control/ui/users.md) zodat wordt hun gevormd toestemmingen verleend.
5. [De gebruiker toevoegen als beheerder van een productprofiel](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) om een account te maken voor een actief productprofiel.
6. [De gebruiker toevoegen als ontwikkelaar van een productprofiel](https://helpx.adobe.com/nl/enterprise/using/manage-developers.html) om een integratie tot stand te brengen.

Voor meer informatie over het toewijzen van machtigingen leest u de documentatie op [toegangsbeheer](../../access-control/home.md).

Alle vereiste machtigingen zijn nu geconfigureerd in Adobe Developer Console, zodat de gebruiker de functie voor het verlopen van referenties kan gebruiken.

### Referenties genereren

Als u een set niet-vervallende gegevens wilt maken, gaat u terug naar de gebruikersinterface van het Platform en selecteert u **[!UICONTROL Queries]** van de linkernavigatie om tot [!UICONTROL Queries] werkruimte. Selecteer vervolgens de **[!UICONTROL Credentials]** tab gevolgd door **[!UICONTROL Generate credentials]**.

![Het dashboard van Vragen met het lusje van Referenties en Genereer geloofsbrieven benadrukte.](../images/ui/credentials/generate-credentials.png)

Er wordt een dialoogvenster weergegeven waarin u referenties kunt genereren. Als u niet-vervallende gegevens wilt maken, moet u de volgende gegevens opgeven:

- **[!UICONTROL Name]**: De naam van de referenties die u genereert.
- **[!UICONTROL Description]**: (Optioneel) Een beschrijving van de referenties die u genereert.
- **[!UICONTROL Assigned to]**: De gebruiker waaraan de geloofsbrieven zullen worden toegewezen. Deze waarde moet het e-mailadres zijn van de gebruiker die de referenties maakt.
- **[!UICONTROL Password]** (Optioneel) Een optioneel wachtwoord voor uw referenties. Als het wachtwoord niet is ingesteld, genereert Adobe automatisch een wachtwoord voor u.

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

U kunt uw niet-vervallende gegevens bewerken of verwijderen. Als u een niet-vervallende referentie wilt bewerken, selecteert u het potloodpictogram (![Een potloodpictogram.](../images/ui/credentials/edit-icon.png)). Als u een niet-vervallende referentie wilt verwijderen, selecteert u het verwijderingspictogram (![Een prullenbakpictogram.](../images/ui/credentials/delete-icon.png)).

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
| **Server/host** | De naam van de server/host waarmee u verbinding maakt. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-vervallende geloofsbrieven en neemt de vorm van aan `server.adobe.io`. De waarde is gevonden onder **[!UICONTROL Host]** in de [!UICONTROL EXPIRING CREDENTIALS] sectie.</ul></li> | `acme.platform.adobe.io` |
| **Poort** | De poort voor de server/host waarmee u verbinding maakt. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-het verlopen geloofsbrieven en onder gevonden **[!UICONTROL Port]** in de [!UICONTROL EXPIRING CREDENTIALS] sectie.</ul></li> | `80` |
| **Database** | De database waarmee u verbinding maakt. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-het verlopen geloofsbrieven en onder gevonden **[!UICONTROL Database]** in de [!UICONTROL EXPIRING CREDENTIALS] sectie. </ul></li> | `prod:all` |
| **Gebruikersnaam** | De gebruikersnaam voor de gebruiker die verbinding maakt met de externe client. <ul><li>Deze waarde wordt gebruikt voor zowel het verlopen van geloofsbrieven als niet-vervallende geloofsbrieven. De notatie heeft de vorm van een alfanumerieke tekenreeks voor `@AdobeOrg`. Deze waarde is te vinden onder **[!UICONTROL Username]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Wachtwoord** | Het wachtwoord voor de gebruiker die verbinding maakt met de externe client. <ul><li>Als u het verlopen geloofsbrieven gebruikt, kan dit onder worden gevonden **[!UICONTROL Password]** binnen de [!UICONTROL EXPIRING CREDENTIALS] sectie.</li><li>Als u niet-vervallende geloofsbrieven gebruikt, is deze waarde de samengevoegde argumenten van technicalAccountID en de referentie die uit het configuratieJSON dossier wordt genomen. De wachtwoordwaarde heeft de vorm: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Een vervallend referentie-wachtwoord is meer dan duizend alfanumerieke tekens. Er wordt geen voorbeeld gegeven.</li><li>Een wachtwoord voor niet-vervallende gegevens ziet er als volgt uit:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Volgende stappen

Nu u begrijpt hoe zowel het verlopen als niet-het verlopen geloofsbrieven werken, kunt u deze geloofsbrieven gebruiken om met externe cliënten te verbinden. Lees voor meer informatie over externe clients de [Verbind cliënten met de gids van de Dienst van de Vraag](../clients/overview.md).
