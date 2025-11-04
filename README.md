# Hohu
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>نظام الاختبارات التفاعلي - الكيمياء</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            background-color: rgba(255, 255, 255, 0.95);
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(90deg, #2c3e50, #4a6491);
            color: white;
            padding: 25px;
            text-align: center;
            border-bottom: 5px solid #3498db;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.2rem;
            opacity: 0.9;
        }
        
        .content {
            display: flex;
            flex-wrap: wrap;
        }
        
        .video-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
            background-color: #f8f9fa;
            border-left: 1px solid #e0e0e0;
        }
        
        .quiz-section {
            flex: 2;
            min-width: 300px;
            padding: 20px;
        }
        
        .video-container {
            background: #2c3e50;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
            color: white;
            text-align: center;
        }
        
        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            overflow: hidden;
            border-radius: 8px;
            margin: 15px 0;
        }
        
        .video-wrapper iframe {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: none;
        }
        
        .lesson-content {
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            margin-top: 15px;
        }
        
        .question {
            background: white;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            display: none;
        }
        
        .question.active {
            display: block;
        }
        
        .question-number {
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
            font-size: 1.1rem;
        }
        
        .question-text {
            font-size: 1.1rem;
            margin-bottom: 20px;
            color: #2c3e50;
        }
        
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        
        .option {
            padding: 12px 15px;
            background: #f8f9fa;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .option:hover {
            background: #e9ecef;
            border-color: #3498db;
        }
        
        .option.selected {
            background: #d1ecf1;
            border-color: #17a2b8;
        }
        
        .option.correct {
            background: #d4edda;
            border-color: #28a745;
            color: #155724;
        }
        
        .option.incorrect {
            background: #f8d7da;
            border-color: #dc3545;
            color: #721c24;
        }
        
        .option.disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }
        
        .option.selected.correct::after {
            content: " ✓";
            font-weight: bold;
            color: #28a745;
        }
        
        .option.selected.incorrect::after {
            content: " ✗";
            font-weight: bold;
            color: #dc3545;
        }
        
        .explanation {
            margin-top: 15px;
            padding: 15px;
            border-radius: 8px;
            display: none;
        }
        
        .explanation.show {
            display: block;
        }
        
        .explanation.correct {
            background: #d4edda;
            border-left: 5px solid #28a745;
        }
        
        .explanation.incorrect {
            background: #f8d7da;
            border-left: 5px solid #dc3545;
        }
        
        .navigation {
            display: flex;
            justify-content: space-between;
            margin-top: 20px;
        }
        
        button {
            padding: 12px 25px;
            background: #3498db;
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: background 0.3s;
        }
        
        button:hover {
            background: #2980b9;
        }
        
        button:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
        }
        
        .results {
            text-align: center;
            padding: 30px;
            display: none;
        }
        
        .results.active {
            display: block;
        }
        
        .student-grade {
            margin: 25px 0;
            padding: 20px;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .grade-circle {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            background: #3498db;
            margin: 0 auto;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 2.5rem;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }
        
        .student-info {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            margin-bottom: 20px;
            text-align: center;
        }
        
        .form-group {
            margin-bottom: 20px;
            text-align: right;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .form-group select {
            width: 100%;
            padding: 12px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        
        .start-btn {
            background: #2ecc71;
            font-size: 1.2rem;
            padding: 15px 40px;
        }
        
        .student-details {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
            border-right: 5px solid #3498db;
        }
        
        .final-percentage {
            font-size: 3rem;
            font-weight: bold;
            color: #2c3e50;
            margin: 20px 0;
            text-align: center;
        }
        
        .final-grade {
            font-size: 2rem;
            color: #3498db;
            margin-bottom: 20px;
            text-align: center;
        }
        
        .progress-indicators {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-bottom: 20px;
            justify-content: center;
        }
        
        .progress-indicator {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            background-color: #e0e0e0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.8rem;
            font-weight: bold;
            color: #555;
            transition: all 0.3s;
        }
        
        .progress-indicator.current {
            background-color: #3498db;
            color: white;
            transform: scale(1.1);
        }
        
        .progress-indicator.answered {
            background-color: #6c757d;
            color: white;
        }
        
        .progress-indicator.correct {
            background-color: #28a745;
            color: white;
        }
        
        .progress-indicator.incorrect {
            background-color: #dc3545;
            color: white;
        }
        
        .timer {
            background: #2c3e50;
            color: white;
            padding: 10px 15px;
            border-radius: 8px;
            text-align: center;
            margin-bottom: 20px;
            font-size: 1.2rem;
            font-weight: bold;
        }
        
        .result-details {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 3px 10px rgba(0, 0, 0, 0.1);
            margin-top: 20px;
            text-align: right;
        }
        
        .question-review {
            margin-bottom: 15px;
            padding: 15px;
            border-radius: 8px;
            background: #f8f9fa;
        }
        
        .question-review.correct {
            border-right: 5px solid #28a745;
        }
        
        .question-review.incorrect {
            border-right: 5px solid #dc3545;
        }

        @media (max-width: 768px) {
            .content {
                flex-direction: column;
            }
            
            .video-section {
                border-left: none;
                border-bottom: 1px solid #e0e0e0;
            }
            
            .grade-circle {
                width: 120px;
                height: 120px;
                font-size: 2rem;
            }
            
            .final-percentage {
                font-size: 2.5rem;
            }
            
            .final-grade {
                font-size: 1.5rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>نظام الاختبارات التفاعلي - الكيمياء</h1>
            <div class="subtitle">اختبار درس المول - 50 سؤالاً - مدة الاختبار: 45 دقيقة</div>
        </header>
        
        <div class="content">
            <div class="quiz-section">
                <div class="student-info" id="studentInfo">
                    <h2>بيانات الطالب</h2>
                    <div class="form-group">
                        <label for="studentName">الاسم الكامل</label>
                        <input type="text" id="studentName" placeholder="أدخل اسمك الكامل">
                    </div>
                    <div class="form-group">
                        <label for="section">الشعبة</label>
                        <select id="section">
                            <option value="">اختر الشعبة</option>
                            <option value="1">الشعبة 1</option>
                            <option value="2">الشعبة 2</option>
                            <option value="3">الشعبة 3</option>
                            <option value="4">الشعبة 4</option>
                            <option value="5">الشعبة 5</option>
                            <option value="6">الشعبة 6</option>
                            <option value="7">الشعبة 7</option>
                        </select>
                    </div>
                    <button class="start-btn" id="startBtn">بدء الاختبار</button>
                </div>
                
                <div class="timer" id="timer" style="display: none;">الوقت المتبقي: <span id="timeLeft">45:00</span></div>
                
                <div class="progress-indicators" id="progressIndicators" style="display: none;"></div>
                
                <div id="quizContainer" style="display: none;"></div>
                
                <div class="results" id="results">
                    <div class="student-grade">
                        <div class="grade-circle" id="gradeCircle">0%</div>
                    </div>
                    
                    <div class="final-percentage" id="finalPercentage">0%</div>
                    <div class="final-grade" id="finalGrade">تقدير: غير محدد</div>
                    
                    <div class="student-details">
                        <h3>معلومات الطالب</h3>
                        <p><strong>الاسم:</strong> <span id="resultName"></span></p>
                        <p><strong>الشعبة:</strong> <span id="resultSection"></span></p>
                        <p><strong>الدرجة:</strong> <span id="resultScore">0</span>/50</p>
                    </div>
                    
                    <div class="result-details" id="resultDetails">
                        <h3>تفاصيل الإجابات</h3>
                    </div>
                    
                    <div class="summary">
                        <p>سيتم إعادة تحميل الصفحة تلقائياً خلال <span id="countdown">60</span> ثانية</p>
                    </div>
                </div>
            </div>
            
            <div class="video-section">
                <div class="video-container">
                    <h3>درس المول في الكيمياء</h3>
                    <div class="video-wrapper">
                        <iframe src="https://www.youtube.com/embed/vAyT1Y6pGs8" frameborder="0" allowfullscreen></iframe>
                    </div>
                </div>
                
                <div class="lesson-content">
                    <h3>معلومات عن الاختبار</h3>
                    <p>• 50 سؤالاً في الكيمياء (درس المول)</p>
                    <p>• مدة الاختبار: 45 دقيقة</p>
                    <p>• لا يمكن الرجوع إلى الأسئلة السابقة</p>
                    <p>• لا يمكن تغيير الإجابة بعد اختيارها</p>
                    <p>• الأسئلة عشوائية مع كل محاولة جديدة</p>
                    
                    <h4>قوانين مهمة:</h4>
                    <ul>
                        <li>عدد المولات = الكتلة ÷ الكتلة المولية</li>
                        <li>الكتلة المولية = مجموع الكتل الذرية</li>
                        <li>عدد الجسيمات = عدد المولات × عدد أفوجادرو</li>
                        <li>النسبة المئوية = (كتلة العنصر ÷ الكتلة المولية) × 100%</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // بنك الأسئلة الكامل (50 سؤالاً)
            const questionBank = [
                {
                    question: "المول هو كمية المادة التي تحتوي على عدد من الجسيمات يساوي عدد الجسيمات في 12 غرام من الكربون-12.",
                    options: ["صح", "خطأ"],
                    correct: 0,
                    explanation: "هذا هو التعريف العلمي الدقيق للمول حسب نظام الوحدات الدولي."
                },
                {
                    question: "عدد أفوجادرو يساوي:",
                    options: ["6.022 × 10²³", "3.01 × 10²³", "1.2 × 10²⁴"],
                    correct: 0,
                    explanation: "عدد أفوجادرو هو 6.022 × 10²³ جسيم/مول وهو عدد الذرات في 12 جرام من الكربون-12."
                },
                {
                    question: "الكتلة المولية للماء H₂O تساوي:",
                    options: ["16 g/mol", "18 g/mol", "20 g/mol"],
                    correct: 1,
                    explanation: "الكتلة المولية للماء = (2 × 1) + 16 = 18 جم/مول"
                },
                {
                    question: "الكتلة المولية لثاني أكسيد الكربون CO₂ تساوي:",
                    options: ["44 g/mol", "28 g/mol", "32 g/mol"],
                    correct: 0,
                    explanation: "الكتلة المولية لـ CO₂ = 12 + (2 × 16) = 44 جم/مول"
                },
                {
                    question: "الكتلة المولية هي:",
                    options: ["كتلة مول واحد من المادة", "عدد الذرات في مول واحد", "الحجم المولي"],
                    correct: 0,
                    explanation: "الكتلة المولية هي كتلة مول واحد من المادة وتقاس بالجرام/مول."
                },
                {
                    question: "وحدة قياس الكتلة المولية:",
                    options: ["mol", "g/mol", "g"],
                    correct: 1,
                    explanation: "الوحدة الدولية للكتلة المولية هي الجرام لكل مول (g/mol)."
                },
                {
                    question: "حجم المول الواحد من أي غاز عند الظروف القياسية يساوي:",
                    options: ["22.4 لتر", "2.24 لتر", "224 لتر"],
                    correct: 0,
                    explanation: "حجم المول الواحد من أي غاز عند الظروف القياسية (STP) هو 22.4 لتر."
                },
                {
                    question: "المادة التي تحتوي على ذرات فقط هي:",
                    options: ["مركب", "عنصر", "خليط"],
                    correct: 1,
                    explanation: "العنصر هو مادة نقية تتكون من نوع واحد فقط من الذرات."
                },
                {
                    question: "الصيغة الجزيئية تبين:",
                    options: ["العدد الفعلي لكل نوع من الذرات", "النسبة بين الذرات فقط", "عدد الجزيئات"],
                    correct: 0,
                    explanation: "الصيغة الجزيئية تبين العدد الفعلي لكل نوع من الذرات في الجزيء."
                },
                {
                    question: "لتحويل الجزيئات إلى مولات نستخدم:",
                    options: ["الضرب في عدد أفوجادرو", "القسمة على عدد أفوجادرو", "الضرب في الكتلة المولية"],
                    correct: 1,
                    explanation: "لتحويل الجزيئات إلى مولات: عدد المولات = عدد الجزيئات ÷ عدد أفوجادرو"
                },
                {
                    question: "لتحويل المولات إلى جزيئات نستخدم:",
                    options: ["الضرب في عدد أفوجادرو", "القسمة على الكتلة المولية", "الضرب في الحجم المولي"],
                    correct: 0,
                    explanation: "لتحويل المولات إلى جزيئات: عدد الجزيئات = عدد المولات × عدد أفوجادرو"
                },
                {
                    question: "عدد الذرات في 1 مول من الأكسجين (O₂):",
                    options: ["6.022×10²³", "1.204×10²⁴", "3.011×10²³"],
                    correct: 1,
                    explanation: "جزيء الأكسجين O₂ يحتوي على ذرتين، لذلك عدد الذرات = 2 × 6.022×10²³ = 1.204×10²⁴"
                },
                {
                    question: "العلاقة الصحيحة بين الكتلة والمولات:",
                    options: ["الكتلة = عدد المولات × الكتلة المولية", "الكتلة = عدد المولات ÷ الكتلة المولية", "الكتلة = الحجم × الكثافة"],
                    correct: 0,
                    explanation: "الكتلة = عدد المولات × الكتلة المولية"
                },
                {
                    question: "وحدة قياس عدد المولات:",
                    options: ["g", "mol", "L"],
                    correct: 1,
                    explanation: "الوحدة الدولية لعدد المولات هي المول (mol)."
                },
                {
                    question: "1 مول من NaCl يحتوي على:",
                    options: ["6.022×10²³ جزيء", "1×10²³ جزيء", "3×10²³ ذرة"],
                    correct: 0,
                    explanation: "كل مول من أي مادة يحتوي على عدد أفوجادرو من الجسيمات (6.022×10²³)."
                },
                {
                    question: "الكتلة المولية للأكسجين (O₂):",
                    options: ["16 g/mol", "32 g/mol", "64 g/mol"],
                    correct: 1,
                    explanation: "الكتلة المولية لـ O₂ = 16 × 2 = 32 جم/مول"
                },
                {
                    question: "الكتلة المولية للهيدروجين (H₂):",
                    options: ["1 g/mol", "2 g/mol", "4 g/mol"],
                    correct: 1,
                    explanation: "الكتلة المولية لـ H₂ = 1 × 2 = 2 جم/مول"
                },
                {
                    question: "أي من المواد التالية تحتوي على أكبر عدد من الذرات؟",
                    options: ["1 مول من H₂O", "1 مول من NaCl", "1 مول من O₂"],
                    correct: 0,
                    explanation: "1 مول من H₂O يحتوي على 3 × 6.022×10²³ ذرة، بينما NaCl يحتوي على 2 × 6.022×10²³ و O₂ يحتوي على 2 × 6.022×10²³"
                },
                {
                    question: "المادة التي تحتوي على أكثر من نوع واحد من الذرات هي:",
                    options: ["العنصر", "المركب", "المحلول"],
                    correct: 1,
                    explanation: "المركب هو مادة تتكون من اتحاد عنصرين أو أكثر بنسب ثابتة."
                },
                {
                    question: "المركب الذي يحتوي على 3 عناصر هو:",
                    options: ["NaHCO₃", "H₂", "Cl₂"],
                    correct: 0,
                    explanation: "NaHCO₃ يحتوي على الصوديوم (Na)، الهيدروجين (H)، الكربون (C)، والأكسجين (O)."
                },
                {
                    question: "عند زيادة عدد المولات تزداد الكتلة الكلية للمادة.",
                    options: ["صح", "خطأ"],
                    correct: 0,
                    explanation: "هذه العلاقة طردية: كلما زاد عدد المولات زادت الكتلة الكلية."
                },
                {
                    question: "إذا كانت الكتلة المولية لمادة ما = 50 g/mol، فإن كتلة 2 mol منها =",
                    options: ["25 g", "50 g", "100 g"],
                    correct: 2,
                    explanation: "الكتلة = عدد المولات × الكتلة المولية = 2 × 50 = 100 جم"
                },
                {
                    question: "عند مضاعفة عدد الجسيمات في عينة فإن عدد المولات:",
                    options: ["يتضاعف", "ينقص للنصف", "لا يتغير"],
                    correct: 0,
                    explanation: "العلاقة بين عدد الجسيمات وعدد المولات علاقة طردية."
                },
                {
                    question: "الغاز الذي يحتل حجماً أكبر عند نفس الظروف هو الغاز الذي يحتوي على:",
                    options: ["عدد مولات أكبر", "كتلة أقل", "عدد جزيئات أقل"],
                    correct: 0,
                    explanation: "حجم الغاز يتناسب طردياً مع عدد المولات عند نفس الظروف."
                },
                {
                    question: "أي مما يلي ليس وحدة مناسبة للمول؟",
                    options: ["mol/L", "mol", "mol⁻¹"],
                    correct: 0,
                    explanation: "mol/L هي وحدة التركيز المولاري وليست وحدة للمول."
                },
                {
                    question: "المركب الذي يحتوي على عنصرين فقط هو:",
                    options: ["H₂O", "CO₂", "NaHCO₃"],
                    correct: 1,
                    explanation: "CO₂ يحتوي على الكربون والأكسجين فقط."
                },
                {
                    question: "المول من الغاز يحتوي على:",
                    options: ["عدد ذرات محدد", "22.4 لتر عند STP", "كتلة ثابتة دائمًا"],
                    correct: 1,
                    explanation: "المول الواحد من أي غاز يشغل 22.4 لتر عند الظروف القياسية."
                },
                {
                    question: "العلاقة بين عدد الجزيئات وعدد المولات علاقة:",
                    options: ["طردية", "عكسية", "لا علاقة"],
                    correct: 0,
                    explanation: "العلاقة طردية: عدد الجزيئات = عدد المولات × عدد أفوجادرو"
                },
                {
                    question: "العلاقة بين الكتلة وعدد المولات علاقة:",
                    options: ["طردية", "عكسية", "ثابتة"],
                    correct: 0,
                    explanation: "العلاقة طردية: الكتلة = عدد المولات × الكتلة المولية"
                },
                {
                    question: "حجم الغاز يعتمد على:",
                    options: ["درجة الحرارة والضغط", "عدد أفوجادرو فقط", "الكتلة المولية فقط"],
                    correct: 0,
                    explanation: "حجم الغاز يتأثر بدرجة الحرارة والضغط حسب قانون الغازات المثالية."
                },
                {
                    question: "احسب الكتلة المولية لـ NaCl (Na = 23, Cl = 35.5):",
                    options: ["56.5 g/mol", "58.5 g/mol", "60 g/mol"],
                    correct: 1,
                    explanation: "الكتلة المولية لـ NaCl = 23 + 35.5 = 58.5 جم/مول"
                },
                {
                    question: "احسب عدد الذرات في 31.1 g من الذهب (Au = 197 u):",
                    options: ["9.50×10²²", "6.02×10²³", "1.97×10²³"],
                    correct: 0,
                    explanation: "عدد المولات = 31.1 ÷ 197 = 0.158 مول، عدد الذرات = 0.158 × 6.022×10²³ = 9.50×10²²"
                },
                {
                    question: "احسب كتلة 15.5 mol من NaCl (M = 58.5 g/mol):",
                    options: ["906.75 g", "580 g", "1000 g"],
                    correct: 0,
                    explanation: "الكتلة = 15.5 × 58.5 = 906.75 جم"
                },
                {
                    question: "احسب عدد المولات في 22 g من CO₂ (M = 44 g/mol):",
                    options: ["0.25 mol", "0.5 mol", "2 mol"],
                    correct: 1,
                    explanation: "عدد المولات = 22 ÷ 44 = 0.5 مول"
                },
                {
                    question: "كم عدد الجزيئات في 0.25 mol من H₂O؟",
                    options: ["1.51×10²³", "6.02×10²³", "3.01×10²³"],
                    correct: 0,
                    explanation: "عدد الجزيئات = 0.25 × 6.022×10²³ = 1.505×10²³ ≈ 1.51×10²³"
                },
                {
                    question: "احسب كتلة 2 mol من الأكسجين (O₂ = 32 g/mol):",
                    options: ["16 g", "32 g", "64 g"],
                    correct: 2,
                    explanation: "الكتلة = 2 × 32 = 64 جم"
                },
                {
                    question: "عدد المولات في 11.2 لتر من غاز عند الظروف القياسية هو:",
                    options: ["0.25 mol", "0.5 mol", "2 mol"],
                    correct: 1,
                    explanation: "عدد المولات = الحجم ÷ 22.4 = 11.2 ÷ 22.4 = 0.5 مول"
                },
                {
                    question: "كم عدد الجزيئات في 3 mol من CO₂؟",
                    options: ["1.8×10²⁴", "3×10²³", "6.02×10²³"],
                    correct: 0,
                    explanation: "عدد الجزيئات = 3 × 6.022×10²³ = 1.8066×10²⁴ ≈ 1.8×10²⁴"
                },
                {
                    question: "احسب كتلة 0.75 mol من H₂O (M = 18 g/mol):",
                    options: ["9 g", "13.5 g", "27 g"],
                    correct: 1,
                    explanation: "الكتلة = 0.75 × 18 = 13.5 جم"
                },
                {
                    question: "احسب عدد المولات في 90 g من H₂O (M = 18 g/mol):",
                    options: ["4 mol", "2 mol", "6 mol"],
                    correct: 0,
                    explanation: "عدد المولات = 90 ÷ 18 = 5 مول"
                },
                {
                    question: "احسب عدد المولات في 0.5 لتر من غاز عند الظروف القياسية (22.4 L/mol):",
                    options: ["0.022 mol", "0.05 mol", "0.002 mol"],
                    correct: 0,
                    explanation: "عدد المولات = 0.5 ÷ 22.4 = 0.0223 مول ≈ 0.022 مول"
                },
                {
                    question: "احسب عدد الجزيئات في 5 g من H₂ (M = 2 g/mol):",
                    options: ["1.505×10²⁴", "6.022×10²³", "3×10²⁴"],
                    correct: 0,
                    explanation: "عدد المولات = 5 ÷ 2 = 2.5 مول، عدد الجزيئات = 2.5 × 6.022×10²³ = 1.505×10²⁴"
                },
                {
                    question: "احسب كتلة 0.25 mol من CO₂ (M = 44 g/mol):",
                    options: ["11 g", "22 g", "44 g"],
                    correct: 0,
                    explanation: "الكتلة = 0.25 × 44 = 11 جم"
                },
                {
                    question: "احسب عدد الجزيئات في 2 mol من NH₃:",
                    options: ["1.204×10²⁴", "6.022×10²³", "3×10²³"],
                    correct: 0,
                    explanation: "عدد الجزيئات = 2 × 6.022×10²³ = 1.2044×10²⁴"
                },
                {
                    question: "احسب عدد المولات في 88 g من CO₂ (M = 44 g/mol):",
                    options: ["1 mol", "2 mol", "0.5 mol"],
                    correct: 1,
                    explanation: "عدد المولات = 88 ÷ 44 = 2 مول"
                },
                {
                    question: "احسب الكتلة المولية لـ H₂SO₄ (H=1, S=32, O=16):",
                    options: ["49 g/mol", "98 g/mol", "64 g/mol"],
                    correct: 1,
                    explanation: "الكتلة المولية = (2×1) + 32 + (4×16) = 2 + 32 + 64 = 98 جم/مول"
                },
                {
                    question: "عدد الجزيئات في 4.48 لتر من غاز عند STP هو:",
                    options: ["1.2×10²³", "6.022×10²³", "2.4×10²³"],
                    correct: 0,
                    explanation: "عدد المولات = 4.48 ÷ 22.4 = 0.2 مول، عدد الجزيئات = 0.2 × 6.022×10²³ = 1.2044×10²³ ≈ 1.2×10²³"
                },
                {
                    question: "احسب كتلة 3 mol من NaOH (M = 40 g/mol):",
                    options: ["80 g", "120 g", "160 g"],
                    correct: 1,
                    explanation: "الكتلة = 3 × 40 = 120 جم"
                },
                {
                    question: "احسب عدد المولات في 54 g من H₂O (M = 18 g/mol):",
                    options: ["2 mol", "3 mol", "4 mol"],
                    correct: 1,
                    explanation: "عدد المولات = 54 ÷ 18 = 3 مول"
                },
                {
                    question: "احسب عدد الجزيئات في 1 mol من CO₂:",
                    options: ["6.022×10²³", "3.011×10²³", "1.204×10²⁴"],
                    correct: 0,
                    explanation: "كل مول من أي مادة يحتوي على عدد أفوجادرو من الجسيمات (6.022×10²³)."
                }
            ];

            // العناصر
            const studentInfo = document.getElementById('studentInfo');
            const progressIndicators = document.getElementById('progressIndicators');
            const quizContainer = document.getElementById('quizContainer');
            const results = document.getElementById('results');
            const startBtn = document.getElementById('startBtn');
            const studentNameInput = document.getElementById('studentName');
            const sectionSelect = document.getElementById('section');
            const resultName = document.getElementById('resultName');
            const resultSection = document.getElementById('resultSection');
            const resultScore = document.getElementById('resultScore');
            const finalPercentage = document.getElementById('finalPercentage');
            const finalGrade = document.getElementById('finalGrade');
            const gradeCircle = document.getElementById('gradeCircle');
            const countdownElement = document.getElementById('countdown');
            const timerElement = document.getElementById('timer');
            const timeLeftElement = document.getElementById('timeLeft');
            const resultDetails = document.getElementById('resultDetails');

            // المتغيرات
            let currentQuestion = 0;
            let totalQuestions = 50;
            let score = 0;
            let userAnswers = {};
            let countdown;
            let timer;
            let timeLeft = 45 * 60;
            let questions = [];

            // خلط الأسئلة والخيارات عشوائياً
            function shuffleArray(array) {
                for (let i = array.length - 1; i > 0; i--) {
                    const j = Math.floor(Math.random() * (i + 1));
                    [array[i], array[j]] = [array[j], array[i]];
                }
                return array;
            }

            function getRandomQuestions() {
                // نسخ الأسئلة الأصلية
                let shuffledQuestions = [...questionBank];
                
                // خلط ترتيب الأسئلة
                shuffledQuestions = shuffleArray(shuffledQuestions);
                
                // خلط ترتيب الخيارات في كل سؤال
                shuffledQuestions.forEach(question => {
                    // حفظ الإجابة الصحيحة قبل الخلط
                    const correctAnswer = question.options[question.correct];
                    
                    // خلط الخيارات
                    question.options = shuffleArray([...question.options]);
                    
                    // تحديث موقع الإجابة الصحيحة بعد الخلط
                    question.correct = question.options.indexOf(correctAnswer);
                });
                
                return shuffledQuestions.slice(0, totalQuestions);
            }

            // إنشاء دوائر التقدم
            function createProgressIndicators() {
                progressIndicators.innerHTML = '';
                for (let i = 0; i < totalQuestions; i++) {
                    const indicator = document.createElement('div');
                    indicator.className = 'progress-indicator';
                    indicator.textContent = i + 1;
                    indicator.id = `indicator${i}`;
                    progressIndicators.appendChild(indicator);
                }
                updateProgressIndicators();
            }

            // تحديث دوائر التقدم
            function updateProgressIndicators() {
                for (let i = 0; i < totalQuestions; i++) {
                    const indicator = document.getElementById(`indicator${i}`);
                    indicator.classList.remove('current', 'answered', 'correct', 'incorrect');
                    
                    if (i === currentQuestion) {
                        indicator.classList.add('current');
                    } else if (userAnswers[i]) {
                        indicator.classList.add('answered');
                        if (userAnswers[i].isCorrect) {
                            indicator.classList.add('correct');
                        } else {
                            indicator.classList.add('incorrect');
                        }
                    }
                }
            }

            // إنشاء الأسئلة
            function createQuestions() {
                quizContainer.innerHTML = '';
                questions.forEach((q, index) => {
                    const questionElement = document.createElement('div');
                    questionElement.className = 'question';
                    questionElement.id = `question${index}`;
                    
                    questionElement.innerHTML = `
                        <div class="question-number">السؤال ${index + 1} من ${totalQuestions}</div>
                        <div class="question-text">${q.question}</div>
                        <div class="options">
                            ${q.options.map((option, optIndex) => 
                                `<div class="option" data-index="${optIndex}">${option}</div>`
                            ).join('')}
                        </div>
                        <div class="explanation"></div>
                        <div class="navigation">
                            <button id="nextBtn${index}" disabled>${index === totalQuestions - 1 ? 'إنهاء الاختبار' : 'التالي'}</button>
                        </div>
                    `;
                    
                    quizContainer.appendChild(questionElement);
                });
            }

            // بدء المؤقت
            function startTimer() {
                timer = setInterval(function() {
                    timeLeft--;
                    
                    const minutes = Math.floor(timeLeft / 60);
                    const seconds = timeLeft % 60;
                    
                    timeLeftElement.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                    
                    if (timeLeft <= 0) {
                        clearInterval(timer);
                        showResults();
                    }
                }, 1000);
            }

            // بدء الاختبار
            startBtn.addEventListener('click', function() {
                const studentName = studentNameInput.value.trim();
                const section = sectionSelect.value;
                
                if (!studentName || !section) {
                    alert('يرجى إدخال الاسم واختيار الشعبة');
                    return;
                }
                
                studentInfo.style.display = 'none';
                timerElement.style.display = 'block';
                progressIndicators.style.display = 'flex';
                quizContainer.style.display = 'block';
                
                // اختيار 50 سؤال عشوائي مع خلط الخيارات
                questions = getRandomQuestions();
                
                createQuestions();
                createProgressIndicators();
                showQuestion(currentQuestion);
                startTimer();
            });

            // عرض السؤال
            function showQuestion(questionNumber) {
                document.querySelectorAll('.question').forEach(q => {
                    q.classList.remove('active');
                });
                
                const currentQuestionElement = document.getElementById(`question${questionNumber}`);
                if (currentQuestionElement) {
                    currentQuestionElement.classList.add('active');
                }
                
                updateProgressIndicators();
            }

            // معالجة اختيار الإجابة
            document.addEventListener('click', function(e) {
                if (e.target.classList.contains('option') && !e.target.classList.contains('disabled')) {
                    const questionElement = e.target.closest('.question');
                    const questionId = parseInt(questionElement.id.replace('question', ''));
                    const options = questionElement.querySelectorAll('.option');
                    const nextBtn = document.getElementById(`nextBtn${questionId}`);
                    const explanation = questionElement.querySelector('.explanation');
                    
                    // تعطيل جميع الخيارات بعد الاختيار
                    options.forEach(option => {
                        option.classList.add('disabled');
                    });
                    
                    // تحديد الخيار المختار
                    const selectedIndex = parseInt(e.target.getAttribute('data-index'));
                    e.target.classList.add('selected');
                    
                    // التحقق من الإجابة
                    const isCorrect = selectedIndex === questions[questionId].correct;
                    
                    // تسجيل الإجابة
                    userAnswers[questionId] = {
                        selectedIndex: selectedIndex,
                        answer: e.target.textContent,
                        isCorrect: isCorrect
                    };
                    
                    // تحديث النتيجة
                    if (isCorrect) score++;
                    
                    // عرض الإجابة الصحيحة والخاطئة
                    options.forEach((option, index) => {
                        if (index === questions[questionId].correct) {
                            option.classList.add('correct');
                        } else if (index === selectedIndex && !isCorrect) {
                            option.classList.add('incorrect');
                        }
                    });
                    
                    // عرض التفسير
                    explanation.textContent = questions[questionId].explanation;
                    explanation.className = `explanation show ${isCorrect ? 'correct' : 'incorrect'}`;
                    
                    // تمكين زر التالي
                    nextBtn.disabled = false;
                    
                    // تحديث دوائر التقدم
                    updateProgressIndicators();
                    
                    // إضافة حدث للزر التالي
                    nextBtn.onclick = function() {
                        if (questionId === totalQuestions - 1) {
                            showResults();
                        } else {
                            currentQuestion++;
                            showQuestion(currentQuestion);
                        }
                    };
                }
            });

            // عرض النتائج
            function showResults() {
                clearInterval(timer);
                quizContainer.style.display = 'none';
                progressIndicators.style.display = 'none';
                timerElement.style.display = 'none';
                results.classList.add('active');
                
                const percentage = Math.round((score / totalQuestions) * 100);
                
                resultName.textContent = studentNameInput.value;
                resultSection.textContent = `الشعبة ${sectionSelect.value}`;
                resultScore.textContent = `${score}/${totalQuestions}`;
                
                finalPercentage.textContent = `${percentage}%`;
                gradeCircle.textContent = `${percentage}%`;
                
                let gradeText = '';
                if (percentage >= 90) {
                    gradeText = 'ممتاز';
                    gradeCircle.style.background = '#28a745';
                } else if (percentage >= 80) {
                    gradeText = 'جيد جداً';
                    gradeCircle.style.background = '#20c997';
                } else if (percentage >= 70) {
                    gradeText = 'جيد';
                    gradeCircle.style.background = '#17a2b8';
                } else if (percentage >= 60) {
                    gradeText = 'مقبول';
                    gradeCircle.style.background = '#ffc107';
                } else {
                    gradeText = 'راسب';
                    gradeCircle.style.background = '#dc3545';
                }
                
                finalGrade.textContent = `تقدير: ${gradeText}`;
                
                // عرض التفاصيل
                showResultDetails();
                
                // العد التنازلي
                let countdownValue = 60;
                countdownElement.textContent = countdownValue;
                
                countdown = setInterval(function() {
                    countdownValue--;
                    countdownElement.textContent = countdownValue;
                    
                    if (countdownValue <= 0) {
                        clearInterval(countdown);
                        location.reload();
                    }
                }, 1000);
            }

            function showResultDetails() {
                resultDetails.innerHTML = '<h3>تفاصيل الإجابات</h3>';
                
                questions.forEach((q, index) => {
                    const reviewElement = document.createElement('div');
                    reviewElement.className = `question-review ${userAnswers[index] && userAnswers[index].isCorrect ? 'correct' : 'incorrect'}`;
                    
                    let userAnswerText = "لم يتم الإجابة";
                    let correctAnswerText = q.options[q.correct];
                    
                    if (userAnswers[index]) {
                        userAnswerText = userAnswers[index].answer;
                    }
                    
                    reviewElement.innerHTML = `
                        <div class="question-text">${index + 1}. ${q.question}</div>
                        <div class="user-answer">إجابتك: ${userAnswerText}</div>
                        <div class="correct-answer">الإجابة الصحيحة: ${correctAnswerText}</div>
                        <div class="explanation">${q.explanation}</div>
                    `;
                    
                    resultDetails.appendChild(reviewElement);
                });
            }
        });
    </script>
</body>
</html>
