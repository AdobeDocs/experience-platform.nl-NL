---
keywords: Experience Platform;huis;populaire onderwerpen;vraagdienst;de dienst van de Vraag;vraag;vraagredacteur;de redacteur van de vraag;de redacteur van de Vraag;
solution: Experience Platform
title: UI-gids voor zoekservice
topic-legacy: guide
description: Adobe Experience Platform Query Service biedt een gebruikersinterface die kan worden gebruikt voor het schrijven en uitvoeren van query's, het weergeven van eerder uitgevoerde query's en het openen van query's die zijn opgeslagen door gebruikers binnen uw IMS-organisatie.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 0%

---


# Referentiegids

Met Adobe Experience Platform Query Service kunt u verbinding maken met externe clients. U kunt met deze externe cliënten verbinden door of het verlopen van geloofsbrieven of niet-vervallende geloofsbrieven te gebruiken.

## Referenties vervallen

U kunt verlopen referenties gebruiken om snel een verbinding met een externe client in te stellen.

![](../images/ui/credentials/expiring-credentials.png)

De sectie **[!UICONTROL Expiring credentials]** bevat de volgende informatie:

- **[!UICONTROL Host]**: De naam van de host waarmee u verbinding wilt maken. Voor het verbinden met de Dienst van de Vraag, zal dit de naam van de IMS Organisatie omvatten u momenteel gebruikt.
- **[!UICONTROL Port]**: Het poortnummer van de host waarmee u verbinding wilt maken.
- **[!UICONTROL Database]**: De naam van de database waarmee u verbinding wilt maken.
- **[!UICONTROL Username]**: De gebruikersnaam die u gebruikt om verbinding te maken met Query Service.
- **[!UICONTROL Password]**: Het wachtwoord dat u zult gebruiken om met de Dienst van de Vraag te verbinden.
- **[!UICONTROL PSQL command]**: Een bevel dat automatisch alle relevante informatie voor u heeft opgenomen om met de Dienst van de Vraag te verbinden gebruikend PSQL op de bevellijn.
- **[!UICONTROL Expires]**: De vervaldatum voor de vervallende geloofsbrieven. De referenties verlopen 24 uur nadat ze zijn gegenereerd.

## Niet-verlopen referenties

U kunt niet-verlopen geloofsbrieven gebruiken aan opstelling een duurdere verbinding aan een externe cliënt.

Selecteer **[!UICONTROL Generate credentials]** om een set niet-vervallende gegevens te maken.

>[!NOTE]
>
>Voordat u niet-vervallende referenties kunt maken, moet u over de machtigingen **Sandboxes** en **Query Service Integration** beschikken. Lees de documentatie op [Toegangsbeheer](../../access-control/home.md) voor meer informatie over het toewijzen van deze machtigingen.

![](../images/ui/credentials/generate-credentials.png)

Het modaal formulier voor het genereren van referenties wordt weergegeven. Als u niet-vervallende gegevens wilt maken, moet u de volgende gegevens opgeven:

- **[!UICONTROL Name]**: De naam van de referenties die u genereert.
- **[!UICONTROL Description]**: (Optioneel) Een beschrijving van de referenties die u genereert.
- **[!UICONTROL Assigned to]**: De gebruiker aan wie de geloofsbrieven zullen worden toegewezen. Deze waarde moet het e-mailadres zijn van de gebruiker die de referenties maakt.
- **[!UICONTROL Password]** (Optioneel) Een optioneel wachtwoord voor uw referenties. Als het wachtwoord niet is ingesteld, genereert Adobe automatisch een wachtwoord voor u.

