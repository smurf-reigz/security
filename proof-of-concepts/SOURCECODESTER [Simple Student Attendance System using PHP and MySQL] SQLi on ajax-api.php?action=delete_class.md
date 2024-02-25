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
> [CWE-540: Inclusion of Sensitive Information in Source Code](https://cwe.mitre.org/data/definitions/540.html)

## **Details:**
> Exposed Login Credentials containing username, email, and passwords on the GitHub Page (hashes redacted by me for responsible disclosure).

```SQL 
INSERT INTO `users` (`id`, `username`, `email`, `password`) VALUES
(1, 'Ajay Kumar', 'ajay@gmail.com', '12***'),
(2, 'Amit', 'amit@gmail.com', '12**'),
(3, 'Keerti Panwar', 'keerti@gmail.com', '$2y$10$g******************lDntZ7ZXDD*********'),
(4, 'Ankita', 'ankita@gmail.com', '$2y$10$ZuW****************************pyEyRhtK'),
(5, 'Keerti Panwar', 'keerti1234@gmail.com', '$2y$10$PL6o************************osRIWEh1H.0Zi');
```

## **Vulnerability Impact:**
> As an attacker, can do the following:
> 1. Crack the passwords provided the hashes are visible.
