---
keywords: Experience Platform; veiligheid; ip-toegang; bevestiging; API gids; vraagdienst; IP controle
title: Eindpunt van IP-validatie
description: Leer hoe te om IP toegang voor zandbakken in de Dienst van de Vraag te bevestigen gebruikend het IP API eindpunt van de Bevestiging.
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 3%

---

# IP-eindpunt voor validatie

>[!AVAILABILITY]
>
>Deze functionaliteit is beschikbaar voor klanten die de Data Distiller-add hebben aangeschaft. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger.

Gebruik het IP eindpunt van de Bevestiging API om te verifiëren of een gespecificeerd IP adres wordt toegelaten om tot een aangewezen zandbak in de Dienst van de Vraag toegang te hebben. Deze controle bevestigt of de toegangsbeperkingen van toepassing zijn of of een IP adres wordt toegelaten om tot gegevens binnen een zandbak toegang te hebben.

## IP valideren voor toegang tot sandbox {#validate-ip-for-sandbox-access}

Gebruik het IP eindpunt van de Bevestiging om te controleren of een bepaald IP adres tot gegevens voor de gespecificeerde zandbak wordt toegelaten. Als er geen IP-beperkingen zijn geconfigureerd voor de sandbox, zijn alle IP-adressen standaard toegestaan. Als er bestaande IP- of CIDR-beperkingen zijn, controleert deze API of het opgegeven IP-adres overeenkomt met een geconfigureerd bereik.

>[!NOTE]
>
>U kunt tot dit eindpunt met of **gebruikerstokens** of **de diensttokens** toegang hebben. Er zijn geen specifieke rolvereisten nodig.

**API formaat**

```http
POST /security/validate/ip-access
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Reactie**

Een succesvolle reactie keert HTTP status 200 met een booleaanse erop wijst terug die of IP wordt toegestaan.

>[!NOTE]
>
>Het veld `isAllowed` in het antwoord retourneert `true` als de opgegeven IP toegang heeft tot de sandbox en `false` in andere gevallen. Deze API biedt ondersteuning voor dynamisch valideren van toegang en voor het garanderen van beveiligingscompatibiliteit voor sandboxomgevingen.

```json
{
"isAllowed": true
}
```
