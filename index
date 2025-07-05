<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Casos Clínicos Interativos de Semiologia</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Clinical Calm -->
    <!-- Application Structure Plan: A single-page application (SPA) with a case selection mechanism. The user first chooses between Case 01 and Case 02. Once a case is selected, its details are displayed, followed by a series of interactive sections for each guiding question (HDA Complement, Antecedents, Syndromic Hypothesis/Etiology). Each question section includes a text area for user input (simulating a response) and a "Revelar Feedback" button. Clicking this button expands a hidden area to display the detailed, expert-provided feedback for that specific question. This structure was chosen to provide a guided, step-by-step clinical reasoning exercise, allowing students to actively engage with the case and immediately compare their thought process with expert insights, fostering deeper learning in semiology. -->
    <!-- Visualization & Content Choices: Case Selection -> Inform/Organize -> HTML Buttons with dynamic content loading -> Allows user to choose their learning path. Case Details (ID, QP, HDA, EF) -> Inform -> HTML Text Blocks -> Presents the core case information clearly. Guiding Questions (HDA, Antecedents, Hypothesis) -> Engage/Inform -> HTML Textarea for input + HTML/JS Accordion for feedback -> Encourages active thinking and self-assessment, with expandable sections to prevent information overload. No Chart.js/Plotly.js as the content is qualitative and focuses on clinical reasoning, not quantitative data visualization. No SVG/Mermaid. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8f9fa;
        }
        .section-card {
            background-color: white;
            border-radius: 0.75rem;
            border: 1px solid #e5e7eb;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
            transition: all 0.3s ease-in-out;
        }
        .feedback-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.5s ease-out, padding 0.5s ease-out;
            background-color: #f0f9ff; /* Light blue background for feedback */
            border-left: 4px solid #3b82f6; /* Blue border */
            border-radius: 0.5rem;
            margin-top: 1rem;
        }
        .feedback-content.active {
            max-height: 1000px; /* Sufficiently large value for expansion */
            padding: 1rem;
            overflow: visible;
        }
        textarea {
            resize: vertical;
            min-height: 100px;
        }
    </style>
