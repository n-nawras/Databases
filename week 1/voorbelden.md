## Stap 1: Alle gegevens in één tabel (beginpunt)

Laten we starten met een eenvoudige tabel waarin alle gegevens in één enkele tabel worden geplaatst. Dit is vaak het eerste ontwerpstadium van een database, maar het kan leiden tot redundantie en inefficiëntie.

### Voorbeeldtabel:

| KlantID | Naam         | Leeftijd | BestellingID | Besteldatum  | Productnaam  |
|---------|--------------|----------|--------------|-------------|--------------|
| 1       | Jan Jansen   | 35       | 101          | 2024-10-01  | Laptop       |
| 2       | Eva de Vries | 28       | 102          | 2024-10-02  | Smartphone   |
| 1       | Jan Jansen   | 35       | 103          | 2024-10-05  | Toetsenbord  |

In dit voorbeeld:
- **Redundantie:** De klantgegevens van Jan Jansen komen meerdere keren voor (KlantID 1).
- **Herhalende groepen:** Een klant kan meerdere bestellingen plaatsen, en producten worden mogelijk herhaald binnen één tabel.

---

## Stap 2: Verbeteren van Tabelstructuren

Nu gaan we deze tabel verbeteren door het toepassen van de stappen zoals het elimineren van herhalende groepen, elimineren van redundantie, en het normaliseren van de tabelstructuur.

### 1. Elimineren van de herhalende groep

Herhalende groepen, zoals meerdere producten bij één bestelling, worden verplaatst naar een aparte tabel. In plaats van meerdere kolommen voor producten (bijv. "Product1", "Product2"), maken we een aparte **BesteldeProducten**-tabel.

#### Nieuwe tabellen:

- **Bestellingen-tabel:**

| BestellingID | KlantID | Besteldatum   |
|--------------|---------|---------------|
| 101          | 1       | 2024-10-01    |
| 102          | 2       | 2024-10-02    |
| 103          | 1       | 2024-10-05    |

- **BesteldeProducten-tabel:**

| BestellingID | Productnaam |
|--------------|-------------|
| 101          | Laptop      |
| 102          | Smartphone  |
| 103          | Toetsenbord |

Nu hebben we de herhalende groep van producten gescheiden in een eigen tabel, en we hebben een relatie tussen bestellingen en producten via **BestellingID**.

---

### 2. Elimineren van redundantie

Redundante gegevens zoals de naam en leeftijd van de klant worden verplaatst naar een aparte **Klantentabel**. In plaats van de klantinformatie te herhalen bij elke bestelling, wordt deze gekoppeld via een **KlantID**.

#### Nieuwe tabellen:

- **Klantentabel:**

| KlantID | Naam         | Leeftijd |
|---------|--------------|----------|
| 1       | Jan Jansen   | 35       |
| 2       | Eva de Vries | 28       |

Nu wordt de klantinformatie slechts één keer opgeslagen in de **Klantentabel** en gekoppeld aan de bestellingen via **KlantID**.

---

### 3. Elk entiteittype zijn eigen tabel

We hebben nu drie entiteiten: **Klant**, **Bestelling**, en **Product**. Elk entiteittype heeft zijn eigen tabel, en de relaties tussen deze tabellen worden beheerd via **KlantID** en **BestellingID**.

- **Klantentabel** (voor klantgegevens)
- **Bestellingen-tabel** (voor bestellingen)
- **BesteldeProducten-tabel** (voor producten per bestelling)

---

### 4. Normaliseren en standaardiseren

Na het opsplitsen van de tabellen door normalisatie, hebben we de gegevens georganiseerd in de **derde normale vorm (3NF)**. Dit betekent:

- **1NF:** Geen herhalende groepen; alle kolommen bevatten enkelvoudige (atomaire) waarden.
- **2NF:** Alle niet-sleutelattributen zijn volledig afhankelijk van de primaire sleutel (bijv. in de **Bestellingen-tabel** zijn alle gegevens afhankelijk van **BestellingID**).
- **3NF:** Er zijn geen transitieve afhankelijkheden; klantinformatie is opgeslagen in de **Klantentabel** en producten in de **BesteldeProducten-tabel**, zonder afhankelijkheden tussen niet-sleutelattributen.

---

### 5. Structuur en populatie

Na de normalisatie ziet de database-structuur er als volgt uit:

- **Klantentabel:**
  - Bevat klantgegevens en wordt geïdentificeerd door **KlantID**.
  
- **Bestellingen-tabel:**
  - Bevat gegevens over bestellingen en is gerelateerd aan klanten via **KlantID**.
  
- **BesteldeProducten-tabel:**
  - Bevat de producten per bestelling en is gerelateerd aan de bestellingen via **BestellingID**.

Nu kunnen we deze tabellen vullen met gegevens.

---

### 6. Tabellen en relaties

De tabellen in de database zijn met elkaar verbonden door relaties:

- **KlantID** is een **primaire sleutel** in de **Klantentabel** en een **vreemde sleutel** in de **Bestellingen-tabel**. Hierdoor kunnen we zien welke klant welke bestelling heeft geplaatst.
- **BestellingID** is een **primaire sleutel** in de **Bestellingen-tabel** en een **vreemde sleutel** in de **BesteldeProducten-tabel**. Hierdoor kunnen we zien welke producten bij welke bestelling horen.

---

## Overzicht van de verbeterde structuur:

**Klantentabel:**

| KlantID | Naam         | Leeftijd |
|---------|--------------|----------|
| 1       | Jan Jansen   | 35       |
| 2       | Eva de Vries | 28       |

**Bestellingen-tabel:**

| BestellingID | KlantID | Besteldatum   |
|--------------|---------|---------------|
| 101          | 1       | 2024-10-01    |
| 102          | 2       | 2024-10-02    |
| 103          | 1       | 2024-10-05    |

**BesteldeProducten-tabel:**

| BestellingID | Productnaam |
|--------------|-------------|
| 101          | Laptop      |
| 102          | Smartphone  |
| 103          | Toetsenbord |
