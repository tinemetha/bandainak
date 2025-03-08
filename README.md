<div class="codepen" data-height="300" data-default-tab="css,result" data-slug-hash="ogNwryb" data-pen-title="lanna-card-game" data-user="MT-C"  data-prefill='{"title":"lanna-card-game","tags":[],"scripts":[],"stylesheets":[]}'>
  <pre data-lang="html">&lt;!DOCTYPE html>
&lt;html lang="en">
&lt;head>
    &lt;meta charset="UTF-8">
    &lt;meta name="viewport" content="width=device-width, initial-scale=1.0">
    &lt;title>บันไดนาค ตามฮอยลวดลายล้านนา&lt;/title>
    &lt;link rel="stylesheet" href="style.css">
&lt;/head>
&lt;body>
    &lt;div class="container">
        &lt;h1>บันไดนาค ตามฮอยลวดลายล้านนา&lt;/h1>
        &lt;p>Click "Draw Cards" to get your set of cards!&lt;/p>

        &lt;div id="card-container">
        
            &lt;div class="card" id="pattern-card-1">&lt;/div>
            &lt;div class="card" id="pattern-card-2">&lt;/div>
            &lt;div class="card" id="inspiration-card">&lt;/div>
        &lt;/div>
        &lt;button onclick="drawCards()">Draw Cards&lt;/button>
        &lt;p id="special-card">&lt;/p>
    &lt;/div>

    &lt;script src="script.js">&lt;/script>
&lt;/body>
&lt;/html>
</pre>
  <pre data-lang="css">body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 0;
    background-color: #f9f5eb;
}

.container {
    width: 80%;
    margin: 0 auto;
}

h1 {
    font-size: 36px;
    color: #333;
}

#pattern-card-1, #pattern-card-2, #pattern-card-3, #inspiration-card, #special-card {
  margin: 10px;
  font-size: 16px;
}
button {
  padding: 10px 20px;
  margin-top: 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  cursor: pointer;
}
button:hover {
  background-color: #45a049;
}


#card-container {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin-top: 30px;
}

.card {
    width: 200px;
    height: 120px;
    padding: 20px;
    background-color: #ffffff;
    border: 2px solid #333;
    border-radius: 8px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
}

#special-card {
    margin-top: 20px;
    font-weight: bold;
}
</pre>
  <pre data-lang="js">// กองการ์ดลวดลายล้านนา (Updated)
const patterns = {
  floral: [
    "ดอกพิกุล", "ดอกบัว", "ดอกจอก", "ดอกพุดตาน", "ดอกประจำยาม", "ดอกกล้วยไม้", "ดอกกุหลาบ"
  ],
  animals: [
    "นาค", "กุญชรวารี", "หงส์", "สิงห์", "นกยูง", "กิเลน", "พญาลวง", "ตัวมอม"
  ],
  basicLines: [
    "ลวดลายโค้ง", "เส้นนอน", "เส้นตั้ง", "ลวดลายขดหอย", "ลวดลายเส้นคลื่น"
  ],
  nature: [
    "ภูเขา", "เมฆ", "สายน้ำ", "พระอาทิตย์", "พระจันทร์"
  ]
};

// กองการ์ดแรงบันดาลใจ 
const inspirations = [
  "ยี่เป็ง", "สงกรานต์", "งานปอยหลวง", "สีแดง", "สีเหลือง", "สีดำ",
  "กลองสะบัดชัย", "ลูกข่าง", "วัดพระธาตุดอยสุเทพ", "ประตูท่าแพ"
];

// กองการ์ดอุปสรรค
const obstacles = [
  "ใช้สีโทนอ่อนเท่านั้น", "ออกแบบโดยใช้ลวดลายได้ไม่เกิน 3 แบบ", "ห้ามใช้สีแดง", 
  "เวลาลดลง 5 นาที", "ต้องรวมลวดลายจากการ์ดทุกใบ", "ต้องใช้อุปกรณ์เฉพาะ"
];

// ฟังก์ชันสุ่มการ์ดจากกองที่กำหนด โดยไม่ให้ซ้ำ
function drawRandomCard(deck) {
  const randomIndex = Math.floor(Math.random() * deck.length);
  const card = deck[randomIndex];
  deck.splice(randomIndex, 1); // ลบการ์ดที่เลือกออกจากกอง
  return card;
}

// ฟังก์ชันสุ่มการ์ดทั้งหมด
function drawCards() {
  const availablePatterns = [
    ...patterns.floral, 
    ...patterns.animals, 
    ...patterns.basicLines, 
    ...patterns.nature
  ]; // รวมกองการ์ดลวดลายทั้งหมด
  const patternCard1 = drawRandomCard(availablePatterns); // การ์ดลวดลายล้านนา 1
  const patternCard2 = drawRandomCard(availablePatterns); // การ์ดลวดลายล้านนา 2
  const inspirationCard = drawRandomCard(inspirations); // การ์ดแรงบันดาลใจ

  const isExplosion = Math.random() &lt; 0.2; // 20% โอกาสเจอการ์ดระเบิด
  const specialMessage = isExplosion 
    ? `💥 การ์ดระเบิด! คุณได้รับอุปสรรค: ${drawRandomCard(obstacles)}`
    : "✨ ไม่มีอุปสรรค!";

  // แสดงผลการ์ด
  document.getElementById("pattern-card-1").innerHTML = `&lt;strong>Pattern 1:&lt;/strong> ${patternCard1}`;
  document.getElementById("pattern-card-2").innerHTML = `&lt;strong>Pattern 2:&lt;/strong> ${patternCard2}`;
  document.getElementById("inspiration-card").innerHTML = `&lt;strong>Inspiration:&lt;/strong> ${inspirationCard}`;
  document.getElementById("special-card").innerHTML = specialMessage;

  document.getElementById("special-card").style.color = isExplosion ? "red" : "green";
}
</pre></div>
<script async src="https://public.codepenassets.com/embed/index.js"></script>
