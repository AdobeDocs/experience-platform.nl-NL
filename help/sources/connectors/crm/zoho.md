---
keywords: Experience Platform;home;populaire onderwerpen;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Zoho CRM Source Connector - Overzicht
description: Leer hoe u Zoho CRM aan Adobe Experience Platform verbindt gebruikend APIs of het gebruikersinterface.
exl-id: 4a010453-3d09-4a47-b04e-5789ae4af48c
source-git-commit: 0e3fee4d78646b1d1d6730495358b3ced4127f4e
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# [!DNL Zoho CRM]

>[!IMPORTANT]
>
>De bron [!DNL Zoho CRM] wordt eind mei 2025 vervangen. U kunt ook de [[!DNL Data Landing Zone]](../cloud-storage/data-landing-zone.md) -bron gebruiken.

Adobe Experience Platform staat toe dat gegevens uit externe bronnen worden opgenomen en biedt u de mogelijkheid om inkomende gegevens te structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens uit diverse bronnen invoeren, zoals toepassingen voor Adobe, opslag in de cloud, databases en vele andere.

Experience Platform biedt ondersteuning voor het opnemen van gegevens van een CRM-systeem van derden. Tot de ondersteuning voor CRM-providers behoren [!DNL Zoho CRM] .

## IP adres lijst van gewenste personen

Een lijst van IP adressen moet aan een lijst van gewenste personen worden toegevoegd alvorens met bronschakelaars te werken. Het niet toevoegen van uw regio-specifieke IP adressen aan uw lijst van gewenste personen kan tot fouten of niet-prestaties leiden wanneer het gebruiken van bronnen. Zie de ](../../ip-address-allow-list.md) pagina van de lijst van gewenste personen van het 0} IP adres {voor meer informatie.[

## Uw verificatiereferenties ophalen voor [!DNL Zoho CRM]

Voordat u gegevens van uw [!DNL Zoho CRM] -account naar Platform kunt verzenden, moet u eerst uw referenties ophalen om de [!DNL Zoho CRM] -bron te verifiëren. Voer de onderstaande stappen uit om uw client-id, clientgeheim, toegangstoken op te halen en token te vernieuwen.

### Uw toepassing registreren

De eerste stap in het terugwinnen van uw authentificatiegeloofsbrieven moet uw toepassing registreren gebruikend de [[!DNL Zoho CRM]  ontwikkelaarsconsole ](https://accounts.zoho.com/). Om uw toepassing te registreren, moet u uw cliënttype van selecteren: JavaScript, web-based, mobiele, niet browser mobiele toepassingen, of zelf-cliënt. Geef vervolgens waarden op voor de naam van uw toepassing, de URL van uw webpagina en een geautoriseerde omleidings-URI die [!DNL Zoho CRM] kan gebruiken om u om te leiden met een giftetoken.

Een geslaagde registratie retourneert uw client-id en clientgeheim.

### Een autorisatieverzoek maken

Daarna, moet u een [ vergunningsverzoek ](https://www.zoho.com/crm/developer/docs/api/v2/auth-request.html) tot stand brengen gebruikend of een web-based toepassing of een zelf-cliënt. Het vergunningsverzoek keert uw subsidieteken terug, dat beurtelings u toestaat om uw toegangstoken terug te winnen.

Wanneer het creëren van een vergunningsverzoek, moet u waarden voor zowel **werkingsgebied** invullen en **toegangstype**. Verwijs naar dit [[!DNL Zoho CRM]  document ](https://www.zoho.com/crm/developer/docs/api/v2/scopes.html) voor meer informatie over werkingsgebied, terwijl uw **toegangstype** altijd aan `offline` zou moeten worden geplaatst.

### Uw toegangs- en vernieuwingstolken genereren

Zodra u uw subsidieteken hebt teruggewonnen, kunt u uw [ toegang produceren en tokens ](https://www.zoho.com/crm/developer/docs/api/v2/access-refresh.html) verfrissen door een verzoek van de POST aan `{ACCOUNTS_URL}/oauth/v2/token` te doen terwijl het verstrekken van uw cliëntidentiteitskaart, cliëntgeheim, giftetoken, en herleiding URI. Tijdens deze stap moet u `grant_type` ook als parameter opnemen en de waarde als `"authorization_code"` instellen.

Een succesvol verzoek keert uw toegang terug en verfrist tekenen, die u dan kunt gebruiken om voor authentiek te verklaren.

Voor gedetailleerde stappen bij het verwerven van uw geloofsbrieven, zie de [[!DNL Zoho CRM]  authentificatiegids ](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Verbind [!DNL Zoho CRM] met [!DNL Platform] gebruikend APIs

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Zoho CRM] en Platform via API&#39;s of de gebruikersinterface:

- [Creeer a [!DNL Zoho CRM]  basisverbinding gebruikend de Dienst API van de Stroom](../../tutorials/api/create/crm/zoho.md)
- [Gegevenstabellen verkennen met de Flow Service API](../../tutorials/api/explore/tabular.md)
- [Een gegevensstroom maken voor een CRM-bron met behulp van de Flow Service API](../../tutorials/api/collect/crm.md)

## Verbind [!DNL Zoho CRM] met [!DNL Platform] gebruikend UI

- [Creeer a [!DNL Zoho CRM]  bronverbinding in UI](../../tutorials/ui/create/crm/zoho.md)
- [Een gegevensstroom maken voor een CRM-bronverbinding in de gebruikersinterface](../../tutorials/ui/dataflow/crm.md)
