---
keywords: Experience Platform;thuis;populaire onderwerpen;Marketo Engage;marketo engageren;marketo
solution: Experience Platform
title: Verifieer uw Marketo-bronconnector
description: Dit document bevat informatie over hoe u uw Marketo-verificatiereferenties kunt genereren.
exl-id: 594dc8b6-cd6e-49ec-9084-b88b1fe8167a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---

# Verifieer uw [!DNL Marketo Engage] bronconnector

Voordat u een [!DNL Marketo Engage] (hierna &quot;[!DNL Marketo]&quot;genoemd) bronschakelaar kunt creëren, moet u eerst opstelling een douanedienst door de [!DNL Marketo] interface, evenals waarden voor uw identiteitskaart Munchkin, cliënt identiteitskaart, en cliëntgeheim terugwinnen.

In de onderstaande documentatie vindt u stappen voor het verkrijgen van verificatiereferenties om een [!DNL Marketo] bronconnector te maken.

## Een nieuwe rol instellen

De eerste stap in het verkrijgen van uw authentificatiegeloofsbrieven is aan opstelling een nieuwe rol door de [[!DNL Marketo] &#x200B;](https://app-sjint.marketo.com/#MM0A1) interface.

Meld u aan bij [!DNL Marketo] en selecteer **[!DNL Admin]** in de bovenste navigatiebalk.

![&#x200B; Admin voor een nieuwe rol &#x200B;](../images/marketo/home.png)

De *[!DNL Users & Role]s* pagina bevat informatie over gebruikers, rollen, en login geschiedenissen. Als u een nieuwe rol wilt maken, selecteert u **[!DNL Roles]** in de bovenste kop en selecteert u vervolgens **[!DNL New Role]** .

![&#x200B; nieuw-rol &#x200B;](../images/marketo/new-role.png)

Het dialoogvenster **[!DNL Create New Role]** wordt weergegeven. Geef een naam en een beschrijving op en selecteer vervolgens de machtigingen die u voor deze rol wilt verlenen. De toestemmingen zijn beperkt tot specifieke werkruimten en de gebruikers kunnen slechts acties in werkruimten uitvoeren die zij toestemmingen binnen hebben.

Selecteer **[!DNL Create]** als u de machtigingen hebt geselecteerd die u wilt verlenen.

![&#x200B; creeer-nieuw-rol &#x200B;](../images/marketo/create-new-role.png)

U kunt beperkte machtigingen voor de API beheren wanneer u rollen maakt met [!DNL Marketo] . In plaats van &quot;Toegang API&quot;te selecteren, kunt u een rol van het minimumniveau van toegang verstrekken door de volgende toestemmingen te selecteren:

* [!DNL Read-Only Activity]
* [!DNL Read-Only Assets]
* [!DNL Read-Only Campaign]
* [!DNL Read-Only Company]
* [!DNL Read-Only Custom Object]
* [!DNL Read-Only Custom Object Type]
* [!DNL Read-Only Named Account]
* [!DNL Read-Only Named Account List]
* [!DNL Read-Only Opportunity]
* [!DNL Read-Only Person]
* [!DNL Read-Only Sales Person]

## Nieuwe gebruiker instellen

Net als rollen kunt u een nieuwe gebruiker instellen vanaf de pagina **[!DNL Users & Roles]** . De pagina **[!DNL Users]** bevat een lijst met actieve gebruikers die momenteel zijn ingericht in Marketo. Selecteer **[!DNL Invite New User]** om een nieuwe gebruiker op te richten.

![&#x200B; nodig-nieuw-gebruiker &#x200B;](../images/marketo/invite-new-user.png)

Er wordt een pop-upmenu weergegeven. Geef de juiste gegevens op voor uw e-mail, voornaam, achternaam en reden. Tijdens deze stap kunt u ook een vervaldatum instellen voor de toegang tot de nieuwe gebruikersaccount die u uitnodigt. Selecteer **[!DNL Next]** als u klaar bent.

>[!IMPORTANT]
>
>Wanneer vestiging moet een nieuwe gebruiker, u toegang tot een gebruiker toewijzen die strikt aan de douanedienst wordt gewijd u creeert.

![&#x200B; gebruiker-info &#x200B;](../images/marketo/new-user-info.png)

Selecteer de desbetreffende velden in de stap **[!DNL Permissions]** en schakel vervolgens het selectievakje **[!DNL API Only]** in om de nieuwe gebruiker een API-rol te geven. Selecteer **[!DNL Next]** om door te gaan.

![&#x200B; toestemmingen &#x200B;](../images/marketo/permissions.png)

Selecteer **[!DNL Send]** om het proces te voltooien.

![&#x200B; bericht &#x200B;](../images/marketo/message.png)

## Een aangepaste service instellen

Nadat u een nieuwe gebruiker hebt ingesteld, kunt u een aangepaste service instellen om uw nieuwe referenties op te halen. Selecteer **[!DNL LaunchPoint]** op de beheerpagina.

![&#x200B; admin-lanceringspunt &#x200B;](../images/marketo/admin-launchpoint.png)

De pagina **[!DNL Installed services]** bevat een lijst met bestaande services. Als u een nieuwe aangepaste service wilt maken, selecteert u **[!DNL New]** en selecteert u vervolgens **[!DNL New Service]** .

![&#x200B; nieuw-dienst &#x200B;](../images/marketo/new-service.png)

Geef uw nieuwe service een beschrijvende weergavenaam en selecteer vervolgens **[!DNL Custom]** in het vervolgkeuzemenu **[!DNL Service]** . Geef een geschikte beschrijving op en selecteer vervolgens de gebruiker die u wilt instellen in het vervolgkeuzemenu **[!DNL API Only User]** . Nadat u de benodigde gegevens hebt ingevuld, selecteert u **[!DNL Create]** om de nieuwe aangepaste service te maken.

![&#x200B; creeer &#x200B;](../images/marketo/create.png)

## Je client-id en clientgeheim ophalen

Als er een nieuwe aangepaste service wordt gemaakt, kunt u nu waarden voor uw client-id en clientgeheim ophalen. Zoek in het menu **[!DNL Installed Services]** de aangepaste service die u wilt openen en selecteer vervolgens **[!DNL View Details]** .

![&#x200B; mening-details &#x200B;](../images/marketo/view-details.png)

Er wordt een dialoogvenster weergegeven met de client-id en het clientgeheim.

![&#x200B; geloofsbrieven &#x200B;](../images/marketo/credentials.png)

## Uw Munchkin-id ophalen

De laatste stap die u moet voltooien om uw [!DNL Marketo] bronaansluiting te verifiëren, is het ophalen van uw Munchkin-id. Selecteer op de beheerpagina **[!DNL Munchkin]** onder het deelvenster **[!DNL Integration]** .

![&#x200B; admin-munchkin &#x200B;](../images/marketo/admin-munchkin.png)

De pagina *[!DNL Munchkin]* wordt weergegeven, met uw unieke Munchkin-id boven in het deelvenster.

![&#x200B; munchkin-Id &#x200B;](../images/marketo/munchkin-id.png)

Gecombineerd met uw cliëntidentiteitskaart en cliëntgeheim, kunt u uw identiteitskaart gebruiken Munchkin om een nieuwe rekening te vormen en [&#x200B; een nieuwe  [!DNL Marketo]  bronverbinding &#x200B;](../../../tutorials/ui/create/adobe-applications/marketo.md) op Experience Platform tot stand te brengen.
