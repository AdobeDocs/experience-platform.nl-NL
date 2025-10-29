---
title: Privéextensiepakketten delen in de Reactor-API
description: Leer hoe u andere bedrijven toestaat om persoonlijke extensiepakketten te delen in de Reactor-API.
exl-id: 3300a630-6d22-46e1-8b1b-b5d12a3ea44c
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Persoonlijke extensiepakketten delen

>[!NOTE]
>
>Gebruikers met de machtiging `develop_extensions` in de eigenaar-organisatie van het extensiepakket kunnen gebruiksmachtigingen voor extensiepakketten voor dat extensiepakket maken, weergeven en verwijderen. Gebruikers in een geautoriseerde organisatie die beschikken over de machtiging `manage_properties` , mogen alleen de gebruiksmachtigingen voor extensiepakketten voor hun organisatie weergeven en hun status bijwerken naar `accepted` als ze dat extensiepakket willen gebruiken, of naar `rejected` als ze het niet willen gebruiken.

Eigenaars van extensiepakketten kunnen andere bedrijven toestemming geven om hun persoonlijke versies te gebruiken via de Reactor-API. Een gebruiksvergunning voor één uitbreidingspakket wordt verleend aan elk goedgekeurd bedrijf, en deze vergunning is goed voor alle huidige en toekomstige privé versies van het pakket.

Deze gids verstrekt een overzicht op hoog niveau van hoe te om de vergunningen van het gebruiksgebruik van het uitbreidingspakket te vormen. Voor meer gedetailleerde begeleiding op hoe te om toestemmingen in Reactor API, met inbegrip van voorbeeld JSON van de structuur van een vergunning te beheren, verwijs naar de [ gids van het de vergunningseindpunt van het uitbreidingspakket ](../endpoints/extension-package-usage-authorizations.md).

## Een autorisatie maken {#create-authorization}

Als u een nieuwe autorisatie wilt maken, hebt u het recht `develop_extensions` . In het volgende voorbeeld ziet u hoe u een gebruiksmachtiging voor een extensiepakket kunt maken met `authorized_org_id` van het bedrijf dat u wilt autoriseren.

**API formaat**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | De `ID` van het extensiepakket waarvoor u een autorisatie wilt maken. |

{style="table-layout:auto"}

**Verzoek**

Met het volgende verzoek wordt een nieuwe vergunning voor het extensiepakket gemaakt voor het opgegeven bedrijf.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes.authorized_org_id` | De `ID` van de organisatie die u wilt autoriseren. |

{style="table-layout:auto"}

De initiële status van de autorisatie bevindt zich in het `pending_approval` -stadium. Voordat het extensiepakket wordt gebruikt, moet de firma de vergunning goedkeuren. Gebruikers van het bedrijf kunnen door het persoonlijke extensiepakket bladeren terwijl de autorisatie in afwachting is van goedkeuring, maar ze kunnen het niet installeren en vinden het niet in hun extensiecatalogus.

## Goedkeuren van een vergunning {#approve-authorization}

Als u een autorisatie wilt goedkeuren, moet u over de `manage_properties` -rechten beschikken. Als het geautoriseerde bedrijf moet u een PATCH-aanvraag verzenden naar de gebruiksautorisatie voor het extensiepakket, inclusief de `ID` van de autorisatie en de status instellen op `approved` .

**API formaat**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | De `ID` van de autorisatie die u wilt goedkeuren. |

{style="table-layout:auto"}

**Verzoek**

Met de volgende PATCH-aanvraag wordt de `state` van een autorisatie ingesteld op `approved` .

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
            },
            "id": ":extension_package_usage_authorization_id",
            "type": "extension_package_usage_authorizations"
        }
      }
```

Zodra de vergunning wordt goedgekeurd, als geautoriseerd bedrijf, kunt u het uitbreidingspakket op uw eigenschappen nu installeren.

>[!NOTE]
>
>Indien de vergunning wordt geweigerd, zal de vergunninghoudende onderneming het verlengingspakket niet kunnen gebruiken.

## Een autorisatie verwijderen {#delete-authorization}

Als eigenaar van een extensiepakket kunt u de autorisatie op elk gewenst moment intrekken door de gebruiksautorisatie voor het extensiepakket te verwijderen. Hierdoor kan het geautoriseerde bedrijf geen privéversies van het extensiepakket in de catalogus weergeven en deze op de eigenschappen installeren. Reeds geïnstalleerde privéversies werken echter na verwijdering naar behoren.

**API formaat**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | De `ID` van de autorisatie die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

Met het volgende DELETE-verzoek worden de machtigingsprioriteiten voor een onderneming opgeheven.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
