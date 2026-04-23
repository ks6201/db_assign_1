# Assignment

### **P1: Data Modeling**

#### **Entities and Attributes**

1. **Theatre**
   * `theatre_id` (PK)
   * `name`
   * `location`

2. **Movie**
   * `movie_id` (PK)
   * `title`
   * `language`
   * `certificate`
   * `format`

3. **Shows**
   * `show_id` (PK)
   * `theatre_id` (FK)
   * `movie_id` (FK)
   * `show_date`
   * `show_time`
   * `screen`

---

### **P1: MySQL Tables**

```sql
CREATE TABLE theatre (
    theatre_id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    location VARCHAR(100)
);
```
![image](https://github.com/user-attachments/assets/a230a969-b208-426b-ba34-e4b4749389bb)

---

```sql
CREATE TABLE movie (
    movie_id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100) NOT NULL,
    language VARCHAR(50) NOT NULL,
    certificate ENUM('U', 'UA', 'A') NOT NULL,
    format ENUM('2D', '3D', 'IMAX') NOT NULL
);
```
![image](https://github.com/user-attachments/assets/4d3d5ecd-e3fd-434b-805c-652f7667810b)

---

```sql
CREATE TABLE shows (
    show_id INT PRIMARY KEY AUTO_INCREMENT,
    theatre_id INT NOT NULL,
    movie_id INT NOT NULL,
    show_date DATE NOT NULL,
    show_time TIME NOT NULL,
    screen VARCHAR(100),
    FOREIGN KEY (theatre_id) REFERENCES theatre(theatre_id),
    FOREIGN KEY (movie_id) REFERENCES movie(movie_id)
);
```
![image](https://github.com/user-attachments/assets/7657e480-117e-4951-9479-aa2d913fd69e)


---

### Sample Data

```sql
INSERT INTO theatre (name, location) VALUES
('PVR: Nexus', 'Forum Mall, Hyderabad');
```
![image](https://github.com/user-attachments/assets/f1c1483a-b698-40b9-8ba3-c2a5f01919ae)

---

```sql
INSERT INTO movie (title, language, certificate, format) VALUES
('Dasara', 'Telugu', 'UA', '2D'),
('Kisi Ka Bhai Kisi Ki Jaan', 'Hindi', 'UA', '2D'),
('Tu Jhoothi Main Makkaar', 'Hindi', 'UA', '2D'),
('Avatar: The Way of Water', 'English', 'UA', '3D');
```
![image](https://github.com/user-attachments/assets/b25a8c3a-abaf-4518-9921-541d3c7637b6)

---

```sql
INSERT INTO shows (theatre_id, movie_id, show_date, show_time, screen) VALUES
(1, 1, '2025-05-25', '12:15:00', '4K DOLBY'),
(1, 2, '2025-05-25', '13:00:00', '4K DOLBY'),
(1, 2, '2025-05-25', '16:10:00', '4K DOLBY'),
(1, 2, '2025-05-25', '18:20:00', '4K DOLBY'),
(1, 2, '2025-05-25', '19:20:00', '4K DOLBY'),
(1, 2, '2025-05-25', '22:30:00', '4K DOLBY'),
(1, 3, '2025-05-25', '13:15:00', '4K DOLBY'),
(1, 4, '2025-05-25', '13:20:00', 'Playhouse');
```
![image](https://github.com/user-attachments/assets/9ac6c4d3-d153-4de5-999a-bfb928543e88)

---

### **P2: Query to List All Shows on a Given Date at a Given Theatre**

```sql
SELECT 
    m.title AS movie_title,
    m.language,
    m.format,
    m.certificate,
    s.show_time,
    s.screen
FROM shows s
JOIN movie m ON s.movie_id = m.movie_id
JOIN theatre t ON s.theatre_id = t.theatre_id
WHERE s.show_date = '2025-05-25'
  AND t.name = 'PVR: Nexus';
```

![image](https://github.com/user-attachments/assets/a3a9d1a5-f0ac-4dad-b3f9-99f632d78748)
