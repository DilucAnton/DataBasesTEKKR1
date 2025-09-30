# DataBasesTEKKR1

## С помощью текущего кода добавим схему базы данных в PG ADMIN

<img width="809" height="432" alt="Снимок экрана 2025-09-30 в 21 50 57" src="https://github.com/user-attachments/assets/18e4eaeb-383a-44c2-8329-c518b97a3843" />


```
CREATE TABLE department (
department_id SERIAL PRIMARY KEY,
name_department VARCHAR(30)
);
INSERT INTO department (`department_id`, `name_department`)
VALUES (1, 'Инженерная школа'), (2, 'Школа естественных наук');

CREATE TABLE subject (
subject_id SERIAL PRIMARY KEY,
name_subject VARCHAR(30)
);
INSERT INTO subject (name_subject)
VALUES ('Русский язык'), ('Математика'), ('Физика'), ('Информатика');

CREATE TABLE program (
program_id SERIAL PRIMARY KEY,
name_program VARCHAR(50),
department_id INT,
plan INT,
FOREIGN KEY (department_id) REFERENCES department(department_id) ON DELETE CASCADE
);

INSERT INTO program (name_program, department_id, plan)
VALUES ('Прикладная математика и информатика', 2, 2),
('Математика и компьютерные науки', 2, 1),
('Прикладная механика', 1, 2),
('Мехатроника и робототехника', 1, 3);

CREATE TABLE enrollee (
enrollee_id SERIAL PRIMARY KEY,
name_enrollee VARCHAR(50)
);

INSERT INTO enrollee (name_enrollee)
VALUES ('Баранов Павел'), ('Абрамова Катя'), ('Семенов Иван'),
('Яковлева Галина'), ('Попов Илья'), ('Степанова Дарья');

CREATE TABLE achievement (
achievement_id SERIAL PRIMARY KEY,
name_achievement VARCHAR(30),
bonus INT
);

INSERT INTO achievement (name_achievement, bonus)
VALUES ('Золотая медаль', 5), ('Серебряная медаль', 3),
    ('Золотой значок ГТО', 3), ('Серебряный значок ГТО', 1);

CREATE TABLE enrollee_achievement (
enrollee_achiev_id SERIAL PRIMARY KEY,
enrollee_id INT,
achievement_id INT,
FOREIGN KEY (enrollee_id) REFERENCES enrollee(enrollee_id) ON DELETE CASCADE,
FOREIGN KEY (achievement_id) REFERENCES achievement(achievement_id) ON DELETE CASCADE
);

INSERT INTO enrollee_achievement (enrollee_id, achievement_id)
VALUES (1, 2), (1, 3), (3, 1), (4, 4), (5, 1),(5, 3);

CREATE TABLE program_subject (
program_subject_id SERIAL PRIMARY KEY,
program_id INT,
subject_id INT,
min_result INT,
FOREIGN KEY (program_id) REFERENCES program(program_id)  ON DELETE CASCADE,
FOREIGN KEY (subject_id) REFERENCES subject(subject_id) ON DELETE CASCADE
);

INSERT INTO program_subject (program_id, subject_id, min_result)
VALUES (1, 1, 40),(1, 2, 50), (1, 4, 60), ( 2, 1, 30),
       (2, 2, 50),(2, 4, 60), (3, 1, 30),(3, 2, 45),
       (3, 3, 45),(4, 1, 40), (4, 2, 45), (4, 3, 45);

CREATE TABLE program_enrollee (
program_enrollee_id SERIAl PRIMARY KEY,
program_id INT,
enrollee_id INT,
FOREIGN KEY (program_id) REFERENCES program(program_id) ON DELETE CASCADE,
FOREIGN KEY (enrollee_id) REFERENCES enrollee(enrollee_id) ON DELETE CASCADE
);

INSERT INTO program_enrollee (program_id, enrollee_id)
VALUES (3, 1), (4, 1), (1, 1), (2, 2), (1, 2),
       (1, 3), (2, 3), (4, 3), (3, 4), (3, 5),
       (4, 5), (2, 6), (3, 6), (4, 6);

CREATE TABLE enrollee_subject (
enrollee_subject_id SERIAL PRIMARY KEY,
enrollee_id INT,
subject_id INT,
result INT,
FOREIGN KEY (enrollee_id) REFERENCES enrollee(enrollee_id) ON DELETE CASCADE,
FOREIGN KEY (subject_id) REFERENCES subject (subject_id) ON DELETE CASCADE
);

INSERT INTO enrollee_subject (enrollee_id, subject_id, result)
VALUES (1, 1, 68), (1, 2, 70), (1, 3, 41), (1, 4, 75), (2, 1, 75), (2, 2, 70),
       (2, 4, 81), (3, 1, 85), (3, 2, 67), (3, 3, 90), (3, 4, 78), (4, 1, 82),
       (4, 2, 86), (4, 3, 70), (5, 1, 65), (5, 2, 67), (5, 3, 60),
       (6, 1, 90), (6, 2, 92), (6, 3, 88), (6, 4, 94);
```



