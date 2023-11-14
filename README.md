# Creating insta-clone

# DDL Commands
# Create Tables


- CREATE TABLE users(userid SERIAL PRIMARY KEY NOT NULL, name VARCHAR NOT NULL);

- CREATE TABLE posts(postid SERIAL PRIMARY KEY NOT NULL, postcontent VARCHAR NOT NULL, postdate DATE NOT NULL DEFAULT CURRENT_DATE, userid SERIAL REFERENCES users(userid));

- CREATE TABLE likes(likeid SERIAL PRIMARY KEY NOT NULL, postid SERIAL REFERENCES posts(postid), userid SERIAL REFERENCES users(userid));

# Inserting values


- INSERT INTO users(name) VALUES('Edina'),('Colin'),('Glenda'),('Paula');

- INSERT INTO posts(postcontent, userid) VALUES('craft',1),('sale',1),('design',1),('tips',1),('lesson',1); INSERT INTO posts(postcontent, userid) VALUES('animal',2),('cartoon',2),('gift',2),('meme',2),('craft',2); INSERT INTO posts(postcontent, userid) VALUES('forest',3),('bikesale',3),('book',3),('award',3),('comedy',3); INSERT INTO posts(postcontent, userid) VALUES('gold',4),('awarness',4),('Experiments',4),('landsale',4),('tricks',4);

- INSERT INTO likes(postid, userid) VALUES(13, 3),(13,4),(13,1),(13,2),(14,1),(14,2),(15,4),(15,2), (17,3),(17,1),(19,3),(19,2),(1,4),(1,3),(4,3),(4,4),(4,2),(7,3),(7,4),(7,1),(7,2),(8,4), (8,1),(9,4),(9,1),(9,3);

# DML commands

Answers:

- list all users.
	SELECT * from users;

