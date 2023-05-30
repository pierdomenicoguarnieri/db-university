# **SOLUZIONI**

1. Selezionare tutti gli studenti nati nel 1990 (160) 

  ```sql
  SELECT *
  FROM `students`
  WHERE YEAR(`date_of_birth`) = 1990;
  ```
  - Oppure

  ```sql
  SELECT *
  FROM `students`
  WHERE `date_of_birth` LIKE '1990%';
  ```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

  ```sql
  SELECT *
  FROM `courses`
  WHERE `cfu` > 10;
  ```

3. Selezionare tutti gli studenti che hanno più di 30 anni

  ```sql
  SELECT *
  FROM `students`
  WHERE (2023 - YEAR(`date_of_birth`)) = 30;
  ```

  - Oppure

  ```sql
  SELECT *
  FROM `students`
  WHERE DATEDIFF(NOW(), `date_of_birth`)/365.25 > 30;
  ```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

  ```sql
  SELECT *
  FROM `courses`
  WHERE `period` = 'I semestre'
  AND `year` = 1;
  ```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

  ```sql
  SELECT *
  FROM `exams`
  WHERE HOUR(`hour`) >= 14
  AND `date` = '2020-06-20';
  ```

6. Selezionare tutti i corsi di laurea magistrale (38)

  ```sql
  SELECT *
  FROM `degrees`
  WHERE `level` = 'magistrale';
  ```

7. Da quanti dipartimenti è composta l'università? (12). 

  ```sql
  SELECT COUNT(*) AS `number_of_departments`
  FROM `departments`;
  ```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

  ```sql
  SELECT COUNT(*) AS `number_of_teachers_without_number`
  FROM `teachers`
  WHERE `phone` IS NULL;
  ```

## **BONUS**

1. Contare quanti iscritti ci sono stati ogni anno 

  ```sql
  SELECT COUNT(*) AS `number_of_students_for_year`, YEAR(`enrolment_date`) AS `enrolment_year`
  FROM `students`
  GROUP BY YEAR(`enrolment_date`);
  ```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

  ```sql
  SELECT COUNT(*) AS `number_of_teachers_with_same_address`, `office_address` AS `office_address`
  FROM `teachers`
  GROUP BY `office_address`
  ```

  - Oppure

  ```sql
  SELECT COUNT(*) AS `number_of_teachers_with_same_address`, `office_address` AS `office_address`
  FROM `teachers`
  GROUP BY `office_address`
  HAVING `number_of_teachers_with_same_address` <> 1;
  ```

3. Calcolare la media dei voti di ogni appello d'esame

  ```sql
  SELECT `exam_id`, AVG(`vote`) AS `average`
  FROM `exam_student`
  GROUP BY `exam_id`;
  ```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

  ```sql
  SELECT `department_id`, COUNT(*) AS `degree_number_for_department`
  FROM `degrees`
  GROUP BY `department_id`;
  ```