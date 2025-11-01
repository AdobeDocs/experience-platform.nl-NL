---
title: Bronfoutberichten
description: Leer over de foutenmeldingen die u wanneer het gebruiken van de Dienst van de Stroom voor bronnen kunt ontmoeten.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '3057'
ht-degree: 0%

---

# Bronfoutberichten

Dit document bevat een catalogus met foutberichten, beschrijvingen en voorgestelde resoluties voor bronnen.

## Algemene fouten

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1000-400` | Ongeldig verzoek | De aanvraag is ongeldig. Controleer de aanvraag en probeer het opnieuw. |
| `1001-401` | Ongeautoriseerd | De gebruiker is niet geautoriseerd. Neem contact op met uw beheerder om toegang te krijgen tot de bron. |
| `1002-403` | Verboden | De gewenste bewerking is niet toegestaan. Controleer de gewenste bewerking en probeer het opnieuw. |
| `1003-404` | Bron niet gevonden | De gevraagde bron is niet gevonden. Controleer het opgegeven verzoek en probeer het opnieuw. |
| `1004-415` | Niet-ondersteund mediatype | De opgegeven payload-indeling wordt niet ondersteund. Controleer uw opgegeven aanvraag en probeer het opnieuw. |
| `1005-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1006-408` | Tijdslimiet aanvraag | Er is een fout opgetreden tijdens het verwerken van de aanvraag. Er is een time-out opgetreden voor het verzoek. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1007-400` | Ongeldige headerparameter | Een ongeldige headerparameter: `{headerName}` is ontvangen. Controleer de headerparameters en probeer het opnieuw. |
| `1008-401` | Ongeldig machtigingstoken | De machtigingstoken heeft geen toegang tot deze organisatie of de organisatie bestaat niet. Controleer of de organisatie bestaat of neem contact op met uw beheerder voor toegang. |
| `1009-403` | IMS org-id ontbreekt of is leeg | De aanvraagheader van de organisatie-id ontbreekt of is leeg. Werk de koptekstwaarde bij en probeer het opnieuw. |
| `1010-500` | Ongeldig gedetailleerd bericht | De parameter in het gedetailleerde bericht is niet correct verstrekt. Controleer de parameter in het gedetailleerde bericht en probeer het opnieuw. |
| `1011-503` | Service niet beschikbaar | De service is tijdelijk niet beschikbaar. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1012-504` | Time-out gateway | Er is een time-out opgetreden bij de gateway. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1013-412` | Voorwaarde is mislukt | Aan de voorwaarde die wordt gedefinieerd door de headers if-Unmodified-Since of if-None-Match is niet voldaan. Controleer dit en probeer het opnieuw. |
| `1014-400` | Ongeldig argument voor verzoek | Het verzoek kan niet worden verwerkt. {detailedMessage} |

## Framework-fouten

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1100-400` | Ongeldig verzoek | Het verzoek kan niet worden verwerkt. {detailedMessage} |
| `1101-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1102-404` | Bron niet gevonden | De gevraagde bron is niet gevonden. {detailedMessage} |
| `1103-503` | Service niet beschikbaar | De service is tijdelijk niet beschikbaar. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1104-504` | Time-out gateway | Er is een time-out opgetreden bij de gateway. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1105-401` | Ongeautoriseerd | De gebruiker is niet geautoriseerd. {detailedMessage} |
| `1106-403` | Verboden | De gewenste bewerking is niet toegestaan. {detailedMessage} |
| `1107-412` | Voorwaarde is mislukt | Aan de voorwaarde die wordt gedefinieerd door de headers if-Unmodified-Since of if-None-Match is niet voldaan. `{detailedMessage}` |

## Coderingsfouten

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1200-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1201-400` | Ongeldig verzoek | De flowId mag niet null of leeg zijn. Geef een geldige flowId op in aanvraag en probeer het opnieuw. |
| `1202-400` | Ongeldig verzoek | publicKeyId mist in de transformaties van de stroom= {transformations}. Geef een publicKeyId op in het verzoek en probeer het opnieuw. |
| `1203-400` | Ongeldig verzoek | De encryptiesleutel bestaat niet tegen keyID= {keyID} in de transformations= van de stroom {transformations}. Controleer de opgegeven keyID en probeer het opnieuw. |
| `1204-400` | Ongeldig verzoek | Het opgegeven versleutelingsalgoritme is ongeldig. Geef een geldig versleutelingsalgoritme op en probeer het opnieuw. |
| `1205-400` | Ongeldig verzoek | Passphrase ontbreekt in de paramesectie in het verstrekte verzoek. Geef passPhrase op in params en probeer het opnieuw. |

