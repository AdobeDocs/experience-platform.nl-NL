---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: SFTP-aansluiting
topic: overview
description: De documentatie hieronder verstrekt informatie over hoe te om een server van SFTP aan Platform te verbinden gebruikend APIs of het gebruikersinterface.
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# (Beta) SFTP-connector

>[!NOTE]
>
>De SFTP-connector bevindt zich in bèta. Zie het [Bronoverzicht](../../home.md#terms-and-conditions) voor meer informatie bij het gebruiken van bèta-geëtiketteerde schakelaars.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform]en [!DNL Azure], zodat u gegevens van deze systemen kunt overbrengen.

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen [!DNL Platform] zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. [!DNL Platform] kunt u gegevens van een FTP- of SFTP-server via batches inbrengen.

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de [IP pagina van de lijst van gewenste personen](../../ip-address-allow-list.md) van het adres voor meer informatie.

## Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- Directory- en bestandsnamen mogen niet eindigen met een slash (`/`). Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?`.
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000`, zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Zie [RFC 2616, Section 2.2 voor regels die Unicode-tekenreeksen in HTTP/1.1 bepalen: Basisregels](https://www.ietf.org/rfc/rfc2616.txt) en [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM4, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (..), en twee stiptekens (.).

## SFTP verbinden met [!DNL Platform]

>[!IMPORTANT]
>
>Gebruikers moeten de interactieve verificatie van het toetsenbord uitschakelen in de configuratie van de SFTP-server voordat ze verbinding maken. Als u de instelling uitschakelt, kunnen wachtwoorden handmatig worden ingevoerd in plaats van via een service of programma. Raadpleeg het [Component Pro-document](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) voor meer informatie over Interactieve toetsenbordverificatie.

De documentatie hieronder verstrekt informatie over hoe te om een server van SFTP aan het [!DNL Platform] gebruiken van APIs of de gebruikersinterface te verbinden:

### API&#39;s gebruiken

- [Een SFTP-connector maken met de Flow Service API](../../tutorials/api/create/cloud-storage/sftp.md)
- [Een systeem voor cloudopslag verkennen met de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Gegevens voor cloudopslag verzamelen met de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### De gebruikersinterface gebruiken

- [Een SFTP-bronconnector maken in de UI](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Een gegevensstroom configureren voor een aansluiting voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)