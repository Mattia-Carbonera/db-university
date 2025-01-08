1. Selezionare tutti gli studenti nati nel 1990 (160):

SELECT COUNT(`id`)
FROM `students`
WHERE YEAR(`date_of_birth`) = "1990";

---

2. Selezionare tutti i corsi che valgono più di 10 crediti (479):

SELECT COUNT(`id`)
FROM `courses`
WHERE `cfu` > "10";

---

3. Selezionare tutti gli studenti che hanno più di 30 anni:

SELECT \*
FROM `students`
WHERE (YEAR(curdate()) - YEAR(`date_of_birth`)) >= 30;

---

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286):

SELECT COUNT(`id`)
FROM `courses`
WHERE `year` = 1 AND `period` LIKE "I semestre";

---

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21):

SELECT COUNT(`id`)
FROM `exams`
WHERE DATE(`date`) = "2020-06-20" AND HOUR(`hour`) >= "14:00";

---

6. Selezionare tutti i corsi di laurea magistrale (38):

SELECT COUNT(`id`)
FROM `degrees`
WHERE `level` LIKE "magistrale";

---

7. Da quanti dipartimenti è composta l'università? (12):

SELECT COUNT(`id`) AS `number`
FROM `departments`;

---

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50):

SELECT COUNT(`id`)
FROM `teachers`
WHERE `phone` IS NOT NULL;

---

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
   degree_id, inserire un valore casuale):

INSERT INTO `db-university`.`students` (`id`, `degree_id`, `name`, `surname`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`, `email`) VALUES (5001, '51', 'Mattia', 'Carbonera', '1998-11-22', 'CRBMTT98S22B352D', '2020-10-07', '63122', 'mattia.carbonera@gmail.com')

---

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126:

UPDATE `teachers`
SET `office_number` = '126'
WHERE `id` = 58;

---

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9:

DELETE FROM `students`
WHERE `id` = 5001;

---
