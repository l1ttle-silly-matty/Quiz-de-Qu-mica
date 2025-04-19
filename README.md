<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz - Classificação da Matéria</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Montserrat', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #800020; /* Cor vinho */
            color: #fff;
            text-align: center;
        }
        h1, h2 {
            margin-top: 20px;
        }
        .question {
            margin-bottom: 30px;
            padding: 20px;
            background: #fff;
            color: #333;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
            max-width: 600px;
            margin-left: auto;
            margin-right: auto;
        }
        .options button {
            margin: 10px 0;
            padding: 10px 15px;
            background-color: #eee;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            width: 100%;
            text-align: left;
            font-size: 16px;
        }
        .options button:hover {
            background-color: #ddd;
        }
        .explanation {
            display: none;
            margin-top: 15px;
            padding: 15px;
            background: #e0f7fa;
            border-left: 5px solid #00796b;
            border-radius: 5px;
        }
        .correct {
            color: green;
            font-weight: bold;
        }
        .incorrect {
            color: red;
            font-weight: bold;
        }
        .explanation p {
            font-size: 14px;
        }
        .mark-letter {
            font-weight: bold;
        }
    </style>
</head>
<body>

<h1>Quiz - Classificação da Matéria</h1>

<section>
    <h2>Resumo Rápido</h2>
    <p>A matéria pode ser classificada em <strong>substâncias puras</strong> (simples ou compostas) e <strong>misturas</strong> (homogêneas ou heterogêneas).</p>
    <p>Transformações podem ser <strong>físicas</strong> (sem alterar a composição) ou <strong>químicas</strong> (com formação de novas substâncias).</p>
</section>

<hr>

<div id="quiz-container"></div>

<script>
const questions = [
    {
        text: "1. Qual das alternativas a seguir contém apenas substâncias compostas?",
        options: {
            a: "N2, P4, S8",
            b: "CO, He, NH3",
            c: "CO2, H2O, C6H12O6",
            d: "N2, O3, H2O",
            e: "H2O, I2, Cl2"
        },
        correct: "c",
        explanation: "Substâncias compostas são formadas por dois ou mais elementos químicos. Exemplo: CO2 (carbono + oxigênio), H2O (hidrogênio + oxigênio)."
    },
    {
        text: "2. O número de substâncias simples entre O3, H2O, Na, P4, CH4, CO2 e CO é:",
        options: {
            a: "2",
            b: "3",
            c: "4",
            d: "5",
            e: "7"
        },
        correct: "c",
        explanation: "Substâncias simples são formadas por apenas um tipo de elemento químico. Exemplo: O3, Na, P4."
    },
    {
        text: "3. Considerando a reação: C + H2O → CO + H2, entre reagentes e produtos estão presentes:",
        options: {
            a: "2 substâncias simples e 2 compostas",
            b: "1 substância simples e 3 compostas",
            c: "3 substâncias simples e 1 composta",
            d: "4 substâncias simples",
            e: "4 substâncias compostas"
        },
        correct: "a",
        explanation: "C (carbono) e H2 (hidrogênio) são substâncias simples; H2O (água) e CO (monóxido de carbono) são compostas."
    },
    {
        text: "4. Complete: \"Uma substância ____ é formada por ____, contendo apenas ____ de um mesmo ____.\"",
        options: {
            a: "composta; moléculas; elementos; átomo",
            b: "composta; moléculas; átomos; elemento",
            c: "química; elementos; moléculas; átomo",
            d: "simples; átomos; moléculas; elemento",
            e: "simples; moléculas; átomos; elemento"
        },
        correct: "d",
        explanation: "Substância simples possui átomos de um único elemento. Exemplo: O2 (oxigênio molecular)."
    },
    {
        text: "5. Quando duas ou mais substâncias se misturam sem reação química e apresentam apenas uma fase visível, temos:",
        options: {
            a: "Substância pura",
            b: "Mistura heterogênea",
            c: "Mistura homogênea",
            d: "Substância simples",
            e: "Substância composta"
        },
        correct: "c",
        explanation: "Mistura homogênea é aquela em que não dá para distinguir os componentes. Exemplo: sal dissolvido na água."
    },
    {
        text: "6. Em um copo com água e óleo, temos:",
        options: {
            a: "Mistura homogênea",
            b: "Mistura heterogênea",
            c: "Substância pura",
            d: "Substância composta",
            e: "Mistura gasosa"
        },
        correct: "b",
        explanation: "Mistura heterogênea apresenta duas ou mais fases visíveis. Exemplo: água e óleo."
    },
    {
        text: "7. Qual a principal diferença entre uma transformação física e uma transformação química?",
        options: {
            a: "Na física há formação de novas substâncias; na química não.",
            b: "A transformação química muda a composição da matéria; a física não.",
            c: "A transformação física muda a composição da matéria; a química não.",
            d: "Ambas formam novas substâncias.",
            e: "Nenhuma delas altera as propriedades da matéria."
        },
        correct: "b",
        explanation: "Transformação física altera só a aparência. Transformação química muda a composição, formando novas substâncias. Exemplo: gelo derretendo (física), ferro enferrujando (química)."
    }
];

function loadQuiz() {
    const container = document.getElementById('quiz-container');
    questions.forEach((q, index) => {
        const div = document.createElement('div');
        div.className = 'question';
        div.innerHTML = `
            <h3>${q.text}</h3>
            <div class="options">
                ${Object.entries(q.options).map(([key, value]) => 
                    `<button onclick="checkAnswer('${key}','${q.correct}',${index})">${key}) ${value}</button>`
                ).join('')}
            </div>
            <div id="explanation-${index}" class="explanation"></div>
        `;
        container.appendChild(div);
    });
}

function checkAnswer(selected, correct, index) {
    const explanation = document.getElementById(`explanation-${index}`);
    if (selected === correct) {
        explanation.innerHTML = `<p class="correct">✅ Correto!</p><p>${questions[index].explanation}</p>`;
    } else {
        explanation.innerHTML = `<p class="incorrect">❌ Errado! A resposta correta era: (${correct})</p><p>${questions[index].explanation}</p>`;
    }
    explanation.style.display = 'block';
}

loadQuiz();
</script>

</body>
</html>
