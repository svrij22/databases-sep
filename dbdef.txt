-- Named .SQL so that Visual Studio recognized the file

-- SQL DDL for 'User' table
CREATE TABLE User (
    userid      INT (10),
    userName    VARCHAR (255),
    password    VARCHAR (255),
    email       VARCHAR (255),
    dateOfBirth DATE,
    joinDate    DATE,
    PRIMARY KEY (
        userid
    )
);

-- SQL DDL for 'Game' table
CREATE TABLE IF NOT EXISTS Game (
    gameid INT(10),
    publisherid INT(10),
    name VARCHAR(255),
    description VARCHAR(255),
    releaseDate DATE,
    PRIMARY KEY (gameid),
    FOREIGN KEY (publisherid) REFERENCES Publisher(publisherid)
);

-- SQL DDL for 'Publisher' table
CREATE TABLE IF NOT EXISTS Publisher (
    publisherid INT(10),
    name VARCHAR(255),
    PRIMARY KEY (publisherid)
);

-- SQL DDL for 'Review' table
CREATE TABLE IF NOT EXISTS Review (
    reviewid INT(10),
    userid INT(10),
    gameid INT(10),
    rating FLOAT,
    comment VARCHAR(1000),
    reviewDate DATE,
    PRIMARY KEY (reviewid),
    FOREIGN KEY (userid) REFERENCES User(userid),
    FOREIGN KEY (gameid) REFERENCES Game(gameid)
);

-- SQL DDL for 'Genre' table
CREATE TABLE IF NOT EXISTS Genre (
    genreid INT(10),
    name VARCHAR(255),
    description VARCHAR(255),
    PRIMARY KEY (genreid)
);

-- SQL DDL for 'Library' table
CREATE TABLE IF NOT EXISTS Library (
    libraryid INT(10),
    userid INT(10),
    PRIMARY KEY (libraryid),
    FOREIGN KEY (userid) REFERENCES User(userid)
);

-- SQL DDL for 'Game_Library' junction table
CREATE TABLE IF NOT EXISTS Game_Library (
    gameid INT(10),
    libraryid INT(10),
    FOREIGN KEY (gameid) REFERENCES Game(gameid),
    FOREIGN KEY (libraryid) REFERENCES Library(libraryid)
);

-- SQL DDL for 'Genre' table
CREATE TABLE IF NOT EXISTS Genre (
    genreid INT(10),
    name VARCHAR(255),
    description VARCHAR(255),
    PRIMARY KEY (genreid)
);

-- SQL DDL for 'Game_Genre' junction table
CREATE TABLE IF NOT EXISTS Game_Genre (
    gameid INT(10),
    genreid INT(10),
    FOREIGN KEY (gameid) REFERENCES Game(gameid),
    FOREIGN KEY (genreid) REFERENCES Genre(genreid)
);

-- SQL DDL for 'Platform' table
CREATE TABLE IF NOT EXISTS Platform (
    platformid INT(10),
    name VARCHAR(255),
    description VARCHAR(255),
    publicationDate DATE,
    PRIMARY KEY (platformid)
);

-- SQL DDL for 'Game_Platform' junction table
CREATE TABLE IF NOT EXISTS Game_Platform (
    gameid INT(10),
    platformid INT(10),
    FOREIGN KEY (gameid) REFERENCES Game(gameid),
    FOREIGN KEY (platformid) REFERENCES Platform(platformid)
);

-- SQL DDL for 'DLC' table
CREATE TABLE IF NOT EXISTS DLC (
    DLCid INT(10),
    gameid INT(10),
    name VARCHAR(255),
    description VARCHAR(255),
    releaseDate DATE,
    price FLOAT(10),
    PRIMARY KEY (DLCid),
    FOREIGN KEY (gameid) REFERENCES Game(gameid)
);

-- SQL DDL for 'Contributor' table
CREATE TABLE IF NOT EXISTS Contributor (
    contributorid INT(10),
    publisherid INT(10),
    name VARCHAR(255),
    PRIMARY KEY (contributorid),
    FOREIGN KEY (publisherid) REFERENCES Publisher(publisherid)
);

-- SQL DDL for 'Contributor_Game' junction table
CREATE TABLE IF NOT EXISTS Contributor_Game (
    gameid INT(10),
    contributorid INT(10),
    FOREIGN KEY (gameid) REFERENCES Game(gameid),
    FOREIGN KEY (contributorid) REFERENCES Contributor(contributorid)
);

-- SQL DDL for 'Developer', 'Artist', 'Composer', and 'Designer' tables

CREATE TABLE IF NOT EXISTS Developer (
    developerid INT(10),
    PRIMARY KEY (developerid),
    FOREIGN KEY (developerid) REFERENCES Contributor(contributorid)
);

CREATE TABLE IF NOT EXISTS Artist (
    artistid INT(10),
    PRIMARY KEY (artistid),
    FOREIGN KEY (artistid) REFERENCES Contributor(contributorid)
);

CREATE TABLE IF NOT EXISTS Composer (
    composerid INT(10),
    PRIMARY KEY (composerid),
    FOREIGN KEY (composerid) REFERENCES Contributor(contributorid)
);

CREATE TABLE IF NOT EXISTS Designer (
    designerid INT(10),
    PRIMARY KEY (designerid),
    FOREIGN KEY (designerid) REFERENCES Contributor(contributorid)
);