---
keywords: Experience Platform;thuis;populaire onderwerpen;identiteitsservice;Identiteitsservice;gedeelde apparaten;Gedeelde apparaten
title: Overzicht van gedeelde apparaten (Beta)
description: De gedeelde Detectie van het Apparaat identificeert verschillende voor authentiek verklaarde gebruikers van het zelfde apparaat, die voor een nauwkeurigere vertegenwoordiging van klantengegevens in identiteitsgrafieken toestaan
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: d7c7bed74d746aba2330ecba62f9f810fbaf0d63
workflow-type: tm+mt
source-wordcount: '1328'
ht-degree: 0%

---

# Overzicht van gedeelde apparaatdetectie (Beta)

>[!IMPORTANT]
>
>De functie [!DNL Shared Device Detection] is in bèta. De kenmerken en documentatie van het programma kunnen worden gewijzigd.

Met Adobe Experience Platform [!DNL Identity Service] kunt u uw klanten en hun gedrag beter laten zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

[!DNL Shared Device] verwijst naar apparaten die door meerdere personen worden gebruikt. Voorbeelden van een gedeeld apparaat zijn tablets, bibliotheekcomputers en kiosken. Met de functie [!DNL Shared Device Detection] kunnen verschillende gebruikers van hetzelfde apparaat niet worden samengevoegd tot één identiteit, waardoor een individu nauwkeuriger kan worden weergegeven.

Met [!DNL Shared Device Detection] kunt u:

* Maak afzonderlijke identiteitsgrafieken voor verschillende gebruikers van hetzelfde apparaat;
* voorkomen dat gegevens van verschillende personen met hetzelfde apparaat worden gemengd;
* Een schonere en nauwkeurigere weergave van uw klanten maken.

>[!TIP]
>
>Configuraties voor [!DNL Shared Device Detection] moeten worden voltooid voordat u Profiel voor gegevensset inschakelt, omdat u de instellingen niet meer kunt wijzigen wanneer grafieken worden gegenereerd in [!DNL Identity Service] .

## Aan de slag met [!DNL Shared Device Detection]

Als u met [!DNL Shared Device Detection] werkt, moet u de verschillende platformservices begrijpen. Voordat u begint te werken met [!DNL Shared Device Detection] , raadpleegt u de documentatie voor de volgende services:

* [[!DNL Identity Service]](./home.md): verbeter een beter beeld van individuele klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen.
   * [ de grafiekkijker van de Identiteit ](./features/identity-graph-viewer.md): visualiseer en in wisselwerking met de kijker van de identiteitsgrafiek om beter te begrijpen hoe de klantenidentiteiten samen worden vastgezet, en op welke manieren.
   * [ Identiteit namespaces ](./features/namespaces.md): Zie de componenten van een volledig gekwalificeerde identiteit, en hoe de identiteit namespaces u toestaat om de context en het type van een identiteit te onderscheiden.

## [!DNL Shared Device Detection] begrijpen

Het is belangrijk de volgende terminologie te begrijpen wanneer het werken met
[!DNL Shared Device Detection]. Zie de tabel hieronder voor een lijst met termen die essentieel zijn voor een goed begrip van [!DNL Shared Device Detection] .

### Terminologie

| Voorwaarden | Definitie |
| --- | --- |
| Gedeeld apparaat | Een gedeeld apparaat is elk apparaat dat door meerdere personen wordt gebruikt. Voorbeelden van gedeelde apparaten zijn tablets, bibliotheekcomputers en kiosken. |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] verwijst naar een configuratie-instelling waarmee gegevens van verschillende gebruikers van hetzelfde apparaat van elkaar kunnen worden gescheiden. |
| Naamruimte van gedeelde identiteit | De naamruimte Gedeelde identiteit vertegenwoordigt het apparaat dat door meerdere gebruikers kan worden gebruikt. De naamruimte Gedeelde identiteit is doorgaans de ECID, maar kan ook worden ingesteld op andere apparaat-id&#39;s. |
| Naamruimte gebruikersnaam gebruiker | De naamruimte van de Identiteit van de Gebruiker vertegenwoordigt de geverifieerde (het programma geopende) gebruiker van een gedeeld apparaat. |
| Laatst geverifieerde gebruiker | De laatste voor authentiek verklaarde gebruiker vertegenwoordigt de gebruiker die het laatst aan een apparaat het programma werd geopend, als een apparaat door veelvoudige rekeningen wordt het programma geopend. |

