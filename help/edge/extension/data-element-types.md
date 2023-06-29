---
title: Typen gegevenselementen in de Adobe Experience Platform Web SDK-extensie
description: Leer over de verschillende types van gegevenselement die door de de markeringsuitbreiding van SDK van het Web van Adobe Experience Platform worden verstrekt.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: eef0b50b12b0e3be34ad519f2d106392c23b7d69
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# Gegevenstelelementtypen

Nadat u de [actietypen](action-types.md) in de [Adobe Experience Platform Web SDK-tagextensie](web-sdk-extension-configuration.md), moet u uw types van gegevenselement vormen. Op deze pagina worden de beschikbare gegevenselemetypen beschreven.

## Identiteitskaart {#identity-map}

Met een identiteitsoverzicht kunt u identiteiten instellen voor de bezoeker van uw webpagina. Een identiteitsoverzicht bestaat uit naamruimten, zoals _telefoon_ of _email_, met elke naamruimte die een of meer id&#39;s bevat. Als de persoon op uw website bijvoorbeeld twee telefoonnummers heeft opgegeven, moet uw naamruimte voor de telefoon twee id&#39;s bevatten.

In de [!UICONTROL Identity map] data element, zult u de volgende stukken informatie voor elke herkenningsteken verstrekken:

* **[!UICONTROL ID]**: De waarde die de bezoeker identificeert. Als de id bijvoorbeeld tot de _telefoon_ naamruimte, de [!UICONTROL ID] kan _555-555-5555_. Deze waarde wordt doorgaans afgeleid van een JavaScript-variabele of een ander stukje gegevens op de pagina. Het is daarom verstandig een gegevenselement te maken dat verwijst naar de paginagegevens en vervolgens verwijst naar het gegevenselement in de [!UICONTROL ID] in het veld [!UICONTROL Identity map] gegevenselement. Als de id op de pagina wordt uitgevoerd en de id-waarde alleen een gevulde tekenreeks is, wordt de id automatisch verwijderd uit het identiteitsoverzicht.
* **[!UICONTROL Authenticated state]**: Een selectie die aangeeft of de bezoeker is geverifieerd.
* **[!UICONTROL Primary]**: Een selectie die aangeeft of de id moet worden gebruikt als primaire id voor de persoon. Als er geen id als primair wordt gemarkeerd, wordt de ECID gebruikt als primaire id.

![UI-afbeelding die het scherm Gegevenselement bewerken weergeeft.](./assets/identity-map-data-element.png)

U moet geen [!DNL ECID] wanneer u een identiteitsoverzicht maakt. Wanneer u de SDK gebruikt, wordt een [!DNL ECID] wordt automatisch gegenereerd op de server en opgenomen in het identiteitsoverzicht.

Het gegevenselement van de identiteitskaarten wordt vaak gebruikt in combinatie met [[!UICONTROL XDM object] type gegevenselement](#xdm-object) en de [[!UICONTROL Set consent] actietype](action-types.md#set-consent).

Meer informatie over [Adobe Experience Platform Identity Service](../../identity-service/home.md).

## XDM-object {#xdm-object}

Het formatteren van uw gegevens aan XDM is gemakkelijker met het XDM objectelement. Wanneer u dit gegevenselement voor het eerst opent, selecteert u de juiste Adobe Experience Platform-sandbox en -schema. Nadat u het schema hebt geselecteerd, ziet u de structuur van uw schema, dat u gemakkelijk kunt invullen.

![UI-afbeelding die de XDM-objectstructuur weergeeft.](assets/XDM-object.png)

Wanneer u bepaalde velden van uw schema opent, zoals `web.webPageDetails.URL`, worden sommige objecten automatisch verzameld. Hoewel meerdere items automatisch worden verzameld, kunt u indien nodig alle items overschrijven. Alle waarden kunnen handmatig of met andere gegevenselementen worden ingevuld.

>[!NOTE]
>
>Vul alleen de gegevens in die u wilt verzamelen. Alles wat niet is ingevuld, wordt weggelaten wanneer de gegevens naar de oplossingen worden verzonden.

## Variabele {#variable}

Een andere manier om XDM-objecten te maken, is het gebruik van de **[!UICONTROL Variable]** gegevenselement. Terwijl het XDM-objectelement wordt gemaakt wanneer ernaar wordt verwezen, bijvoorbeeld binnen een `sendEvent` de **[!UICONTROL Variable]** gegevenselement kan worden bijgewerkt via [!UICONTROL Update variable] handelingen. Als u het gegevenselement wilt gebruiken, selecteert u de juiste Adobe Experience Platform-sandbox en -schema.

![UI-afbeelding die het scherm Gegevenselement maken weergeeft.](assets/variable-data-element.png)

Zodra u dit gegevenselement hebt gecreeerd kunt u gebruiken [Variabele bijwerken](./action-types.md#update-variable) handelingen om het gegevenselement te wijzigen. Gebruik vervolgens binnen de send-gebeurtenisacties het element met variabele gegevens voor de XDM-optie.

## Volgende stappen {#next-steps}

Meer informatie over specifieke gebruiksgevallen, zoals [toegang krijgen tot ECID](accessing-the-ecid.md).
