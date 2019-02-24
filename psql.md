# PostgreSQL - PSQL

## PSQL

- Pro rychlé přihlášení: ```sudo -u postgres psql postgres```
- Pro psql help: ```\?``` pro SQL help ```\h```
- Pro konec: ```\q```
- pro vypsání všech databází: ```\l```
- Pro připojení do databáze: ```\c <jméno databáse>``` 
- Ukaž tabulky: ```\dt```

## PostgreSQL
- příkazy můžu psát přímo do psql po přihlášení a připojení do DB
- __CREATE TABLE__
```sql
CREATE TABLE TABLE_NAME (
    column datatype constraints
)

-- Příklad: --
CREATE TABLE MOJE_TABULKA (
    ID              SERIAL      NOT NULL    UNIQUE,
    KRESTNI_JMENO   TEXT        NOT NULL,
    PRIJMENI        TEXT        NOT NULL,
    EMAIL           TEXT        NOT NULL,
    TYP_UZIVATELE   CHAR(3)     NOT NULL,
    CASOVA_ZNAMKA   TIMESTAMP   NOT NULL,
    PRIMARY KEY(ID)
);
```
- __INSERT TABLE__
    - Pokud mám generované věci např. timestamp nebo auto inkrement např. primární klíč: použiju ```DEFAULT```
```sql
INSERT INTO TABLE_NAME (SLOUPEC, ...) VALUES (...);

-- Příklad: --
INSERT INTO MOJE_TABULKA (ID, KRESTNI_JMENO, PRIJMENI, EMAIL, TYP_UZIVATELE, CASOVA_ZNAMKA) VALUES (DEFAULT, 'JMENO', 'PŘÍJMENÍ', 'coolemail@rad.cz', 'AST', NOW()::timestamp);
```

## Zdroje 
[POSTGRESQL tutorial](http://www.postgresqltutorial.com/psql-commands/)

[POSTGRES guide](http://postgresguide.com/utilities/psql.html)

[POSTGRES A PSQL cheatsheet](https://gist.github.com/Kartones/dd3ff5ec5ea238d4c546)