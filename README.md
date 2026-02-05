## Om detta repository

Detta repository innehåller ett komplett databasdesign-projekt för ett bibliotekssystem. Projektet inkluderar SQL-implementering, ER-diagram, dokumentation och visualiseringar som demonstrerar databaskoncept och databashantering.

## Projektinnehåll

### Library.png
ER-diagram visualisering (223 KB) som visar:
- **Entity-Relationship Diagram** - visuell representation av databasen
- Tabeller och deras relationer
- Primärnycklar och främmande nycklar
- Kardinalitet mellan entiteter
- Databasstruktur och schema

### Library.drawio
Redigerbar diagramfil (39 KB) för:
- **Draw.io/Diagrams.net-fil** - källfil för ER-diagrammet
- Möjlighet att redigera och uppdatera databasen design
- Versionskontroll av databasarkitektur
- Exportering till olika format

### Library-sql
SQL-skriptfil (9 KB) som innehåller:
- **CREATE TABLE**-satser för alla tabeller
- **Tabellstrukturer** med datatyper och constraints
- **Primary Keys** och **Foreign Keys**
- **Indexering** för optimerad prestanda
- **INSERT**-satser för exempeldata
- **Queries** för databasoperationer

### Library system database.docx
Omfattande dokumentation (26 KB) som täcker:
- Projektbeskrivning och syfte
- Kravspecifikation
- Databasdesign och normalisering
- ER-diagram förklaringar
- SQL-queries och exempel
- Användarscenarier

## Bibliotekssystem - Översikt

Detta databasystem hanterar:

### Kärnfunktionalitet:
- **Böcker** - katalogisering av bibliotekets samlingar
- **Medlemmar** - registrering av biblioteksanvändare
- **Lån** - hantering av utlåning och återlämning
- **Författare** - information om bokförfattare
- **Kategorier** - klassificering av böcker
- **Personal** - biblioteksanställda och deras roller

### Processer som stöds:
- Låna böcker
- Återlämna böcker
- Registrera nya medlemmar
- Lägg till nya böcker
- Sök efter böcker
- Hantera försenade återlämningar
- Generera rapporter

## Teknologi & Verktyg

- **Databassystem:** SQL (kan användas med MySQL, PostgreSQL, SQL Server)
- **Diagram:** Draw.io / Diagrams.net
- **Dokumentation:** Microsoft Word
- **Visualisering:** PNG-export av ER-diagram

## Komma igång

### Förutsättningar

För att använda detta databasprojekt behöver du:

- **Databashanteringssystem (DBMS):**
  - MySQL (rekommenderat)
  - PostgreSQL
  - SQL Server
  - SQLite
  
- **Verktyg:**
  - MySQL Workbench / pgAdmin / DBeaver
  - Textredigerare eller SQL-editor
  - Draw.io (för att redigera diagram)