</head>
<body class="text-gray-800">

    <div class="container mx-auto p-4 md:p-8 max-w-5xl">

        <header class="text-center mb-12">
            <h1 class="text-4xl md:text-5xl font-bold text-gray-900 mb-2">Casos Clínicos Interativos de Semiologia</h1>
            <p class="text-xl text-gray-600">Para Discussão</p>
        </header>

        <!-- Case Selection Section -->
        <section id="case-selection" class="section-card p-6 md:p-8 mb-8 text-center">
            <h2 class="text-2xl font-bold mb-4">Selecione um Caso Clínico para Iniciar</h2>
            <div class="flex flex-col md:flex-row justify-center gap-4">
                <button onclick="loadCase('case01')" class="bg-blue-600 text-white px-6 py-3 rounded-lg shadow-md hover:bg-blue-700 transition-colors text-lg font-semibold">
                    Caso 01: FCA, 48 anos
                </button>
                <button onclick="loadCase('case02')" class="bg-blue-600 text-white px-6 py-3 rounded-lg shadow-md hover:bg-blue-700 transition-colors text-lg font-semibold">
                    Caso 02: PSS, 54 anos
                </button>
            </div>
        </section>

        <!-- Main Case Content Section (Hidden until a case is selected) -->
        <div id="case-content" class="hidden">
            <!-- Case Details -->
            <section id="case-details" class="section-card p-6 md:p-8 mb-8">
                <h2 class="text-2xl font-bold text-blue-700 mb-4">Detalhes do Caso</h2>
                <div class="space-y-3 text-lg text-gray-700">
                    <p><strong class="font-semibold">Identificação:</strong> <span id="case-id"></span></p>
                    <p><strong class="font-semibold">Queixa Principal:</strong> <span id="case-qp"></span></p>
                    <p><strong class="font-semibold">HDA (Resumida):</strong> <span id="case-hda"></span></p>
                    <p><strong class="font-semibold">Exame Físico:</strong> <span id="case-ef"></span></p>
                </div>
            </section>

            <!-- Question 1: Complementar HDA -->
            <section id="question-hda" class="section-card p-6 md:p-8 mb-8">
                <h2 class="text-2xl font-bold mb-4">Questão 1: Complementando a HDA</h2>
                <p class="mb-4 text-lg text-gray-700"><span id="hda-prompt"></span></p>
                <textarea class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-base" placeholder="Escreva suas perguntas e considerações aqui..."></textarea>
                <button onclick="toggleFeedback('hda')" class="mt-4 bg-blue-500 text-white px-5 py-2 rounded-lg hover:bg-blue-600 transition-colors font-semibold">
                    Revelar Feedback
                </button>
                <div id="hda-feedback" class="feedback-content text-gray-800"></div>
            </section>

            <!-- Question 2: Antecedentes -->
            <section id="question-antecedents" class="section-card p-6 md:p-8 mb-8">
                <h2 class="text-2xl font-bold mb-4">Questão 2: Investigando os Antecedentes</h2>
                <p class="mb-4 text-lg text-gray-700"><span id="antecedents-prompt"></span></p>
                <textarea class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-base" placeholder="Escreva suas perguntas e considerações aqui..."></textarea>
                <button onclick="toggleFeedback('antecedents')" class="mt-4 bg-blue-500 text-white px-5 py-2 rounded-lg hover:bg-blue-600 transition-colors font-semibold">
                    Revelar Feedback
                </button>
                <div id="antecedents-feedback" class="feedback-content text-gray-800"></div>
            </section>

            <!-- Question 3: Hipótese Sindrômica e Diagnóstico Etiológico -->
            <section id="question-hypothesis" class="section-card p-6 md:p-8 mb-8">
                <h2 class="text-2xl font-bold mb-4">Questão 3: Hipótese e Diagnóstico</h2>
                <p class="mb-4 text-lg text-gray-700"><span id="hypothesis-prompt"></span></p>
                <textarea class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-base" placeholder="Escreva sua hipótese e diagnósticos aqui..."></textarea>
                <button onclick="toggleFeedback('hypothesis')" class="mt-4 bg-blue-500 text-white px-5 py-2 rounded-lg hover:bg-blue-600 transition-colors font-semibold">
                    Revelar Feedback
                </button>
                <div id="hypothesis-feedback" class="feedback-content text-gray-800"></div>
            </section>
        </div>

    </div>

    <script>
        const cases = {
            'case01': {
                id: 'FCA, 48 anos, sexo feminino, professora, residente em Barbalha.',
                qp: 'fraqueza há 4 meses',
                hda: 'Paciente queixa-se de fraqueza e desânimo há aproximadamente 4 meses, o que tem prejudicado seu desempenho no trabalho e nas tarefas do dia a dia. Neste período notou também dispnéia aos esforços, ficando, por exemplo, muito cansada ao subir escadas.',
                ef: 'PA = 120/80 mmHg FC = 90 bpm TA = 36,5oC. Fácies atípica, bom estado geral, mucosas hipocoradas (++/4+), hidratada, anictérica, acianótica, afebril. Linfonodos não palpáveis. Sem edemas. AP : murmúrio vesicular fisiológico. Ausência de ruídos adventícios. AC: ritmo regular, em 2T, bulhas normofonéticas, sem sopros. Abdome: normotenso, presença de massa palpável no hipogástrio, indolor, endurecida, móvel, com cerca de 6 cm de diâmetro. Fígado e baço não palpáveis.',
                questions: {
                    hda: {
                        prompt: 'Após as queixas espontâneas da paciente, descritas acima no resumo, como devemos complementar a coleta dessa HDA? Que perguntas devem ser realizadas?',
                        feedback: `Para complementar a HDA, devemos investigar:
                        - **Fraqueza e Desânimo:** Início exato, progressão (piora ou melhora), fatores de alívio/piora, impacto nas atividades diárias (especificar quais tarefas são mais afetadas), sintomas associados (tontura, vertigem, síncope, dor de cabeça, sonolência diurna, insônia).
                        - **Dispneia aos Esforços:** Classificação (graus de dispneia), se é progressiva, se ocorre em repouso, se há ortopneia ou dispneia paroxística noturna, tosse, expectoração, dor torácica.
                        - **Sintomas Sistêmicos:** Anorexia, perda de peso, febre, sudorese noturna.
                        - **Sintomas Específicos de Anemia/Ferropenia:** Pica (desejo por substâncias não alimentares como gelo, terra), coiloníquia (unhas em colher), glossite (língua lisa e dolorosa), disfagia (síndrome de Plummer-Vinson), parestesias.
                        - **Sintomas de Sangramento:** Melena, hematoquezia, epistaxe, gengivorragia, hematúria, menorragia (fluxo menstrual intenso, duração, frequência, uso de absorventes), metrorragia (sangramento uterino irregular).`
                    },
                    antecedents: {
                        prompt: 'Com relação aos antecedentes, quais questionamentos não podem deixar de ser feitos a partir dos dados já expostos?',
                        feedback: `Considerando os dados, é essencial questionar sobre:
                        - **Ginecológicos/Obstétricos:** História menstrual detalhada (menarca, ciclos, duração, volume, presença de coágulos, dismenorreia), gestações (número, intercorrências, tipo de parto), uso de DIU (especialmente de cobre, que pode aumentar o fluxo).
                        - **Cirurgias Anteriores:** Especialmente cirurgias gastrointestinais (gastrectomia, cirurgia bariátrica) que podem afetar a absorção de ferro.
                        - **Medicamentos em Uso:** Uso de AINEs, anticoagulantes, antiagregantes plaquetários (que podem causar sangramento gastrointestinal).
                        - **Doenças Crônicas:** Doenças inflamatórias intestinais (Crohn, retocolite), doença renal crônica, doenças hepáticas, hipotireoidismo.
                        - **História Familiar:** Anemia na família, doenças genéticas.
                        - **Dieta:** Consumo de alimentos ricos em ferro (carnes vermelhas, feijão, vegetais verde-escuros), hábitos alimentares restritivos (vegetarianismo, veganismo).
                        - **Hábitos de Vida:** Consumo de álcool (pode afetar absorção e causar sangramento), tabagismo.
                        - **Viagens Recentes/Exposição:** Para investigar possíveis parasitoses.`
                    },
                    hypothesis: {
                        prompt: 'Formule uma hipótese sindrômica principal e, a partir dela, cite que outros achados de exame físico poderiam ser encontrados nessa paciente.',
                        feedback: `**Hipótese Sindrômica Principal:** Síndrome Anêmica (devido à fraqueza, desânimo, dispneia aos esforços, palidez de mucosas, taquicardia) associada à Síndrome de Massa Abdominal (massa palpável em hipogástrio).

                        **Outros achados de exame físico que poderiam ser encontrados:**
                        - **Pele e Anexos:** Coiloníquia (unhas em colher), cabelos secos e quebradiços, pele seca.
                        - **Mucosas:** Glossite (língua lisa, atrófica, dolorosa), queilite angular (rachaduras nos cantos da boca), estomatite.
                        - **Cardiovascular:** Sopros cardíacos sistólicos (funcionais devido à anemia), taquicardia mais acentuada.
                        - **Neurológico:** Parestesias (raro em ferropenia isolada, mais comum em B12, mas pode ocorrer em deficiências combinadas ou severas).
                        - **Gastrointestinal:** Dor à palpação abdominal na região da massa, ou sinais de sangramento (se a massa for a causa da perda sanguínea).`
                    }
                }
            },
            'case02': {
                id: 'PSS, 54 anos, sexo masculino, mecânico, natural e procedente de Barbalha.',
                qp: 'fraqueza há 4 meses',
                hda: 'Paciente refere que há cerca de 4 meses vem apresentando dor abdominal e adinamia intensa. Relatava ainda surgimento de várias nodulações em região cervical, de crescimento progressivo',
                ef: 'O exame inicial evidenciou paciente em bom estado geral, corado, hidratado, anictérico, acianótico, afebril, eupneico, consciente e orientado. Pressão arterial de 150×90 mmHg e frequência cardíaca de 68 bpm. Exame cardíaco e pulmonar apresentavam-se normais. Ao exame de abdome apresentou esplenomegalia palpável à 10 cm do rebordo costal esquerdo; hepatomegalia palpável à 7 cm do rebordo costal direito. Linfadenopatias palpáveis e visíveis nas cadeias ganglionares cervicais, supraclaviculares, axilares e inguinais.',
                questions: {
                    hda: {
                        prompt: 'Após as queixas espontâneas da paciente, descritas acima no resumo, como devemos complementar a coleta dessa HDA? Que perguntas devem ser realizadas?',
                        feedback: `Para complementar a HDA, devemos investigar:
                        - **Fraqueza e Adinamia:** Início exato, progressão (piora ou melhora), fatores de alívio/piora, impacto nas atividades diárias, sintomas associados (fadiga, dispneia, tontura, sonolência).
                        - **Dor Abdominal:** Localização exata, irradiação, tipo (cólica, queimação, pontada), intensidade, fatores de melhora/piora (relação com alimentação, evacuação), sintomas associados (náuseas, vômitos, diarreia, constipação, alteração do hábito intestinal, melena, hematoquezia).
                        - **Nodulações Cervicais:** Início, progressão do crescimento (rápido/lento), número, dor, consistência, mobilidade, presença de outras nodulações em outras regiões do corpo.
                        - **Sintomas B:** Febre (padrão, sudorese noturna, perda de peso involuntária).
                        - **Outros Sintomas Sistêmicos:** Prurido, tosse, dispneia, saciedade precoce, plenitude pós-prandial.
                        - **Exposição:** Histórico de exposição a agentes químicos, radiação, infecções crônicas (tuberculose, HIV), viagens.
                        - **História de Transfusões:** Se já realizou transfusões sanguíneas.`
                    },
                    antecedents: {
                        prompt: 'Com relação aos antecedentes, quais questionamentos não podem deixar de ser feitos a partir dos dados já expostos?',
                        feedback: `Considerando os dados, é essencial questionar sobre:
                        - **Doenças Preexistentes:** Histórico de doenças hematológicas (anemias prévias, doenças da medula óssea), doenças infecciosas crônicas (tuberculose, HIV, hepatites), doenças autoimunes, doenças oncológicas.
                        - **Cirurgias Anteriores:** Especialmente esplenectomia ou cirurgias abdominais.
                        - **Medicamentos em Uso:** Imunossupressores, quimioterápicos, uso crônico de AINEs.
                        - **História Familiar:** Casos de câncer, doenças hematológicas, doenças autoimunes na família.
                        - **Hábitos de Vida:** Consumo de álcool (cirrose, hepatopatia), tabagismo.
                        - **Ocupação:** Exposição a substâncias químicas ou tóxicas (mecânico).
                        - **Viagens/Áreas Endêmicas:** Para investigar doenças infecciosas que causam hepatoesplenomegalia e linfadenopatias (ex: leishmaniose, esquistossomose).`
                    },
                    hypothesis: {
                        prompt: 'Formule uma hipótese sindrômica principal e, a partir dela, pesquise possíveis diagnósticos etiológicos para o caso apresentado.',
                        feedback: `**Hipótese Sindrômica Principal:** Síndrome Linfoproliferativa/Mieloproliferativa (devido a linfadenopatias generalizadas, hepatoesplenomegalia e sintomas sistêmicos como fraqueza e adinamia) e Síndrome Dolorosa Abdominal.

                        **Possíveis Diagnósticos Etiológicos (para pesquisa):**
                        - **Neoplasias Hematológicas:**
                            - **Linfomas:** Hodgkin e Não-Hodgkin (explicam linfadenopatias generalizadas, hepatoesplenomegalia e sintomas B).
                            - **Leucemias:** Leucemia Linfoide Crônica (LLC), Leucemia Mieloide Crônica (LMC) (podem apresentar linfadenopatias e hepatoesplenomegalia).
                            - **Mielofibrose:** Pode causar esplenomegalia maciça e sintomas constitucionais.
                        - **Doenças Infecciosas:**
                            - **Mononucleose Infecciosa:** Linfadenopatia, hepatoesplenomegalia, fadiga.
                            - **Tuberculose:** Linfadenopatias, sintomas B.
                            - **HIV:** Linfadenopatia generalizada persistente.
                            - **Leishmaniose Visceral:** Hepatoesplenomegalia, febre, fraqueza.
                            - **Esquistossomose:** Hepatoesplenomegalia (em áreas endêmicas).
                        - **Doenças Autoimunes:** Sarcoidose (raro, mas pode causar linfadenopatias).
                        - **Outras:** Doença de Gaucher (doença de depósito, rara).

                        **Observação:** A fraqueza e adinamia são sintomas inespecíficos, mas no contexto das linfadenopatias e hepatoesplenomegalia, sugerem uma doença sistêmica subjacente, sendo as hematológicas as mais prováveis.`
                    }
                }
            }
        };

        let currentCase = null;

        function loadCase(caseId) {
            currentCase = cases[caseId];
            document.getElementById('case-id').textContent = currentCase.id;
            document.getElementById('case-qp').textContent = currentCase.qp;
            document.getElementById('case-hda').textContent = currentCase.hda;
            document.getElementById('case-ef').textContent = currentCase.ef;

            document.getElementById('hda-prompt').textContent = currentCase.questions.hda.prompt;
            document.getElementById('antecedents-prompt').textContent = currentCase.questions.antecedents.prompt;
            document.getElementById('hypothesis-prompt').textContent = currentCase.questions.hypothesis.prompt;

            document.getElementById('hda-feedback').innerHTML = currentCase.questions.hda.feedback;
            document.getElementById('antecedents-feedback').innerHTML = currentCase.questions.antecedents.feedback;
            document.getElementById('hypothesis-feedback').innerHTML = currentCase.questions.hypothesis.feedback;

            // Hide all feedback sections initially
            document.querySelectorAll('.feedback-content').forEach(el => {
                el.classList.remove('active');
            });

            document.getElementById('case-content').classList.remove('hidden');
        }

        function toggleFeedback(questionKey) {
            const feedbackElement = document.getElementById(`${questionKey}-feedback`);
            feedbackElement.classList.toggle('active');
        }
    </script>

</body>
</html>
