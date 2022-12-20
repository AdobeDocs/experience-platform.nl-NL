---
title: Platform-gegevens beheren met Python en SQLAlchemy
description: Leer hoe u SQLAlchemy kunt gebruiken om uw Platform gegevens te beheren met Python in plaats van SQL.
source-git-commit: 6b7de4236982181eaac2aa37d525604cba31198e
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Gegevens van Platforms beheren met [!DNL Python] en [!DNL SQLAlchemy]

Leer hoe u SQLAlchemy kunt gebruiken voor meer flexibiliteit bij het beheer van uw Adobe Experience Platform-gegevens. Voor degenen die niet zo vertrouwd met SQL zijn, kan SQLAlchemy ontwikkelingstijd zeer verbeteren wanneer het werken met relationele gegevensbanken. Dit document bevat instructies en voorbeelden om verbinding te maken [!DNL SQLAlchemy] aan de Dienst van de Vraag en beginnen Python te gebruiken om met uw gegevensbestanden in wisselwerking te staan.

[!DNL SQLAlchemy] is een Object Relational Mapper (ORM) en een [!DNL Python] codebibliotheek die gegevens kan overbrengen die in een SQL gegevensbestand worden opgeslagen in [!DNL Python] objecten. U kunt dan CRUD-bewerkingen uitvoeren op gegevens die in het Platform data Lake worden opgeslagen met behulp van [!DNL Python] code. Hierdoor hoeft u geen gegevens te beheren met alleen PSQL.

## Aan de slag

Om de vereiste geloofsbrieven te verkrijgen voor het verbinden [!DNL SQLAlchemy] aan Experience Platform, moet u toegang tot de werkruimte van Vragen in Platform UI hebben. Neem contact op met uw organisatiebeheerder als u momenteel geen toegang hebt tot de werkruimte Query&#39;s.

## [!DNL Query Service] geloofsbrieven {#credentials}

Meld u aan bij de gebruikersinterface van het Platform en selecteer **[!UICONTROL Queries]** van de linkernavigatie, gevolgd door **[!UICONTROL Credentials]**. Voor volledige aanwijzingen over het zoeken naar uw aanmeldingsgegevens leest u de [aanmeldingsgids](../ui/credentials.md).

![Het tabblad Credentials met verlopen referenties voor Query Service gemarkeerd.](../images/use-cases/credentials.png)

Hoewel haven 80 de geadviseerde haven voor een verbinding aan de Dienst van de Vraag is, kunt u haven 5432 ook gebruiken.

>[!IMPORTANT]
>
>Als u het verlopen geloofsbrieven (zoals die in het beeld hierboven worden gezien) gebruikt om met de Dienst van de Vraag te verbinden, zal het zittingsleven voor uw verbinding na de vastgestelde periode verlopen die in de montages van uw organisatie wordt bepaald. Deze periode is standaard 24 uur. Raadpleeg de documentatie voor meer informatie over [een client verbinden met niet-vervallende gegevens](../ui/credentials.md#non-expiring-credentials), of hoe [verander het zittingsleven voor uw vervalsende geloofsbrieven](../ui/credentials.md#expiring-credentials).

Als u toegang hebt tot uw QS-referenties, opent u uw [!DNL Python] keuzevrijheid.

### Referenties opslaan in [!DNL Python] {#store-credentials}

In uw [!DNL Python] editor, importeer de `urllib.parse.quote` bibliotheek en sla elke referentie-variabele op als een parameter. De `urllib.parse` biedt een standaardinterface voor het onderbreken van URL-tekenreeksen in componenten. De aanhalingsfunctie vervangt speciale tekens in de URL-tekenreeks om de gegevens veilig te maken voor gebruik als URL-componenten. Hieronder ziet u een voorbeeld van de vereiste code:

>[!TIP]
>
>Gebruiken [!DNL Python]Drievoudige aanhalingstekens van het type om de tekenreeks voor het wachtwoord voor meerdere regels in te voeren.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>Het wachtwoord dat u opgeeft voor verbinding [!DNL SQLAlchemy] aan Experience Platform zal verlopen als u het verlopen geloofsbrieven gebruikt. Zie de [sectie met referenties](#credentials) voor meer informatie .

### Een motorinstantie maken [#create-engine]

Nadat de variabelen zijn gemaakt, importeert u de `create_engine` en maak een tekenreeks om uw referenties voor Query Service in SQLAlchemy te compileren en op te maken. De `create_engine` wordt vervolgens gebruikt om een motorinstantie te maken.

>[!NOTE]
>
>`create_engine`retourneert een instantie van een engine. Nochtans, opent het niet de verbinding aan de Dienst van de Vraag tot een vraag wordt geroepen die een verbinding vereist.

SSL moet zijn ingeschakeld wanneer u Platform benadert met clients van derden. Als onderdeel van de engine gebruikt u de opdracht `connect_args` om aanvullende trefwoordargumenten in te voeren. U wordt aangeraden de SSL-modus in te stellen op `require`. Zie de [Documentatie over SSL-modi](../clients/ssl-modes.md) voor meer informatie over toegestane waarden .

In het onderstaande voorbeeld wordt het [!DNL Python] code nodig om een engine- en verbindingstekenreeks te initialiseren.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>Het wachtwoord dat u opgeeft voor verbinding [!DNL SQLAlchemy] aan Experience Platform zal verlopen als u het verlopen geloofsbrieven gebruikt. Zie de [sectie met referenties](#credentials) voor meer informatie .

U bent nu klaar om de gegevens van het Platform te vragen gebruikend [!DNL Python]. In het onderstaande voorbeeld wordt een array met tabelnamen van Query Service geretourneerd.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
