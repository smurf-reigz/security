## Vulnerability Details

**Credits**: Reigz Macolor (https://github.com/reigz/)<br/>
**Tested On**: PHP-MYSQL-User-Login-System <https://github.com/keerti1924/PHP-MYSQL-User-Login-System>
**Affected Version**: keerti1924/PHP-MYSQL-User-Login-System 1.0

**Affected Site Page**: *<br/>
**Affected Endpoint**: <https://github.com/keerti1924/PHP-MYSQL-User-Login-System/blob/main/login.sql> <br/>
CWE-540: Inclusion of Sensitive Information in Source Code

## **Details:**
Exposed Login Credentails on GitHub Page

```SQL 
INSERT INTO `users` (`id`, `username`, `email`, `password`) VALUES
(1, 'Ajay Kumar', 'ajay@gmail.com', '12345'),
(2, 'Amit', 'amit@gmail.com', '1234'),
(3, 'Keerti Panwar', 'keerti@gmail.com', '$2y$10$g.xv9BS7DZbZ0KT/.fkGouuD8duIUWY2lDntZ7ZXDDUW6h09ZDiqe'),
(4, 'Ankita', 'ankita@gmail.com', '$2y$10$ZuWPf98dGPFogVM8MoKGxOVZ4v1mXD.WrJQ7rwfvdYLWMpyEyRhtK'),
(5, 'Keerti Panwar', 'keerti1234@gmail.com', '$2y$10$PL6oQH71xCh3F3BALBuVYu6SLn2AVQ41o.i5vi2LosRIWEh1H.0Zi');
```

## **Vulnerability Impact:**
As an attacker, can do the following:
1. Crack the passwords provided the hashes are visible.
