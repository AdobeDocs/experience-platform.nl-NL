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

Nadat u de [actietypen](action-types.md) in de [Adobe Experience Platform Web SDK-tagextensie](web-sdk-extension-configuration.md), moet u uw types van gegevenselement vormen. Op deze pagina worden de beschikbare gegevenselemetypen beschreven.

## Identiteitskaart {#identity-map}

Met een identiteitsoverzicht kunt u identiteiten instellen voor de bezoeker van uw webpagina. Een identiteitsoverzicht bestaat uit naamruimten, zoals `CRMID`, `Phone` of `Email`, met elke naamruimte die een of meer id&#39;s bevat. Als de persoon op uw website bijvoorbeeld twee telefoonnummers heeft opgegeven, moet uw naamruimte voor de telefoon twee id&#39;s bevatten.

In de [!UICONTROL Identity map] data element, zult u de volgende stukken informatie voor elke herkenningsteken verstrekken:

* **[!UICONTROL ID]**: De waarde die de bezoeker identificeert. Als de id bijvoorbeeld tot de _telefoon_ naamruimte, [!UICONTROL ID] kan _555-555-5555_. Deze waarde wordt doorgaans afgeleid van een JavaScript-variabele of een ander stukje gegevens op de pagina. Het is daarom verstandig een gegevenselement te maken dat verwijst naar de paginagegevens en vervolgens verwijst naar het gegevenselement in het dialoogvenster [!UICONTROL ID] in het veld [!UICONTROL Identity map] gegevenselement. Als de id op de pagina wordt uitgevoerd en de id-waarde alleen een gevulde tekenreeks is, wordt de id automatisch verwijderd uit het identiteitsoverzicht.
* **[!UICONTROL Authenticated state]**: Een selectie die aangeeft of de bezoeker is geverifieerd.
* **[!UICONTROL Primary]**: Een selectie die aangeeft of de id moet worden gebruikt als primaire id voor de persoon. Als er geen id als primair wordt gemarkeerd, wordt de ECID gebruikt als primaire id.

![UI-afbeelding die het scherm Gegevenselement bewerken weergeeft.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe beveelt aan identiteiten te verzenden die een persoon vertegenwoordigen, zoals `Luma CRM Id` als primaire identiteit.
>
>Als het identiteitsbewijs de personsidentificatie bevat (bijvoorbeeld `Luma CRM Id`), wordt de persoon-id de primaire id. Anders, `ECID` wordt de primaire identiteit.

U moet geen [!DNL ECID] wanneer u een identiteitsoverzicht maakt. Wanneer u de SDK gebruikt, wordt een [!DNL ECID] wordt automatisch gegenereerd op de server en opgenomen in het identiteitsoverzicht.

Het gegevenselement van de identiteitskaarten wordt vaak gebruikt in combinatie met [[!UICONTROL XDM object] gegevenstype van gegevenselement](#xdm-object) en de [[!UICONTROL Set consent] actietype](action-types.md#set-consent).

Meer informatie over [Adobe Experience Platform Identity Service](../../../../identity-service/home.md).

## XDM-object {#xdm-object}

Het formatteren van uw gegevens aan XDM is gemakkelijker met het XDM objectelement. Wanneer u dit gegevenselement voor het eerst opent, selecteert u de juiste Adobe Experience Platform-sandbox en -schema. Nadat u het schema hebt geselecteerd, ziet u de structuur van uw schema, dat u gemakkelijk kunt invullen.

![UI-afbeelding die de XDM-objectstructuur weergeeft.](assets/XDM-object.png)

Wanneer u bepaalde velden van uw schema opent, zoals `web.webPageDetails.URL`, worden sommige objecten automatisch verzameld. Hoewel meerdere items automatisch worden verzameld, kunt u indien nodig alle items overschrijven. Alle waarden kunnen handmatig of met andere gegevenselementen worden ingevuld.

>[!NOTE]
>
>Vul alleen de gegevens in die u wilt verzamelen. Alles wat niet is ingevuld, wordt weggelaten wanneer de gegevens naar de oplossingen worden verzonden.

## Variabele {#variable}

U kunt payload-objecten maken met de opdracht **[!UICONTROL Variable]** gegevenselement. Beide [!UICONTROL XDM] en [!UICONTROL Data] objecten worden ondersteund.

* Wanneer u [!UICONTROL XDM]selecteert u de gewenste [!UICONTROL Sandbox] en [!UICONTROL Schema].
* Wanneer u [!UICONTROL Data]selecteert u de gewenste oplossingen. Beschikbare oplossingen omvatten [!UICONTROL Adobe Analytics] en [!UICONTROL Adobe Target].

![Afbeelding van de interface Codes waarin de opties voor gegevenselementen worden weergegeven.](assets/variable-data-element.png)

Nadat u dit gegevenselement hebt gemaakt, kunt u de opdracht [Variabele bijwerken](./action-types.md#update-variable) handeling om deze te wijzigen. Indien gereed, kunt u dit gegevenselement opnemen in het dialoogvenster [Gebeurtenis Send](./action-types.md#send-event) handeling om gegevens naar een gegevensstroom te verzenden.

## Media: kwaliteit van ervaring {#quality-experience}

A **[!UICONTROL Quality of Experience]** data element is nuttig wanneer het verzenden van het stromen media gebeurtenissen naar Adobe Experience Platform. U kunt dit element toevoegen tijdens het maken van een mediasessie. De volgende media-gebeurtenissen bevatten bijgewerkte gegevens over de kwaliteit van de ervaring.

![UI-afbeelding met het scherm Create Quality of Experience Data Element.](assets/qoe-data-element.png)

## Volgende stappen {#next-steps}

Meer informatie over specifieke gebruiksgevallen, zoals [toegang krijgen tot ECID](accessing-the-ecid.md).
