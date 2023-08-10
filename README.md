# Fourtask
<?php

    // قم بتوصيل قاعدة البيانات
    $servername = "localhost";
    $username = "root";
    $password = "";
    $dbname = "sensor";

    // إنشاء اتصال
    $conn = new mysqli($servername, $username, $password, $dbname);

    // التحقق من اتصال قاعدة البيانات
    if ($conn->connect_error) {
        die("فشل الاتصال: " . $conn->connect_error);
    }

    $number = $_GET['number'];
    $sql = "INSERT INTO senseor (Number) VALUES ('$number')";

    
    // تنفيذ الاستعلام
    if ($conn->query($sql) === TRUE) {
        echo "<br>good";
    } else {
        echo "حدث خطأ أثناء إضافة القيمة: " . $conn->error;
    }

    $sql = "SELECT * FROM senseor WHERE id=(SELECT MAX(id)FROM senseor)";

// تنفيذ الاستعلام وحفظ النتيجة في متغير
$result = $conn->query($sql);

// التحقق من وجود بيانات وإظهارها
if ($result->num_rows > 0) {
    // عرض البيانات في صفحة HTML
    while($row = $result->fetch_assoc()) {
        echo "num: "   . $_GET["number"] ;echo " <br>ID : " . $row["id"];
    }
} else {
    echo "لا يوجد بيانات في الجدول";
}
    // إغلاق الاتصال بقاعدة البيانات
    $conn->close();

?>
