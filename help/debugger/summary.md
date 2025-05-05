---
title: Tabblad Samenvatting
description: Leer hoe u het tabblad Overzicht in het Adobe Experience Platform Debugger kunt gebruiken.
keywords: foutopsporing;beleving van de extensie Platform Foutopsporing;chroom;extensie;samenvatting;wissen;verzoeken;samenvattingsscherm;oplossing;informatie;analyse;doel;dtm;publieksbeheer;starten;id-service
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---

# Tabblad Samenvatting

Als u Adobe Experience Platform Debugger wilt uitvoeren, opent u de pagina die u wilt controleren in de browser en selecteert u het pictogram (![](images/start-icon.jpg)) op de browserbalk. De uitbreiding opent op het **Samenvatting** lusje.

![](images/summary.jpg)

Dit scherm bevat informatie over elke Adobe Experience Cloud-oplossing. De getoonde informatie varieert per oplossing, maar omvat typisch informatie met inbegrip van de oplossingsbibliotheek en versie (bijvoorbeeld, &quot;AppMeasurement v2.9&quot;) en rekeningsherkenningstekens (zoals de het rapportsuite identiteitskaart van de Analyse, de cliëntcode van het Doel, identiteitskaart van de partner van de Audience Manager, etc.)

## Informatie die wordt weergegeven in Foutopsporing Experience Platform

Foutopsporing van het Experience Platform toont de volgende informatie voor elke oplossing:

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Rapportsuite(s) </p> </td> 
   <td colname="col2"> <p>Een <a href="https://experiencecloud.adobe.com/resources/help/en_US/reference/report_suites_admin.html" format="html" scope="external"> rapportreeks </a> bepaalt volledige, onafhankelijke rapportering op een gekozen website, een reeks websites, of een ondergroep van Web-pagina's </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versie </p> </td> 
   <td colname="col2"> <p>De versie <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=nl-NL" format="html" scope="external"> AppMeasurement </a> die voor de pagina wordt bepaald </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versie bezoeker </p> </td> 
   <td colname="col2"> <p>De versie van de <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=nl-NL" format="html" scope="external"> bezoekersidentiteitskaart </a> bibliotheek. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Paginanaam </p> </td> 
   <td colname="col2"> <p>De <a href="https://experiencecloud.adobe.com/resources/help/en_US/sc/implement/pageName.html" format="html" scope="external"> pageName </a> variabele die naar Analytics wordt verzonden die een gebruikersvriendelijke naam van de plaats bevat. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Modules </p> </td> 
   <td colname="col2"> <p>De door Adobe Analytics geladen modules </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Partner </p> </td> 
   <td colname="col2"> <p>De <a href="https://experiencecloud.adobe.com/resources/help/en_US/aam/r_dil_get_partner.html" format="html" scope="external"> partnernaam </a> voor de instantie van de DIL </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versie </p> </td> 
   <td colname="col2"> <p>Het <a href="https://experiencecloud.adobe.com/resources/help/en_US/aam/r_api_return_versions_dil.html" format="html" scope="external"> versienummer </a> voor de instantie van DIL </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>De <a href="https://experiencecloud.adobe.com/resources/help/en_US/aam/ids-in-aam.html" format="html" scope="external"> unieke gebruikersnaam </a> die aan de instantie DIL is gekoppeld </p> </td> 
  </tr> 
 </tbody> 
</table>

