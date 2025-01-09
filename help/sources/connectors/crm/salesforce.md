---
title: Overzicht Salesforce Source Connector
description: Leer hoe u Salesforce met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
exl-id: 597778ad-3cf8-467c-ad5b-e2850967fdeb
source-git-commit: ee659ded9701132b12d5b93672b4c958e9720028
workflow-type: tm+mt
source-wordcount: '1528'
ht-degree: 0%

---

# [!DNL Salesforce]

>[!IMPORTANT]
>
>U kunt nu de [!DNL Salesforce] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van het Experience Platform leren, zie het [ Experience Platform multi-cloud overzicht ](../../../landing/multi-cloud.md).


Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen terwijl u de mogelijkheid krijgt om inkomende gegevens te structureren, te labelen en te verbeteren met behulp van de platformservices. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-systeem van derden. Tot de ondersteuning voor CRM-providers behoren [!DNL Salesforce] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Veldtoewijzing van [!DNL Salesforce] naar XDM

Om een bronverbinding tussen [!DNL Salesforce] en Platform tot stand te brengen, moeten de [!DNL Salesforce] brongegevensgebieden aan hun aangewezen doelXDM gebieden worden in kaart gebracht alvorens in Platform wordt opgenomen.

Zie het volgende voor gedetailleerde informatie over de regels voor het in kaart brengen van velden tussen [!DNL Salesforce] datasets en Platform:

