## Problem Statment
In this project, you’re going to make your own table with some small set of “famous people”, then make more tables about things they do and join those to create nice human readable lists.
For example, here are types of famous people and the questions your data could answer:
- Movie stars: What movies are they in? Are they married to each other?
- Singers: What songs did they write? Where are they from?
- Authors: What books did they write?
- Fictional characters: How are they related to other characters? What books do they show up in?

Database schema:

![image](https://user-images.githubusercontent.com/104938319/178063389-37f3f1a3-84d2-497c-9d4a-e68531e54821.png)

characters table:

![image](https://user-images.githubusercontent.com/104938319/178063453-63270384-41da-47d4-b4f7-80b252a7437e.png)

hobies table:

![image](https://user-images.githubusercontent.com/104938319/178063471-5be684ff-e1ca-464c-a3a3-333421321dea.png)

relationships table:

![image](https://user-images.githubusercontent.com/104938319/178063498-b36db4ed-7440-46aa-8f88-1b66a9fc50ec.png)

## Solution
```sql
-- create table of hunger games characters and insert records
CREATE TABLE characters (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
	name TEXT,
	district INTEGER
);

INSERT INTO characters (name, district) VALUES
    ("Katniss Everdeen", 12),
    ("Peeta Mellark", 12),
    ("Gale Hawthorn", 12),
    ("Finnick Odair", 4),
    ("Rue", 11),
    ("Johanna Mason", 7),
    ("Beetee", 3),
    ("Wiress", 3),
    ("Annie Cresta", 4);
    
-- create hobbies table and insert records
CREATE TABLE hobbies (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
	character_id INTEGER,
	hobby TEXT
);

INSERT INTO hobbies (character_id, hobby) VALUES 
    (1, "archery"),
    (2, "baking"),
    (4, "fishing"),
    (5, "climbing"),
    (6, "melee"),
    (7, "electronics");

-- create relationships table and insert records
CREATE TABLE relationships (
	id INTEGER PRIMARY KEY AUTOINCREMENT,
	character1_id INTEGER,
	character2_id INTEGER,
	relationship TEXT
);

INSERT INTO relationships (character1_id, character2_id, relationship) VALUES
    (1, 2, "significant other"),
	(4, 9, "significant other"),
	(1, 5, "friends"),
	(1, 3, "friends"),
	(1, 6, "frenemies"),
	(2, 3, "rivals");

-- list characters and their hobbies
SELECT characters.name, hobbies.hobby
    FROM characters
    JOIN hobbies
    ON characters.id = hobbies.character_id
    ;
```
Result:

![image](https://user-images.githubusercontent.com/104938319/178063575-0923a3ca-92d7-4ae6-8264-74d2890ce79d.png)

```sql
-- list all characters and their hobbies, even if they have no hobbies
SELECT characters.name, hobbies.hobby
    FROM characters
    LEFT OUTER JOIN hobbies
    ON characters.id = hobbies.character_id
    ;
```

Result:

![image](https://user-images.githubusercontent.com/104938319/178063634-27615b79-9442-48d8-b081-b3a200e99ce6.png)

```sql
-- show character relationship pairs using character names
SELECT a.name, b.name, relationships.relationship
    FROM relationships
    JOIN characters a
    ON a.id = relationships.character1_id
    JOIN characters b
    ON b.id = relationships.character2_id
    ;
```

Result:

![image](https://user-images.githubusercontent.com/104938319/178063677-82d5639f-b8ef-404f-8948-fdd3cda047b6.png)