{style="table-layout:auto"}

[!DNL Shared Device Detection] werkt door twee namespaces te vestigen: **Gedeelde Namespace van de Identiteit** en **Namespace van de Identiteit van de Gebruiker**.

* De naamruimte Gedeelde identiteit vertegenwoordigt het apparaat dat door meerdere gebruikers kan worden gebruikt. Adobe raadt klanten aan ECID te gebruiken als de gedeelde apparaat-id.
* De naamruimte voor de gebruikersnaam wordt toegewezen aan de naamruimte voor de identiteit die overeenkomt met de aanmeldings-id van een gebruiker. Dit kan de CRM-id, het e-mailadres, de gehashte e-mail of het telefoonnummer van de gebruiker zijn.

Een gedeeld apparaat, als een tablet, heeft één enkele **Gedeelde Namespace van de Identiteit**. Anderzijds, heeft elke gebruiker van een gedeeld apparaat hun eigen aangewezen **Namespace van de Identiteit van de Gebruiker** die met hun respectieve login IDs beantwoordt. Een tablet die Kevin en Nora bijvoorbeeld delen voor e-commerce gebruik heeft een eigen ECID van `1234`, terwijl Kevin zijn eigen naamruimte voor de gebruikersnaam heeft die is toegewezen aan zijn `kevin@email.com` -account en Nora haar eigen naamruimte voor de gebruikersnaam heeft toegewezen aan haar `nora@email.com` -account.

[!DNL Shared Device Detection] kan onderscheid maken tussen verschillende gebruikers van hetzelfde apparaat door de naamruimte voor gedeelde identiteit te koppelen (bijvoorbeeld ECID) met de gebruikersnaam die als laatste is geverifieerd (aanmeldings-id).

### Hoe identiteitsgegevens naar een identiteitsgrafiek worden verzonden

Neem het volgende voorbeeld om u te helpen begrijpen hoe [!DNL Shared Device Detection] werkt:

>[!NOTE]
>
>In dit diagram, wordt de Gedeelde Namespace van de Identiteit gevormd aan ECID en de Namespace van de Identiteit van de Gebruiker wordt gevormd aan identiteitskaart CRM

![ diagram ](./images/shared-device/diagram.png)

* Kevin en Nora delen een tablet om een e-commercewebsite te bezoeken. Ze beschikken echter allebei over hun eigen onafhankelijke accounts waarmee ze online kunnen bladeren en winkelen.
   * Als gedeeld apparaat heeft de tablet een bijbehorende ECID, die de webbrowser cookie-id van de tablet vertegenwoordigt;
* Veronderstel dat Kevin de tablet en **login** aan zijn e-commercerekening gebruikt om voor hoofdtelefoons te doorbladeren, betekent dit dan dat identiteitskaart van CRM van Kevin (**Identiteitskaart Namespace van de Gebruiker**) nu met ECID van de tablet (**Gedeelde Identiteitskaart Namespace**) wordt verbonden. De browsergegevens van het tablet zijn nu opgenomen in Kevin&#39;s identiteitsgrafiek.
   * Als Kevin **zich** afmeldt en Nora de tablet en **login** aan haar eigen rekening gebruikt en een camera koopt, dan is haar identiteitskaart van CRM nu verbonden met ECID van de tablet. De browsergegevens van de tablet zijn daarom opgenomen in de identiteitsgrafiek van Nora.
   * Als Nora **niet logout** en Kevin het tablet gebruikt, maar **login niet**, dan zijn de het doorbladeren van de tablet gegevens nog opgenomen met Nora, omdat zij als voor authentiek verklaarde gebruiker blijft en haar identiteitskaart van CRM is nog verbonden met ECID van de tablet.
   * Als Nora **logout** en Kevin het tablet gebruikt, maar **login niet**, dan zijn de het doorbladeren van de tablet gegevens nog opgenomen met de identiteitsgrafiek van Nora, omdat als **laatst voor authentiek verklaarde gebruiker**, haar identiteitskaart van CRM verbonden met ECID van de tablet blijft.
   * Als Kevin **opnieuw** het programma opent, dan wordt zijn identiteitskaart van CRM nu verbonden met ECID van de tablet, omdat hij nu de laatste voor authentiek verklaarde gebruiker is en de het doorbladeren gegevens van de tablet nu met zijn identiteitsgrafiek worden opgenomen.

