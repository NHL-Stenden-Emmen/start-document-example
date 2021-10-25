> :warning: Ondanks dat er een Nederlandse versie beschikbaar is raden wij je aan het startdocument in het Engels te maken.

# Startdocument voor winkel

Startdocument van **Jan Doornbos**. Studentnummer **1234567**.

## Probleemomschrijving

We hebben een winkel met twee typen klanten. Een normale klant: deze heeft en klantnummer, naam en een woonplaats. Er is ook een premium klant: deze is hetzelfde als de normale klant, maar heeft ook een kortingspercentage. Alle klanten hebben een prefix voor het klantnummer: `MM__`. Deze prefix is gelijk voor alle klanten. Als deze prefix wordt aangepast, moet deze voor ALLE klanten worden aangepast. Maak een methode die deze prefix gecombineerd met het klantnummer teruggeeft. De winkel heeft ook producten. Producten hebben een naam en een prijs. De winkel kan bestellingen ontvangen.

Ontwerp en programeer een applicatie gebaseerd op bovenstaande tekst. De winkel wil ook een methode die alle klanten kan ophalen uit een bepaalde woonplaats. Vanwege legacy problemen, moet er ook een methode komen die alle klanten verwijdert die een lager klantnummer hebben dan een opgegeven klantnummer. De financiele afdeling wil ook weten wat de winst is van de store.

Zorg ervoor dat je applicatie goed gedocumenteerd is met Javadoc. Vergeet de applicatie ook niet te Unit testen.

## Input & Output

In deze sectie worden de in- en output en de berekeningen omschreven.

### Input

In de tabel hieronder wordt alle input (alles wat de gebruiker moet invoeren om de applicatie te laten werken) omschreven.

|Case|Type|Voorwaarden|
|----|----|-----------|
|Het klantnummer|`integer`|0 < `number` < 20|
|De naam van een klant|`String`|not empty|
|De woonplaats van een klant|`String`|not empty|
|De korting die een klant kan krijgen|`double`|0 < `number` <= 100|
|Naam van een product|`String`|not empty|
|Prijs van een product|`double`|`number` > 0|

### Output

|Case|Type|
|----|----|
|Klanten uit een bepaalde woonplaats|`ArrayList<Customer>`|
|De totale winst van de winkel|`double`|
|De prijs van een bestelling|`double`|

### Berekeningen

|Case|Calculation|
|----|-----------|
|Bedrag van een order|De som van alle product prijzen|

### Opmerkingen

* De input zal worden gevalideerd.
* Alleen de `Main` zal `System.out.println` bevatten.
* Er zullen Unit tests aanwezig zijn.

## Klassendiagram

![Class Diagram](images/classdiagram.png "Second Version of the class diagram")

## Testplan

In deze sectie worden de testcases omschreven voor het testen van de applicatie.

### Test Data

In de volgende tabellen vind je alle data die nodig is voor het uitvoeren van de testcases.

#### Product

|ID|Input|Code|
|--|-----|----|
| `playstation`|name: PlayStation<br />price: 250|`new Product("PlayStation", 250)`|
|`imac`|name: iMac<br />price: 1400|`new Product("iMac", 1400)`|

#### Customer

|ID|Input|Code|
|--|-----|----|
|`jan`|number: 1<br />name: Jan<br />city: Emmen|`new Customer(1, "Jan", "Emmen")`|
|`martijn`|number: 2<br />name: Martijn<br />city: Emmen<br />discount: 20%| `new PremiumCustomer(2, "Martijn", "Emmen", 20.0)`|

#### Store

|ID|Input|Code|
|--|-----|----|
|`mediamarkt`||`new Store()`|

#### Order

|ID|Input|Code|
|--|-----|----|
|`appleorder`|customer: `jan`|`new Order(jan)`|
|`psorder`|customer: `martijn`|`new Order(martijn)`|

#### Producten aan Order toevoegen

|Order|Code|
|-----|----|
|`appleorder`|`addProduct(imac)`|
|`psorder`|`addProduct(playstation)`|
|`psorder`|`addProduct(playstation)`|

### Testcases

In deze sectie worden de testcases omschreven. Elke testcase moet worden uitgevoerd met bovenstaande testdata als startpunt.

#### #1 Klantnummer prefix

Het verifieren van de prefix van een klant. De klantnaam zou moeten worden geprefixed.

|Stap|Input|Actie|Verwachte output|
|----|-----|-----|----------------|
|1|`jan`|`getNumberWithPrefix()`|MM_1|

#### #2 Haal alle klanten uit een bepaalde woonplaats op

Het testen van de methode die alle klanten uit een bepaalde woonplaats kan ophalen.

|Stap|Input|Actie|Verwachte output|
|----|-----|-----|----------------|
|1|`mediamarkt`|`getCustomersFromCity("Emmen")`|Empty ArrayList|
|3|`mediamarkt`|`addOrder(appleorder)`||
|4|`mediamarkt`| `getCustomersFromCity("Emmen")`| ArrayList with customer `jan` |

#### #3 Verwijderen van klanten

Testen van het verwijderen van klanten. Alle klanten met een lager klantnummer dan het opgegeven nummer moeten zijn verwijderd.

|Stap|Input|Actie|Verwachte output|
|----|-----|-----|----------------|
|1|`mediamarkt`|`removeCustomers(1)`||
|2| `mediamarkt` |`getCustomers()`|ArrayList with only customer `martijn`|

#### #4 Haal prijs van een bestelling op

Testen van de prijs van een bestelling. Let op: de `psorder` heeft een `PremiumCustomer`.

|Stap|Input|Actie|Verwachte output|
|----|-----|-----|----------------|
|1|`appleorder`|`getPrice()`|1400|
|2|`psorder`|`getPrice()`|400|

#### #5 De winkel winst

Testen van de totale winst van de winkel.

|Stap|Input|Actie|Verwachte output|
|----|-----|-----|----------------|
|1|`mediamarkt`|`addOrder(appleorder)`||
|2|`mediamarkt`|`getProfit()`| 1400|
|3|`mediamarkt`|`addOrder(psorder)`||
|4|`mediamarkt`|`getProfit()`| 1900|