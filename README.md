<!DOCTYPE html>
<html lang="ka">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>აუდიო ქვიზი - გულის ტონები</title>
  <style>
    body {
      font-family: sans-serif;
      max-width: 700px;
      margin: auto;
      padding: 20px;
    }
    .question {
      margin-bottom: 30px;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 12px;
    }
    button {
      margin: 5px 0;
      display: block;
      padding: 10px;
      width: 100%;
      border-radius: 8px;
      border: 1px solid #888;
      cursor: pointer;
    }
    .correct {
      background-color: #c8f7c5;
    }
    .wrong {
      background-color: #f8d7da;
    }
    audio {
      margin: 10px 0;
    }
  </style>
</head>
<body>
<h2>გულის ტონების სავარჯიშო ქვიზი</h2>
<div id="quiz-container"></div>
<script>
const quizData = [
{
      audio: "audio/1.mp3",
      correct: "გულის მესამე ტონი",
      choices: ['გულის მესამე ტონი', 'გულის მე-4 ტონი', 'პირველი ტონის გახლეჩა', 'მეორე ტონის გახლეჩა-გაორება']
    },
{
      audio: "audio/2.mp3",
      correct: "გულის მე-4 ტონი",
      choices: ['გულის მე-4 ტონი', 'გულის მესამე ტონი', 'ტკაცუნა პირველი ტონი', 'ფუნქციური სისტოლური შუილი']
    },
{
      audio: "audio/3.mp3",
      correct: "პირველი ტონის გახლეჩა",
      choices: ['პირველი ტონის გახლეჩა', 'მეორე ტონის გახლეჩა-გაორება', 'პერიკარდიუმის ხახუნის ხმიანობა', 'ჰოლოსისტოლური შუილი']
    },
{
      audio: "audio/4.mp3",
      correct: "მეორე ტონის გახლეჩა-გაორება",
      choices: ['მეორე ტონის გახლეჩა-გაორება', 'პირველი ტონის გახლეჩა', 'გულის მესამე ტონი', 'კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება']
    },
{
      audio: "audio/5.mp3",
      correct: "პერიკარდიუმის ხახუნის ხმიანობა",
      choices: ['პერიკარდიუმის ხახუნის ხმიანობა', 'ტკაცუნა პირველი ტონი', 'მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე', 'ფუნქციური სისტოლური შუილი']
    },
{
      audio: "audio/6.mp3",
      correct: "ტკაცუნა პირველი ტონი",
      choices: ['ტკაცუნა პირველი ტონი', 'გულის მესამე ტონი', 'გულის მე-4 ტონი', 'მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტაზე']
    },
{
      audio: "audio/7.mp3",
      correct: "მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტაზე",
      choices: ['მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტოზე', 'მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტოზე', 'კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება', 'ჰოლოსისტოლური შუილი']
    },
{
      audio: "audio/8.mp3",
      correct: "მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტაზე",
      choices: ['მეორე ტონის შესუსტება და დეკრეშჩენდოს ტიპის დიასტოლური შუილი აორტოზე', 'მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტოზე', 'ფუნქციური სისტოლური შუილი', 'პერიკარდიუმის ხახუნის ხმიანობა']
    },
{
      audio: "audio/9.mp3",
      correct: "კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება",
      choices: ['კრეშჩენდო-დეკრეშჩენდო ტიპის სისტოლური შუილი, მეორე ტონის გაორება', 'ფუნქციური სისტოლური შუილი', 'ჰოლოსისტოლური შუილი', 'გულის მესამე ტონი']
    },
{
      audio: "audio/10.mp3",
      correct: "ფუნქციური სისტოლური შუილი",
      choices: ['ფუნქციური სისტოლური შუილი', 'ჰოლოსისტოლური შუილი', 'მეორე ტონის გახლეჩა-გაორება', 'ტკაცუნა პირველი ტონი']
    },
{
      audio: "audio/11.mp3",
      correct: "ჰოლოსისტოლური შუილი",
      choices: ['ჰოლოსისტოლური შუილი', 'ფუნქციური სისტოლური შუილი', 'პერიკარდიუმის ხახუნის ხმიანობა', 'მეორე ტონის შესუსტება და უხეში სისტოლური შუილი აორტოზე']
    },

];
const container = document.getElementById('quiz-container');
quizData.forEach((q, index) => {
  const div = document.createElement('div');
  div.className = 'question';
  div.innerHTML = `<h3>კითხვა ${index + 1}</h3><audio controls src="${q.audio}"></audio>`;
  q.choices.forEach(choice => {
    const btn = document.createElement('button');
    btn.textContent = choice;
    btn.onclick = () => {
      btn.classList.add(choice === q.correct ? 'correct' : 'wrong');
      Array.from(div.querySelectorAll('button')).forEach(b => {
        if (b.textContent === q.correct) b.classList.add('correct');
        b.disabled = true;
      });
    };
    div.appendChild(btn);
  });
  container.appendChild(div);
});
</script>
</body>
</html>
