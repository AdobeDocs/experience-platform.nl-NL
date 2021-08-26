---
title: Typen gegevenselementen in de Adobe Experience Platform Web SDK-extensie
description: Leer over de verschillende types van gegevenselement die door de de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform worden verstrekt.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 1%

---

# Gegevenstelelementtypen

Nadat u de [actietypen](action-types.md) in [Adobe Experience Platform Web SDK markeringsuitbreiding](web-sdk-extension-configuration.md) plaatst, vorm uw types van gegevenselement.

Op deze pagina worden de beschikbare gegevenselemetypen beschreven.


## Samenvoegings-id gebeurtenis

Dit gegevenselement verstrekt een identiteitskaart van de gebeurtenisfusie wanneer gebruikt. Er is geen configuratie nodig voor dit gegevenselement. Het gegevenselement dat wordt opgegeven, blijft hetzelfde totdat de bezoeker de pagina verlaat of totdat het handelingstype &quot;Id van handeling voor samenvoegen van gebeurtenissen opnieuw instellen&quot; wordt gebruikt.

## Identiteitskaart

Met een identiteitsoverzicht kunt u identiteiten instellen voor de bezoeker van uw webpagina. Een identiteitsoverzicht bestaat uit namespaces, zoals _phone_ of _email_, met elke namespace die één of meerdere herkenningstekens bevatten. Als de persoon op uw website bijvoorbeeld twee telefoonnummers heeft opgegeven, moet uw naamruimte voor de telefoon twee id&#39;s bevatten.

In het [!UICONTROL Identity map] gegevenselement, zult u de volgende stukken informatie voor elk herkenningsteken verstrekken:

* **[!UICONTROL ID]**: De waarde die de bezoeker identificeert. Als de id bijvoorbeeld tot de naamruimte _phone_ behoort, kan [!UICONTROL ID] _555-555-555_ zijn. Deze waarde wordt doorgaans afgeleid van een JavaScript-variabele of een ander stukje gegevens op de pagina. Het is daarom verstandig een gegevenselement te maken dat verwijst naar de paginagegevens en vervolgens te verwijzen naar het gegevenselement in het veld [!UICONTROL ID] in het gegevenselement [!UICONTROL Identity map]. Als de id op de pagina wordt uitgevoerd en de id-waarde alleen een gevulde tekenreeks is, wordt de id automatisch verwijderd uit het identiteitsoverzicht.
* **[!UICONTROL Authenticated state]**: Een selectie die aangeeft of de bezoeker is geverifieerd.
* **[!UICONTROL Primary]**: Een selectie die aangeeft of de id moet worden gebruikt als primaire id voor de persoon. Als er geen id als primair wordt gemarkeerd, wordt de ECID gebruikt als primaire id.

U moet geen ECID opgeven wanneer u een identiteitsoverzicht maakt. Wanneer u de SDK gebruikt, wordt automatisch een ECID gegenereerd op de server en opgenomen in het identiteitsoverzicht.

Het gegevenselement van de identiteitskaartgegevens wordt vaak gebruikt in combinatie met het [[!UICONTROL XDM object] gegevenstype](#xdm-object) en het [[!UICONTROL Set consent] handelingstype](action-types.md#set-consent).

Meer informatie over [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=nl).

![](./assets/identity-map-data-element.png)

## XDM-object {#xdm-object}

Gebruik XDM-indeling om gegevens naar de Adobe Experience Platform Web SDK te verzenden. Het formatteren van uw gegevens is gemakkelijker met het XDM objectelement. Wanneer u dit gegevenselement voor het eerst opent, selecteert u de juiste Adobe Experience Platform-sandbox en -schema. Nadat u het schema hebt geselecteerd, ziet u de structuur van uw schema, dat u gemakkelijk kunt invullen.

![](./assets/XDM-object.png)

Wanneer u bepaalde velden in uw schema opent, zoals `web.webPageDetails.URL`, worden sommige items automatisch verzameld. Hoewel meerdere items automatisch worden verzameld, kunt u indien nodig alle items overschrijven. Alle waarden kunnen handmatig of met andere gegevenselementen worden ingevuld.

>[!NOTE]
>
>Vul alleen de gegevens in die u wilt verzamelen. Alles wat niet is ingevuld, wordt weggelaten wanneer de gegevens naar de oplossingen worden verzonden.
