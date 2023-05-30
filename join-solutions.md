# **SOLUZIONI**

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

  ```sql
  SELECT `students`.`id`, `students`.`name`, `students`.`surname`, `students`.`registration_number`
  FROM `degrees`
  INNER JOIN `students`
  ON `degrees`.`id` = `students`.`degree_id`
  WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
  ```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

  ```sql
  SELECT `degrees`.`id`, `degrees`.`name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`
  FROM `departments`
  INNER JOIN `degrees`
  ON `departments`.`id` = `degrees`.`department_id`
  WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
  AND `degrees`.`level` = 'magistrale';
  ```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

  ```sql
  SELECT `courses`.`id`, `courses`.`name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`
  FROM `courses`
  INNER JOIN `course_teacher`
  ON `courses`.`id` = `course_teacher`.`course_id`
  INNER JOIN `teachers`
  ON `teachers`.`id` = `course_teacher`.`teacher_id`
  WHERE `teachers`.`id` = 44;
  ```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

  ```sql
  SELECT `students`.`id`, `students`.`surname`, `students`.`name`, `students`.`date_of_birth`, `students`.`email`, `students`.`registration_number`, `departments`.`name`, `degrees`.`name`
  FROM `departments`
  INNER JOIN `degrees`
  ON `departments`.`id` = `degrees`.`department_id`
  INNER JOIN `students`
  ON `degrees`.`id` = `students`.`degree_id`
  ORDER BY `students`.`surname`, `students`.`name`;
  ```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

  ```sql
  SELECT `degrees`.`id` AS `degree_id`, `degrees`.`name` AS `degree.name`, `degrees`.`level`, `courses`.`name` AS `course_name`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname`, `teachers`.`phone`, `teachers`.`email`
  FROM `degrees`
  INNER JOIN `courses`
  ON `degrees`.`id` = `courses`.`degree_id`
  INNER JOIN  `course_teacher`
  ON `courses`.`id` = `course_teacher`.`course_id`
  INNER JOIN `teachers`
  ON `teachers`.`id` = `course_teacher`.`teacher_id`;
  ```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

  ```sql
  SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`, `teachers`.`phone`, `teachers`.`email`
  FROM `departments`
  INNER JOIN `degrees`
  ON `departments`.`id` = `degrees`.`department_id`
  INNER JOIN `courses`
  ON `degrees`.`id` = `courses`.`degree_id`
  INNER JOIN  `course_teacher`
  ON `courses`.`id` = `course_teacher`.`course_id`
  INNER JOIN `teachers`
  ON `teachers`.`id` = `course_teacher`.`teacher_id`
  WHERE `departments`.`name` = 'Dipartimento di Matematica';
  ```

7. Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

  ```sql
  SELECT `exams`.`id` AS `exam_id`, COUNT(`exam_student`.`exam_id`) AS `tries`, MAX(`exam_student`.`vote`) AS ``, `exam_student`.`student_id`, `students`.`name`, `students`.`surname`
  FROM `exams`
  INNER JOIN `exam_student`
  ON `exams`.`id` = `exam_student`.`exam_id`
  INNER JOIN `students`
  ON `students`.`id` = `exam_student`.`student_id`
  GROUP BY `exam_student`.`student_id`
  ORDER BY `exams`.`id`;
  ```

  - Filtrando con voti >= 18

  ```sql
  SELECT `exams`.`id` AS `exam_id`, COUNT(`exam_student`.`exam_id`) AS `tries`, MAX(`exam_student`.`vote`) AS ``, `exam_student`.`student_id`, `students`.`name`, `students`.`surname`
  FROM `exams`
  INNER JOIN `exam_student`
  ON `exams`.`id` = `exam_student`.`exam_id`
  INNER JOIN `students`
  ON `students`.`id` = `exam_student`.`student_id`
  WHERE `exam_student`.`vote` >= 18
  GROUP BY `exam_student`.`student_id`
  ORDER BY `exams`.`id`;
  ```