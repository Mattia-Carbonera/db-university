1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT
`students`.`id` AS `student_id`,
`students`.`name` AS `student_name`,
`students`.`surname` AS `student_surname`,
`degrees`.`name` AS `degrees_name`

FROM `students`

INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`

WHERE `degrees`.`id` = 53;

---

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

SELECT
`departments`.`id` AS `departments_id`,
`departments`.`name` AS `departments_name`,
`degrees`.`id` AS `degrees_id`,
`degrees`.`name` AS `degrees_name`

FROM `departments`

INNER JOIN `degrees`
ON `departments`.`id` = `degrees`.`department_id`

WHERE
`departments`.`name` = 'Dipartimento di Neuroscienze' AND
`degrees`.`level` = 'magistrale';

---

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT
`courses`.`id` AS `courses_id`,
`courses`.`name` AS `courses_name`,
`teachers`.`name` AS `teachers_name`,
`teachers`.`surname` AS `teachers_surname`

FROM `courses`

INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`

INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`

WHERE `teachers`.`id` = 44;

---

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome

SELECT
`students`._,
`degrees`._,
`departments`.`name` AS `departments_name`

FROM `students`

INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`

INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`

ORDER BY
`students`.`surname`,
`students`.`name`;

---

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT
`courses`.`id` AS `course_id`,
`courses`.`name` AS `course_name`,
`degrees`.`name` AS `degree_name`,
`teachers`.`name` AS `teachers_name`,
`teachers`.`surname` AS `teachers_surname`

FROM `degrees`

INNER JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`

INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`

INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`

---

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

SELECT
`teachers`.`id` AS `teacher_id`,
`teachers`.`name` AS `teacher_name`,
`teachers`.`surname` AS `teacher_surname`,
`departments`.`name` AS `department_name`

FROM `university`.`teachers`

JOIN `university`.`course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`

JOIN `university`.`courses`
ON `course_teacher`.`course_id` = `courses`.`id`

JOIN `university`.`degrees`
ON `degrees`.`id` = `courses`.`degree_id`

JOIN `university`.`departments`
ON `departments`.`id` = `degrees`.`department_id`

WHERE `departments`.`name` = "Dipartimento di Matematica"
GROUP BY `teachers`.`id`;

---

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

SELECT
`exam_student`.`student_id`,
`students`.`name` AS `student_name`,
`students`.`surname` AS `student_surname`,

COUNT(`exam_student`.`vote`) AS `attempts`,
MAX(`exam_student`.`vote`) AS `vote_max`

FROM `exam_student`

JOIN `students`
ON `students`.`id` = `exam_student`.`student_id`

WHERE `exam_student`.`vote` >= 18
GROUP BY `exam_student`.`student_id`;

---
