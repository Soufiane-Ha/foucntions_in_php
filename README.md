# Foucntions_in_php
> # INSERT

1.1. Founction for insert data for tableu (General form of the addition function using PDO)
````
function addData($conn, $table, $data) {

    $columns = implode(", ", array_keys($data));
    $placeholders = ":" . implode(", :", array_keys($data));

    $sql = "INSERT INTO $table ($columns) VALUES ($placeholders)";
    $stmt = $conn->prepare($sql);

    if ($stmt->execute($data)) {
        return true; 
    } else {
        return false; 
    }
}
````
1.2. Usage 
````
`include 'connect.php';

$newUser = [
    'name' => 'ali',
    'email' => 'ali@example.com',
    'password' => password_hash('123456', PASSWORD_DEFAULT)
];

if (addData($conn, 'users', $newUser)) {
    echo "تمت الإضافة بنجاح!";
} else {
    echo "حدث خطأ أثناء الإضافة!";
}
````
2.1. Simple practical example (table and field selector)

````
function addUser($conn, $name, $email, $password) {
    $sql = "INSERT INTO users (name, email, password) VALUES (:name, :email, :password)";
    $stmt = $conn->prepare($sql);
    $stmt->bindParam(':name', $name);
    $stmt->bindParam(':email', $email);
    $stmt->bindParam(':password', $password);
    
    return $stmt->execute();
}

````
2.1. Usage 
````
include 'connect.php';

$name = "Ahmed";
$email = "ahmed@test.com";
$password = password_hash("1234", PASSWORD_DEFAULT);

if (addUser($conn, $name, $email, $password)) {
    echo "تمت إضافة المستخدم بنجاح";
} else {
    echo "حدث خطأ أثناء الإضافة";
}

````
> # EDIT
> # UPDATE
> # DELETE
> # RECHERCH
> # FILTRAG