- [Contactpersonen](../adobe-applications/mapping/salesforce.md#contact)
- [Leads](../adobe-applications/mapping/salesforce.md#lead)
- [Accounts](../adobe-applications/mapping/salesforce.md#account)
- [Kansen](../adobe-applications/mapping/salesforce.md#opportunity)
- [Contactrollen opportunity](../adobe-applications/mapping/salesforce.md#opportunity-contact-role)
- [Campagnes](../adobe-applications/mapping/salesforce.md#campaign)
- [Campagneleden](../adobe-applications/mapping/salesforce.md#campaign-member)
- [Contactpersoon account](../adobe-applications/mapping/salesforce.md#account-contact-relation)

## Het hulpprogramma voor automatisch genereren van naamruimten en schema [!DNL Salesforce] instellen

Als u de [!DNL Salesforce] bron wilt gebruiken als onderdeel van [!DNL B2B-CDP] , moet u eerst een hulpprogramma [!DNL Postman] instellen om automatisch uw [!DNL Salesforce] naamruimten en schema&#39;s te genereren. In de volgende documentatie vindt u aanvullende informatie over het instellen van het hulpprogramma [!DNL Postman] :

- U kunt namespace en schema auto-generatie nutsinzameling en milieu van deze [ bewaarplaats GitHub ](https://github.com/adobe/experience-platform-postman-samples/tree/master/Postman%20Collections/CDP%20Namespaces%20and%20Schemas%20Utility) downloaden.
- Voor informatie bij het gebruiken van Platform APIs met inbegrip van details over hoe te om waarden voor vereiste kopballen te verzamelen en steekproefAPI vraag te lezen, zie de gids op [ begonnen wordt met Platform APIs ](../../../landing/api-guide.md).
- Voor informatie over hoe te om uw geloofsbrieven voor Platform APIs te produceren, zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md).
- Voor informatie over hoe te opstelling [!DNL Postman] voor Platform APIs, zie het leerprogramma op [ vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../landing/postman.md).

Met een platformontwikkelaarsconsole en [!DNL Postman] -configuratie kunt u nu de juiste omgevingswaarden toepassen op uw [!DNL Postman] -omgeving.

De volgende tabel bevat voorbeeldwaarden en aanvullende informatie over het vullen van de [!DNL Postman] -omgeving:

| Variabele | Beschrijving | Voorbeeld |
| --- | --- | --- |
| `CLIENT_SECRET` | Een unieke id die wordt gebruikt om de `{ACCESS_TOKEN}` te genereren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{CLIENT_SECRET}` terug te winnen. | `{CLIENT_SECRET}` |
| `JWT_TOKEN` | JSON Web Token (JWT) is een verificatiereferentie die wordt gebruikt om uw {ACCESS_TOKEN} te genereren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{JWT_TOKEN}` te produceren. | `{JWT_TOKEN}` |
| `API_KEY` | Een unieke id die wordt gebruikt om aanroepen van Experience Platform-API&#39;s te verifiëren. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{API_KEY}` terug te winnen. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `ACCESS_TOKEN` | Het toestemmingstoken dat wordt vereist om vraag aan Experience Platform APIs te voltooien. Zie het leerprogramma op [ voor authentiek verklaren en tot Experience Platform APIs toegang heeft ](../../../landing/api-authentication.md) voor informatie over hoe te om uw `{ACCESS_TOKEN}` terug te winnen. | `Bearer {ACCESS_TOKEN}` |
| `META_SCOPE` | Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ent_dataservices_sdk` . | `ent_dataservices_sdk` |
| `CONTAINER_ID` | De `global` container houdt alle standaard Adobe en partner van het Experience Platform verstrekte klassen, de groepen van het schemagebied, gegevenstypes, en schema&#39;s. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op `global` . | `global` |
| `PRIVATE_KEY` | Een referentie die wordt gebruikt om de [!DNL Postman] -instantie te verifiëren voor Experience Platform-API&#39;s. Zie het leerprogramma bij de console van de opstellingsontwikkelaar en [ vestiging de console van de opsteller en  [!DNL Postman]](../../../landing/postman.md) voor instructies op hoe te om uw {PRIVATE_KEY} terug te winnen. | `{PRIVATE_KEY}` |
| `TECHNICAL_ACCOUNT_ID` | Een referentie die wordt gebruikt om te integreren in Adobe I/O. | `D42AEVJZTTJC6LZADUBVPA15@techacct.adobe.com` |
| `IMS` | Het Identity Management System (IMS) biedt het framework voor verificatie van Adobe-services. Met betrekking tot [!DNL Marketo] is deze waarde vast en altijd ingesteld op: `ims-na1.adobelogin.com` . | `ims-na1.adobelogin.com` |
| `IMS_ORG` | Een onderneming die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden. Zie het leerprogramma op [ vestiging de console van de ontwikkelaar en  [!DNL Postman]](../../../landing/postman.md) voor instructies op hoe te om uw `{ORG_ID}` informatie terug te winnen. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `SANDBOX_NAME` | De naam van de virtuele sandboxpartitie die u gebruikt. | `prod` |
| `TENANT_ID` | Een id die wordt gebruikt om ervoor te zorgen dat de bronnen die u maakt, correct worden genoemd en zich binnen uw organisatie bevinden. | `b2bcdpproductiontest` |
| `PLATFORM_URL` | Het URL-eindpunt waarnaar u API-aanroepen maakt. Deze waarde is vast en wordt altijd ingesteld op: `http://platform.adobe.io/` . | `http://platform.adobe.io/` |
| `munchkinId` | De unieke id voor uw [!DNL Marketo] -account. Zie het leerprogramma op [ voor authentiek verklaren uw  [!DNL Marketo]  instantie ](../adobe-applications/marketo/marketo-auth.md) voor informatie over hoe te om uw `munchkinId` terug te winnen. | `123-ABC-456` |
| `sfdc_org_id` | De organisatie-id voor uw [!DNL Salesforce] -account. Zie de volgende [[!DNL Salesforce]  gids ](https://help.salesforce.com/articleView?id=000325251&amp;type=1&amp;mode=1) voor meer informatie bij het verwerven van uw [!DNL Salesforce] organisatie identiteitskaart | `00D4W000000FgYJUA0` |
| `has_abm` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Account-Based Marketing] . | `false` |
| `has_msi` | Een booleaanse waarde die aangeeft of u bent geabonneerd op [!DNL Marketo Sales Insight] . | `false` |

{style="table-layout:auto"}

### Scripts uitvoeren

Als de verzameling van [!DNL Postman] is ingesteld en de omgeving is ingesteld, kunt u het script nu uitvoeren via de interface van [!DNL Postman] .

Selecteer in de interface [!DNL Postman] de hoofdmap van het hulpprogramma voor automatische generator en selecteer vervolgens **[!DNL Run]** in de bovenste koptekst.

![ wortel-omslag ](../../images/tutorials/create/salesforce/root-folder.png)

De interface [!DNL Runner] wordt weergegeven. Controleer van hieruit of alle selectievakjes zijn ingeschakeld en selecteer vervolgens **[!DNL Run Namespaces and Schemas Autogeneration Utility]** .

![ looppas-generator ](../../images/tutorials/create/salesforce/run-generator.png)

Een succesvol verzoek leidt tot B2B namespaces en schema&#39;s volgens bètaspecificaties.

## De [!DNL Salesforce] -bron instellen voor Experience Platform op Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Deze sectie is van toepassing op implementaties van Experience Platform dat op Amazon Web Services (AWS) loopt. Experience Platform dat op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van het Experience Platform leren, zie het [ Experience Platform multi-cloud overzicht ](../../../landing/multi-cloud.md).

Volg de onderstaande stappen om te leren hoe u uw [!DNL Salesforce] -account kunt instellen voor Experience Platform op Amazon Web Services (AWS).

### Vereisten

Als u uw [!DNL Salesforce] -account wilt koppelen aan een Experience Platform in een AWS-gebied, hebt u het volgende nodig:

- Een [!DNL Salesforce] -account met API-toegang.
- A [!DNL Salesforce Connected App] dat u vervolgens kunt gebruiken om JWT_BEARER OAuth-flow in te schakelen.
- De benodigde machtigingen in [!DNL Salesforce] voor toegang tot gegevens.

U moet ook de volgende IP-adressen toevoegen aan uw lijst van gewenste personen om uw [!DNL Salesforce] -account te koppelen aan het Experience Platform op Amazon Web Services (AWS):

- `34.193.63.59`
- `44.217.93.240`
- `44.194.79.229`

### Een [!DNL Salesforce Connected App] maken

Gebruik eerst het volgende om een certificaat/sleutelpaar PEM-bestanden te maken.

```shell
openssl req -newkey rsa:4096 -new -nodes -x509 -days 3650 -keyout key.pem -out cert.pem  
```

1. In het [!DNL Salesforce] dashboard, uitgezochte montages (![ het montagespictogram.](/help/images/icons/settings.png) ) en selecteer vervolgens **[!DNL Setup]** .
2. Navigeer naar [!DNL App Manager] en selecteer vervolgens **[!DNL New Connection App]** .
3. Geef een naam op voor uw app en zorg dat de overige velden automatisch kunnen worden ingevuld.
4. Schakel het vak voor [!DNL Enable OAuth Settings] in.
5. Stel een callback-URL in. Omdat deze optie niet wordt gebruikt voor JWT, kunt u `https://localhost` gebruiken.
6. Schakel het vak voor [!DNL Use Digital Signatures] in.
7. Upload het bestand cert.perm dat eerder is gemaakt.

#### Vereiste machtigingen toevoegen

Voeg de volgende machtigingen toe:

1. Gebruikersgegevens beheren via API&#39;s (api)
2. Toegang tot aangepaste machtigingen (custom_permissions)
3. Toegang tot de dienst van identiteitskaart URL (identiteitskaart, profiel, e-mail, adres, telefoon)
4. Unieke id&#39;s benaderen (openid)
5. Verzoeken op elk gewenst moment uitvoeren (refresh_token, offline_access)

Nadat u de machtigingen hebt toegevoegd, schakelt u het vak voor **[!DNL Issue JSON Web Token (JWT)-based access tokens for named user]** in.

Selecteer vervolgens **[!DNL Save]** , **[!DNL Continue]** en **[!DNL Manage Customer Details]** . Gebruik het deelvenster met consumentendetails om het volgende op te halen:

- **Consumentensleutel**: U zult later deze Consumentensleutel als uw cliëntidentiteitskaart gebruiken, wanneer het voor authentiek verklaren van uw [!DNL Salesforce] rekening aan Experience Platform.
- **Consumentengeheim**: U zult later dit consumentengeheim als uw cliëntidentiteitskaart gebruiken, wanneer het voor authentiek verklaren van uw [!DNL Salesforce] rekening aan Experience Platform.

### Uw [!DNL Salesforce] -gebruiker autoriseren voor de aangesloten app

Voer de onderstaande stappen uit om toestemming te krijgen voor het gebruik van de Connected App:

1. Navigeer naar **[!DNL Manage Connected Apps]** .
2. Selecteer **[!DNL Edit]**.
3. Configureer **[!DNL Permitted Users]** als **[!DNL Admin approved users are pre-authorized]** en selecteer **[!DNL Save]** .
4. Navigeer naar **[!DNL Settings]> [!DNL Manage Users] >[!DNL Profiles]** .
5. Bewerk het profiel dat aan de gebruiker is gekoppeld.
6. Navigeer naar **[!DNL Connected App Access]** en selecteer vervolgens de app die u in een eerdere stap hebt gemaakt.

### Token voor JWT-tower genereren

Voer de onderstaande stappen uit om uw token voor de JWT-toonder te genereren.

#### Sleutelpaar omzetten in pkcs12

Als u uw JWT-token voor toonder wilt genereren, moet u eerst de volgende opdracht gebruiken om uw certificaat/sleutelpaar om te zetten in de indeling pkcs12. Tijdens deze stap, moet u ook **een uitvoerwachtwoord** plaatsen wanneer ertoe aangezet.

```shell
openssl pkcs12 -export -in cert.pem -inkey key.pem -name jwtcert >jwtcert.p12
```

#### Java-sleutelarchief maken op basis van pkcs12

Vervolgens gebruikt u de volgende opdracht om een Java-sleutelarchief te maken op basis van de pkcs12 die u zojuist hebt gegenereerd. Tijdens deze stap, moet u a **ook een wachtwoord van het bestemmingssleutelarchief** plaatsen wanneer ertoe aangezet. Daarnaast moet u het vorige exportwachtwoord opgeven als het bronsleutelarchiefwachtwoord.

```shell
keytool -importkeystore -srckeystore jwtcert.p12 -destkeystore keystore.jks -srcstoretype pkcs12 -alias jwtcert
```

#### Bevestig dat keystroke.jks een jwtcert-alias bevat

Gebruik vervolgens de volgende opdracht om te bevestigen dat de `keystroke.jks` een `jwtcert` -alias bevat. Tijdens deze stap, zult u worden ertoe aangezet om het wachtwoord van het bestemmingssleutelarchief te verstrekken dat in de vorige stap werd geproduceerd.

```shell
keytool -keystore keystore.jks -list
```

#### Ondertekend token genereren

Tot slot gebruikt u de Java-klasse JWTExample hieronder om uw ondertekende token te genereren.

```java
package org.example;
 
import org.apache.commons.codec.binary.Base64;
 
import java.io.*;
import java.security.*;
import java.text.MessageFormat;
 
public class Main {
 
    public static void main(String[] args) {
 
        String header = "{\"alg\":\"RS256\"}";
        String claimTemplate = "'{'\"iss\": \"{0}\", \"sub\": \"{1}\", \"aud\": \"{2}\", \"exp\": \"{3}\"'}'";
 
        try {
            StringBuffer token = new StringBuffer();
 
            //Encode the JWT Header and add it to our string to sign
            token.append(Base64.encodeBase64URLSafeString(header.getBytes("UTF-8")));
 
            //Separate with a period
            token.append(".");
 
            //Create the JWT Claims Object
            String[] claimArray = new String[5];
            claimArray[0] = "{CLIENT_ID}";
            claimArray[1] = "{AUTHORIZED_SALESFORCE_USERNAME}";
            claimArray[2] = "{SALESFORCE_LOGIN_URL}";
            claimArray[3] = Long.toString((System.currentTimeMillis() / 1000) + 2629746*4);
            MessageFormat claims;
            claims = new MessageFormat(claimTemplate);
            String payload = claims.format(claimArray);
 
            //Add the encoded claims object
            token.append(Base64.encodeBase64URLSafeString(payload.getBytes("UTF-8")));
 
            //Load the private key from a keystore
            KeyStore keystore = KeyStore.getInstance("JKS");
            keystore.load(new FileInputStream("path/to/keystore"), "keystorepassword".toCharArray());
            PrivateKey privateKey = (PrivateKey) keystore.getKey("jwtcert", "privatekeypassword".toCharArray());
 
            //Sign the JWT Header + "." + JWT Claims Object
            Signature signature = Signature.getInstance("SHA256withRSA");
            signature.initSign(privateKey);
            signature.update(token.toString().getBytes("UTF-8"));
            String signedPayload = Base64.encodeBase64URLSafeString(signature.sign());
 
            //Separate with a period
            token.append(".");
 
            //Add the encoded signature
            token.append(signedPayload);
 
            System.out.println(token.toString());
 
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

| Eigenschap | Configuraties |
| --- | --- |
| `claimArray[0]` | Werk `claimArray[0]` bij met uw client-id. |
| `claimArray[1]` | Werk `claimArray[1]` bij met de [!DNL Salesforce] -gebruikersnaam die op basis van de app is geautoriseerd. |
| `claimArray[2]` | Werk `claimArray[2]` bij met de aanmeldings-URL van [!DNL Salesforce] . |
| `claimArray[3]` | Werk `claimArray[3]` bij met een vervaldatum die in milliseconden sinds de epoche-tijd is opgemaakt. `3660624000000` is bijvoorbeeld 12-31-2085. |
| `/path/to/keystore` | Vervang `/path/to/keystore` door het juiste pad naar het bestand keystore.jks |
| `keystorepassword` | Vervang `keystorepassword` door het wachtwoord voor het doelsleutelarchief. |
| `privatekeypassword` | Vervang `privatekeypassword` door het wachtwoord voor het bronsleutelarchief. |

## Volgende stappen

Nadat u de vereiste configuratie voor uw [!DNL Salesforce] -account hebt voltooid, kunt u doorgaan met het verbinden van uw [!DNL Salesforce] -account met Experience Platform en uw CRM-gegevens invoeren. Lees de documentatie hieronder voor meer informatie:

### Verbinding maken [!DNL Salesforce] met platform met behulp van API&#39;s

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Salesforce] en Platform via API&#39;s of de gebruikersinterface:

- [Een Salesforce-basisverbinding maken met de Flow Service API](../../tutorials/api/create/crm/salesforce.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)

### Verbinding maken [!DNL Salesforce] met platform via de gebruikersinterface

- [Een Salesforce-bronverbinding maken in de gebruikersinterface](../../tutorials/ui/create/crm/salesforce.md)
- [Een gegevensstroom maken voor een CRM-verbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)