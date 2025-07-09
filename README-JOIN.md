<!-- Join: -->

<!-- 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia  -->
<!-- Le tabelle collegate sono students e degrees e la condizione è che il .name di degrees sia 'Corso di Laurea in Economia' -->

SELECT 
`students`.`name` AS `student_name`,
`students`.`surname`,
`students`.`fiscal_code`,
`students`.`registration_number`,
`students`.`enrolment_date`,
`students`.`email`,
`degrees`.`name` AS `degree_name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id`= `degrees`.`id`
WHERE `degrees`.`name`= 'Corso di Laurea in Economia';

<!-- 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze  -->
<!-- Le tabelle collegate sono departments e degrees e la condizione è che il .name di departments sia 'Dipartimento di Neuroscienze' e che il . level di degrees sia 'magistrale'-->

SELECT
`degrees`.`name`,
`degrees`.`level`,
`degrees`.`address`,
`degrees`.`email`,
`degrees`.`website`,
`departments`.`name`
FROM `departments`
JOIN `degrees`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale';

<!-- 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)  -->
<!-- Le tabelle collegate sono teachers, courses e course_teacher e la condizione è che il .id di teachers sia 44 -->

SELECT
`courses`.`name`,
`courses`.`description`,
`courses`.`period`,
`courses`.`year`,
`courses`.`cfu`,
`courses`.`website`,
`teachers`.`name`,
`teachers`.`surname`,
`teachers`.`email`,
`teachers`.`office_address`,
`teachers`.`office_number`
FROM `teachers`
JOIN `course_teacher`
ON `course_teacher`.`teacher_id`= `teachers`.`id`
JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44;

<!-- 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome  -->
<!-- Le tabelle collegsate sono students, degrees e departments e i dati sono ordinati tramite order by tramite students.surname e successivamente tramite students.name -->

SELECT 
`students`.`surname` AS `student_surname`,
`students`.`name` AS `student_name`,
`students`.`date_of_birth`,
`students`.`fiscal_code`,
`students`.`enrolment_date`,
`students`.`registration_number`,
`students`.`email`,
`degrees`.`name`,
`degrees`.`level`,
`degrees`.`address`,
`degrees`.`email`,
`degrees`.`website`,
`departments`.`name`,
`departments`.`address`,
`departments`.`phone`,
`departments`.`email`,
`departments`.`website`,
`departments`.`head_of_department`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `student_surname`, `student_name`;

<!-- 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti  -->
<!-- Le tabelle collegate sono degrees, courses, course_teacher e teachers -->

SELECT
`degrees`.`name`,
`degrees`.`level`,
`degrees`.`address`,
`degrees`.`email`,
`degrees`.`website`,
`courses`.`name`,
`courses`.`description`,
`courses`.`period`,
`courses`.`year`,
`courses`.`cfu`,
`courses`.`website`,
`teachers`.`name`,
`teachers`.`surname`,
`teachers`.`phone`,
`teachers`.`email`,
`teachers`.`office_address`,
`teachers`.`office_number`
FROM `degrees`
JOIN `courses`
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `course_teacher`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`;

<!-- 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)  -->
<!-- Le tabelle collegate sono (esageratamente tante) -->

SELECT
`teachers`.*,
`departments`.`name`
FROM `teachers`
JOIN `course_teacher`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';

<!-- 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18. -->
