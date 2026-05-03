# differential-equations-quiz
نتائج الخامس 
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نتائج الطلاب - الخامس الأدبي</title>
    <style>
        body {
            background-color: black; /* الظهر لون اسود */
            color: white;
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            border: 2px solid #555;
            padding: 30px;
            border-radius: 10px;
            background-color: #111;
        }
        input {
            padding: 12px;
            margin: 10px 0;
            width: 80%;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 16px;
            text-align: center;
        }
        button {
            padding: 12px 25px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 15px;
            font-weight: bold;
        }
        button:hover {
            background-color: #0056b3;
        }
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 25px;
            background-color: #222;
        }
        table, th, td {
            border: 1px solid #555;
        }
        th, td {
            padding: 12px;
            text-align: center;
            font-size: 18px;
        }
        th {
            color: white; /* لون اسماء المواد ابيض */
            background-color: #333;
        }
        .error {
            color: #ff4d4d;
            margin-top: 15px;
            font-weight: bold;
        }
        #resultSection {
            display: none;
        }
    </style>
</head>
<body>

    <div class="container" id="loginSection">
        <h2>نظام استخراج نتائج الطلاب</h2>
        <p>يرجى إدخال رقم المدرسة والرقم السري للطالب</p>
        <input type="text" id="schoolCode" placeholder="رقم المدرسة (مثال: ali2027)">
        <input type="text" id="studentCode" placeholder="الرقم السري للطالب (مثال: SL2001)">
        <br>
        <button onclick="checkResult()">عرض النتيجة</button>
        <div id="errorMessage" class="error"></div>
    </div>

    <div class="container" id="resultSection">
        <h2 style="color: #4CAF50;">النتيجة متوفرة</h2>
        <h3>اسم الطالب: <span id="studentName" style="color: white;"></span></h3>
        <table>
            <tr>
                <th>المادة</th>
                <th>الدرجة</th>
            </tr>
            <tr>
                <th>التربية الإسلامية</th>
                <td id="grade0"></td>
            </tr>
            <tr>
                <th>اللغة العربية</th>
                <td id="grade1"></td>
            </tr>
            <tr>
                <th>اللغة الانكليزية</th>
                <td id="grade2"></td>
            </tr>
            <tr>
                <th>الرياضيات</th>
                <td id="grade3"></td>
            </tr>
            <tr>
                <th>التاريخ</th>
                <td id="grade4"></td>
            </tr>
            <tr>
                <th>الجغرافية</th>
                <td id="grade5"></td>
            </tr>
            <tr>
                <th>اقتصاد</th>
                <td id="grade6"></td>
            </tr>
            <tr>
                <th>الفلسفة</th>
                <td id="grade7"></td>
            </tr>
            <tr>
                <th>التربية الرياضية</th>
                <td id="grade8"></td>
            </tr>
            <tr>
                <th>التربية الفنية</th>
                <td id="grade9"></td>
            </tr>
        </table>
        <br>
        <button onclick="goBack()" style="background-color: #dc3545;">خروج / رجوع</button>
    </div>

    <script>
        // قاعدة بيانات الطلاب والدرجات من الملف المرفق
        const students = {
            "SL2001": { name: "إبراهيم جاسم محمد", grades: [25, 25, 25, 25, 58, 38, 35, 63, 60, 60] },
            "SL2002": { name: "إبراهيم طاهر محمود", grades: [75, 25, 25, 50, 43, 35, 55, 25, 60, 60] },
            "SL2003": { name: "أبو عبيدة حسين محمود", grades: [25, 25, 25, 28, 30, 36, 35, 55, 60, 60] },
            "SL2004": { name: "احمد صدام احمد", grades: [25, 25, 35, 25, 25, 37, 35, 25, 60, 60] },
            "SL2005": { name: "احمد علي حسين محيميد", grades: [80, 76, 90, 50, 80, 70, 65, 58, 70, 70] },
            "SL2006": { name: "احمد علي حمادي", grades: [64, 25, 50, 29, 55, 35, 50, 78, 60, 60] },
            "SL2007": { name: "احمد علي عامر جاسم", grades: [57, 40, 65, 31, 44, 35, 35, 58, 60, 60] },
            "SL2008": { name: "احمد محمد احمد", grades: [62, 50, 70, 50, 52, 36, 50, 72, 60, 60] },
            "SL2009": { name: "احمد محمد عبد فياض", grades: [62, 53, 25, 31, 52, 37, 51, 37, 60, 60] },
            "SL2010": { name: "ادهام يوسف صايل", grades: [38, 25, 30, 39, 25, 37, 35, 50, 60, 60] },
            "SL2011": { name: "ادهم اكرم ابراهيم", grades: [50, 40, 40, 31, 35, 35, 35, 50, 60, 60] },
            "SL2012": { name: "انس عباس زيدان", grades: [60, 42, 35, 36, 62, 50, 40, 62, 60, 60] },
            "SL2013": { name: "انس قاسم مرشد", grades: [68, 25, 35, 29, 44, 36, 40, 25, 60, 60] },
            "SL2014": { name: "انمار بشير جاسم", grades: [64, 57, 40, 25, 55, 50, 35, 37, 60, 60] }
        };

        const REQUIRED_SCHOOL_CODE = "ali2027";

        function checkResult() {
            const schoolCode = document.getElementById("schoolCode").value.trim();
            const studentCode = document.getElementById("studentCode").value.trim().toUpperCase();
            const errorDiv = document.getElementById("errorMessage");

            if (schoolCode !== REQUIRED_SCHOOL_CODE) {
                errorDiv.innerText = "رقم المدرسة غير صحيح!";
                return;
            }

            if (!students[studentCode]) {
                errorDiv.innerText = "الرقم السري للطالب غير صحيح!";
                return;
            }

            // إخفاء رسالة الخطأ وعرض الدرجات
            errorDiv.innerText = "";
            const student = students[studentCode];
            
            document.getElementById("studentName").innerText = student.name;
            for(let i=0; i<10; i++){
                let gradeElement = document.getElementById("grade" + i);
                gradeElement.innerText = student.grades[i];
                
                // تمييز درجات الرسوب باللون الأحمر لسهولة القراءة
                if(student.grades[i] < 50) {
                    gradeElement.style.color = "#ff4d4d";
                } else {
                    gradeElement.style.color = "white";
                }
            }

            // إخفاء واجهة الدخول وإظهار النتيجة
            document.getElementById("loginSection").style.display = "none";
            document.getElementById("resultSection").style.display = "block";
        }

        function goBack() {
            // الرجوع لواجهة الدخول وتصفير الحقول
            document.getElementById("loginSection").style.display = "block";
            document.getElementById("resultSection").style.display = "none";
            document.getElementById("studentCode").value = "";
        }
    </script>
</body>
</html>
