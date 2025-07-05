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
    <!-- Application Structure Plan: A single-page application (SPA) with a case selection mechanism. The user first chooses between Case 01 and Case 02. Once a case is selected, its details are displayed, followed by a series of interactive sections for each guiding question (HDA Complement, Antecedents, Syndromic Hypothesis/Etiology). Each main question now contains multiple sub-questions of varying types (multiple-choice, checkbox, textarea, and a new 'true_false_images' type). Each sub-question has its own "Verificar Resposta" button. Clicking this button triggers a simplified evaluation of the user's input against predefined correct answers or keywords, displaying a "Certa", "Errada", or "Incompleta" status, and then expands a hidden area to display the detailed, expert-provided feedback for that specific sub-question. For 'true_false_images' type, each statement within the sub-question is evaluated individually, displaying its own status and feedback. This structure was chosen to provide a more granular, step-by-step clinical reasoning exercise, allowing students to actively engage with the case, receive immediate basic feedback on specific points, and then compare their thought process with expert insights, fostering deeper learning in semiologia. -->
    <!-- Visualization & Content Choices: Case Selection -> Inform/Organize -> HTML Buttons with dynamic content loading -> Allows user to choose their learning path. Case Details (ID, QP, HDA, EF) -> Inform -> HTML Text Blocks -> Presents the core case information clearly. Guiding Questions (HDA, Antecedents, Hypothesis) -> Engage/Inform -> HTML Input fields (radio, checkbox, textarea, true/false radio buttons with images) + HTML/JS Evaluation + HTML/JS Accordion for feedback -> Encourages active thinking and self-assessment, with expandable sections to prevent information overload. Evaluation is based on direct comparison for objective types and keyword matching for textareas. Placeholder images are used for illustrative purposes. No Chart.js/Plotly.js as the content is qualitative and focuses on clinical reasoning, not quantitative data visualization. No SVG/Mermaid. -->
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
            border-left: 44px solid #3b82f6; /* Blue border */
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
        .feedback-status {
            margin-top: 0.5rem;
            padding: 0.5rem;
            border-radius: 0.5rem;
            font-weight: 600;
            text-align: center;
        }
        .status-correct {
            background-color: #d1fae5; /* Green-100 */
            color: #065f46; /* Green-800 */
        }
        .status-incomplete {
            background-color: #fef3c7; /* Yellow-100 */
            color: #92400e; /* Yellow-800 */
        }
        .status-incorrect {
            background-color: #fee2e2; /* Red-100 */
            color: #991b1b; /* Red-800 */
        }
        .sub-question-container {
            border: 1px solid #e5e7eb;
            border-radius: 0.5rem;
            padding: 1rem;
            margin-bottom: 1rem;
            background-color: #f9fafb;
        }
        .true-false-item {
            display: flex;
            align-items: center;
            margin-bottom: 1rem;
            padding: 0.75rem;
            border: 1px solid #e0e7ff;
            border-radius: 0.5rem;
            background-color: #ffffff;
            box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
        }
        .true-false-item img {
            width: 80px;
            height: 80px;
            border-radius: 0.25rem;
            margin-right: 1rem;
            object-fit: cover;
        }
        .true-false-item .text-and-options {
            flex-grow: 1;
        }
        .true-false-item .options {
            display: flex;
            gap: 1rem;
            margin-top: 0.5rem;
        }
        .true-false-item .item-status {
            margin-left: 1rem;
            padding: 0.25rem 0.75rem;
            border-radius: 0.25rem;
            font-weight: 500;
            font-size: 0.875rem;
        }
        .true-false-item .item-feedback {
            margin-top: 0.5rem;
            font-size: 0.875rem;
            color: #4b5563;
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

            <!-- Questions Container -->
            <div id="questions-container">
                <!-- Questions will be dynamically loaded here -->
            </div>
        </div>

    </div>

    <script>
        const cases = {
            'case01': {
                id: 'FCA, 48 anos, sexo feminino, professora, residente em Barbalha.',
                qp: 'fraqueza há 4 meses',
                hda: 'Paciente queixa-se de fraqueza e desânimo há aproximadamente 4 meses, o que tem prejudicado seu desempenho no trabalho e nas tarefas do dia a dia. Neste período notou também dispnéia aos esforços, ficando, por exemplo, muito cansada ao subir escadas.',
                ef: 'PA = 120/80 mmHg FC = 90 bpm TA = 36,5oC. Fácies atípica, bom estado geral, mucosas hipocoradas (++/4+), hidratada, anictérica, acianótica, afebril. Linfonodos não palpáveis. Sem edemas. AP : murmúrio vesicular fisiológico. Ausência de ruídos adventícios. AC: ritmo regular, em 2T, bulhas normofonéticas, sem sopros. Abdome: normotenso, presença de massa palpável no hipogástrio, indolor, endurecida, móvel, com cerca de 6 cm de diâmetro. Fígado e baço não palpáveis.',
                sections: [
                    {
                        title: 'Questão 1: Complementando a HDA',
                        subQuestions: [
                            {
                                id: 'hda-symptoms',
                                type: 'checkbox',
                                prompt: 'Quais dos seguintes sintomas associados à fraqueza e desânimo você investigaria para complementar a HDA?',
                                options: [
                                    'Tontura', 'Dor no peito ao repouso', 'Vertigem', 'Erupções cutâneas', 'Síncope', 'Dor de cabeça', 'Sonolência diurna',
                                    'Pica (desejo por substâncias não alimentares)', 'Visão turva', 'Coiloníquia (unhas em colher)', 'Dor articular',
                                    'Melena', 'Hematoquezia', 'Menorragia'
                                ],
                                correctAnswers: [
                                    'Tontura', 'Vertigem', 'Síncope', 'Dor de cabeça', 'Sonolência diurna',
                                    'Pica (desejo por substâncias não alimentares)', 'Coiloníquia (unhas em colher)',
                                    'Melena', 'Hematoquezia', 'Menorragia'
                                ],
                                feedback: `Para complementar a HDA, é crucial investigar a fundo os sintomas relacionados à fraqueza e desânimo, que podem indicar o grau da anemia e suas repercussões sistêmicas. Além disso, a busca ativa por sintomas de sangramento é fundamental, especialmente a menorragia, que é uma causa comum de perda crônica de ferro em mulheres. Sintomas específicos de ferropenia, como pica e coiloníquia, embora menos comuns, são altamente sugestivos e devem ser questionados. Sintomas como dor no peito ao repouso, erupções cutâneas, visão turva e dor articular não são tipicamente associados à anemia ferropriva.`
                            },
                            {
                                id: 'hda-justification',
                                type: 'textarea',
                                prompt: 'Justifique a relevância de investigar esses sintomas para este caso.',
                                keywords: ['anemia', 'ferropenia', 'sangramento', 'perda de ferro', 'absorção', 'repercussões sistêmicas'],
                                feedback: `A investigação detalhada desses sintomas é vital para:
                                - **Quantificar a gravidade da anemia:** Sintomas como tontura, síncope e dispneia aos mínimos esforços indicam anemia mais severa.
                                - **Identificar a causa da deficiência de ferro:** A menorragia é uma causa óbvia de perda sanguínea crônica. Outros sangramentos (melena, hematoquezia) indicariam perda gastrointestinal.
                                - **Avaliar o impacto na qualidade de vida:** O cansaço e a dificuldade de concentração já estão afetando o trabalho da paciente.
                                - **Buscar sinais específicos de ferropenia:** Pica e coiloníquia são manifestações diretas da deficiência de ferro em tecidos com alta taxa de proliferação.`
                            }
                        ]
                    },
                    {
                        title: 'Questão 2: Investigando os Antecedentes',
                        subQuestions: [
                            {
                                id: 'antecedents-gyn',
                                type: 'checkbox',
                                prompt: 'Quais antecedentes ginecológicos são cruciais para a investigação da menorragia neste caso?',
                                options: [
                                    'Menarca',
                                    'Histórico de infecções urinárias de repetição',
                                    'Ciclos menstruais (regularidade, duração, volume)',
                                    'Dor lombar crônica',
                                    'Presença de coágulos',
                                    'Dismenorreia',
                                    'Uso de DIU (tipo)',
                                    'Cefaleia tensional',
                                    'Número de gestações e tipo de parto'
                                ],
                                correctAnswers: [
                                    'Menarca',
                                    'Ciclos menstruais (regularidade, duração, volume)',
                                    'Presença de coágulos',
                                    'Dismenorreia',
                                    'Uso de DIU (tipo)',
                                    'Número de gestações e tipo de parto'
                                ],
                                feedback: `A história ginecológica detalhada é fundamental para caracterizar a menorragia e identificar possíveis causas. A menarca e a regularidade dos ciclos ajudam a estabelecer um padrão. A duração, volume e presença de coágulos quantificam a perda sanguínea. O uso de DIU (especialmente de cobre) é uma causa comum de menorragia. As gestações e partos podem influenciar a anatomia uterina. Histórico de infecções urinárias de repetição, dor lombar crônica e cefaleia tensional não são antecedentes ginecológicos diretamente relevantes para a investigação da menorragia.`
                            },
                            {
                                id: 'antecedents-medical',
                                type: 'checkbox',
                                prompt: 'Quais outros antecedentes médicos/cirúrgicos seriam importantes de questionar para este caso?',
                                options: [
                                    'Cirurgias gastrointestinais (bariátrica, gastrectomia)',
                                    'Uso de AINEs ou anticoagulantes',
                                    'História familiar de diabetes',
                                    'Doenças inflamatórias intestinais (Crohn, retocolite)',
                                    'Doença renal crônica',
                                    'Alergia a frutos do mar',
                                    'Hipotireoidismo',
                                    'História de apendicite na infância',
                                    'História familiar de anemia ou doenças genéticas'
                                ],
                                correctAnswers: [
                                    'Cirurgias gastrointestinais (bariátrica, gastrectomia)',
                                    'Uso de AINEs ou anticoagulantes',
                                    'Doenças inflamatórias intestinais (Crohn, retocolite)',
                                    'Doença renal crônica',
                                    'Hipotireoidismo',
                                    'História familiar de anemia ou doenças genéticas'
                                ],
                                feedback: `É vital investigar:
                                - **Cirurgias gastrointestinais:** Podem levar à má absorção de ferro (ex: gastrectomia, cirurgia bariátrica).
                                - **Medicamentos:** AINEs e anticoagulantes podem causar sangramento oculto.
                                - **Doenças crônicas:** Doenças inflamatórias intestinais (perda sanguínea e má absorção), doença renal crônica (deficiência de eritropoietina e inflamação), hipotireoidismo (pode estar associado à anemia).
                                - **História familiar:** Sugere predisposição genética.
                                - **Dieta e Hábitos:** Baixo consumo de carne vermelha e uso de álcool são fatores de risco. História familiar de diabetes, alergia a frutos do mar e história de apendicite na infância não são antecedentes diretamente relevantes para a investigação da anemia ferropriva neste contexto.`
                            }
                        ]
                    },
                    {
                        title: 'Questão 3: Hipótese e Diagnóstico',
                        subQuestions: [
                            {
                                id: 'hypothesis-syndrome',
                                type: 'radio',
                                prompt: 'Qual é a principal hipótese sindrômica para a paciente, considerando os achados clínicos e de exame físico?',
                                options: ['Síndrome Anêmica', 'Síndrome de Massa Abdominal', 'Ambas as síndromes'],
                                correctAnswer: 'Ambas as síndromes',
                                feedback: `A paciente apresenta claramente sintomas de Síndrome Anêmica (fraqueza, desânimo, dispneia, palidez, taquicardia) e um achado objetivo de Síndrome de Massa Abdominal (massa palpável em hipogástrio). Ambas são hipóteses sindrômicas principais e devem ser investigadas.`
                            },
                            {
                                id: 'hypothesis-etiology-diagnosis',
                                type: 'checkbox',
                                prompt: 'Qual(is) o(s) diagnóstico(s) etiológico(s) mais provável(is) para a anemia e a massa abdominal neste caso?',
                                options: [
                                    'Anemia Ferropriva secundária à menorragia por mioma uterino',
                                    'Anemia por deficiência de Vitamina B12 e cisto ovariano',
                                    'Anemia de Doença Crônica e endometriose',
                                    'Anemia Ferropriva por má absorção e pólipo intestinal'
                                ],
                                correctAnswers: ['Anemia Ferropriva secundária à menorragia por mioma uterino'],
                                feedback: `A combinação de anemia ferropriva (sugerida pelos sintomas e palidez), menorragia (fluxo menstrual intenso) e a presença de uma massa abdominal palpável em hipogástrio é altamente sugestiva de **Anemia Ferropriva secundária à menorragia por mioma uterino**. Miomas são tumores benignos comuns no útero que podem causar sangramento excessivo.`
                            },
                            {
                                id: 'hypothesis-etiology-justification',
                                type: 'textarea',
                                prompt: 'Justifique sua escolha do diagnóstico etiológico mais provável.',
                                keywords: ['menorragia', 'mioma', 'massa abdominal', 'perda de ferro', 'sangramento'],
                                feedback: `A justificativa para o diagnóstico de Anemia Ferropriva secundária à menorragia por mioma uterino reside na tríade de achados:
                                - **Anemia:** Sintomas como fraqueza, desânimo, dispneia e palidez.
                                - **Menorragia:** O fluxo menstrual muito intenso é uma causa clássica de perda crônica de ferro.
                                - **Massa Abdominal:** A presença de uma massa palpável no hipogástrio em uma mulher de 48 anos com menorragia é altamente sugestiva de mioma uterino, que é uma condição que pode causar sangramento uterino anormal e, consequentemente, anemia ferropriva.`
                            },
                            {
                                id: 'hypothesis-additional-findings',
                                type: 'true_false_images', // Novo tipo de interação
                                prompt: 'Avalie as seguintes afirmações sobre outros achados de exame físico que corroborariam sua hipótese de anemia ferropriva e mioma uterino (V para Verdadeiro, F para Falso):',
                                statements: [
                                    {
                                        text: 'Coiloníquia (unhas em colher) seria um achado esperado.',
                                        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/e9/Koilonychia.jpg/220px-Koilonychia.jpg', // Imagem real
                                        correctAnswer: true,
                                        feedback: 'Verdadeiro: A coiloníquia é um sinal clássico de deficiência crônica de ferro.'
                                    },
                                    {
                                        text: 'Queilite angular (rachaduras nos cantos da boca) seria um achado esperado.',
                                        image: 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Angular_cheilitis_2016.jpg/220px-Angular_cheilitis_2016.jpg', // Imagem real
                                        correctAnswer: true,
                                        feedback: 'Verdadeiro: A queilite angular também pode ser um sinal de deficiência de ferro.'
                                    },
                                    {
                                        text: 'Sopros cardíacos sistólicos funcionais seriam um achado esperado.',
                                        image: 'https://placehold.co/150x100/ADD8E6/000000?text=Sopro+Cardíaco',
                                        correctAnswer: true,
                                        feedback: 'Verdadeiro: Anemias severas podem causar sopros funcionais devido à hiperdinamia circulatória.'
                                    },
                                    {
                                        text: 'Icterícia seria um achado esperado.',
                                        image: 'https://placehold.co/150x100/ADD8E6/000000?text=Icterícia',
                                        correctAnswer: false,
                                        feedback: 'Falso: Icterícia não é um achado típico de anemia ferropriva; é mais comum em anemias hemolíticas ou doenças hepáticas.'
                                    },
                                    {
                                        text: 'Linfadenopatia generalizada seria um achado esperado.',
                                        image: 'https://placehold.co/150x100/ADD8E6/000000?text=Linfadenopatia',
                                        correctAnswer: false,
                                        feedback: 'Falso: Linfadenopatia generalizada não é um achado esperado na anemia ferropriva ou mioma uterino; sugere outras condições como infecções ou neoplasias hematológicas.'
                                    },
                                    {
                                        text: 'Exame ginecológico: palpação bimanual de útero aumentado/irregular seria um achado esperado.',
                                        image: 'https://placehold.co/150x100/ADD8E6/000000?text=Útero+Aumentado',
                                        correctAnswer: true,
                                        feedback: 'Verdadeiro: A palpação bimanual é crucial para confirmar o aumento uterino e a irregularidade da superfície, achados típicos de miomatose.'
                                    },
                                    {
                                        text: 'Esplenomegalia seria um achado esperado.',
                                        image: 'https://placehold.co/150x100/ADD8E6/000000?text=Esplenomegalia',
                                        correctAnswer: false,
                                        feedback: 'Falso: Esplenomegalia não é um achado comum na anemia ferropriva ou mioma uterino; é mais associada a doenças hematológicas ou infecciosas.'
                                    }
                                ]
                            }
                        ]
                    }
                ]
            },
            'case02': {
                id: 'PSS, 54 anos, sexo masculino, mecânico, natural e procedente de Barbalha.',
                qp: 'fraqueza há 4 meses',
                hda: 'Paciente refere que há cerca de 4 meses vem apresentando dor abdominal e adinamia intensa. Relatava ainda surgimento de várias nodulações em região cervical, de crescimento progressivo',
                ef: 'O exame inicial evidenciou paciente em bom estado geral, corado, hidratado, anictérico, acianótico, afebril, eupneico, consciente e orientado. Pressão arterial de 150×90 mmHg e frequência cardíaca de 68 bpm. Exame cardíaco e pulmonar apresentavam-se normais. Ao exame de abdome apresentou esplenomegalia palpável à 10 cm do rebordo costal esquerdo; hepatomegalia palpável à 7 cm do rebordo costal direito. Linfadenopatias palpáveis e visíveis nas cadeias ganglionares cervicais, supraclaviculares, axilares e inguinais.',
                sections: [
                    {
                        title: 'Questão 1: Complementando a HDA',
                        subQuestions: [
                            {
                                id: 'hda-pain',
                                type: 'checkbox',
                                prompt: 'Quais características da dor abdominal você investigaria para complementar a HDA?',
                                options: ['Localização exata', 'Irradiação', 'Tipo (cólica, queimação, pontada)', 'Intensidade (escala de 0-10)', 'Fatores de melhora/piora (relação com alimentação, evacuação)', 'Sintomas associados (náuseas, vômitos, diarreia, constipação, alteração do hábito intestinal, melena, hematoquezia)'],
                                correctAnswers: ['Localização exata', 'Irradiação', 'Tipo (cólica, queimação, pontada)', 'Intensidade (escala de 0-10)', 'Fatores de melhora/piora (relação com alimentação, evacuação)', 'Sintomas associados (náuseas, vômitos, diarreia, constipação, alteração do hábito intestinal, melena, hematoquezia)'],
                                feedback: `A caracterização completa da dor abdominal é essencial para direcionar a investigação. A localização e irradiação podem indicar o órgão afetado. O tipo e a intensidade ajudam a diferenciar causas. A relação com alimentação ou evacuação, e sintomas associados, são pistas importantes para distúrbios gastrointestinais ou sistêmicos.`
                            },
                            {
                                id: 'hda-nodules',
                                type: 'checkbox',
                                prompt: 'Quais perguntas sobre as nodulações cervicais são essenciais para a HDA?',
                                options: ['Início e duração', 'Progressão do crescimento (rápido/lento)', 'Número de nodulações', 'Presença de dor', 'Consistência (macia, elástica, endurecida)', 'Mobilidade (fixa ou móvel)', 'Presença de outras nodulações em outras regiões do corpo'],
                                correctAnswers: ['Início e duração', 'Progressão do crescimento (rápido/lento)', 'Número de nodulações', 'Presença de dor', 'Consistência (macia, elástica, endurecida)', 'Mobilidade (fixa ou móvel)', 'Presença de outras nodulações em outras regiões do corpo'],
                                feedback: `A investigação das nodulações é crucial para diferenciar causas benignas de malignas. O crescimento rápido e a consistência endurecida/fixa podem sugerir malignidade. O presença de dor pode indicar inflamação. A busca por outras nodulações (linfadenopatias generalizadas) é vital para doenças sistêmicas como linfomas.`
                            },
                            {
                                id: 'hda-systemic',
                                type: 'textarea',
                                prompt: 'Quais outros sintomas sistêmicos (como sintomas B) e exposições você investigaria?',
                                keywords: ['febre', 'sudorese noturna', 'perda de peso', 'prurido', 'tosse', 'exposição química', 'radiação', 'infecções crônicas'],
                                feedback: `É fundamental investigar:
                                - **Sintomas B:** Febre (padrão, duração), sudorese noturna (intensa, que encharca a roupa), perda de peso involuntária (quantificar). Esses sintomas são clássicos de doenças linfoproliferativas.
                                - **Outros sintomas sistêmicos:** Prurido (pode ser associado a linfomas), tosse, dispneia, saciedade precoce (devido à esplenomegalia).
                                - **Exposição:** Histórico de exposição a agentes químicos, radiação (relacionado à ocupação de mecânico), infecções crônicas (tuberculose, HIV, hepatites), viagens (para áreas endêmicas de leishmaniose, esquistossomose).`
                            }
                        ]
                    },
                    {
                        title: 'Questão 2: Investigando os Antecedentes',
                        subQuestions: [
                            {
                                id: 'antecedents-medical-history',
                                type: 'checkbox',
                                prompt: 'Quais antecedentes médicos preexistentes são cruciais para a investigação deste caso?',
                                options: ['Histórico de doenças hematológicas (anemias prévias, doenças da medula óssea)', 'Doenças infecciosas crônicas (tuberculose, HIV, hepatites)', 'Doenças autoimunes', 'Doenças oncológicas', 'Cirurgias anteriores (esplenectomia, abdominais)', 'Medicamentos em uso (imunossupressores, quimioterápicos, AINEs)'],
                                correctAnswers: ['Histórico de doenças hematológicas (anemias prévias, doenças da medula óssea)', 'Doenças infecciosas crônicas (tuberculose, HIV, hepatites)', 'Doenças autoimunes', 'Doenças oncológicas', 'Cirurgias anteriores (esplenectomia, abdominais)', 'Medicamentos em uso (imunossupressores, quimioterápicos, AINEs)'],
                                feedback: `O histórico médico é vital para o diagnóstico diferencial. Doenças hematológicas prévias, infecções crônicas (que podem causar linfadenopatias e hepatoesplenomegalia), doenças autoimunes e oncológicas são importantes. Cirurgias (especialmente esplenectomia) e uso de medicamentos (imunossupressores, quimioterápicos, AINEs) também fornecem pistas cruciais.`
                            },
                            {
                                id: 'antecedents-lifestyle',
                                type: 'checkbox',
                                prompt: 'Quais hábitos de vida e exposições relacionadas à ocupação você questionaria?',
                                options: ['Consumo de álcool', 'Tabagismo', 'Exposição a substâncias químicas ou tóxicas (relacionado à ocupação de mecânico)', 'Viagens recentes para áreas endêmicas'],
                                correctAnswers: ['Consumo de álcool', 'Tabagismo', 'Exposição a substâncias químicas ou tóxicas (relacionado à ocupação de mecânico)', 'Viagens recentes para áreas endêmicas'],
                                feedback: `Hábitos de vida como consumo de álcool (pode levar a hepatopatias e esplenomegalia) e tabagismo são relevantes. A ocupação de mecânico sugere a necessidade de investigar exposição a substâncias químicas ou tóxicas. Viagens para áreas endêmicas são cruciais para doenças infecciosas como leishmaniose e esquistossomose.`
                            }
                        ]
                    },
                    {
                        title: 'Questão 3: Hipótese e Diagnóstico',
                        subQuestions: [
                            {
                                id: 'hypothesis-syndrome-2',
                                type: 'radio',
                                prompt: 'Qual é a principal hipótese sindrômica para o paciente, considerando linfadenopatias generalizadas, hepatoesplenomegalia e sintomas sistêmicos?',
                                options: ['Síndrome Anêmica', 'Síndrome Linfoproliferativa/Mieloproliferativa', 'Síndrome Dolorosa Abdominal', 'Síndrome de Má Absorção'],
                                correctAnswer: 'Síndrome Linfoproliferativa/Mieloproliferativa',
                                feedback: `A presença de linfadenopatias generalizadas e hepatoesplenomegalia, juntamente com sintomas sistêmicos como fraqueza e adinamia, aponta fortemente para uma Síndrome Linfoproliferativa/Mieloproliferativa. A dor abdominal é um sintoma associado, mas não a síndrome principal que engloba o quadro.`
                            },
                            {
                                id: 'hypothesis-etiology-2',
                                type: 'textarea',
                                prompt: 'Formule a hipótese sindrômica completa e pesquise possíveis diagnósticos etiológicos para o caso apresentado, justificando a escolha.',
                                keywords: ['linfoma', 'leucemia', 'mielofibrose', 'mononucleose', 'tuberculose', 'hiv', 'leishmaniose', 'esquistossomose'],
                                feedback: `**Hipótese Sindrômica Principal:** Síndrome Linfoproliferativa/Mieloproliferativa (devido a linfadenopatias generalizadas, hepatoesplenomegalia e sintomas sistêmicos como fraqueza e adinamia).

                                **Possíveis Diagnósticos Etiológicos (para pesquisa e justificativa):**
                                - **Neoplasias Hematológicas:**
                                    - **Linfomas (Hodgkin e Não-Hodgkin):** São as principais causas de linfadenopatias generalizadas e hepatoesplenomegalia, frequentemente associadas a sintomas B (febre, sudorese noturna, perda de peso) e adinamia.
                                    - **Leucemias (Linfoides Crônicas, Mieloides Crônicas):** Podem cursar com linfadenopatias e hepatoesplenomegalia significativas, além de sintomas constitucionais.
                                    - **Mielofibrose:** Caracterizada por esplenomegalia maciça e sintomas constitucionais, pode ser uma consideração.
                                - **Doenças Infecciosas:**
                                    - **Mononucleose Infecciosa:** Causa linfadenopatia e hepatoesplenomegalia, mas geralmente em pacientes mais jovens e com quadro agudo.
                                    - **Tuberculose (formas disseminadas):** Pode causar linfadenopatias e esplenomegalia, com sintomas B.
                                    - **HIV:** Pode apresentar linfadenopatia generalizada persistente e hepatoesplenomegalia.
                                    - **Leishmaniose Visceral (Calazar):** Endêmica em algumas regiões, causa hepatoesplenomegalia maciça, febre, fraqueza e linfadenopatias.
                                    - **Esquistossomose:** Em áreas endêmicas, pode levar à hepatoesplenomegalia.
                                - **Doenças Autoimunes:** Sarcoidose (raro, mas pode causar linfadenopatias).

                                **Observação:** A fraqueza e adinamia são sintomas inespecíficos, mas no contexto das linfadenopatias e hepatoesplenomegalia, sugerem uma doença sistêmica subjacente, sendo as hematológicas as mais prováveis, exigindo investigação aprofundada.`
                            }
                        ]
                    }
                ]
            }
        };

        let currentCase = null;

        function loadCase(caseId) {
            currentCase = cases[caseId];
            document.getElementById('case-id').textContent = currentCase.id;
            document.getElementById('case-qp').textContent = currentCase.qp;
            document.getElementById('case-hda').textContent = currentCase.hda;
            document.getElementById('case-ef').textContent = currentCase.ef;

            const questionsContainer = document.getElementById('questions-container');
            questionsContainer.innerHTML = ''; // Clear previous questions

            currentCase.sections.forEach((section, sectionIndex) => {
                const sectionElement = document.createElement('section');
                sectionElement.id = `question-section-${sectionIndex}`;
                sectionElement.className = 'section-card p-6 md:p-8 mb-8';
                sectionElement.innerHTML = `<h2 class="text-2xl font-bold mb-4">${section.title}</h2>`;

                section.subQuestions.forEach((subQuestion, subQuestionIndex) => {
                    const subQuestionContainer = document.createElement('div');
                    subQuestionContainer.className = 'sub-question-container mb-4';
                    subQuestionContainer.innerHTML = `<p class="mb-3 text-lg text-gray-700">${subQuestion.prompt}</p>`;

                    let inputHtml = '';
                    let inputId = `${subQuestion.id}-${sectionIndex}-${subQuestionIndex}`;

                    if (subQuestion.type === 'textarea') {
                        inputHtml = `<textarea id="${inputId}" class="w-full p-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 text-base" placeholder="Escreva sua resposta aqui..."></textarea>`;
                    } else if (subQuestion.type === 'radio') {
                        subQuestion.options.forEach((option, optionIndex) => {
                            inputHtml += `
                                <div class="mb-2">
                                    <input type="radio" id="${inputId}-${optionIndex}" name="${inputId}" value="${option}" class="mr-2">
                                    <label for="${inputId}-${optionIndex}" class="text-base text-gray-700">${option}</label>
                                </div>
                            `;
                        });
                    } else if (subQuestion.type === 'checkbox') {
                        subQuestion.options.forEach((option, optionIndex) => {
                            inputHtml += `
                                <div class="mb-2">
                                    <input type="checkbox" id="${inputId}-${optionIndex}" name="${inputId}" value="${option}" class="mr-2">
                                    <label for="${inputId}-${optionIndex}" class="text-base text-gray-700">${option}</label>
                                </div>
                            `;
                        });
                    } else if (subQuestion.type === 'true_false_images') {
                        subQuestion.statements.forEach((statement, statementIndex) => {
                            const statementId = `${inputId}-${statementIndex}`;
                            inputHtml += `
                                <div class="true-false-item">
                                    ${statement.image ? `<img src="${statement.image}" alt="${statement.text.split('(')[0].trim()}" class="w-20 h-20 object-cover rounded-md mr-4">` : ''}
                                    <div class="text-and-options">
                                        <p class="text-base text-gray-700 mb-2">${statement.text}</p>
                                        <div class="options">
                                            <label class="inline-flex items-center">
                                                <input type="radio" name="${statementId}" value="true" class="form-radio text-blue-600">
                                                <span class="ml-2 text-gray-700">V</span>
                                            </label>
                                            <label class="inline-flex items-center ml-4">
                                                <input type="radio" name="${statementId}" value="false" class="form-radio text-blue-600">
                                                <span class="ml-2 text-gray-700">F</span>
                                            </label>
                                        </div>
                                        <div id="${statementId}-status" class="item-status hidden"></div>
                                        <div id="${statementId}-feedback" class="item-feedback hidden"></div>
                                    </div>
                                </div>
                            `;
                        });
                    }
                    
                    subQuestionContainer.innerHTML += inputHtml;
                    subQuestionContainer.innerHTML += `
                        <button onclick="checkAnswer('${subQuestion.id}', '${subQuestion.type}', '${inputId}', ${sectionIndex}, ${subQuestionIndex})" class="mt-4 bg-blue-500 text-white px-5 py-2 rounded-lg hover:bg-blue-600 transition-colors font-semibold">
                            Verificar Resposta
                        </button>
                        <div id="${inputId}-status" class="feedback-status hidden"></div>
                        <div id="${inputId}-feedback" class="feedback-content text-gray-800"></div>
                    `;
                    sectionElement.appendChild(subQuestionContainer);
                });
                questionsContainer.appendChild(sectionElement);
            });

            document.getElementById('case-content').classList.remove('hidden');
        }

        function checkAnswer(subQuestionId, type, inputId, sectionIndex, subQuestionIndex) {
            const caseKey = currentCase.id.split(',')[0].toLowerCase().includes('fca') ? 'case01' : 'case02';
            const subQuestionData = cases[caseKey].sections[sectionIndex].subQuestions[subQuestionIndex];
            const feedbackElement = document.getElementById(`${inputId}-feedback`);
            const statusElement = document.getElementById(`${inputId}-status`);

            let isCorrectOverall = true; // For true_false_images, assume correct until proven otherwise
            let overallStatusText = '';
            let overallStatusClass = '';

            if (type === 'textarea') {
                const userAnswer = document.getElementById(inputId).value.toLowerCase();
                const keywords = subQuestionData.keywords.map(k => k.toLowerCase());
                let foundKeywordsCount = 0;
                keywords.forEach(keyword => {
                    if (userAnswer.includes(keyword)) {
                        foundKeywordsCount++;
                    }
                });

                if (foundKeywordsCount === keywords.length) {
                    isCorrectOverall = true;
                    overallStatusText = 'Resposta Certa! 🎉';
                    overallStatusClass = 'status-correct';
                } else if (foundKeywordsCount > 0) {
                    isCorrectOverall = false; // Even if some are correct, it's incomplete
                    overallStatusText = 'Resposta Incompleta. 🤔';
                    overallStatusClass = 'status-incomplete';
                } else {
                    isCorrectOverall = false;
                    overallStatusText = 'Resposta Errada. 😔';
                    overallStatusClass = 'status-incorrect';
                }
            } else if (type === 'radio') {
                const selectedOption = document.querySelector(`input[name="${inputId}"]:checked`);
                if (selectedOption && selectedOption.value === subQuestionData.correctAnswer) {
                    isCorrectOverall = true;
                    overallStatusText = 'Resposta Certa! 🎉';
                    overallStatusClass = 'status-correct';
                } else {
                    isCorrectOverall = false;
                    overallStatusText = 'Resposta Errada. 😔';
                    overallStatusClass = 'status-incorrect';
                }
            } else if (type === 'checkbox') {
                const selectedOptions = Array.from(document.querySelectorAll(`input[name="${inputId}"]:checked`)).map(cb => cb.value);
                const correctAnswers = subQuestionData.correctAnswers;

                const allCorrectSelected = correctAnswers.every(ans => selectedOptions.includes(ans));
                const noIncorrectSelected = selectedOptions.every(ans => correctAnswers.includes(ans)); 

                if (allCorrectSelected && noIncorrectSelected) {
                    isCorrectOverall = true;
                    overallStatusText = 'Resposta Certa! 🎉';
                    overallStatusClass = 'status-correct';
                } else if (selectedOptions.length > 0 && correctAnswers.some(ans => selectedOptions.includes(ans))) {
                    isCorrectOverall = false;
                    overallStatusText = 'Resposta Incompleta. 🤔';
                    overallStatusClass = 'status-incomplete';
                } else {
                    isCorrectOverall = false;
                    overallStatusText = 'Resposta Errada. 😔';
                    overallStatusClass = 'status-incorrect';
                }
            } else if (type === 'true_false_images') {
                let allStatementsCorrect = true;
                subQuestionData.statements.forEach((statement, statementIndex) => {
                    const statementId = `${inputId}-${statementIndex}`;
                    const selectedOption = document.querySelector(`input[name="${statementId}"]:checked`);
                    const itemStatusElement = document.getElementById(`${statementId}-status`);
                    const itemFeedbackElement = document.getElementById(`${statementId}-feedback`);

                    let itemIsCorrect = false;
                    let itemStatusText = '';
                    let itemStatusClass = '';

                    if (selectedOption) {
                        if (selectedOption.value === String(statement.correctAnswer)) {
                            itemIsCorrect = true;
                            itemStatusText = 'Certo';
                            itemStatusClass = 'status-correct';
                        } else {
                            itemIsCorrect = false;
                            itemStatusText = 'Errado';
                            itemStatusClass = 'status-incorrect';
                            allStatementsCorrect = false; // Mark overall as incorrect if any statement is wrong
                        }
                    } else {
                        itemIsCorrect = false;
                        itemStatusText = 'Não respondido';
                        itemStatusClass = 'status-incomplete';
                        allStatementsCorrect = false; // Mark overall as incomplete if any statement is not answered
                    }

                    itemStatusElement.textContent = itemStatusText;
                    itemStatusElement.className = `item-status ${itemStatusClass}`;
                    itemStatusElement.classList.remove('hidden');

                    itemFeedbackElement.innerHTML = statement.feedback;
                    itemFeedbackElement.classList.add('active');
                });

                if (allStatementsCorrect) {
                    overallStatusText = 'Todas as afirmações corretas! 🎉';
                    overallStatusClass = 'status-correct';
                } else {
                    overallStatusText = 'Verifique as afirmações marcadas. 🤔';
                    overallStatusClass = 'status-incomplete'; // Or status-incorrect if we want a stricter overall check
                }

                // Display overall status for the entire true_false_images question
                statusElement.textContent = overallStatusText;
                statusElement.className = `feedback-status ${overallStatusClass}`;
                statusElement.classList.remove('hidden');
                
                // No single overall feedback for true_false_images, individual feedbacks are shown
                feedbackElement.classList.remove('active'); 
            }

            // For non-true_false_images types, display overall status and feedback
            if (type !== 'true_false_images') {
                statusElement.textContent = overallStatusText;
                statusElement.className = `feedback-status ${overallStatusClass}`;
                statusElement.classList.remove('hidden');

                feedbackElement.innerHTML = subQuestionData.feedback;
                feedbackElement.classList.add('active');
            }
        }
    </script>

</body>
</html>