<img width="1245" height="695" alt="Снимок экрана 2025-09-30 в 21 51 25" src="https://github.com/user-attachments/assets/e7ee78d1-55dc-4ba6-be78-9038eb8ce178" />

### 1. Вывести абитуриентов, которые хотят поступать на определенную образовательную программу


<img width="1318" height="1342" alt="image" src="https://github.com/user-attachments/assets/2a7b12a7-a4b3-4c3c-9e0b-c1d5f5fb28a1" />

### 2. Вывести образовательные программы, на которые для поступления необходим определенный предмет ЕГЭ.

<img width="650" height="651" alt="Снимок экрана 2025-09-30 в 22 00 09" src="https://github.com/user-attachments/assets/b8d5f1b1-4993-4d44-b0ef-a46beffaa37f" />

### 3. Вывести статистическую информацию по каждому предмету ЕГЭ (минимальный и максимальный балл, количество абитуриентов, которые этот предмет сдавали).
<img width="779" height="683" alt="Снимок экрана 2025-09-30 в 22 00 37" src="https://github.com/user-attachments/assets/c7b95757-423e-4283-9f7c-7336a675dfef" />


### 4. Вывести образовательные программы, минимальные баллы по каждому предмету которых, превышают заданное значение.
<img width="674" height="612" alt="Снимок экрана 2025-09-30 в 22 02 22" src="https://github.com/user-attachments/assets/1ceb1ac1-165b-46f9-a99a-268262e5b182" />


### 5. Вывести образовательные программы. которые имеют самый большой план набора.

<img width="559" height="602" alt="Снимок экрана 2025-09-30 в 22 03 02" src="https://github.com/user-attachments/assets/7477fdcb-6859-48f7-83ad-d52ffb014c2e" />

### 6. Посчитать, сколько дополнительных баллов получит каждый абитуриент.

<img width="830" height="703" alt="Снимок экрана 2025-09-30 в 22 04 30" src="https://github.com/user-attachments/assets/b7495093-206c-4891-a255-0404aeff77cb" />

### 7. Посчитать конкурс на каждую образовательную программу.

<img width="830" height="660" alt="Снимок экрана 2025-09-30 в 22 05 07" src="https://github.com/user-attachments/assets/40c6f126-57af-4d88-86a3-43c95a1b5175" />

### 8. Вывести образовательные программы, на которые для поступления необходимы два определенных предмета ЕГЭ.

<img width="676" height="658" alt="Снимок экрана 2025-09-30 в 22 06 26" src="https://github.com/user-attachments/assets/7d96f7c5-dab1-4034-b3c4-791a62fd609b" />

### 9. Посчитать количество баллов каждого абитуриента на каждую образовательную программу по результатам ЕГЭ.

<img width="815" height="747" alt="Снимок экрана 2025-09-30 в 22 06 58" src="https://github.com/user-attachments/assets/8f593e47-fda9-45f2-82d7-2737412c37ad" />

### 10. Вывести абитуриентов, которые не могут быть зачислены на образовательную программу.

<img width="886" height="623" alt="Снимок экрана 2025-09-30 в 22 08 07" src="https://github.com/user-attachments/assets/1c717428-88c2-48ef-b5a9-0412a401fb80" />

### 11. Создается таблица с суммой баллов абитуриентов по предметам ЕГЭ в соответствии с поданными заявлениями.

<img width="846" height="652" alt="Снимок экрана 2025-09-30 в 22 10 51" src="https://github.com/user-attachments/assets/4d448e21-1269-4ef6-8eb3-24a42127d88a" />


### 12. Из таблицы удаляются абитуриенты, если они не набрали минимального балла по предмету, необходимому для поступления на образовательную программу.

<img width="643" height="624" alt="Снимок экрана 2025-09-30 в 22 11 59" src="https://github.com/user-attachments/assets/8f9bb4ad-3292-4018-9373-e3ceeab3c4bc" />

### 13. Абитуриентам, у которых есть медаль или значок ГТО, добавляются дополнительные баллы.

<img width="798" height="736" alt="Снимок экрана 2025-09-30 в 22 13 21" src="https://github.com/user-attachments/assets/1786a960-d459-407a-bd9a-2c484de7e78c" />

### 14. Абитуриенты сортируются в соответствии с набранными баллами по каждой образовательной программе;
<img width="572" height="746" alt="Снимок экрана 2025-09-30 в 22 15 36" src="https://github.com/user-attachments/assets/8eca18ab-ae1b-4285-8fb8-0fac92aee66f" />


### 15. Формируется список абитуриентов, рекомендованных к зачислению ( вставляется столбец для нумерации, осуществляется нумерация студентов по образовательной программе, выбираются абитуриенты с наибольшими баллами в соответствии с планом набора).


<img width="746" height="746" alt="Снимок экрана 2025-09-30 в 22 17 15" src="https://github.com/user-attachments/assets/7fd48ab2-abb5-4341-abeb-d7db63fe9681" />


