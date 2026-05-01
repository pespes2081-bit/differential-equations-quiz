# differential-equations-quiz
differential-equations-quiz
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>أسئلة المعادلات التفاضلية</title>
<link href="https://fonts.googleapis.com/css2?family=Amiri:ital,wght@0,400;0,700;1,400&family=Cairo:wght@300;400;600;700;900&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0e1a;
    --surface: #111827;
    --surface2: #1a2235;
    --border: rgba(99,179,237,0.15);
    --border2: rgba(99,179,237,0.3);
    --accent: #63b3ed;
    --accent2: #90cdf4;
    --gold: #f6c90e;
    --gold2: #fde68a;
    --green: #68d391;
    --green-bg: rgba(104,211,145,0.1);
    --red: #fc8181;
    --red-bg: rgba(252,129,129,0.1);
    --text: #e2e8f0;
    --text2: #94a3b8;
    --text3: #64748b;
    --radius: 12px;
    --radius-sm: 8px;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Cairo', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    direction: rtl;
  }

  /* Background pattern */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background:
      radial-gradient(ellipse 800px 600px at 20% 10%, rgba(99,179,237,0.06) 0%, transparent 70%),
      radial-gradient(ellipse 600px 400px at 80% 80%, rgba(246,201,14,0.04) 0%, transparent 70%);
    pointer-events: none;
    z-index: 0;
  }

  .container {
    max-width: 780px;
    margin: 0 auto;
    padding: 2rem 1.25rem 4rem;
    position: relative;
    z-index: 1;
  }

  /* Header */
  .header {
    text-align: center;
    margin-bottom: 2.5rem;
    padding: 2.5rem 2rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    position: relative;
    overflow: hidden;
  }
  .header::after {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, transparent, var(--accent), var(--gold), var(--accent), transparent);
  }
  .header-icon {
    font-size: 3rem;
    margin-bottom: 0.75rem;
    display: block;
    filter: drop-shadow(0 0 20px rgba(99,179,237,0.5));
  }
  .header h1 {
    font-family: 'Amiri', serif;
    font-size: clamp(1.6rem, 4vw, 2.2rem);
    font-weight: 700;
    color: var(--accent2);
    letter-spacing: 0.02em;
    margin-bottom: 0.4rem;
  }
  .header p {
    font-size: 0.9rem;
    color: var(--text3);
    font-weight: 300;
  }

  /* Score bar */
  .score-bar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    padding: 1rem 1.5rem;
    margin-bottom: 1.25rem;
    gap: 1rem;
    flex-wrap: wrap;
  }
  .score-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .score-num {
    font-size: 1.6rem;
    font-weight: 700;
    color: var(--gold);
    line-height: 1;
  }
  .score-label { font-size: 0.8rem; color: var(--text3); }

  .progress-wrap {
    flex: 1;
    min-width: 140px;
  }
  .progress-bar {
    height: 6px;
    background: rgba(255,255,255,0.06);
    border-radius: 3px;
    overflow: hidden;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--gold));
    border-radius: 3px;
    transition: width 0.5s cubic-bezier(0.4,0,0.2,1);
  }
  .progress-text {
    font-size: 0.75rem;
    color: var(--text3);
    margin-top: 4px;
    text-align: center;
  }

  /* Section tabs */
  .tabs {
    display: flex;
    gap: 8px;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
  }
  .tab {
    padding: 8px 18px;
    border: 1px solid var(--border);
    border-radius: 50px;
    background: transparent;
    color: var(--text3);
    font-family: 'Cairo', sans-serif;
    font-size: 0.85rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s;
  }
  .tab:hover { border-color: var(--border2); color: var(--text2); }
  .tab.active {
    background: var(--accent);
    border-color: var(--accent);
    color: #0a0e1a;
  }

  /* Question card */
  .q-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.75rem;
    margin-bottom: 1.5rem;
    animation: fadeUp 0.3s ease;
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(12px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .q-meta {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 1rem;
  }
  .q-badge {
    font-size: 0.72rem;
    font-weight: 700;
    padding: 3px 10px;
    border-radius: 50px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }
  .badge-mcq { background: rgba(99,179,237,0.15); color: var(--accent); }
  .badge-tf  { background: rgba(104,211,145,0.15); color: var(--green); }
  .badge-fill{ background: rgba(246,201,14,0.15);  color: var(--gold); }
  .badge-essay{ background: rgba(167,139,250,0.15); color: #a78bfa; }

  .q-num { font-size: 0.8rem; color: var(--text3); margin-right: auto; }

  .q-text {
    font-family: 'Amiri', serif;
    font-size: 1.15rem;
    line-height: 1.9;
    color: var(--text);
    margin-bottom: 1.25rem;
    white-space: pre-line;
  }

  /* MCQ options */
  .opt {
    display: flex;
    align-items: flex-start;
    gap: 12px;
    width: 100%;
    padding: 12px 16px;
    margin-bottom: 8px;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    background: var(--surface2);
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    font-size: 0.9rem;
    color: var(--text);
    text-align: right;
    transition: all 0.18s;
    line-height: 1.6;
  }
  .opt:hover:not(:disabled) { border-color: var(--border2); background: rgba(99,179,237,0.06); }
  .opt:disabled { cursor: default; }
  .opt-letter {
    min-width: 24px;
    height: 24px;
    border-radius: 50%;
    background: rgba(255,255,255,0.06);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.78rem;
    font-weight: 700;
    flex-shrink: 0;
    margin-top: 1px;
  }
  .opt.correct { border-color: var(--green); background: var(--green-bg); }
  .opt.correct .opt-letter { background: var(--green); color: #0a0e1a; }
  .opt.wrong { border-color: var(--red); background: var(--red-bg); }
  .opt.wrong .opt-letter { background: var(--red); color: #0a0e1a; }

  /* T/F buttons */
  .tf-row { display: flex; gap: 10px; }
  .tf-btn {
    flex: 1;
    padding: 14px;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    background: var(--surface2);
    cursor: pointer;
    font-family: 'Cairo', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--text);
    transition: all 0.18s;
  }
  .tf-btn:hover:not(:disabled) { border-color: var(--border2); background: rgba(99,179,237,0.06); }
  .tf-btn:disabled { cursor: default; }
  .tf-btn.correct { border-color: var(--green); background: var(--green-bg); color: var(--green); }
  .tf-btn.wrong   { border-color: var(--red);   background: var(--red-bg);   color: var(--red); }

  /* Fill input */
  .fill-inp {
    width: 100%;
    padding: 12px 16px;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    background: var(--surface2);
    color: var(--text);
    font-family: 'Cairo', sans-serif;
    font-size: 0.95rem;
    direction: rtl;
    text-align: right;
    outline: none;
    transition: border 0.2s;
    margin-bottom: 8px;
  }
  .fill-inp:focus { border-color: var(--accent); }
  .fill-inp:disabled { opacity: 0.7; cursor: default; }

  .hint-text {
    font-size: 0.78rem;
    color: var(--text3);
    font-style: italic;
    margin-bottom: 10px;
    padding-right: 4px;
  }

  /* Essay */
  .essay-ta {
    width: 100%;
    padding: 12px 16px;
    border: 1px solid var(--border);
    border-radius: var(--radius-sm);
    background: var(--surface2);
    color: var(--text);
    font-family: 'Cairo', sans-serif;
    font-size: 0.9rem;
    direction: rtl;
    text-align: right;
    outline: none;
    resize: vertical;
    min-height: 100px;
    transition: border 0.2s;
    margin-bottom: 10px;
    line-height: 1.7;
  }
  .essay-ta:focus { border-color: #a78bfa; }

  /* Buttons */
  .btn {
    padding: 9px 20px;
    border: 1px solid var(--border2);
    border-radius: var(--radius-sm);
    background: transparent;
    color: var(--text2);
    font-family: 'Cairo', sans-serif;
    font-size: 0.85rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.18s;
  }
  .btn:hover { background: rgba(255,255,255,0.06); color: var(--text); }
  .btn-accent {
    background: var(--accent);
    border-color: var(--accent);
    color: #0a0e1a;
  }
  .btn-accent:hover { background: var(--accent2); border-color: var(--accent2); }

  /* Feedback */
  .feedback {
    margin-top: 12px;
    padding: 12px 16px;
    border-radius: var(--radius-sm);
    font-size: 0.88rem;
    line-height: 1.6;
    font-weight: 600;
  }
  .feedback.ok { background: var(--green-bg); border: 1px solid rgba(104,211,145,0.3); color: var(--green); }
  .feedback.err { background: var(--red-bg); border: 1px solid rgba(252,129,129,0.3); color: var(--red); }

  /* Model answer */
  .model-box {
    margin-top: 14px;
    padding: 14px 16px;
    background: rgba(167,139,250,0.07);
    border: 1px solid rgba(167,139,250,0.2);
    border-radius: var(--radius-sm);
    border-right: 3px solid #a78bfa;
  }
  .model-label {
    font-size: 0.75rem;
    color: #a78bfa;
    font-weight: 700;
    margin-bottom: 8px;
    letter-spacing: 0.05em;
  }
  .model-text {
    font-size: 0.9rem;
    color: var(--text2);
    line-height: 1.8;
    white-space: pre-line;
  }

  /* Navigation */
  .nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    margin-top: 0.5rem;
  }
  .nav-counter { font-size: 0.82rem; color: var(--text3); }

  /* Result screen */
  .result-screen {
    display: none;
    text-align: center;
    padding: 3rem 2rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    margin-bottom: 1.5rem;
  }
  .result-screen.show { display: block; animation: fadeUp 0.4s ease; }
  .result-big {
    font-size: 5rem;
    font-weight: 900;
    color: var(--gold);
    line-height: 1;
    margin-bottom: 0.5rem;
  }
  .result-pct { font-size: 1.1rem; color: var(--text2); margin-bottom: 1.5rem; }
  .result-grade {
    display: inline-block;
    font-size: 1.3rem;
    font-weight: 700;
    padding: 8px 28px;
    border-radius: 50px;
    margin-bottom: 2rem;
  }

  @media (max-width: 520px) {
    .score-bar { flex-direction: column; align-items: flex-start; }
    .tabs { gap: 6px; }
    .tab { padding: 7px 13px; font-size: 0.8rem; }
    .tf-row { flex-direction: column; }
  }
</style>
</head>
<body>
<div class="container">

  <div class="header">
    <span class="header-icon">∂</span>
    <h1>أسئلة المعادلات التفاضلية</h1>
    <p>Differential Equations Quiz — اختيار متعدد | صح وخطأ | أملأ الفراغ | مقالي</p>
  </div>

  <div class="score-bar">
    <div class="score-item">
      <div>
        <div class="score-num" id="score-disp">0</div>
        <div class="score-label">درجة صحيحة</div>
      </div>
    </div>
    <div class="progress-wrap">
      <div class="progress-bar"><div class="progress-fill" id="prog" style="width:0%"></div></div>
      <div class="progress-text" id="prog-text">0% مكتمل</div>
    </div>
    <div class="score-item">
      <div>
        <div class="score-num" id="answered-disp">0</div>
        <div class="score-label">سؤال مجاب</div>
      </div>
    </div>
  </div>

  <div class="tabs" id="tabs"></div>
  <div id="q-area"></div>
  <div class="result-screen" id="result-screen">
    <div class="result-big" id="r-score">0</div>
    <div class="result-pct" id="r-pct"></div>
    <div class="result-grade" id="r-grade"></div>
    <button class="btn btn-accent" onclick="restartAll()">إعادة الاختبار من البداية</button>
  </div>
  <div class="nav" id="nav-bar">
    <button class="btn" onclick="prev()">&#8594; السابق</button>
    <span class="nav-counter" id="nav-counter"></span>
    <button class="btn" onclick="next()">التالي &#8592;</button>
  </div>

</div>

<script>
const LETTERS = ['أ','ب','ج','د'];

const sections = [
  {
    id:'mcq', label:'اختيار متعدد', badge:'badge-mcq', badgeText:'MCQ',
    questions:[
      {q:"الصياغة التكاملية لمسألة القيمة الابتدائية\ndy/dx = F(x,y) , y(x₀) = y₀\nهي:",opts:["y = y₀ + ∫F(x,y)dx من x₀ إلى x","y = y₀ × ∫F(s,y)ds","y = ∫F(s,y(s))ds من x₀ إلى x","y = y₀ + ∫F(s,y(s))ds من x₀ إلى x"],ans:3},
      {q:"طريقة التقريبات المتتالية (بيكار) تبدأ بأخذ التقريب الأول من:",opts:["الشرط الابتدائي y₀","الصفر","المشتقة","الدالة المجهولة مباشرة"],ans:0},
      {q:"التقريب الثاني في طريقة بيكار يُحسب بالصيغة:",opts:["y₂ = y₀ + ∫F(s, y₁(s))ds من x₀ إلى x","y₂ = y₁ + F(x,y₁)","y₂ = ∫F(s,y₀)ds","y₂ = y₁ × F(x,y₁)"],ans:0},
      {q:"نظرية الوجود والوحدانية (بيكار-ليندلوف) تضمن وجود حل وحيد إذا كانت F(x,y):",opts:["مستمرة فقط","قابلة للتكامل","مستمرة وتحقق شرط ليبشتز بالنسبة لـ y","تفاضلية فقط"],ans:2},
      {q:"شرط ليبشتز يعني أنه يوجد ثابت K > 0 بحيث:",opts:["|F(x,y₁) - F(x,y₂)| ≤ K|y₁ - y₂|","|F(x,y₁) - F(x,y₂)| = K","|F(x,y₁)| ≤ K","F(x,y₁) = F(x,y₂)"],ans:0},
      {q:"تسمى الدالة التي تحقق المعادلة التفاضلية والشرط الابتدائي معاً بـ:",opts:["الحل العام","الحل الخاص","حل مسألة القيمة الابتدائية","الحل التقريبي"],ans:2},
      {q:"المعادلات التفاضلية تُستخدم كنماذج رياضية لـ:",opts:["الظواهر الفيزيائية فقط","الاقتصاد فقط","ظواهر فيزيائية واقتصادية وبيولوجية وهندسية","العمليات الحسابية البحتة"],ans:2},
      {q:"الحل العام للمعادلة التفاضلية هو:",opts:["حل خاص واحد","عائلة من الحلول تحتوي على ثوابت اعتباطية","الحل الذي يحقق الشرط الابتدائي فقط","تقريب عددي للحل"],ans:1},
      {q:"مسألة القيمة الابتدائية تتكون من:",opts:["معادلة تفاضلية فقط","شرط ابتدائي فقط","معادلة تفاضلية + شرط ابتدائي يحدد الحالة","حل خاص + حل عام"],ans:2},
      {q:"متتالية بيكار تتقارب نحو الحل الحقيقي عندما تكون F:",opts:["ثابتة","مستمرة وتحقق شرط ليبشتز","خطية فقط","من الدرجة الثانية"],ans:1},
      {q:"نظرية كرونوول تُستخدم في المعادلات التفاضلية لإثبات:",opts:["وجود الحل فقط","وحدانية الحل عبر تقدير الفرق بين حلين","تقارب المتتالية","استمرارية الدالة F"],ans:1},
      {q:"إذا كانت ∂F/∂y محدودة على منطقة مغلقة، فإن شرط ليبشتز:",opts:["لا يتحقق","يتحقق تلقائياً","يتطلب إثباتاً إضافياً","يعتمد على x فقط"],ans:1},
      {q:"الهدف من دراسة نظرية المعادلات التفاضلية هو:",opts:["إيجاد صيغ صريحة لكل المعادلات","فهم سلوك الحل حتى بدون حل صريح","حل المعادلات الجبرية","رسم الرسوم البيانية"],ans:1},
      {q:"في نظرية بيكار-ليندلوف، يُشترط أن تكون F مستمرة على منطقة D تحتوي على النقطة:",opts:["الأصل (0,0)","(x₀, y₀)","(1, 1)","(x₀, 0)"],ans:1},
      {q:"الصياغة التكاملية للمسألة الثانية\ny'' + g(t,y) = 0 , y(0)=y₀ , y'(0)=z₀\nهي:",opts:["y(t) = y₀ + z₀t − ∫₀ᵗ(t−s)g(s,y(s))ds","y(t) = ∫g(t,y)dt","y(t) = y₀ + ∫y'(s)ds","y(t) = z₀t + y₀"],ans:0},
      {q:"الهدف من مسألة القيمة الابتدائية ليس فقط إيجاد دالة تحقق المعادلة بل أيضاً:",opts:["إيجاد ثوابت المعادلة","إيجاد حل معروف على المجال R","تحديد الشرط الابتدائي","حساب المشتقة"],ans:1},
      {q:"طريقة التقريبات المتتالية تُسمى أيضاً:",opts:["طريقة أويلر","طريقة رونج-كوتا","طريقة بيكار","طريقة تايلور"],ans:2},
      {q:"في الرياضيات التطبيقية، المعادلة التفاضلية كنموذج رياضي يهدف إلى:",opts:["تمثيل ظاهرة واقعية وفهم سلوكها","حل معادلات جبرية","إيجاد النهايات","دراسة التفاضل فقط"],ans:0},
      {q:"الدالة F(x,y) = 2xy تحقق شرط ليبشتز على المستطيل لأن:",opts:["F ثابتة","∂F/∂y = 2x محدودة على المستطيل","F تساوي صفراً","المعادلة خطية"],ans:1},
      {q:"حل مسألة القيمة الابتدائية y' = y , y(0)=1 هو:",opts:["y = x","y = eˣ","y = ln(x)","y = x²"],ans:1}
    ]
  },
  {
    id:'tf', label:'صح / خطأ', badge:'badge-tf', badgeText:'صح / خطأ',
    questions:[
      {q:"المعادلة التفاضلية هي معادلة تربط دالة مجهولة بمشتقاتها أو تفاضلاتها.",ans:true},
      {q:"الصياغة التكاملية والمعادلة التفاضلية مع الشرط الابتدائي متكافئتان تماماً.",ans:true},
      {q:"طريقة بيكار للتقريبات المتتالية تبدأ دائماً من التقريب y₁ = 0.",ans:false,explain:"تبدأ من الشرط الابتدائي y₀ وليس الصفر."},
      {q:"في نظرية الوجود والوحدانية، يكفي أن تكون F مستمرة فقط لضمان وحدانية الحل.",ans:false,explain:"الاستمرار يضمن الوجود فقط، أما الوحدانية فتحتاج شرط ليبشتز."},
      {q:"شرط ليبشتز هو: |F(x,y₁)−F(x,y₂)| ≤ K|y₁−y₂| لثابت K موجب.",ans:true},
      {q:"إذا كانت ∂F/∂y محدودة ومستمرة على منطقة، فإن F تحقق شرط ليبشتز تلقائياً.",ans:true},
      {q:"الحل الخاص هو الحل الذي يحقق شرطاً ابتدائياً محدداً.",ans:true},
      {q:"المعادلات التفاضلية لا تُستخدم في نمذجة الظواهر الفيزيائية.",ans:false,explain:"المعادلات التفاضلية أساسية في نمذجة كل الظواهر الفيزيائية."},
      {q:"متتالية بيكار تتقارب نحو الحل الحقيقي عندما تحقق F شرط ليبشتز.",ans:true},
      {q:"نظرية كرونوول تُستخدم لإثبات وحدانية حل مسألة القيمة الابتدائية.",ans:true},
      {q:"الحل العام يحتوي على ثوابت اعتباطية بينما الحل الخاص لا يحتوي عليها.",ans:true},
      {q:"وجود حل لمسألة القيمة الابتدائية يعني دائماً وحدانية الحل.",ans:false,explain:"الوجود لا يستلزم الوحدانية، الوحدانية تحتاج شرطاً إضافياً (ليبشتز)."},
      {q:"الدالة F(x,y)=y² تحقق شرط ليبشتز على أي مستطيل مغلق محدود.",ans:true},
      {q:"طريقة بيكار تُعطي دائماً الحل الدقيق في التقريب الأول.",ans:false,explain:"التقريب الأول تقريبي، الدقة تزداد تدريجياً مع زيادة التقريبات."},
      {q:"نظرية بيكار-ليندلوف تضمن حلاً وحيداً في جوار النقطة الابتدائية وليس بالضرورة على كامل R.",ans:true},
      {q:"الصياغة التكاملية للدرجة الثانية هي: y(t)=y₀+z₀t−∫₀ᵗ(t−s)g(s,y(s))ds.",ans:true},
      {q:"لا يشترط في الحل أن يكون محدوداً على كامل المحور الحقيقي.",ans:true},
      {q:"الهدف الرئيسي من نظرية المعادلات التفاضلية هو فهم سلوك الحل وليس فقط إيجاده.",ans:true},
      {q:"الحل الخاص لـ y'=y , y(0)=1 هو y=eˣ.",ans:true},
      {q:"إذا كانت F(x,y)=|y|، فإنها تحقق شرط ليبشتز بثابت K=1.",ans:true}
    ]
  },
  {
    id:'fill', label:'أملأ الفراغ', badge:'badge-fill', badgeText:'فراغ',
    questions:[
      {q:"الصياغة التكاملية: y(x) = y₀ + ∫ _______ ds من x₀ إلى x",ans:"F(s,y(s))",hint:"الدالة داخل التكامل"},
      {q:"تتحقق نظرية الوجود والوحدانية إذا كانت F مستمرة وتحقق شرط _______",ans:"ليبشتز",hint:"اسم الشرط الرياضي المطلوب"},
      {q:"شرط ليبشتز: |F(x,y₁)−F(x,y₂)| ≤ _______ × |y₁−y₂|",ans:"K",hint:"ثابت موجب"},
      {q:"التقريب الأول في بيكار: y₁(x) = y₀ + ∫ F(s, _______) ds",ans:"y₀",hint:"التقريب الصفري"},
      {q:"طريقة التقريبات المتتالية تُسمى أيضاً طريقة _______",ans:"بيكار",hint:"اسم عالم رياضيات فرنسي"},
      {q:"نظرية _______ تُستخدم لإثبات وحدانية الحل",ans:"كرونوول",hint:"نظرية مشهورة في التحليل"},
      {q:"الحل العام يحتوي على ثوابت _______ بينما الحل الخاص لا يحتوي",ans:"اعتباطية",hint:"ثوابت غير محددة القيمة"},
      {q:"في الصياغة التكاملية للدرجة الثانية: y(t) = y₀ + z₀t − ∫(t−s) _______ ds",ans:"g(s,y(s))",hint:"الدالة في المعادلة التفاضلية"},
      {q:"نظرية بيكار-ليندلوف تضمن حلاً _______ في جوار النقطة الابتدائية",ans:"وحيداً",hint:"صفة الحل من حيث عدده"},
      {q:"يُقال أن الدالة F تحقق شرط ليبشتز إذا كانت المشتقة الجزئية _______ محدودة",ans:"∂F/∂y",hint:"المشتقة الجزئية بالنسبة لـ y"}
    ]
  },
  {
    id:'essay', label:'مقالي', badge:'badge-essay', badgeText:'مقالي',
    questions:[
      {q:"عرّف المعادلة التفاضلية واذكر مثالاً على تطبيقها في الفيزياء.",model:"المعادلة التفاضلية هي معادلة تربط دالة مجهولة y بمشتقاتها.\nمثال: قانون نيوتن F=ma يمكن كتابته m·y''=F(t,y,y') لوصف حركة جسم.\nمثال آخر: dy/dt = ky تصف النمو الأسي (نمو جرثومي أو تحلل مشع)."},
      {q:"ما الفرق بين الحل العام والحل الخاص لمعادلة تفاضلية؟",model:"الحل العام: يحتوي على ثوابت اعتباطية ويمثل عائلة من الحلول.\nمثال: y = Ce^x هو الحل العام لـ y'=y.\n\nالحل الخاص: يتحدد بتطبيق شرط ابتدائي يُعين قيمة الثابت.\nمثال: إذا y(0)=1 فإن C=1 والحل الخاص y=eˣ."},
      {q:"ما المقصود بمسألة القيمة الابتدائية؟ وما مكوناتها الأساسية؟",model:"مسألة القيمة الابتدائية تتكون من:\n1) معادلة تفاضلية: dy/dx = F(x,y) تمثل القانون العام للنظام.\n2) شرط ابتدائي: y(x₀) = y₀ يحدد الحالة الابتدائية.\n\nالهدف: إيجاد دالة تحقق كلاً من المعادلة والشرط الابتدائي معاً."},
      {q:"اشرح طريقة بيكار للتقريبات المتتالية مع كتابة صيغة التقريبات.",model:"نبدأ بالتقريب الصفري: y₀(x) = y₀ (الشرط الابتدائي)\nثم نبني المتتالية:\n  y_{n+1}(x) = y₀ + ∫_{x₀}^{x} F(s, y_n(s)) ds\n\nنكرر العملية حتى يتقارب y_n إلى الحل الحقيقي.\nالمتتالية تتقارب إذا حققت F شرط ليبشتز على المنطقة."},
      {q:"اذكر وأشرح شرط ليبشتز، ولماذا هو مهم في نظرية الوجود والوحدانية؟",model:"شرط ليبشتز: تحقق F الشرط إذا وُجد K>0 بحيث:\n  |F(x,y₁) − F(x,y₂)| ≤ K|y₁ − y₂|\nلكل (x,y₁),(x,y₂) في المنطقة D.\n\nالأهمية:\n- يضمن عدم التذبذب الحاد للدالة.\n- يمنع وجود حلين مختلفين لنفس الشرط الابتدائي (الوحدانية).\n- إذا كانت ∂F/∂y موجودة ومحدودة فإن الشرط يتحقق تلقائياً."},
      {q:"ما دور نظرية كرونوول في إثبات وحدانية حل مسألة القيمة الابتدائية؟",model:"لإثبات الوحدانية نفرض وجود حلين y₁ و y₂، ونُعرّف:\n  u(x) = |y₁(x) − y₂(x)|\n\nباستخدام شرط ليبشتز نحصل على:\n  u(x) ≤ K ∫_{x₀}^{x} u(s) ds\n\nبتطبيق نظرية كرونوول نستنتج u(x) = 0\nأي y₁(x) = y₂(x)، مما يثبت الوحدانية."},
      {q:"لماذا ندرس نظرية المعادلات التفاضلية رغم صعوبة إيجاد حل صريح؟",model:"معظم المعادلات التفاضلية لا تملك حلاً صريحاً بصيغة مغلقة.\nلكن النظرية تمكّننا من:\n1) معرفة ما إذا كان الحل موجوداً أصلاً.\n2) إثبات وحدانية الحل.\n3) دراسة سلوك الحل (استقرار، حدود، تذبذب).\n4) الحصول على حلول تقريبية دقيقة (بيكار، رونج-كوتا)."},
      {q:"ما المقصود بالنمذجة الرياضية باستخدام المعادلات التفاضلية؟ أعطِ ثلاثة أمثلة.",model:"النمذجة الرياضية: صياغة ظاهرة واقعية كمعادلة تفاضلية لفهمها والتنبؤ بها.\n\nأمثلة:\n1) حركة بندول: θ'' + (g/L)sin(θ) = 0\n2) نمو جرثومي: dN/dt = kN\n3) دوائر كهربائية: L(dI/dt) + RI = V(t)\n\nالنمذجة تربط الرياضيات بالواقع وتسمح باستنتاج نتائج عملية."},
      {q:"اثبت أن الصياغة التكاملية مكافئة لمسألة القيمة الابتدائية.",model:"مسألة القيمة الابتدائية: y' = F(x,y) , y(x₀)=y₀\n\nاتجاه (←): إذا y'=F(x,y) وy(x₀)=y₀، نكامل من x₀ إلى x:\n  ∫_{x₀}^{x} y'(s)ds = ∫_{x₀}^{x} F(s,y(s))ds\n  y(x) − y(x₀) = ∫_{x₀}^{x} F(s,y(s))ds\n  y(x) = y₀ + ∫_{x₀}^{x} F(s,y(s))ds ✓\n\nاتجاه (→): إذا y(x) = y₀ + ∫F(s,y(s))ds، نفاضل:\n  y'(x) = F(x,y(x))\nوبوضع x=x₀: y(x₀) = y₀ ✓"},
      {q:"ما شروط نظرية بيكار-ليندلوف؟ وماذا تضمن؟",model:"الشروط:\n1) F مستمرة على مستطيل D = {|x−x₀|≤a, |y−y₀|≤b} يحتوي (x₀,y₀).\n2) F تحقق شرط ليبشتز بالنسبة لـ y على D.\n\nالنتيجة: توجد فترة I=[x₀−h, x₀+h] حيث h=min(a, b/M)\nوM=max|F| على D، بحيث توجد دالة y واحدة فقط تحقق:\n  y'=F(x,y) , y(x₀)=y₀ على I."}
    ]
  }
];

let curSec=0, curQ=0, score=0;
const answered={};

function key(){ return curSec+'-'+curQ; }

function buildTabs(){
  const el=document.getElementById('tabs');
  el.innerHTML=sections.map((s,i)=>
    `<button class="tab${i===0?' active':''}" onclick="goSection(${i})">${s.label}</button>`
  ).join('');
}

function goSection(i){
  curSec=i; curQ=0;
  document.querySelectorAll('.tab').forEach((t,j)=>t.classList.toggle('active',j===i));
  render();
}

function render(){
  const sec=sections[curSec];
  const q=sec.questions[curQ];
  const k=key();
  const done=answered[k];
  let html='';

  html+=`<div class="q-card">`;
  html+=`<div class="q-meta">
    <span class="q-badge ${sec.badge}">${sec.badgeText}</span>
    <span class="q-num">سؤال ${curQ+1} / ${sec.questions.length}</span>
  </div>`;
  html+=`<div class="q-text">${q.q}</div>`;

  if(curSec===0){
    q.opts.forEach((o,i)=>{
      let cls='opt';
      if(done!==undefined){
        if(i===q.ans) cls+=' correct';
        else if(i===done && done!==q.ans) cls+=' wrong';
      }
      html+=`<button class="${cls}" onclick="answerMCQ(${i})" ${done!==undefined?'disabled':''}>
        <span class="opt-letter">${LETTERS[i]}</span><span>${o}</span>
      </button>`;
    });
    if(done!==undefined){
      const ok=done===q.ans;
      html+=`<div class="feedback ${ok?'ok':'err'}">${ok?'✓ إجابة صحيحة!':'✗ الإجابة الصحيحة: '+LETTERS[q.ans]+') '+q.opts[q.ans]}</div>`;
    }
  }

  else if(curSec===1){
    let c1='tf-btn',c2='tf-btn';
    if(done!==undefined){
      if(q.ans===true){c1+=' correct'; if(done===false) c2+=' wrong';}
      else{c2+=' correct'; if(done===true) c1+=' wrong';}
    }
    html+=`<div class="tf-row">
      <button class="${c1}" onclick="answerTF(true)" ${done!==undefined?'disabled':''}>✓ صح</button>
      <button class="${c2}" onclick="answerTF(false)" ${done!==undefined?'disabled':''}>✗ خطأ</button>
    </div>`;
    if(done!==undefined){
      const ok=done===q.ans;
      let fb=ok?'✓ إجابة صحيحة!':'✗ الإجابة هي: '+(q.ans?'صح':'خطأ');
      if(!ok && q.explain) fb+=' — '+q.explain;
      html+=`<div class="feedback ${ok?'ok':'err'}">${fb}</div>`;
    }
  }

  else if(curSec===2){
    const val=done||'';
    html+=`<input class="fill-inp" id="fill-inp" type="text" placeholder="اكتب إجابتك هنا..." value="${val}" ${done?'disabled':''}/>`;
    if(q.hint) html+=`<div class="hint-text">💡 تلميح: ${q.hint}</div>`;
    if(!done) html+=`<button class="btn btn-accent" onclick="checkFill()">تحقق من الإجابة</button>`;
    if(done){
      const ok=normalize(done)===normalize(q.ans);
      html+=`<div class="feedback ${ok?'ok':'err'}">${ok?'✓ إجابة صحيحة!':'✗ الإجابة الصحيحة: '+q.ans}</div>`;
    }
  }

  else if(curSec===3){
    html+=`<textarea class="essay-ta" id="essay-ta" placeholder="اكتب إجابتك هنا...">${done||''}</textarea>`;
    if(!done){
      html+=`<button class="btn btn-accent" onclick="showModel()">عرض الإجابة النموذجية</button>`;
    } else {
      html+=`<div class="model-box"><div class="model-label">الإجابة النموذجية</div><div class="model-text">${q.model}</div></div>`;
    }
  }

  html+=`</div>`;
  document.getElementById('q-area').innerHTML=html;

  const total=sections.reduce((a,s)=>a+s.questions.length,0);
  const doneCount=Object.keys(answered).length;
  const pct=Math.round(doneCount/total*100);
  document.getElementById('prog').style.width=pct+'%';
  document.getElementById('prog-text').textContent=pct+'% مكتمل';
  document.getElementById('score-disp').textContent=score;
  document.getElementById('answered-disp').textContent=doneCount;
  document.getElementById('nav-counter').textContent=`${curQ+1} / ${sec.questions.length}`;

  if(doneCount===total){
    document.getElementById('result-screen').classList.add('show');
    const pctScore=Math.round(score/total*100);
    document.getElementById('r-score').textContent=score+'/'+total;
    document.getElementById('r-pct').textContent='نسبة إجاباتك الصحيحة: '+pctScore+'%';
    let grade='', gcls='';
    if(pctScore>=90){grade='ممتاز 🏆';gcls='background:#f6c90e;color:#0a0e1a';}
    else if(pctScore>=75){grade='جيد جداً ⭐';gcls='background:rgba(104,211,145,0.2);color:#68d391;border:1px solid #68d391';}
    else if(pctScore>=60){grade='جيد 👍';gcls='background:rgba(99,179,237,0.2);color:#63b3ed;border:1px solid #63b3ed';}
    else{grade='بحاجة لمراجعة 📚';gcls='background:rgba(252,129,129,0.15);color:#fc8181;border:1px solid #fc8181';}
    document.getElementById('r-grade').textContent=grade;
    document.getElementById('r-grade').style.cssText=gcls;
  }
}

function normalize(s){ return s.trim().replace(/\s+/g,' '); }

function answerMCQ(i){
  if(answered[key()]!==undefined)return;
  answered[key()]=i;
  if(i===sections[curSec].questions[curQ].ans)score++;
  render();
}
function answerTF(v){
  if(answered[key()]!==undefined)return;
  answered[key()]=v;
  if(v===sections[curSec].questions[curQ].ans)score++;
  render();
}
function checkFill(){
  const inp=document.getElementById('fill-inp');
  if(!inp||!inp.value.trim())return;
  const k=key();
  answered[k]=inp.value.trim();
  const ok=normalize(inp.value)===normalize(sections[curSec].questions[curQ].ans);
  if(ok)score++;
  render();
}
function showModel(){
  const ta=document.getElementById('essay-ta');
  answered[key()]=ta?ta.value:'(تم الاطلاع على النموذج)';
  render();
}
function next(){
  const sec=sections[curSec];
  if(curQ<sec.questions.length-1){curQ++;render();}
  else if(curSec<sections.length-1){goSection(curSec+1);}
}
function prev(){
  if(curQ>0){curQ--;render();}
  else if(curSec>0){
    curSec--;curQ=sections[curSec].questions.length-1;
    document.querySelectorAll('.tab').forEach((t,j)=>t.classList.toggle('active',j===curSec));
    render();
  }
}
function restartAll(){
  Object.keys(answered).forEach(k=>delete answered[k]);
  score=0; curSec=0; curQ=0;
  document.querySelectorAll('.tab').forEach((t,j)=>t.classList.toggle('active',j===0));
  document.getElementById('result-screen').classList.remove('show');
  render();
}

buildTabs();
render();
</script>
</body>
</html>
