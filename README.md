# Creating insta-clone

# Create Tables

- CREATE TABLE users(userid SERIAL PRIMARY KEY NOT NULL, name VARCHAR NOT NULL);

- CREATE TABLE posts(postid SERIAL PRIMARY KEY NOT NULL, postcontent VARCHAR NOT NULL, postdate DATE NOT NULL DEFAULT CURRENT_DATE, userid SERIAL REFERENCES users(userid));

- 