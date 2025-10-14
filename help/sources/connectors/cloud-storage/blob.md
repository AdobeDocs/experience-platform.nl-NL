---
title: Azure Blob Source Connector - Overzicht
description: Leer hoe u uw Azure Blob-account kunt verbinden met Experience Platform
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 8e932a25026bef2b785cfddfb8b668b1dd47eb0d
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---

# [!DNL Azure Blob Storage] bron

[!DNL Azure Blob Storage] is een opslagservice voor objecten in de cloud die wordt geboden door [!DNL Microsoft Azure] . Het is ontworpen om grote hoeveelheden ongestructureerde gegevens, zoals tekst, beelden, video&#39;s, steunen, en logboeken op te slaan. Met [!DNL Azure Blob Storage] kunt u grote hoeveelheden ongestructureerde gegevens opslaan en beheren, zoals documenten, afbeeldingen, video&#39;s en audiobestanden. Het is ideaal voor het maken van back-ups en het archiveren van gegevens, het ondersteunen van noodherstel en het verwerken van grote gegevenswerklasten voor analyses.

Gebruik de [!DNL Azure Blob Storage] -bron om uw account te verbinden en gegevens van [!DNL Azure Blob Storage] in te voeren in Adobe Experience Platform.

## Vereisten {#prerequisites}

Lees de volgende secties om de vereiste instellingen te voltooien voordat u uw [!DNL Azure Blob Storage] -account aansluit op Experience Platform.

### IP adres lijst van gewenste personen