## REST API-fouten

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1300-400` | Ongeldig verzoek | De aanvraag voor een patchverbinding wordt niet ondersteund voor {connectorType} -connector. Controleer het opgegeven verzoek en probeer het opnieuw. |
| `1301-400` | Ongeldig verzoek | De opgegeven parameter authSpecType: {authSpecType} wordt niet ondersteund. Geef een geldig auteur-specificatietype op en probeer het opnieuw. |
| `1302-400` | Ongeldig verzoek | Het verstrekte authentificatietype = {authType} wordt niet gesteund voor connector= {connectorType}. Gelieve te verstrekken een geldig autentype voor de bepaalde schakelaar. |
| `1303-400` | Ongeldig verzoek | De URL kan niet met de opgegeven parameter auth worden gecodeerd omdat URL-codering niet wordt ondersteund voor {value} . Controleer de auteparams en probeer het opnieuw. |
| `1304-400` | Ongeldig verzoek | Het verplichte veld {field} wordt niet opgegeven. Geef {field} op en probeer het opnieuw. |
| `1305-400` | Ongeldig verzoek | Het opgegeven connectortype = {connectorType} wordt niet ondersteund voor deze bewerking. |
| `1306-400` | Ongeldig verzoek | De doelverbinding kan niet null zijn tijdens het valideren van de specificatie-id van de doelverbinding. Controleer het opgegeven verzoek en probeer het opnieuw. |
| `1307-400` | Ongeldig verzoek | The target connection spec ID is not valid={targetConnectionSpecId}. De toegestane waarde is: `c604ff05-7f1a-43c0-8e18-33bf874cb11c` . |
| `1308-400` | Ongeldig verzoek | Het verzoek kan niet worden verwerkt. Foutbericht: {msftErrorMessage} |
| `1309-400` | Ongeldig verzoek | De opgegeven coderingstransformatie is ongeldig omdat {requiredParam} ontbreekt in de params. Geef {requiredParam} op en probeer het opnieuw. |
| `1310-400` | Ongeldig verzoek | De verstrekte publicKeyId in de params is verlopen. Geef een geldige publicKeyId op en probeer het opnieuw. |
| `1311-400` | Ongeldig verzoek | De publicKeyId in params is ongeldig. Geef een geldige publicKeyId op en probeer het opnieuw. |
| 1312-400 | Ongeldig verzoek | De verstrekte parameterwaarde {paramValue} is geen geldige input voor property= {requestParam}. Geef een geldige parameterwaarde op en probeer het opnieuw. |
| `1313-400` | Ongeldig verzoek | Het padkenmerk {attribute} bestaat niet. Controleer of het kenmerk bestaat en probeer het opnieuw. |
| `1314-400` | Ongeldig verzoek | Er is een complex pad opgegeven, maar dit is niet toegestaan. Controleer of er geen complex pad is opgegeven en probeer het opnieuw. |
| `1315-400` | Ongeldig verzoek | Het opgegeven pad {path} moet verwijzen naar een array met records. Controleer of het opgegeven pad naar de array met records verwijst en probeer het opnieuw. |
| `1316-400` | Ongeldig verzoek | De opgegeven pagineringsparams mogen niet leeg zijn. Geef geldige paginaparams op en probeer het opnieuw. |
| `1317-400` | Ongeldig verzoek | De opgegeven planningsparams zijn leeg, maar mogen niet leeg zijn. Geef geldige planningsparameters op en probeer het opnieuw. |
| `1318-400` | Ongeldig verzoek | {combinedMessage}. Controleer het opgegeven verzoek en probeer het opnieuw. |
| `1319-400` | Ongeldig verzoek | De {param} moet onderdeel zijn van een bovenliggende verzameling. Geef {param} op in de bovenliggende verzameling en probeer het opnieuw. |
| `1320-400` | Ongeldig verzoek | De waarde {idType} mag niet null of leeg zijn. Geef een geldige waarde op {idType} en probeer het opnieuw. |
| `1321-400` | Ongeldig verzoek | De lengte van {idType} moet één zijn, opgegeven grootte is {size} . Geef een geldige grootte op en probeer het opnieuw. |
| `1322-400` | Ongeldig verzoek | De bronverbinding kan niet ongeldig zijn voor de bouw van schemaref. Geef een geldige bronverbinding op en probeer het opnieuw. |
| `1323-400` | Ongeldig verzoek | De waarde {entity} mag niet null of leeg zijn in de bronverbinding: {sourceConnection} . Geef een geldige waarde op {entity} en probeer het opnieuw. |
| `1324-400` | Ongeldig verzoek | De doelverbinding kan niet ongeldig zijn wanneer het halen van dataset ID. Geef een geldige doelverbinding op en probeer het opnieuw. |
| `1325-400` | Ongeldig verzoek | De parameter dataSetId mag niet null of leeg zijn in de doelverbinding: {TargetConnection} . Geef een geldige param voor de gegevenssetId op en probeer het opnieuw. |
| `1326-400` | Ongeldig verzoek | De bronverbinding kan niet null zijn bij het ophalen van de bronindeling. Geef een geldige bronverbinding op en probeer het opnieuw. |
| `1327-400` | Ongeldig verzoek | Het formaat van geleverde brongegevens= {sourceFormat} in SourceConnection wordt niet gesteund. De toegestane waarden zijn: {values} . Geef toegestane waarden op en probeer het opnieuw. |
| `1328-400` | Ongeldig verzoek | De toewijzingstransformatie kan niet null zijn bij het extraheren van {param} . Geef een geldige transformatie voor toewijzing op en probeer het opnieuw. |
| `1329-400` | Ongeldig verzoek | De parameter: {param} mag niet null of leeg zijn in de opgegeven aanvraag. Geef een geldige waarde op {param} en probeer het opnieuw. |
| `1330-400` | Ongeldig verzoek | Er zijn geen kolommen gevonden voor tabel {tableName}. Geef een geldige tabelnaam op en probeer het opnieuw. |
| `1331-400` | Ongeldig verzoek | Kolomscheidingsteken mag niet meer dan één teken in SourceConnection zijn: {sourceConnection} . Geef een geldig scheidingsteken voor de kolom op en probeer het opnieuw. |
| `1332-400` | Ongeldig verzoek | De bronverbindingsaanvraag met connectionSpecId: {connectionSpecId} kan geen baseConnectionId hebben. Verwijder de baseConnectionId en probeer het opnieuw. |
| `1333-400` | Onjuiste aanvragen | flowRunAction= {flowRunAction} wordt niet gesteund voor bron met spec id= {specId}. Voer een geldige handeling voor het uitvoeren van de flow in en probeer het opnieuw. |
| `1334-400` | Ongeldig verzoek | De query-parameter : {param} mag niet leeg zijn. Geef een geldige waarde op {param} en probeer het opnieuw. |
| `1335-400` | Ongeldig verzoek | Er is een fout opgetreden tijdens het serialiseren van de filterparams voor verkennen. Controleer de parameteraanvraag voor het filter en probeer het opnieuw. |
| `1336-400` | Ongeldig verzoek | Verken van verbinding wordt niet ondersteund voor verbindings-ID: {connectionSpecId}. Geef de ondersteunde verbindingsspecificatie-id op en probeer het opnieuw. |
| `1337-400` | Ongeldig verzoek | {QueryParam} kan niet leeg zijn voor objectType= {objectType}. Geef een geldige waarde op {QueryParam} en probeer het opnieuw. |
| `1338-400` | Ongeldig verzoek | De {connectionType} -verbindings-id mag niet null zijn in flowRequest. Geef een geldige {connectionType} verbinding-id op in flowRequest. |
| `1339-400` | Ongeldig verzoek | Het formaat van organisatie= {imsOrg} die in het verzoek wordt verstrekt is ongeldig. Geef een geldige organisatie-id op en probeer het opnieuw. |
| `1340-400` | Ongeldig verzoek | Er is een fout opgetreden tijdens het parseren van {time} . Controleer de tijdnotatie in de aanvraag en probeer het opnieuw. |
| `1341-400` | Ongeldig verzoek | De geleverde ODI Json is leeg. Geef geldige ODI Json op en probeer het opnieuw. |
| `1342-400` | Ongeldig verzoek | Het segment &#39;dls :folder&#39; in &#39;odi.json&#39; bevat geen definities. Geef de juiste definities op in &#39;odi.json&#39; en probeer het opnieuw. |
| `1343-400` | Ongeldig verzoek | De segmenten &#39;dls :entityReferences&#39; en &#39;dls :partitionSpec&#39; in &#39;odi.json&#39; ontbreken beide in definities. Geef de juiste definities op in &#39;odi.json&#39; en probeer het opnieuw. |
| `1344-400` | Ongeldig verzoek | De definitie voor &#39;dls :partitionSpec&#39; in &#39;odi.json&#39; is ongeldig omdat er meer dan één partitieSpecs zijn gevonden. Geef de juiste definities op in &#39;odi.json&#39; en probeer het opnieuw. |
| `1345-400` | Ongeldig verzoek | De definities ontbreken in 1 of meer segmenten in wegen: &quot;dls :partitionSpec/dls :fileFormat&#39;, &quot;dls :partitionSpec/dls :partitionTemplate&#39;, &quot;dls :partitionSpec/dls :fileFormat/@type&#39;, &quot;dls :partitionSpec/dls :fileFormat/dls :csvDelimiters&quot;in &quot;odi.json&quot;. Geef de juiste definities op in &#39;odi.json&#39; en probeer het opnieuw. |
| `1346-400` | Ongeldig verzoek | De definitie &#39;@type&#39; in &#39;dls :fileFormat&#39; in &#39;odi.json&#39; is ongeldig. Geef de juiste definities op in &#39;odi.json&#39; en probeer het opnieuw. |
| `1347-400` | Ongeldig verzoek | De definitie dls :csvDelimiters&#39; in &#39;odi.json&#39; wordt niet ondersteund. De gesteunde csvDelimiters zijn: [&#39;, ]. Geef de juiste definities op in &#39;odi.json&#39; en probeer het opnieuw. |
| `1348-400` | Ongeldig verzoek | Er is een fout opgetreden bij het deserialiseren van &#39;dls :entityReferences&#39;. Controleer of de gegevens een geldige indeling hebben en probeer het opnieuw. |
| `1349-400` | Ongeldig verzoek | De opgegeven filterparams zijn ongeldig. Geef geldige filterparams op en probeer het opnieuw. |
| `1350-400` | Ongeldig verzoek | Er is geen operator opgegeven voor filter aan de bron. Geef een geldige filteraanvraag op met de juiste operator en probeer het opnieuw. |
| `1351-400` | Ongeldig verzoek | De opgegeven operator {operator} wordt niet ondersteund voor filter aan de bron voor deze connector. Geef een geldige operator op en probeer het opnieuw. |
| `1352-400` | Ongeldig verzoek | De opgegeven operator {operator} kan niet worden toegewezen aan een ondersteunde native operator voor {ql} . Geef een geldige operator op en probeer het opnieuw. |
| `1353-400` | Ongeldig verzoek | Het filter aan de bron wordt nog niet ondersteund voor {connectorType} -connector. Raadpleeg de ondersteunde connectors in de documentatie: https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=nl-NL. |
| `1354-400` | Ongeldig verzoek | De querytaal {ql} wordt nog niet ondersteund voor filter aan de bron. Geef een geldige querytaal op en probeer het opnieuw. |
| `1355-400` | Ongeldig verzoek | Het opgegeven filtertype is ongeldig. Het ondersteunde filtertype is: PQL. Geef een geldig filtertype op en probeer het opnieuw. |
| `1356-400` | Ongeldig verzoek | De opgegeven filterindeling is ongeldig. De ondersteunde filterindeling is: pql/json. Geef een geldige filterindeling op en probeer het opnieuw. |
| `1357-400` | Ongeldig verzoek | Het opgegeven filter is ongeldig. De waarde moet met gedetailleerde filters worden verstrekt. Geef een geldig filter op en probeer het opnieuw. |
| `1358-400` | Ongeldig verzoek | De opgegeven parameter &#39;objectType&#39; is ongeldig. Geef een geldig objecttype op en probeer het opnieuw. |
| `1359-400` | Ongeldig verzoek | De parameter {param} ontbreekt in de aanvraag. Geef een geldige waarde op {param} en probeer het opnieuw. |
| `1360-400` | Ongeldig verzoek | De begintijd kan niet in het verleden worden ingesteld. Geef een geldige begintijd op en probeer het opnieuw. |
| `1361-400` | Ongeldig verzoek | Interval is niet toegestaan bij eenmalig gebruik. Verwijder het interval of wijzig de frequentie en probeer het opnieuw. |
| `1362-400` | Ongeldig verzoek | Interval mag niet kleiner zijn dan {minInterval} . Geef een geldige intervalwaarde op en probeer het opnieuw. |
| `1363-400` | Ongeldig verzoek | Interval {interval} is niet toegestaan met frequentie: {frequency} . Geef een geldige intervalwaarde op en probeer het opnieuw. |
| `1364-400` | Ongeldig verzoek | De backfill-markering is niet toegestaan wanneer de frequentie is ingesteld op 1. Verwijder de backfill-markering wanneer de frequentie eenmaal is ingesteld en probeer het opnieuw. |
| `1365-400` | Ongeldig verzoek | Het pad {path} in ops is ongeldig. Geef een geldig pad op {path} en probeer het opnieuw. |
| `1366-400` | Ongeldig verzoek | De begintijd is verstreken en de updatebewerking is niet langer toegestaan. |
| `1367-400` | Ongeldig verzoek | De deltakolom wordt vereist in exemplaartransformatie wanneer het creëren van een schakelaar van CRM. Geef een deltakolom op en probeer het opnieuw. |
| `1368-400` | Ongeldig verzoek | Modus is niet toegestaan in stroomaanvraag. Controleer uw aanvraag en probeer het opnieuw. |
| `1369-400` | Ongeldig verzoek | De deltabkolom in copy transform is niet toegestaan wanneer de frequentie eenmaal is ingesteld. Verwijder de deltakolom en probeer het opnieuw. |
| `1370-400` | Ongeldig verzoek | De bronkolommen kunnen niet worden opgehaald voor opname omdat de toewijzingstransformatie ontbreekt. Voeg de toewijzingstransformatie toe en probeer het opnieuw. |
| `1371-400` | Ongeldig verzoek | De detectie van bestandseigenschappen wordt niet ondersteund voor {connectorType} -connector. Geef de bestandseigenschappen handmatig op. |
| `1372-400` | Ongeldig verzoek | De huidige bewerking is niet toegestaan. Verkennen via verbindingsspecificatie is niet toegestaan voor verbinding spec ID= {connectionSpecId}. |
| `1373-400` | Ongeldig verzoek | Het flowSpecType ontbreekt in het verzoek. Geef een geldig flowSpecType op en probeer het opnieuw. |
| `1374-400` | Ongeldig verzoek | De opgegeven queryparameters zijn ongeldig. U kunt niet de markering determineProperties en user-defined eigenschappen in het zelfde verzoek hebben. Corrigeer de aanvraag en probeer het opnieuw. |
| `1375-400` | Ongeldig verzoek | De detectie van bestandseigenschappen is mislukt. Voer handmatig eigenschappen in. |
| `1376-400` | Ongeldig verzoek | De detectie van bestandseigenschappen wordt niet ondersteund voor connectionSpec id={connectionSpecId}. Geef de bestandseigenschappen handmatig op. |
| `1377-400` | Ongeldig verzoek | De opgegeven parameter value is null en kan niet worden vergeleken met operator {operator} . Geef een geldige waarde op en probeer het opnieuw. |
| `1378-400` | Ongeldig verzoek | Er is een fout opgetreden tijdens het valideren van de invoerkolom {column} voor filter bij bron. De kolomnaam moet een geldige kolom in de tabel zijn. Geef een geldige kolomnaam op en probeer het opnieuw. |
| `1379-400` | Ongeldig verzoek | Er is een fout opgetreden tijdens het valideren van de invoer {value} voor filter bij de bron. Het kolomgegevenstype bij bron is {columnDataType} en waardeDataType [ Koord ] past niet aan. Geef een geldige waarde op {value} en probeer het opnieuw. |
| `1380-400` | Ongeldig verzoek | Failed to create flow run. Foutbericht: {message} |
| `1381-400` | Ongeldig verzoek | WindowEndTime= {endTime} kan niet vóór Window StartTime= {startTime} zijn. Geef een geldige eindtijd op en probeer het opnieuw. |
| `1382-400` | Ongeldig verzoek | De deltabkolom moet overeenkomen met de waarde die aanwezig is in de transformaties voor kopiëren van de flow. Geef een geldige deltakolom op en probeer het opnieuw. |
| `1383-400` | Ongeldig verzoek | De deltabkolom ontbreekt in de params die worden ontvangen voor het maken van een flowuitvoering. Geef een deltakolom op in params en probeer het opnieuw. |
| `1384-400` | Ongeldig verzoek | De params= {params} die voor het creëren van stroomlooppas worden verstrekt zijn ongeldig of leeg. Geef geldige parameters op en probeer het opnieuw. |
| `1385-400` | Ongeldig verzoek | De verstrekte connectorType= {connectorType} wordt niet gesteund voor het creëren van stroomlooppas. Geef een geldig type connector op en probeer het opnieuw. |
| `1386-400` | Ongeldig verzoek | De flowId= {flowId} met planningParams frequency= {frequency} wordt niet gesteund voor het creëren van stroomlooppas. Geef een geldige frequentie op en probeer het opnieuw. |
| `1387-400` | Ongeldig verzoek | De flowRunId= {flowRunId} is in een ongeldige staat= {state} voor het opnieuw teweegbrengen. Probeer het later opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1388-400` | Ongeldig verzoek | De flow= {flow} is in state= {state} en kan niet opnieuw worden teweeggebracht. De flow moet zijn ingeschakeld om opnieuw te worden geactiveerd. |
| `1389-400` | Ongeldig verzoek | Er is een fout opgetreden tijdens het parseren van de opgegeven base64-gecodeerde tekenreeks. Geef een geldige gecodeerde filtertekenreeks op en probeer het opnieuw. |
| `1390-400` | Ongeldig verzoek | De operator &#39;not&#39; kan niet meer dan één vergelijking hebben. Geef een geldig aantal vergelijkingen op en probeer het opnieuw. |
| `1391-400` | Ongeldig verzoek | Failed to parse SchemaMetaData in sourceConnection for Id={sourceConnectionId}. Controleer het schemaMetaData in uw verzoek en probeer het opnieuw. |
| `1392-400` | Ongeldig verzoek | Failed to parse Transformations in flow request for flowId={flowId}. Controleer de transformaties in uw verzoek en probeer het opnieuw. |
| `1393-400` | Ongeldig verzoek | De opgegeven parameter {parameter} is null of leeg. Geef een geldige waarde op {parameter} en probeer het opnieuw. |
| `1394-400` | Ongeldig verzoek | De minimumwaarde voor een parameter {parameter} is 1. Geef een geldige waarde op {parameter} en probeer het opnieuw. |
| `1395-400` | Ongeldig verzoek | De bronverbinding die in de flow wordt gevonden, is null of leeg. Geef een geldige bronverbinding op in de flow en probeer het opnieuw. |
| `1396-400` | Ongeldig verzoek | Een overeenkomende indeling kan niet worden gevonden. Geef een overeenkomende indeling op en probeer het opnieuw. |
| `1397-400` | Ongeldig verzoek | De opgegeven frequentie : {frequency} is ongeldig. Geef een geldige frequentie op en probeer het opnieuw. |
| `1398-400` | Ongeldig verzoek | De opgegeven bewerking : {action} wordt niet ondersteund. Controleer de opgegeven bewerking en probeer het opnieuw. |
| `1399-400` | Ongeldig verzoek | Een geldig requestFileType is niet gevonden. Geef een geldig requestFileType op en probeer het opnieuw. |
| `1400-400` | Ongeldig verzoek | De opgegeven parameter &#39;templateType&#39; is ongeldig. Geef een geldig sjabloontype op en probeer het opnieuw. |
| `1401-400` | Ongeldig verzoek | The provided flow run action= {flowRunAction} is not supported. Voer een geldige handeling voor het uitvoeren van de flow in en probeer het opnieuw. |
| `1402-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1403-400` | Ongeldig verzoek | De begintijd is verstreken en u kunt de frequentie niet meer in één keer wijzigen. |
| `1404-400` | Ongeldig verzoek | De begintijd is verstreken en u kunt de backfill niet meer bijwerken. |

