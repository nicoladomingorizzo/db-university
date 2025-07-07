# db-university

- Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi `Dipartimenti` (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni `Dipartimento` offre più `Corsi di Laurea` (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni `Corso di Laurea` prevede diversi `Corsi` (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni `Corso` può essere tenuto da diversi `Insegnanti`;
- ogni `Corso` prevede più appelli d'`Esame`;
- ogni `Studente` è iscritto ad un solo `Corso di Laurea`;
- ogni `Studente` può iscriversi a più appelli di `Esame`;
- per ogni appello d'`Esame` a cui lo `Studente` ha partecipato, è necessario memorizzare il `voto ottenuto`, anche se non sufficiente.
<!-- Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.
Utilizzare https://www.drawio.com/ per la creazione dello schema.
Esportare quindi il diagramma in pnge caricarlo nella repo come visto in classe -->

## Entity
- deparment
~~- course~~
- teacher
- exam
- student

## Tables

- deparments
- teachers
~~- courses~~
- exams
- students

### departments (primary)

- id
- address_department

#### courses (secondary)

- id
- department_id
- address_course

##### detail_course (secondary+)

- id
- course_id
- address_detail_course

### teachers (primary)

- id
- name
- lastname

#### detail_teacher (secondary)

- id
- teacher_id
- role
- subject

### exams (primary)

- id
- name

### students (primary)

- id
- name
- lastname

#### detail_student (secondary)

- id
- student_id
- address
- mobile
- email
- courses

### pivot: detail_exam

- id
- student_id
- exam_id
- vote


### student_vote (secondary)

- id
- student_id
- course_id
- vote