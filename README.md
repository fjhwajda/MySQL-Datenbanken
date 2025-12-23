# MySQL-Datenbanken-Baisics
Eine SQL‑Datenbank besteht aus einigen grundlegenden Bausteinen, die in fast jedem relationalen System vorkommen. Diese Konzepte bleiben inhaltlich gleich, auch wenn sich die konkrete SQL‑Syntax je nach System leicht unterscheidet. Dazu gehören Tabellen zur strukturierten Datenspeicherung, Schlüssel zur eindeutigen Identifikation, Beziehungen zwischen Tabellen, Abfragen zum Lesen von Daten sowie Befehle zum Einfügen, Ändern und Löschen. In diesem Dokument werden diese Kernkonzepte zusammengefasst, um den Einstieg in SQL‑Datenbanken zu erleichtern.
## Commands

Datenbank erstellen
```sql
CREATE DATABASE name;
```
Listet alle Datenbanken auf dem Server
```sql
SHOW DATABASE;
```
Wechselt auf die Datenbank
```sql
USE name;
```
Löscht die Datenbank inkl. aller Tabellen
```sql
DROP DATABASE name;
```
Legt eine Tabelle an
```sql
CREATE TABLE name;
```
Zeigt alle tabelle an
```sql
SHOW TABLES;
```
Zeigt Spaltenname, Typ und Eigenschaften an
```sql
DESCRIBE name;
```
Fügt der Tabelle name eine neue spalte hinzu
```sql
ALTER TABLE name
ADD COLUMN test DATATYPE;
```
Entfernt die Spalte test in der Tabelle name
```sql
ALTER TABLE name
DROP COLUMN test;
```
Löscht die Tabelle name
```sql
DROP TABLE name;
```
Entfernt alle Zeilen aus name, behält die Struktur
```sql
TRUNCATE TABLE name;
```
Fügt eine neue Zeile mit Werten in die Tabelle
```sql
INSERT INTO name
(c1,c2) VALUES (v1,v2);
```
Fügt mehrere zeilen in einem befehlt ein
```sql
INSERT INTO name
(...) VALUES (...),(...);
```
Wählt alle Spalten und Zeile aus Tabelle aus.
```sql
SELECT * FROM name;
```
Wählt bestimmte Spalten und filter Zeilen nach condition
```sql
SELECT col1, col2 FROM
name WHERE
condition;
```
Gibt nur unterschiedliche Werte der Spalte col1 aus tabelle name zurück
```sqL
SELECT DISTRICT col1 FROM
name; 
```
Ändert Spaltenwert in zeile die condition erfüllen
```sql
UPDATE name SET
col = val WHERE
condition;
```
Löscht Zeilen aus Tabellen die condition erfüllen
```sql
DELETE FROM name
WHERE condition;
```
Verknüpft Tabelle `a` und `b` gibt nur übereinstimmende Zeilen zurück
```sql
SELECT ... FROM a INNER
JOIN b ON a.key = b.key;
```
Gibt all Zeile aus a und passende aus b, fehlende b werte sind NULL
```sql
SELECT ... FROM a LEFT
JOIN b ON ...;
```
Gruppiert ergebnisse nach col und filtert Gruppen mit Aggregatbedingungen
```sql
GROUP BY col HAVING
COUNT(*) > n;
```
Sortiert Ergenisse nach col und begrenz auf anzahl n.
```Sql
ORDER BY col ASC
DESC LIMIT n;
```
Legt index auf Tabelle name und col an, um Abfragen zu beschleunigen
```sql
CREATE INDEX idx ON
name(col);
```
Legt einen Datenbank nutzer mit PAsswort an
```sql
CREATE USER 
'user'@'host' IDENTIFIED BY 'pw';
```
Vergibt rRechte (z.b SELECT) an eine Benutzer in der Datenbank
```sql
GRANT SELECT, INSERT ON
db.* TO 'user'@'host';
```
Zeigt Berechtigungen eines Benutzers an
```sql
SHOW GRANTS FOR
'user'@'host';
```
Exportiert die Datenbank name in eine SQL Dumpdatei.
```sql
mysqldump -u user -p
name > dump.sql
```
Importiert eine SQL Dumpdatei.
```sql
mysql -u user -p
name < dump.sql
```
### Definitionen
#### identifier = Name für DB/Tabelle/Spalte
```sql
CREATE DATABASE name;
id #Beziechnung für Spatlte; Buchstaben, Zahlen, Zeichen usw.
```
#### datatype = 
```sql
INT #(ganze zahl)
VARCHAR #(legt max zeichen länge an) 
DATE #(Zeit und Datum)-
```
#### constraint = Regel  
```sql
NOT NULL #(darf nicht leer sein)
UNIQUE #(einzigartig, nicht wiederhohlt)
PRIMARY KEY #(Primärschlüssel)
```
verhindert Fehler, wenn schon Exisitert
```sql
CREATE DATABASE [IF NOT EXISTS] name;
```
Verhinder Fehler, genaues löschen.
```sql
USE name;
DROP DATABSE [IF EXISTS] name;
```
Automatisch generiert, fortlaufend zahl für neue Zeile
```sql
AUTO_INCREMENT
--Beispiel
id INT UNSIGNED NOT NULL AUTO_INCREMT PRIMARY KEY;
```
Tabelle erstellen beispiel:
```sql
CREATE TABLE users (
id INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
username VARCHAR(50) NOT NULL UNIQUE,
email VARCHAR(255) DEFAULT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```