**de Markeringen van Adobe Experience Platform**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Naam </p> </td> 
   <td colname="col2"> <p>De naam van de eigenschap tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=nl-NL" format="https" scope="external"> </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versie </p> </td> 
   <td colname="col2"> <p>De versie van Turbine </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Bouwdatum </p> </td> 
   <td colname="col2"> <p>De tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html?lang=nl-NL" format="https" scope="external"> bibliotheek </a> bouwdatum </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Omgeving </p> </td> 
   <td colname="col2"> <p>De <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=nl-NL" format="https" scope="external"> omgeving </a> die door de tagbibliotheek wordt gebruikt </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Extensies </p> </td> 
   <td colname="col2"> <p>De extensies die op de pagina worden gebruikt </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform Web SDK**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Bibliotheekversie </p> </td> 
   <td colname="col2"> <p>Het aantal van het Web SDK van Adobe Experience Platform <a href="https://experienceleague.adobe.com/docs/experience-platform/web-sdk/extension/web-sdk-ext-release-notes.html" format="html" scope="external"> bibliotheekversie </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Naamruimte</p> </td> 
   <td colname="col2"> <p>De naam die is geïdentificeerd in de extensie</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Eigenschap-id </p> </td> 
   <td colname="col2"> <p>De naam van de eigenschap tag die is opgegeven in de extensie </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Edge-domein </p> </td> 
   <td colname="col2"> <p>Het domein dat de extensie Adobe Experience Platform verzendt en gegevens ontvangt van </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>IMS-organisatie-ID </p> </td> 
   <td colname="col2"> <p>De organisatie waarnaar u de gegevens wilt verzenden bij Adobe, zoals opgegeven in de extensie </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Aanmelding ingeschakeld </p> </td> 
   <td colname="col2"> <p>Geeft aan of logboekregistratie is ingeschakeld voor deze eigenschap</p> </td> 
  </tr> 
 </tbody> 
</table>

**de Dienst van identiteitskaart van Adobe Experience Cloud**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Org ID Experience Cloud </p> </td> 
   <td colname="col2"> <p>Uw <a href="https://experiencecloud.adobe.com/resources/help/en_US/mcvid/" format="https" scope="external"> Organisatie-id </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versie </p> </td> 
   <td colname="col2"> <p>De versie van de <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=nl-NL" format="html" scope="external"> bezoekersidentiteitskaart </a> bibliotheek </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Clientcode </p> </td> 
   <td colname="col2"> <p>Uw doel- <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=nl-NL" format="html" scope="external"> clientcode </a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versie </p> </td> 
   <td colname="col2"> <p>Uw huidige versie <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html?lang=nl-NL" format="html" scope="external"> at.js </a> of mbox.js </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Algemene aanvraagnaam </p> </td> 
   <td colname="col2"> <p><a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html?lang=nl-NL" format="html" scope="external"> globale mbox </a> verwijst naar de enige servervraag die bij de bovenkant van elke Web-pagina in uw implementatie van het Doel wordt gemaakt </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Gebeurtenis bij laden van pagina </p> </td> 
   <td colname="col2"> <p>Het type van <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=nl-NL" format="html" scope="external"> gebeurtenis </a> dat brandt wanneer de pagina laadt </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Naam aanvraag </p> </td> 
   <td colname="col2"> <p>De naam van een verzoek rond een <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html?lang=nl-NL" format="html" scope="external"> plaats </a> op de pagina. Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Naam activiteit </p> </td> 
   <td colname="col2"> <p>De naam van de doelcampagne of -activiteit <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html?lang=nl-NL" format="html" scope="external"> </a> . Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Activiteits-id </p> </td> 
   <td colname="col2"> <p>De id van de doelactiviteit. Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Naam van ervaring </p> </td> 
   <td colname="col2"> <p>De naam van het Doel <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html?lang=nl-NL" format="html" scope="external"> ervaring </a>. Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Ervaring-id </p> </td> 
   <td colname="col2"> <p>De id van de doelervaring. Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Naam voorstel</p> </td> 
   <td colname="col2"> <p>De naam van het Doel <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=nl-NL" format="html" scope="external"> aanbieding </a>. Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Aanbieding-id </p> </td> 
   <td colname="col2"> <p>De id van de Target-aanbieding. Beschikbaar zonder authentificatie slechts als u de het Zuiveren gebeurtenisluisteraar in uw code of markeringsmanager implementeert en de noodzakelijke <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=nl-NL" format="html" scope="external"> reactietokens </a> in het Doel UI aanzet. </p> </td> 
  </tr> 
 </tbody> 
</table>
