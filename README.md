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

- list all posts.
	SELECT * from posts;

- List posts that are liked by colin .
	select posts.postcontent as likedByColin from posts left join likes on posts.postid = likes.postid where likes.userid = 2;


- As a Glenda, she wants to know who are all liked her post book. 
	select users.name as liked_glenda_post from users inner join likes on users.userid=likes.userid where likes.postid=13;


- Edina needs to know the post count which are liked by others. 
	SELECT COUNT(distinct posts.postid) FROM posts inner join likes on posts.postid = likes.postid where posts.userid = 1;

- Paula needs to check the count of awarness and trickes likes count.
	SELECT COUNT(likes.likeid)
	FROM likes where likes.postid = 17 or likes.postid=20;

- List Posts of Edina which has likes and also not liked posts.
	SELECT COUNT(likes.likeid) FROM likes where likes.postid = 17 or likes.postid=19;

- Search all users posts with Text "sal".
	SELECT * FROM posts WHERE postcontent LIKE '%sal%';


- Get the count of colin posts.
	SELECT COUNT(*) FROM posts WHERE userid = 2;

- Get count of likes for the post cartoon. user colin.
	select COUNT(likes.likeid) AS cartoon_likes from likes where likes.postid = 7;

- Get the maximum likes posts.
	select postid, count(postid) from likes GROUP BY postid HAVING COUNT(postid)>1 order by count(postid) desc limit 2;

- In Edina, sort posts by title in forward.
	select * from posts where userid=1 ORDER BY postcontent;

- In Paula, sort post by date backward.
	select * from posts where userid=4 ORDER BY postdate DESC;

- Filter today posted posts.
	select * from posts where postdate= 'today';


# University database


- CREATE TABLE university (
    university_id SERIAL PRIMARY KEY,
    university_name VARCHAR
);
CREATE TABLE college (
    college_id SERIAL PRIMARY KEY,
    college_name VARCHAR,
    university_id INTEGER REFERENCES university(university_id)
);
CREATE TABLE course (
    course_id SERIAL PRIMARY KEY,
    course_name VARCHAR
);
CREATE TABLE college_course (
    college_course_id SERIAL PRIMARY KEY,
    college_id INTEGER REFERENCES college(college_id),
    course_id INTEGER REFERENCES course(course_id)
);
create table subject(
subject_id serial primary key not null , subject_name VARCHAR not null);
