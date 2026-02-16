# Schema Database Universita 

| Entita (tabella) | Colonne (con tipi) | Relazioni |
| --- | --- | --- |
| Dipartimenti (DEPARTMENTS) | id INT (PK), name VARCHAR(100), address VARCHAR(255), phone VARCHAR(20), email VARCHAR(100) | 1:N con DEGREE_COURSES (department_id) |
| Corsi di laurea (DEGREE_COURSES) | id INT (PK), name VARCHAR(150), level ENUM('L','LM','LMC'), duration_years INT, website VARCHAR(255), department_id INT (FK) | N:1 con DEPARTMENTS; 1:N con COURSES (degree_course_id); 1:N con STUDENTS (degree_course_id) |
| Corsi (COURSES) | id INT (PK), name VARCHAR(100), description TEXT, cfu INT, year INT, degree_course_id INT (FK) | N:1 con DEGREE_COURSES; 1:N con EXAMS (course_id); N:M con TEACHERS via COURSE_TEACHER |
| Docenti (TEACHERS) | id INT (PK), name VARCHAR(50), surname VARCHAR(50), email VARCHAR(100), phone VARCHAR(20), office VARCHAR(50) | N:M con COURSES via COURSE_TEACHER |
| Corso - docente (COURSE_TEACHER) | id INT (PK), course_id INT (FK), teacher_id INT (FK) | N:1 con COURSES; N:1 con TEACHERS |
| Studenti (STUDENTS) | id INT (PK), registration_number VARCHAR(20), name VARCHAR(50), surname VARCHAR(50), email VARCHAR(100), date_of_birth DATE, enrollment_date DATE, degree_course_id INT (FK) | N:1 con DEGREE_COURSES; N:M con EXAMS via EXAM_ENROLLMENTS |
| Appelli d'esame (EXAMS) | id INT (PK), date DATE, time TIME, course_id INT (FK) | N:1 con COURSES; 1:N con EXAM_ENROLLMENTS (exam_id) |
| Iscrizioni esami (EXAM_ENROLLMENTS) | id INT (PK), student_id INT (FK), exam_id INT (FK), grade INT | N:1 con STUDENTS; N:1 con EXAMS |