## Uitzonderingen op Flow Service (1600-1699)

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1600-400` | Ongeldig verzoek | Het verzoek kan niet worden verwerkt. {detailedMessage} |
| `1601-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1602-404` | Bron niet gevonden | De gevraagde bron is niet gevonden. {detailedMessage} |
| `1603-503` | Service niet beschikbaar | De service is tijdelijk niet beschikbaar. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1604-504` | Time-out gateway | Er is een time-out opgetreden bij de gateway. Probeer het opnieuw. Neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1605-401` | Ongeautoriseerd | De gebruiker is niet geautoriseerd. {detailedMessage} |
| `1606-403` | Verboden | De gewenste bewerking is niet toegestaan. {detailedMessage} |
| `1607-412` | Voorwaarde is mislukt | Aan de voorwaarde die wordt gedefinieerd door de headers if-Unmodified-Since of if-None-Match is niet voldaan. {detailedMessage} |

## Fouten in de landingszone van gegevens

| Foutcode | Titel | Gedetailleerd bericht |
| --- | --- | --- |
| `1700-500` | Interne fout | Er is een interne fout opgetreden. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1701-400` | Ongeldig verzoek | De opgegeven landingszone is inactief. Activeer de landingszone en probeer het opnieuw. |
| `1702-400` | Ongeldig verzoek | Het SAS Type= {sasType} wordt verstrekt voor de landingszone wordt niet toegestaan. Geef een geldige SAS op en probeer het opnieuw. |
| `1703-400` | Ongeldig verzoek | Vernieuwen van referenties is niet toegestaan. |
| `1704-400` | Ongeldig verzoek | De sleutels die voor storageAccountName= {accountName} in subscriptionId= {subscriptionId} en resourceGroupName= {resourceGroupName} zijn teruggekeerd zijn misvormd. Controleer uw aanvraag en probeer het opnieuw. Neem contact op met de ondersteuningsafdeling als het probleem zich blijft voordoen. |
| `1705-400` | Ongeldig verzoek | De opgegeven actie voor het aanlanden van gegevenszones wordt niet ondersteund. Voer een geldige handeling in en probeer het opnieuw. |
| `1706-400` | Ongeldig verzoek | De toegestane activeringen config wordt niet correct gevormd voor landingszone= {landingZoneType}. Probeer het opnieuw en neem contact op met de klantenondersteuning als het probleem zich blijft voordoen. |
| `1707-400` | Ongeldig verzoek | De dienst ontbrak aan opstarten omdat de het landen zoneconfiguratie niet ongeldig of leeg kan zijn. Controleer of de configuratie van de landingszone niet null is en probeer het opnieuw. |
| `1708-400` | Ongeldig verzoek | De container config kan niet ongeldig zijn in landingZoneType= {landingZoneType}. Controleer of de configuratie van de container niet null is en probeer het opnieuw. |
| `1709-400` | Ongeldig verzoek | De SAS details kunnen niet ongeldig voor {tokenConfig} in landingZoneType= {landingZoneType} zijn. Geef een geldige SAS op in de configuratie en probeer het opnieuw. |
| `1710-400` | Ongeldig verzoek | De opgegeven landingszone van het type: {landingZoneUseCase} wordt niet ondersteund. Geef een geldig type landingszone op en probeer het opnieuw. |
| `1711-400` | Ongeldig verzoek | De SAS-gegevens zijn niet gevonden voor de opgegeven landingszone van het type: {landingZoneUseCase}. Controleer of de SAS-gegevens voor het opgegeven landingstype zijn verstrekt. |
| `1712-400` | Ongeldig verzoek | De opgegeven actie voor de landingszone: {actionType} is niet toegestaan. Geef een geldige handeling op voor het aanlanden van gegevens en probeer het opnieuw. |
| `1713-400` | Ongeldig verzoek | {OperationType} is niet toegestaan voor de opgegeven {tokenType} . Controleer uw aanvraag en probeer het opnieuw. |
| `1714-400` | Ongeldig verzoek | clientId= {clientId} wordt niet toegestaan om deze verrichting uit te voeren. Controleer uw aanvraag met machtigingen en probeer het opnieuw. |
