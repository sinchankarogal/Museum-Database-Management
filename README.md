# Museum-Database-Management

### Project Description
 Consider a database to keep track of information for an art museum with  the following 
requirements : 
<br>
The museum has a collection of ART_OBJECTS. Each ART_OBJECT has a unique Id_no, an Artist (if known), a Year (when it was created, if known), a Title, and a Description. The art objects are categorized in several ways, as discussed below. 
<br>

 ART_OBJECTS are categorized based on their type. There are three main types— PAINTING, SCULPTURE, and STATUE—plus another type called OTHER to accommodate objects that do not fall into one of the three main types. 
<br>
 A PAINTING has a Paint_type (oil, watercolor, etc.), material on which it is Drawn_on (paper, canvas, wood, etc.), and Style (modern, abstract, etc.). 
<br>
 A SCULPTURE or a statue has a Material from which it was created (wood, stone, etc.), Height, Weight, and Style. 
<br>
 An art object in the OTHER category has a Type (print, photo, etc.) and Style. 
<br>
ART_OBJECTs are categorized as either PERMANENT_COLLECTION (objects that are owned by the museum) and BORROWED. Information captured about objects in the PERMANENT_COLLECTION includes Date_acquired, Status (on display, on loan, or stored), and Cost. Information captured about ORROWED objects includes the Collection from which it was borrowed, Date_borrowed, and Date_returned. 
<br>
 Information describing the country or culture of Origin (Italian, Egyptian, American, Indian, and so forth) and Epoch (Renaissance, Modern, Ancient, and so forth) is captured for each T_OBJECT. 
<br>
 The museum keeps track of ARTIST information, if known: Name, DateBorn (if known), Date_died (if not living), Country_of_origin, Epoch, Main_style, and Description. The Name is assumed to be unique. 
<br>
 Different EXHIBITIONS occur, each having a Name, Start_date, and End_date. EXHIBITIONS are related to all the art objects that were on display during the exhibition.  
<br>
 Information is kept on other COLLECTIONS with which the museum interacts; this information includes Name (unique), Type (museum,  personal, etc.), Description, Address, Phone, and current Contact_person. 
Design an entity–relationship diagram for the mail-order database and Convert it into a Schema diagram.  
 <br>
Identify the appropriate functional requirements for the above database, write the SQL 
queries, and show the results.
<br>


### Creating Table

```sql

CREATE TABLE ARTIST (
    NAME VARCHAR(255) PRIMARY KEY,
    DATEBORN INT,
    DATE_DIED INT,
    MAIN_STYLE VARCHAR(255),
    DESCRIPTION VARCHAR(255),
    EPOCH VARCHAR(255),
    COUNTRY_OF_ORIGIN VARCHAR(255)
);

CREATE TABLE ART_OBJECT (
    ID_NO INT PRIMARY KEY,
    YEAR INT,
    TITLE VARCHAR(255),
    DESCRIPTION VARCHAR(255),
    STYLE VARCHAR(255),
    ORIGIN VARCHAR(255),
    ARTIST_NAME VARCHAR(255),
    FOREIGN KEY (ARTIST_NAME) REFERENCES ARTIST(NAME)
);

CREATE TABLE EXHIBITION (
    NAME VARCHAR(255) PRIMARY KEY,
    START_DATE VARCHAR(255),
    END_DATE VARCHAR(255),
    ART_OBJ_ID INT,
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO)
);

CREATE TABLE COLLECTION (
    NAME VARCHAR(255) PRIMARY KEY,
    ART_OBJ_ID INT,
    TYPE VARCHAR(255),
    DESCRIPTION VARCHAR(255),
    CONTACT_PERSON VARCHAR(255),
    PHONE VARCHAR(255),
    ADDRESS VARCHAR(255),
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO)
);

CREATE TABLE BORROWED_COLLECTION (
    BORROWED_ID VARCHAR(255) PRIMARY KEY,
    DATE_RETURNED VARCHAR(255),
    ART_OBJ_ID INT,
    DATE_BORROWED VARCHAR(255),
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO)
);

CREATE TABLE PERMANENT_COLLECTION (
    DATE_AQUIRED VARCHAR(255) ,
    PERMANENT_ID VARCHAR(255) PRIMARY KEY,
    STATUS INT,
    COST INT,
    ART_OBJ_ID INT,
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO)
);

CREATE TABLE STATUE (
    ART_OBJ_ID INT,
    STYLE VARCHAR(255),
    HEIGHT FLOAT,
    WEIGHT FLOAT,
    MATERIAL VARCHAR(255),
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO),
    PRIMARY KEY(ART_OBJ_ID,STYLE)
);

CREATE TABLE SCULPTURE (
    ART_OBJ_ID INT,
    STYLE VARCHAR(255),
    HEIGHT FLOAT,
    WEIGHT INT,
    MATERIAL VARCHAR(255),
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO),
    PRIMARY KEY(ART_OBJ_ID,STYLE)
);

CREATE TABLE PAINTING (
    ART_OBJ_ID INT,
    STYLE VARCHAR(255),
    DRAWN_ON VARCHAR(255),
    PAINT_TYPE VARCHAR(255),
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO),
    PRIMARY KEY(ART_OBJ_ID,STYLE)

);

CREATE TABLE OTHER (
    ART_OBJ_ID INT,
    STYLE VARCHAR(255),
    TYPE VARCHAR(255),
    FOREIGN KEY (ART_OBJ_ID) REFERENCES ART_OBJECT(ID_NO),
    PRIMARY KEY(ART_OBJ_ID,STYLE)
);

```

