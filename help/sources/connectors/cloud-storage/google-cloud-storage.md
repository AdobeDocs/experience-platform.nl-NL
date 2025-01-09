---
keywords: Experience Platform;home;populaire onderwerpen;Google Cloud Storage;Google Cloud-opslag
solution: Experience Platform
title: Google Cloud Storage Source Connector - Overzicht
description: Leer hoe u Google Cloud Storage met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: f7ebd213-f914-4c49-aebd-1df4514ffec0
source-git-commit: ee659ded9701132b12d5b93672b4c958e9720028
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Google Cloud Storage-connector

>[!IMPORTANT]
>
>U kunt nu de [!DNL Google Cloud Storage] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van het Experience Platform leren, zie het [ Experience Platform multi-cloud overzicht ](../../../landing/multi-cloud.md).

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure] , zodat u gegevens van deze systemen kunt overbrengen.

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen naar Platform zonder dat u deze hoeft te downloaden, opmaken of uploaden. De opgenomen gegevens kunnen als JSON of Parquet worden geformatteerd die met het Model van de Gegevens van de Ervaring (XDM), of in een afgebakend formaat volgzaam is. Elke stap van het proces is geïntegreerd in de bronwerkstroom. Met Platform kunt u gegevens uit [!DNL Google Cloud Storage] tot en met batches inbrengen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Vereiste instellingen voor verbinding met uw [!DNL Google Cloud Storage] -account

Als u verbinding wilt maken met Platform, moet u eerst interoperabiliteit inschakelen voor uw [!DNL Google Cloud Storage] -account. Als u de instelling voor interoperabiliteit wilt openen, opent u [!DNL Google Cloud Platform] en selecteert u **[!UICONTROL Settings]** in de optie **[!UICONTROL Cloud Storage]** in het navigatievenster.

<!-- ![](../../images/tutorials/create/google-cloud-storage/nav.png) -->

De pagina **[!UICONTROL Settings]** wordt weergegeven. Hier vindt u informatie over uw [!DNL Google] project-id en informatie over uw [!DNL Google Cloud Storage] -account. Selecteer **[!UICONTROL Interoperability]** in de bovenste koptekst voor toegang tot de instellingen voor interoperabiliteit.

<!-- ![](../../images/tutorials/create/google-cloud-storage/project-access.png) -->

De pagina **[!UICONTROL Interoperability]** bevat informatie over verificatie, toegangstoetsen en het standaardproject dat aan uw serviceaccount is gekoppeld. Selecteer **[!UICONTROL Create a Key for a Service Account]** om een nieuwe toegangs sleutel-id en een geheime toegangssleutel voor uw serviceaccount te genereren.

<!-- ![](../../images/tutorials/create/google-cloud-storage/interoperability.png) -->

U kunt uw onlangs gegenereerde toegangs sleutel-id en geheime toegangssleutel gebruiken om uw [!DNL Google Cloud Storage] -account te verbinden met Platform.

Voor meer informatie, te lezen gelieve de gids over [ het creëren van en het beheren van de sleutels van de de dienstrekening ](https://cloud.google.com/iam/docs/creating-managing-service-account-keys) van de [!DNL Google Cloud] documentatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [ RFC 2616, Sectie 2.2: BasisRegels ](https://www.ietf.org/rfc/rfc2616.txt) en [ RFC 3987 ](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

## Verbinden [!DNL Google Cloud Storage] met platform

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Google Cloud Storage] en Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Een Google Cloud Storage-basisverbinding maken met de Flow Service API](../../tutorials/api/create/cloud-storage/google.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Een Google Cloud Storage-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