U moet gebied-specifieke IP adressen aan uw lijst van gewenste personen toevoegen alvorens uw bronnen aan Experience Platform aan te sluiten. Lees de gids op [&#x200B; voegend op lijst van gewenste personen IP adressen om met Experience Platform &#x200B;](../../ip-address-allow-list.md) voor meer informatie te verbinden.

>[!IMPORTANT]
>
>De [!DNL Azure Blob] -bron ondersteunt geen connectiviteit tussen dezelfde regio&#39;s voor Experience Platform. Als uw [!DNL Azure] -instantie hetzelfde netwerkgebied gebruikt als Experience Platform, kan geen verbinding met Experience Platform-bronnen tot stand worden gebracht. Momenteel wordt alleen connectiviteit tussen regio&#39;s ondersteund.

### Naamgevingsbeperkingen voor bestanden en mappen

Hieronder volgt een lijst met beperkingen waarmee u rekening moet houden wanneer u een naam geeft aan uw bestand of map voor cloudopslag.

- Namen van mappen en bestandscomponenten mogen niet langer zijn dan 255 tekens.
- De folder en de dossiernamen kunnen niet met een voorwaartse schuine streep (`/`) beëindigen. Indien beschikbaar wordt deze automatisch verwijderd.
- De volgende gereserveerde URL-tekens moeten correct worden beschermd: `! ' ( ) ; @ & = + $ , % # [ ]`
- De volgende tekens zijn niet toegestaan: `" \ / : | < > * ?` .
- Ongeldige URL-padtekens niet toegestaan. Codepunten zoals `\uE000` zijn weliswaar geldig in NTFS-bestandsnamen, maar zijn geen geldige Unicode-tekens. Bovendien zijn sommige ASCII- of Unicode-tekens, zoals besturingstekens (0x00 tot 0x1F, \u0081, enz.), niet toegestaan. Voor regels die de koorden van Unicode in HTTP/1.1 bepalen zie [&#x200B; RFC 2616, Sectie 2.2: BasisRegels &#x200B;](https://www.ietf.org/rfc/rfc2616.txt) en [&#x200B; RFC 3987 &#x200B;](https://www.ietf.org/rfc/rfc3987.txt).
- De volgende bestandsnamen zijn niet toegestaan: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, puntteken (.) en twee stippen ( ...).

### [!DNL Azure Blob Storage] verifiëren voor Experience Platform {#authentication}

U kunt uw [!DNL Azure Blob Storage] -account verbinden met Experience Platform door de volgende verificatietypen te gebruiken:

- **de belangrijkste authentificatie van de Rekening**: Gebruikt de toegangssleutel van de opslagrekening om met uw [!DNL Azure Blob Storage] rekening voor authentiek te verklaren en te verbinden.
- **Gedeelde toegangshandtekening (SAS)**: Gebruikt een SAS URI om gedelegeerde, tijd-beperkte toegang tot middelen in uw [!DNL Azure Blob Storage] rekening te verlenen.
- **de hoofd gebaseerde authentificatie van de Dienst**: Gebruikt een Azure Actieve de dienstprincipal van de Folder (AAD) (cliënt identiteitskaart en geheim) om aan uw rekening van de Opslag van Azure Blob veilig voor authentiek te verklaren.

>[!BEGINTABS]

>[!TAB  de belangrijkste authentificatie van de Rekening ]

Geef waarden op voor de volgende referenties om uw [!DNL Azure Blob Storage] -account aan te sluiten op Experience Platform met behulp van accountsleutelverificatie.

| Credentials | Beschrijving |
| --- | --- |
| `connectionString` | De [!DNL Azure Blob Storage] verbindingstekenreeks voor uw opslagaccount. Deze tekenreeks bevat de informatie die is vereist voor verificatie en verbinding met uw [!DNL Azure Blob Storage] -instantie. Voorbeeld: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY};EndpointSuffix=core.windows.net` |
| `container` | De naam van de [!DNL Azure Blob Storage] -container waarin uw gegevensbestanden zijn opgeslagen. Een container ordent een set balken, vergelijkbaar met een map in een bestandssysteem. |
| `folderPath` | Het pad binnen de opgegeven container waarin de bestanden zich bevinden. Dit is een optioneel submappad (virtuele map) in de container. Indien leeg gelaten, wordt de hoofdmap van de container gebruikt. |
| `connectionSpec.id` | De verbindingsSPC identiteitskaart keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecs op het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Azure Blob Storage] is `4c10e202-c428-4796-9208-5f1f5732b1cf` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |

Meer over hoe te om rekeningszeer belangrijke authentificatie met [!DNL Azure Blob Storage] te gebruiken, lees de officiële [&#x200B; Microsoft Azure authentificatiegids &#x200B;](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#account-key-authentication).

>[!TAB  Gedeelde toegangshandtekening ]

Geef waarden op voor de volgende referenties om uw [!DNL Azure Blob Storage] -account aan te sluiten op Experience Platform met een handtekening voor gedeelde toegang.

| Credentials | Beschrijving |
| --- | --- |
| `SasURI` | De URI van de handtekening voor gedeelde toegang die u kunt gebruiken als alternatief verificatietype om uw account te verbinden. Het patroon van SAS URI is: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv={STORAGE_VERSION}&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}`. Voor meer informatie, zie dit [!DNL Azure] document op [&#x200B; gedeelde toegangshandtekening URIs &#x200B;](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| `container` | De naam van de [!DNL Azure Blob Storage] -container waarin uw gegevensbestanden zijn opgeslagen. Een container ordent een set balken, vergelijkbaar met een map in een bestandssysteem. |
| `folderPath` | Het pad binnen de opgegeven container waarin de bestanden zich bevinden. Dit is een optioneel submappad (virtuele map) in de container. Indien leeg gelaten, wordt de hoofdmap van de container gebruikt. |
| `connectionSpec.id` | De verbindingsSPC identiteitskaart keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecs op het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor [!DNL Azure Blob Storage] is `4c10e202-c428-4796-9208-5f1f5732b1cf` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |

Meer over leren hoe te om gedeelde toegangshandtekening met [!DNL Azure Blob Storage] te gebruiken, lees de officiële [&#x200B; Microsoft Azure authentificatiegids &#x200B;](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication).

>[!TAB  de dienst belangrijkste gebaseerde authentificatie ]

Geef waarden op voor de volgende referenties om uw [!DNL Azure Blob Storage] -account aan te sluiten op Experience Platform met behulp van verificatie op basis van basis van serviceprincipes.

| Credentials | Beschrijving |
| --- | --- |
| `serviceEndpoint` | Het eindpunt-URL van uw [!DNL Azure Blob Storage] -account. Doorgaans in de notatie: `https://{ACCOUNT_NAME}.blob.core.windows.net`. |
| `accountKind` | Het type van uw [!DNL Azure Blob Storage] account. Veelvoorkomende waarden zijn `Storage` (general purpose V1), `StorageV2` (general purpose V2), `BlobStorage` en `BlockBlobStorage` . |
| `servicePrincipalId` | De client/toepassings-id van de Azure Active Directory (AAD) service principal die voor verificatie wordt gebruikt. |
| `servicePrincipalKey` | Het clientgeheim of wachtwoord dat aan de Azure service principal is gekoppeld. |
| `tenant` | De Azure Active Directory (AAD) huurder-id waar de serviceprincipal is geregistreerd. |
| `container` | De naam van de Azure Blob Storage-container waarin uw gegevensbestanden zijn opgeslagen. |
| `folderPath` | Het pad binnen de opgegeven container waarin de bestanden zich bevinden. Dit is een optioneel submappad (virtuele map) in de container. Indien leeg gelaten, wordt de hoofdmap van de container gebruikt. |
| `connectionSpec.id` | De verbindingsSPC identiteitskaart keert de schakelaareigenschappen van een bron, met inbegrip van authentificatiespecs op het creëren van de basis en bronverbindingen terug. De verbindingsspecificatie-id voor Azure Blob Storage is `4c10e202-c428-4796-9208-5f1f5732b1cf` . **Nota**: Deze referentie wordt slechts vereist wanneer het verbinden door [!DNL Flow Service] API. |

Om meer over te leren hoe te om de dienst belangrijkste gebaseerde authentificatie met [!DNL Azure Blob Storage] te gebruiken, lees de officiële [&#x200B; Microsoft Azure authentificatiegids &#x200B;](https://learn.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage?tabs=data-factory#service-principal-authentication).

>[!ENDTABS]

## Verbinden [!DNL Azure Blob Storage] met [!DNL Experience Platform]

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen Azure Blob en Adobe Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

- [Verbind  [!DNL Azure Blob Storage]  met Experience Platform](../../tutorials/api/create/cloud-storage/blob.md)
- [De gegevensstructuur en inhoud van een cloudopslagbron verkennen met behulp van de Flow Service API](../../tutorials/api/explore/cloud-storage.md)
- [Een gegevensstroom maken voor een cloudopslagbron met behulp van de Flow Service API](../../tutorials/api/collect/cloud-storage.md)

### UI gebruiken

- [Verbind  [!DNL Azure Blob Storage]  met Experience Platform](../../tutorials/ui/create/cloud-storage/blob.md)
- [Een gegevensstroom maken voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