Nadat u alle vereiste gegevens hebt opgegeven, selecteert u **[!UICONTROL Generate credentials]** om uw referenties te genereren.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Nadat de knop **[!UICONTROL Generate credentials]** is geselecteerd, wordt een configuratiebestand weergegeven dat informatie bevat zoals de naam van een technische account, de id van een technische account en de referentie. Aangezien Adobe **not** de gegenereerde referentie opneemt, moet u **must** het gedownloade bestand veilig opslaan en een overzicht van de referentie bijhouden.
>
>Bovendien, als de geloofsbrieven niet voor 90 dagen worden gebruikt, zullen de geloofsbrieven worden gesnoeid.

Nu u uw geproduceerde geloofsbrieven hebt bewaard, selecteer **[!UICONTROL Close]**. U kunt nu een lijst zien van al uw niet-vervallende geloofsbrieven.

![](../images/ui/credentials/list-credentials.png)

U kunt uw niet-vervallende gegevens bewerken of verwijderen. Als u een referentie wilt bewerken die niet vervalt, selecteert u het potloodpictogram (![](../images/ui/credentials/edit-icon.png)). Als u een niet-vervallende referentie wilt verwijderen, selecteert u het verwijderingspictogram (![](../images/ui/credentials/delete-icon.png)).

Wanneer u een niet-verkennende referentie bewerkt, wordt een modaal veld weergegeven. U kunt de volgende gegevens opgeven om bij te werken:

- **[!UICONTROL Name]**: De naam van de referenties die u genereert.
- **[!UICONTROL Description]**: (Optioneel) Een beschrijving van de referenties die u genereert.
- **[!UICONTROL Assigned to]**: De gebruiker aan wie de geloofsbrieven zullen worden toegewezen. Deze waarde moet het e-mailadres zijn van de gebruiker die de referenties maakt.

![](../images/ui/credentials/update-credentials.png)

Nadat u alle vereiste gegevens hebt opgegeven, selecteert u **[!UICONTROL Update account]** om de update naar uw referenties te voltooien.

## Referenties gebruiken om verbinding te maken met externe clients

U kunt of de het verlopen of niet-verlopen geloofsbrieven gebruiken om met externe cliënten, zoals de Studio van Gegevens Aqua, Leider, of Power BI te verbinden.

Wanneer u verbinding maakt met deze externe clients, moet u over het algemeen de volgende informatie opnemen:

- **Server/host**: De naam van de server/host waarmee u verbinding maakt. Deze waarde heeft de vorm van `server.adobe.io` en kan onder **[!UICONTROL Host]** binnen de het verlopen geloofsbrieven sectie worden gevonden.
- **Poort**: De poort voor de server/host waarmee u verbinding maakt. Deze waarde is te vinden onder **[!UICONTROL Port]** binnen de vervallende geloofsbrieven sectie. Een voorbeeldwaarde voor de poort zou `80` zijn.
- **Gebruikersnaam**: De gebruikersnaam voor de gebruiker die verbinding maakt met de externe client. Dit heeft de vorm van `ID@AdobeOrg` en kan onder **[!UICONTROL Username]** binnen de het verlopen geloofsbrieven sectie worden gevonden.
- **Wachtwoord**: Het wachtwoord voor de gebruiker die verbinding maakt met de externe client. Als u het verlopen geloofsbrieven gebruikt, kan dit onder **[!UICONTROL Password]** binnen de het verlopen geloofsbrieven sectie worden gevonden. Als u niet-vervallende geloofsbrieven gebruikt, wordt deze waarde samengesteld van zowel technische rekening identiteitskaart als referentie in de vorm: `technicalAccountId:credential`.
- **Database**: De database waarmee u verbinding maakt. Deze waarde is te vinden onder **[!UICONTROL Database]** binnen de vervallende geloofsbrieven sectie. Een voorbeeldwaarde voor het gegevensbestand zou `prod:all` zijn.

## Volgende stappen

Nu u begrijpt hoe zowel het verlopen als niet-het verlopen geloofsbrieven werken, kunt u deze geloofsbrieven gebruiken om met externe cliënten te verbinden. Lees voor meer informatie over externe clients de handleiding [Verbind clients met Query Service](../clients/overview.md).