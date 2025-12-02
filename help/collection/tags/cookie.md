---
title: koekje
description: Cookies voor de eigenschap tag handmatig schrijven, bewerken of verwijderen.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 2%

---

# `cookie`

Het `_satellite.cookie` -object bevat methoden waarmee u cookies waarnaar de tagregels kunnen verwijzen, kunt schrijven, bewerken of verwijderen. Het is een gedeeltelijke kopie van [`js-cookie` &#x200B;](https://github.com/js-cookie/js-cookie), die vele kerneigenschappen van die bibliotheek bevatten.

## `cookie.set()`

De methode `set()` schrijft een cookie waarnaar de eigenschap tag kan verwijzen.

```ts
_satellite.cookie.set(name: string, value: string, attributes?: {
  expires?: number | Date;
  path?: string;
  domain?: string;
  secure?: boolean;
  sameSite?: 'Strict' | 'Lax' | 'None';
}): string
```

De volgende methodeparameters zijn beschikbaar:

| Naam | Type | Vereist | Beschrijving |
|---|---|---|---|
| **`name`** | `string` | Ja | De naam van het cookie. |
| **`value`** | `string` | Ja | De waarde van de cookie |
| **`attributes`** | `object` | Nee | Aanvullende kenmerken voor de cookie. |

Het `attributes` -object ondersteunt de volgende eigenschappen:

| Kenmerknaam | Type | Vereist | Standaard | Beschrijving |
|---|---|---|---|---|
| **`expires`** | `number` of [`Date` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date) | Nee | Het cookie verloopt aan het einde van de browsersessie | Het aantal dagen dat de cookie moet verlopen. |
| **`path`** | `string` | Nee | Zichtbare cookie voor de hele site | Waar op uw domein is de cookie zichtbaar. |
| **`domain`** | `string` | Nee | Cookie is zichtbaar voor het domein waaronder het is gemaakt | Een geldig domein (met of zonder een subdomein) waar het cookie zichtbaar is. Als een domein zonder subdomein wordt omvat, is het koekje zichtbaar aan alle subdomeinen onder dat domein. |
| **`secure`** | `boolean` | Nee | Geen kenmerkset | Bepaalt als het koekje een veilig protocol (`https://`) vereist. Indien weggelaten, is er geen veilig protocolvereiste. |
| **`sameSite`** | `'Strict' \| 'Lax' \| 'None'` | Nee | Geen kenmerkset | Hiermee kunt u het kenmerk [`sameSite` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/HTTP/Reference/Headers/Set-Cookie#samesitesamesite-value) van een cookie instellen. Als u `sameSite` instelt op `None` , moet u ook `secure` instellen op `true` . |

```js
// Sets a cookie valid across the entire site, expires on session close
_satellite.cookie.set('simple_session_cookie', 'value');

// Sets a cookie that expires 7 days from now, valid across the entire site
_satellite.cookie.set('seven_day_cookie', 'value', { expires: 7 });

// Sets a cookie that expires 14 days from now, valid only on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { expires: 14, path: '/' });

// Cross-site compatible cookie (requires HTTPS)
_satellite.cookie.set('cross_site_cookie', 'value', { secure: true, sameSite: 'None' });
```

Als u deze methode aanroept, wordt het gewenste cookie geschreven en wordt de geserialiseerde cookie-tekenreeks geretourneerd die is geschreven. Deze tekenreeks wordt vooral gebruikt voor foutopsporing of logboekdoeleinden.

```text
'written_cookie=value; path=/'
```

>[!TIP]
>
>Eerdere versies van het gebruikte tagobject `_satellite.setCookie()` . De methode `setCookie()` is vervangen door `_satellite.cookie.set()` .

## `cookie.get()`

De methode `get()` retourneert een cookiewaarde.

```ts
_satellite.cookie.get(name: string): string | undefined;
```

| Naam | Type | Vereist | Beschrijving |
|---|---|---|---|
| **`name`** | `string` | Ja | De cookienaam waarvan u de waarde wilt ophalen (hoofdlettergevoelig). |

Als de naam van het cookie bestaat, wordt de waarde van het cookie geretourneerd. Als de cookienaam niet bestaat, keert `undefined` terug.

>[!TIP]
>
>Eerdere versies van het gebruikte tagobject `_satellite.getCookie()` . De methode `getCookie()` is vervangen door `_satellite.cookie.get()` .

## `cookie.remove()`

Met de methode `remove()` verwijdert u een cookie die u hebt ingesteld.

```ts
_satellite.cookie.remove(name: string, attributes?: {
  path?: string;
  domain?: string;
}): void
```

| Naam | Type | Vereist | Beschrijving |
|---|---|---|---|
| **`name`** | `string` | Ja | De cookienaam die u wilt verwijderen. |
| **`attributes`** | `object` | Nee | De kenmerken van het cookie dat u wilt verwijderen. Als u een cookie instelt met de kenmerken `path` of `domain` , neemt u die kenmerken op wanneer u de cookie verwijdert. Als deze kenmerken niet worden opgenomen, wordt het cookie niet verwijderd. |

```js
// Creates a session cookie
_satellite.cookie.set('session_cookie', 'Cookie value');

// Removes the above cookie
_satellite.cookie.remove('session_cookie');

// Creates a cookie that is only visible on the current page
_satellite.cookie.set('page_specific_cookie', 'value', { path: '/' });

// This remove method does nothing because it does not match the path and domain attributes of the cookie set
_satellite.cookie.remove('page_specific_cookie');

// This remove method works correctly for the page-specific cookie
_satellite.cookie.remove('page_specific_cookie', { path: '/' });
```

>[!TIP]
>
>Eerdere versies van het gebruikte tagobject `_satellite.removeCookie()` . De methode `removeCookie()` is vervangen door `_satellite.cookie.remove()` .