### Hoe [!DNL Profile Service] profielfragmenten samenvoegt met [!DNL Shared Device Detection] ingeschakeld

[!DNL Profile Service] neemt nota van profielfragmenten en samengevoegde profielen. Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Wanneer [!DNL Shared Device Detection] is ingeschakeld, definieert [!DNL Profile] de primaire identiteit van het profielfragment op basis van het feit of de ervaringsgebeurtenis is geverifieerd of niet-geverifieerd

Een **voor authentiek verklaarde ervaringsgebeurtenis** is een actie die door een gebruiker wordt voltooid terwijl het programma geopend aan een apparaat. Voor voor authentiek verklaarde ervaringsgebeurtenissen, is de primaire identiteit de **Namespace van de Identiteit van de Gebruiker** (Login identiteitskaart). Een **niet voor authentiek verklaarde ervaringsgebeurtenis** is een actie die door een gebruiker wordt voltooid die niet het programma wordt geopend aan een apparaat. Voor ongeautoriseerde ervaringsgebeurtenissen, is de primaire identiteit **Gedeelde Namespace van de Identiteit** (ECID).

Voor meer informatie, zie het [[!DNL Real-Time Customer Profile]  overzicht ](../profile/home.md).

## Gebruikersinterface voor gedeelde apparaten

Selecteer in de gebruikersinterface van het platform de optie **[!UICONTROL Identities]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Identity settings]** .

![ identiteit-dashboard ](./images/shared-device/identity-dashboard.png)

De pagina [!UICONTROL Shared device settings] wordt weergegeven en biedt u een interface voor het configureren van gedeelde apparaatinstellingen voor uw gegevens. De instellingen voor gedeelde apparaten worden standaard uitgeschakeld.

Wanneer gedeelde apparaatinstellingen zijn ingeschakeld, kunnen gegevens van verschillende gebruikers van hetzelfde apparaat van elkaar worden gescheiden. Met deze configuratie-instelling kunt u identiteitsgrafieken helderder en nauwkeuriger weergeven, waarbij de gebruikersidentiteiten van hetzelfde apparaat niet met elkaar worden gecombineerd.

Selecteer **[!UICONTROL Enable]** om de instellingen van uw gedeelde apparaat te wijzigen.

![ toelaten-gedeeld-apparaat ](./images/shared-device/enable-shared-device.png)

De configuratieopties [!UICONTROL Shared Identity Namespace] en [!UICONTROL User Identity Namespace] worden weergegeven, zodat u de naamruimten kunt wijzigen die u wilt gebruiken.

![ reeks-namespaces ](./images/shared-device/set-namespaces.png)

[!UICONTROL Shared Identity Namespace] vertegenwoordigt één apparaat dat door veelvoudige verschillende gebruikers wordt gebruikt. Deze naamruimte is altijd ingesteld op **[!UICONTROL ECID]** omdat alle platformgebruikers **[!UICONTROL ECID]** gebruiken als de id van de webbrowser.

![ delen-identiteit-namespace ](./images/shared-device/shared-identity-namespace.png)

Met [!UICONTROL User Identity Namespace] kunt u verschillende gebruikers van hetzelfde apparaat identificeren en voorkomen dat gegevens in dezelfde identiteitsgrafiek worden gecombineerd.

![ gebruiker-identity-namespace ](./images/shared-device/user-identity-namespace.png)

Selecteer de zoekbalk van **[!UICONTROL User Identity Namespace]** en voer een naamruimte voor identiteit in of selecteer een naamruimte voor identiteit in het vervolgkeuzemenu.

>[!TIP]
>
>De [!UICONTROL User Identity Namespace] moet worden toegewezen aan de naamruimte identity die overeenkomt met de aanmeldings-id van de eindgebruiker. U kunt onder andere de volgende opties kiezen: klant-id, e-mail en gehashte e-mail.

![ e-mails ](./images/shared-device/emails.png)

Selecteer **[!UICONTROL Save]** nadat u de [!UICONTROL Shared Device Settings] -configuratie hebt geconfigureerd.

![ sparen ](./images/shared-device/save.png)

Er verschijnt een pop-upvenster waarin u wordt gevraagd uw selectie te bevestigen. Selecteer **[!UICONTROL Yes]** om de configuratie-instelling te voltooien.

![ bevestig ](./images/shared-device/confirm.png)