### Inserting values

```sql

INSERT INTO ARTIST VALUES ('Pablo Picasso', 1881, 1973,
'Cubism','Co-founder of the Cubist movement.', '20th century modern art ','Spain');
INSERT INTO ARTIST VALUES ('Michelangelo', 1475 ,1564,
'Renaissance','One of the greatest artists of all time.', 'High Renaissance','Italy');
INSERT INTO ARTIST VALUES ('Vincent van Gogh', 1853 ,1890,'Post-Impressionism',
'Famous artistof the Post-Impressionist movement.','19th century modern art',' Netherlands');
INSERT INTO ARTIST VALUES ('Auguste Rodin', 1840 ,1917,'Impressionism',
'Best known for his bronze statue "The Thinker".','19th century modern art',' France');
INSERT INTO ARTIST VALUES ('Leonardo da Vinci', 1452, 1519,'Renaissance',
'Polymath and one of the greatest artists of all time.','High Renaissance','Italy');
INSERT INTO ARTIST VALUES ('Henry Moore', 1898,1986 ,'Modernist',
'Best known for his abstract bronze sculptures.','20th century modern art ','England');
INSERT INTO ARTIST VALUES ('Rembrandt van Rijn', 1606 ,1669, 'Baroque',
'A leading Dutch master of the Baroque era.','Dutch Golden Age','Netherlands');
INSERT INTO ARTIST VALUES ('Pharaoh Khafre', 1809 ,1890,' Ancient','Egyptian A Pharaoh of ancient Egypt,
Old Kingdom Egyptknown for his reign during which the Great Sphinx of Giza was built.','Old Kingdom ','Egypt');
INSERT INTO ARTIST VALUES ('Yoko Ono', 1933 ,1998,'Conceptual',
'A multimedia artist and peace activist',' 20th century modern art','Japan');
INSERT INTO ARTIST VALUES ('Banksy',1975,NULL,'Street art','A pseudonymous England-based street artist',
' 21st century modern art','England');
INSERT INTO ARTIST VALUES ('Johannes Vermeer', 1632, 1675,'Baroque','A Dutch master of the Baroque era.',
'Dutch Golden Age ','Netherlands');
INSERT INTO ARTIST VALUES ('Edvard Munch', 1863 ,1944,'Expressionism',
'A leading figure of the Expressionist movement.','19th/20th century modern art','Norway' );
INSERT INTO ARTIST VALUES ('Antonio Canova', 1757 ,1822,'Neoclassicism',
'A leading sculptor of the Neoclassical period.',' 19th century modern art','Italy');
INSERT INTO ARTIST VALUES ('Henri Matisse', 1869, 1954,'Fauvism',
'A pioneer of the Fauvist movement 20th century modern art','20th century modern art','France');
INSERT INTO ARTIST VALUES ('Grant Wood', 1891, 1942,'Regionalism',
'A leading figure of the Regionalist art movement in the US.','20th century modern art','US');
INSERT INTO ARTIST VALUES ('Frida Kahlo', 1907, 1954, 'Surrealism', 
'A self-taught painter and leading figure in Mexican folk art.','20th century modern art','Mexico');
INSERT INTO ARTIST VALUES ('John William Waterhouse', 1849, 1917,'PreRaphaelite',
'A leading member of the Pre-Raphaelite Brotherhood',' Victorian era','England');
INSERT INTO ARTIST VALUES ('Salvador Dali', 1904, 1989,'Surrealism',
'A leading figure in the Surrealist movement.',' 20th century modern art','Spain');
INSERT INTO ARTIST VALUES ('Rene Magritte', 1898, 1967,
'Surrealism','A leading figure in the Surrealist movement.','20th century modern art','Belgian');
INSERT INTO ARTIST VALUES ('Edward Hopper', 1882, 1967,'Realism',
'A leading American realist painter and printmaker.','20th century modern art',' US');

INSERT INTO ART_OBJECT VALUES (1,1937,'Guernica','Oil painting','Modern','Spanish ','Pablo Picasso');
INSERT INTO ART_OBJECT VALUES (2,1501 ,'David','Marble statue','Renaissance','Italian','Michelangelo');
INSERT INTO ART_OBJECT VALUES (3,1889,'The Starry Night','Oil painting','Post-Impressionist ','Dutch','Vincent van Gogh');
INSERT INTO ART_OBJECT VALUES (4,1881,'The Thinker','Bronze sculpture ','Modern','French','Auguste Rodin');
INSERT INTO ART_OBJECT VALUES (5,1498,'The Last Supper ','Fresco painting','Renaissance','Italian','Leonardo da Vinci');
INSERT INTO ART_OBJECT VALUES (6,1944,'Reclining Figure','Sculpture ','Modern','British ','Henry Moore');
INSERT INTO ART_OBJECT VALUES (7,1642 ,'Night Watch ','Oil painting','Baroque','Dutch','Rembrandt van Rijn');
INSERT INTO ART_OBJECT VALUES (8,1500,'Egyptian Sphinx','Statue ','Ancient','Egypt ','Pharaoh Khafre');
INSERT INTO ART_OBJECT VALUES (9,1966,'Cut Piece ','Other','Conceptual','Japan ','Yoko Ono');
INSERT INTO ART_OBJECT VALUES (10,2010,'Girl with Balloon ','Spray Painting','Street Art','London','Banksy');
INSERT INTO ART_OBJECT VALUES (11,1665 ,'Girl with pearl Earring','Painting','Dutch Golden Age ','Mauritshuis','Johannes Vermeer');
INSERT INTO ART_OBJECT VALUES (12,1893,'The Scream','Painting','Expressionism','Norway','Edvard Munch');
INSERT INTO ART_OBJECT VALUES (13,1803,'Psyche Revived by Cupid’s Kiss','Sculpture ','Neoclassicism','Paris','Antonio Canova');
INSERT INTO ART_OBJECT VALUES (14,1953 ,'The Snail','Painting','Fauvism','African ','Henri Matisse');
INSERT INTO ART_OBJECT VALUES (15,1930 ,'American Gothic','Oil painting','Regionalism ','American','Grant Wood');
INSERT INTO ART_OBJECT VALUES (16,1929,'The Two Fridas','Painting','Surrealism','Mexican','Frida Kahlo');
INSERT INTO ART_OBJECT VALUES (17,1888,'The Lady of Shallot','Oil painting','Pre-Raphaelitism','English ','John William Waterhouse');
INSERT INTO ART_OBJECT VALUES (18,1931 ,'The Persistence of Memory ','Oil painting','Surrealism','Spanish ','Salvador Dali');
INSERT INTO ART_OBJECT VALUES (19,1964,'The son of Man','Oil painting','Surrealism','Belgian','Rene Magritte');
INSERT INTO ART_OBJECT VALUES (20,1942,'Nighthawks','Oil painting','Realism','American  ','Edward Hopper');

INSERT INTO PAINTING VALUES (1,'Modern','Canvas','Oil');
INSERT INTO PAINTING VALUES (3,'Renaissance','Canvas','Oil'); 
INSERT INTO PAINTING VALUES (5,'Renaissance','Wall','Fresco');
INSERT INTO PAINTING VALUES (7,'Baroque','Canvas','Oil');
INSERT INTO PAINTING VALUES (10,'Street Art', 'Wall','Spray');
INSERT INTO PAINTING VALUES (11,'Dutch Golden Age' ,'Wall','Spray');
INSERT INTO PAINTING VALUES (12,'Expressionism' ,'Canvas','Oil');
INSERT INTO PAINTING VALUES (14,'Fauvism' ,'Canvas','Fresco');
INSERT INTO PAINTING VALUES (15,'Regionalism' ,'Canvas','Oil');
INSERT INTO PAINTING VALUES (16,'Surrealism' ,'Canvas','Oil');
INSERT INTO PAINTING VALUES (17,'Pre-Raphaelitism' ,'Canvas','Oil'); 
INSERT INTO PAINTING VALUES (18,'Surrealism' ,'Canvas','Oil');
INSERT INTO PAINTING VALUES (19,'Surrealism' ,'Wall','Oil');
INSERT INTO PAINTING VALUES (20,'Realism' ,'Canvas','Oil'); 

INSERT INTO SCULPTURE VALUES (4,'Modern', 1.2, 162,'Bronze');
INSERT INTO SCULPTURE VALUES (6,'Modern', 2.6, 460,'Bronze'); 
INSERT INTO SCULPTURE VALUES (13,'Neoclassicism', 1.75, 567,'Marble');

INSERT INTO OTHER VALUES (9 ,'Conceptual',' ');

INSERT INTO STATUE VALUES (2,'Renaissance',5.17, 635,'marble');
INSERT INTO STATUE VALUES (8,'Ancient',20,987,'marble');
 
INSERT INTO COLLECTION (NAME, ART_OBJ_ID, TYPE, DESCRIPTION, CONTACT_PERSON, PHONE, ADDRESS) 
VALUES ('Museum of modern art',1,'Painting','Collection of modern masterpieces','James','45699875',
'53rd St, New York, NY 10019');

INSERT INTO COLLECTION (NAME, ART_OBJ_ID, TYPE, DESCRIPTION, CONTACT_PERSON, PHONE, ADDRESS) 
VALUES ('National Gallery',3,'Painting','Collection of Impressionist masterpieces','Johnson','875535688',
'123main street, LONDON');

INSERT INTO COLLECTION (NAME, ART_OBJ_ID, TYPE, DESCRIPTION, CONTACT_PERSON, PHONE, ADDRESS) 
VALUES ('Metropolitan Museum',5,'Painting','Renaissance','Emily smith','44567932','456 Park Ave, NY, NY 10003');

INSERT INTO EXHIBITION VALUES('Paris international exhibition','2023-07-09','2023-01-14',1);
INSERT INTO EXHIBITION VALUES('Renaissance Masterpieces','2019-05-15','2019-07-24',2);
INSERT INTO EXHIBITION VALUES('Modern art show','2022-11-01','2022-12-01',4);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('01-01-2021', 'P01', 1, 200000, 1);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('05-04-2022', 'P02', 2, 150000, 2);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('16-09-2018', 'P03', 4, 100000, 4);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('22-11-2020', 'P04', 8, 340000, 8);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('17-03-2000', 'P05', 12, 100000, 12);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('29-01-2014', 'P06', 13, 88000, 13);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('09-06-2004', 'P07', 16, 150000, 16);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('30-05-2022', 'P08', 18, 230000, 18);

INSERT INTO PERMANENT_COLLECTION (DATE_AQUIRED, PERMANENT_ID, STATUS, COST, ART_OBJ_ID)
VALUES ('04-08-2003', 'P09', 20, 1200000, 20);

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B01', '15-12-2021', 3, '15-12-2020');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B02', '09-12-2018', 5, '08-04-2018');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B03', '05-05-2022', 6, '11-09-2019');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B04', '12-12-2020', 7, '12-09-2020');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B05', '25-12-2022', 9, '17-11-2015');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B06', '15-07-2015', 10, '09-09-2012');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B07', '11-05-2022', 11, '11-05-2020');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B08', '01-01-2023', 14, '14-04-2021');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B09', '05-05-2020', 15, '15-05-2005');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B10', '30-12-2022', 17, '23-12-2020');

INSERT INTO BORROWED_COLLECTION (BORROWED_ID, DATE_RETURNED, ART_OBJ_ID, DATE_BORROWED)
VALUES ('B11','01-02-2017',19,'19-06-2013');


```

###Query



