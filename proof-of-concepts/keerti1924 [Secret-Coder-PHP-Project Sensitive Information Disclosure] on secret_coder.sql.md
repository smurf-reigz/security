## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [Secret-Coder-PHP-Project 1.0](https://github.com/keerti1924/Secret-Coder-PHP-Project/) <br/>

**Affected Version**:
> keerti1924/Secret-Coder-PHP-Project 1.0

**Affected Site Page**: 
> /login.php<br/>

**Affected Code**: 
> <https://github.com/keerti1924/Secret-Coder-PHP-Project/blob/main/secret_coder.sql> <br/>

**Related CWE:**
> [CWE-540: Inclusion of Sensitive Information in Source Code](https://cwe.mitre.org/data/definitions/540.html)

## **Details:**
> Exposed Login Credentials containing username, email, and passwords on the GitHub Page (hashes redacted by me for responsible disclosure).

```SQL 
INSERT INTO `users` (`id`, `username`, `email`, `password`) VALUES
(1, 'ajay', 'ajay@gmail.com', '$2y$10$8*************2s*********************wmh***************'),
(2, 'anjali', 'anjali@gmail.com', '$2y$10$**************************************************e'),
(3, 'ankit', 'ankit@gmail.com', '$2y$10$J***********************************************jaYda');
```

## **Vulnerability Impact:**
> As an attacker, can do the following:
> 1. Crack the passwords provided the hashes are visible.
