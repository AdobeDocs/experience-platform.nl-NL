---
title: Typen gegevenselementen in de Adobe Experience Platform Web SDK Extension
description: Leer over de verschillende types van gegevenselement die door de de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform worden verstrekt.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: fbca8a47c500e89d82cf636e8cb639f2bb59c2e6
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 0%

---


# Gegevenstelelementtypen

Nadat u uw [ actietypes ](action-types.md) in de [ de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension-configuration.md) plaatst, moet u uw types van gegevenselement vormen. Op deze pagina worden de beschikbare gegevenselemetypen beschreven.

## Identiteitskaart {#identity-map}

Met een identiteitsoverzicht kunt u identiteiten instellen voor de bezoeker van uw webpagina. Een identiteitsoverzicht bestaat uit naamruimten zoals `CRMID` , `Phone` of `Email` , waarbij elke naamruimte een of meer id&#39;s bevat. Als de persoon op uw website bijvoorbeeld twee telefoonnummers heeft opgegeven, moet uw naamruimte voor de telefoon twee id&#39;s bevatten.

In het gegevenselement [!UICONTROL Identity map] geeft u de volgende gegevens voor elke id op:

* **[!UICONTROL ID]**: De waarde die de bezoeker identificeert. Bijvoorbeeld, als het herkenningsteken tot de _telefoon_ namespace behoort, kan [!UICONTROL ID] _555-555-5555_ zijn. Deze waarde wordt doorgaans afgeleid van een JavaScript-variabele of een ander stukje gegevens op de pagina. Het is daarom verstandig een gegevenselement te maken dat naar de paginagegevens verwijst en vervolgens te verwijzen naar het gegevenselement in het [!UICONTROL ID] -veld in het [!UICONTROL Identity map] -gegevenselement. Als de id op de pagina wordt uitgevoerd en de id-waarde alleen een gevulde tekenreeks is, wordt de id automatisch verwijderd uit het identiteitsoverzicht.
* **[!UICONTROL Authenticated state]**: een selectie die aangeeft of de bezoeker is geverifieerd.
* **[!UICONTROL Primary]**: Een selectie die aangeeft of de id moet worden gebruikt als primaire id voor de individu. Als er geen id als primair wordt gemarkeerd, wordt de ECID gebruikt als primaire id.

![ beeld UI die het Edit scherm van het Element van Gegevens tonen.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe raadt aan identiteiten die een persoon vertegenwoordigen, zoals `Luma CRM Id` , als primaire identiteit te verzenden.
>
>Als het identiteitsoverzicht de persoon-id bevat (bijvoorbeeld `Luma CRM Id`), wordt de persoon-id de primaire id. Anders wordt `ECID` de primaire identiteit.

Geef geen [!DNL ECID] op wanneer u een identiteitsoverzicht maakt. Wanneer u de SDK gebruikt, wordt automatisch een [!DNL ECID] gegenereerd op de server en opgenomen in het identiteitsoverzicht.

Het element van de identiteitskaartgegevens wordt vaak gebruikt in combinatie met het [[!UICONTROL XDM object] type van gegevenselement ](#xdm-object) en het [[!UICONTROL Set consent] actietype ](action-types.md#set-consent).

Lees meer over [ de Dienst van de Identiteit van Adobe Experience Platform ](../../../../identity-service/home.md).

## XDM-object {#xdm-object}

Het formatteren van uw gegevens aan XDM is gemakkelijker met het XDM objectelement. Wanneer u dit gegevenselement voor het eerst opent, selecteert u de juiste Adobe Experience Platform-sandbox en -schema. Nadat u het schema hebt geselecteerd, ziet u de structuur van uw schema, dat u gemakkelijk kunt invullen.

![ beeld UI die de XDM objecten structuur toont.](assets/XDM-object.png)

Wanneer u bepaalde velden in uw schema opent, zoals `web.webPageDetails.URL` , worden sommige items automatisch verzameld. Hoewel meerdere items automatisch worden verzameld, kunt u indien nodig alle items overschrijven. Alle waarden kunnen handmatig of met andere gegevenselementen worden ingevuld.

>[!NOTE]
>
>Vul alleen de gegevens in die u wilt verzamelen. Alles wat niet is ingevuld, wordt weggelaten wanneer de gegevens naar de oplossingen worden verzonden.

## Variabele {#variable}

U kunt payload-objecten maken met het gegevenselement **[!UICONTROL Variable]** . Zowel [!UICONTROL XDM] - als [!UICONTROL Data] -objecten worden ondersteund.

* Wanneer u [!UICONTROL XDM] selecteert, selecteert u de gewenste [!UICONTROL Sandbox] en [!UICONTROL Schema] .
* Wanneer u [!UICONTROL Data] selecteert, selecteert u de gewenste oplossingen. Beschikbare oplossingen zijn [!UICONTROL Adobe Analytics] en [!UICONTROL Adobe Target] .

![ Beeld van Markeringen UI die de opties van het gegevenselement tonen.](assets/variable-data-element.png)

Nadat u dit gegevenselement creeert, kunt u de [ veranderlijke ](./action-types.md#update-variable) actie van de Update gebruiken om het te wijzigen. Wanneer klaar, kunt u dit gegevenselement in [ omvatten verzendt gebeurtenis ](./action-types.md#send-event) actie om gegevens naar een gegevensstroom te verzenden.

## Media: kwaliteit van ervaring {#quality-experience}

Een **[!UICONTROL Quality of Experience]** -gegevenselement is handig wanneer u streaming media-gebeurtenissen naar Adobe Experience Platform verzendt. U kunt dit element toevoegen tijdens het maken van een mediasessie. De volgende media-gebeurtenissen bevatten bijgewerkte gegevens over de kwaliteit van de ervaring.

![ beeld UI die de Create Kwaliteit van het scherm van het Element van Gegevens van de Ervaring toont.](assets/qoe-data-element.png)

## Volgende stappen {#next-steps}

Leer over specifieke gebruiksgevallen zoals [ die tot ECID ](accessing-the-ecid.md) toegang hebben.
