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


CREATE TABLE university (
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
CREATE TABLE course_subject (
    course_subject_id SERIAL PRIMARY KEY NOT NULL,
    college_course_id INTEGER REFERENCES college_course (college_course_id),
    subject_id INTEGER REFERENCES subject(subject_id)
);

create table semester(semester_id  SERIAL PRIMARY KEY NOT NULL, month VARCHAR NOT null,year INTEGER NOT null);
create table student(student_id serial primary key not null,student_name VARCHAR not null, course_subject_id INTEGER REFERENCES course_subject (course_subject_id));
create table marks(mark_id serial primary key not null,student_id integer references student(student_id),semester_id integer references semester(semester_id),marks integer)




alter table marks add subject_id integer REFERENCES subject(subject_id);
alter table student add dob integer ;
ALTER TABLE student
ADD phone integer;
ALTER TABLE student
ADD address VARCHAR;
ALTER TABLE student
ADD year_of_join date;
alter table student
drop column course_subject_id;
alter table student
add column college_course_id INTEGER REFERENCES college_course (college_course_id);
--alter table student
--drop column year_join;
alter table student
drop column college_course_id;
ALTER TABLE student
add column college_id INTEGER REFERENCES college(college_id);
ALTER TABLE student
add column course_id INTEGER REFERENCES course(course_id);
alter table course_subject
drop column college_course_id;
ALTER TABLE course_subject
add column course_id INTEGER REFERENCES course(course_id);


--insert 

insert into university ( university_name ) values ('pondicherry university;')

insert into college (college_name, university_id) values('rajiv gandhi college of engineering and technology',1);
insert into college (college_name, university_id) values('Ganesh college college of enginering',1),
('manakula vinayagar institute of technology',1),
('venkateshwara engineering pondicherry',1),
('puducherry technological university',1);

insert into course (course_name) values ('computer science engineering'),('electrical and electronics engineering'),
('electrical and computer engineering'),('mechanical engineering'),('information technology engineering');

insert into subject (subject_name) values('computer programming'),('maths1'),('termodynamics'),('physics'),('chemistry'),('electrical and electronics');
insert into subject (subject_name) values('engineering mechanics'),('data base'),('cloud computing'),('artificial intelligence ');



insert into college_course (college_id,course_id) values(1,1),(1,2),(1,3),(1,4),(1,5);
insert into college_course (college_id,course_id) values(2,1),(2,2),(2,3),(2,4),(2,5);
insert into college_course (college_id,course_id) values(3,1),(3,2),(3,3),(3,4),(3,5);
insert into college_course (college_id,course_id) values(4,1),(4,2),(4,3),(4,4),(4,5);
insert into college_course (college_id,course_id) values(5,1),(5,2),(5,3),(5,4),(5,5);

insert into course_subject(subject_id,course_id) values(1,1),(2,1),(8,1),(9,1),(10,1),(2,2),(4,2),(5,2),(6,2),(7,2),(2,3),(3,3),(5,3),(6,3),(7,3),
(2,4),(3,4),(5,4),(6,4),(7,4),(1,5),(2,5),(8,5),(9,5),(10,5);


alter table semester rename "month" to "sem_month";
alter table semester rename "year" to "sem_year";


insert into semester(sem_month,sem_year)
values ('april',2023);


ALTER TABLE student
ALTER COLUMN phone
TYPE bigint;

ALTER TABLE student
drop column year_of_join;

ALTER TABLE student
add column year_joined integer;


ALTER TABLE student
drop column dob;

	ALTER TABLE student
	add column d_o_b date;





INSERT INTO public.student (student_name,phone,address,college_id,course_id,year_joined,d_o_b) VALUES
	 ('Rin',9092434586,'Puducherry',1,1,2022,'2001-04-11'),
	 ('Naruto',9392434596,'Puducherry',2,2,2022,'2001-03-03'),
	 ('Sakura',9876453765,'Puducherry',3,3,2022,'2000-11-04'),
	 ('Sasuke',8765897654,'Puducherry',4,4,2022,'2001-07-19'),
	 ('Itachi',6876543278,'Leaf village',5,5,2022,'2001-12-01');
	 
	
	
INSERT INTO public.marks (student_id,semester_id,marks,subject_id) VALUES
	 (1,1,95,1),
	 (1,1,93,2),
	 (1,1,89,8),
	 (1,1,93,9),
	 (1,1,89,10),
	 (2,1,53,4),
	 (2,1,59,5),
	 (2,1,65,6),
	 (2,1,76,7),
	 (2,1,75,2);
INSERT INTO public.marks (student_id,semester_id,marks,subject_id) VALUES
	 (3,1,100,2),
	 (3,1,99,3),
	 (3,1,98,5),
	 (3,1,100,6),
	 (3,1,100,7),
	 (4,1,30,2),
	 (4,1,40,3),
	 (4,1,68,5),
	 (4,1,90,6),
	 (4,1,100,7);
INSERT INTO public.marks (student_id,semester_id,marks,subject_id) VALUES
	 (5,1,40,1),
	 (5,1,50,2),
	 (5,1,60,8),
	 (5,1,70,9),
	 (5,1,60,10);
	
	Task - 1
----------
- Build a University students ranking system database.
- University will have multiple colleges
- Each college will have many courses,
- Each Courses will have many subject
- The university follows semester pattern
- Need to store the marks for each subject , semester wise
- design the table structure and relationships
- feed necessary data to query the output

- completed first task

Task - 2
----------
Querys
------
- get students count college wise

	- SELECT c.college_name, COUNT(s.student_id) AS student_count
FROM college c
JOIN student s ON c.college_id = s.college_id
GROUP BY c.college_name;

	(or)

SELECT
    c.college_name,
    (
        SELECT COUNT(*)
        FROM student s
        WHERE s.college_id = c.college_id
    ) AS student_count
FROM college c;


- get students count in a college, course wise
- get the university rank holder across all courses(1 student)
- get the list of rank holders each course
- get the college topper across all courses
- get the college toppers each course
- get the failed students count each subject 
- get over all students list with semester marks
- get the student list who wasnt appear to the exams
	
	
	
	
	
	
	
	
	
	
	