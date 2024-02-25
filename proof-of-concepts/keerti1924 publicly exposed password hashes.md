## Vulnerability Details

**Credits**: Reigz Macolor (https://github.com/reigz/)<br/>
**Tested On**: PHP-MYSQL-User-Login-System <https://github.com/keerti1924/PHP-MYSQL-User-Login-System><br/>
**Affected Version**: keerti1924/PHP-MYSQL-User-Login-System 1.0

**Affected Site Page**: /login.php<br/>
**Affected Code**: <https://github.com/keerti1924/PHP-MYSQL-User-Login-System/blob/main/login.sql> <br/>
CWE-540: Inclusion of Sensitive Information in Source Code

## **Details:**
Exposed Login Credentials containing username, email, and passwords on the GitHub Page (hashes redacted by me for responsible disclosure).

```SQL 
INSERT INTO `users` (`id`, `username`, `email`, `password`) VALUES
(1, 'Ajay Kumar', 'ajay@gmail.com', '12***'),
(2, 'Amit', 'amit@gmail.com', '12**'),
(3, 'Keerti Panwar', 'keerti@gmail.com', '$2y$10$g******************lDntZ7ZXDD*********'),
(4, 'Ankita', 'ankita@gmail.com', '$2y$10$ZuW****************************pyEyRhtK'),
(5, 'Keerti Panwar', 'keerti1234@gmail.com', '$2y$10$PL6o************************osRIWEh1H.0Zi');
```

## **Vulnerability Impact:**
As an attacker, can do the following:
1. Crack the passwords provided the hashes are visible.
