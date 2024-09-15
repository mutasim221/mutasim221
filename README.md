<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>امتحان متعدد الخيارات</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
      direction: rtl;
      text-align: right;
    }
    .container {
      width: 80%;
      margin: 20px auto;
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    h1 {
      text-align: center;
      color: #333;
    }
    .question {
      margin-bottom: 20px;
    }
    .question h2 {
      font-size: 20px;
      color: #333;
    }
    .options {
      list-style: none;
      padding: 0;
    }
    .options li {
      margin-bottom: 10px;
    }
    .options input {
      margin-left: 10px;
    }
    .timer {
      font-size: 18px;
      color: #333;
      text-align: center;
      margin-bottom: 20px;
    }
    .submit-btn {
      display: block;
      width: 100%;
      padding: 10px;
      background-color: #28a745;
      color: white;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
    }
    .submit-btn:hover {
      background-color: #218838;
    }
    .result {
      font-size: 24px;
      color: #333;
      text-align: center;
      margin-top: 20px;
    }
  </style>
</head>
<body>

  <div class="container">
    <h1>امتحان متعدد الخيارات</h1>
    <div class="timer" id="timer">الوقت المتبقي: 10:00</div>

    <form id="quizForm">
      <div class="question">
        <h2>1. ما هي عاصمة الأردن؟</h2>
        <ul class="options">
          <li><input type="radio" name="q1" value="0"> الزرقاء</li>
          <li><input type="radio" name="q1" value="0"> إربد</li>
          <li><input type="radio" name="q1" value="1"> عمان</li>
          <li><input type="radio" name="q1" value="0"> الكرك</li>
        </ul>
      </div>

      <div class="question">
        <h2>2. ما هو أكبر كوكب في النظام الشمسي؟</h2>
        <ul class="options">
          <li><input type="radio" name="q2" value="1"> المشتري</li>
          <li><input type="radio" name="q2" value="0"> الأرض</li>
          <li><input type="radio" name="q2" value="0"> المريخ</li>
          <li><input type="radio" name="q2" value="0"> زحل</li>
        </ul>
      </div>

      <!-- أضف المزيد من الأسئلة هنا، بنفس النمط -->

      <button type="button" class="submit-btn" onclick="submitQuiz()">إرسال الإجابات</button>
    </form>

    <div class="result" id="result"></div>
  </div>

  <script>
    // عداد الوقت (10 دقائق)
    let timeLeft = 600;
    const timerElement = document.getElementById("timer");

    function updateTimer() {
      const minutes = Math.floor(timeLeft / 60);
      const seconds = timeLeft % 60;
      timerElement.textContent = `الوقت المتبقي: ${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
      if (timeLeft > 0) {
        timeLeft--;
      } else {
        submitQuiz();
      }
    }

    setInterval(updateTimer, 1000);

    function submitQuiz() {
      const form = document.getElementById("quizForm");
      const resultElement = document.getElementById("result");
      let score = 0;

      // عدد الأسئلة
      const totalQuestions = 20;

      // التحقق من الإجابات الصحيحة
      for (let i = 1; i <= totalQuestions; i++) {
        const question = form[`q${i}`];
        if (question) {
          const selectedAnswer = [...question].find(input => input.checked);
          if (selectedAnswer && selectedAnswer.value === "1") {
            score++;
          }
        }
      }

      // عرض النتيجة
      resultElement.textContent = `نتيجتك: ${score} من ${totalQuestions}`;
      resultElement.style.color = score >= 10 ? "green" : "red";
    }
  </script>

</body>
</html>
