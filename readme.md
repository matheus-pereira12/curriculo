<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Currículo Interativo - Matheus Pereira</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- Chosen Palette: Warm Neutrals & Slate Blue -->
    <!-- Application Structure Plan: A single-page application designed as a personal dashboard. It starts with a hero section for immediate impact, followed by an interactive skills dashboard where a doughnut chart acts as a filter for detailed skills. The career path is presented as a clickable timeline to show progression clearly. This structure was chosen to transform the linear resume into an exploratory experience, allowing recruiters to dive into the areas that interest them most, promoting engagement over passive reading. -->
    <!-- Visualization & Content Choices: 
        - Skills Section: Goal is to organize and compare skills. A Chart.js doughnut chart was chosen to visually group skills into core areas (Análise, Gestão Ágil, Projetos). Interaction: Clicking a chart segment filters and displays specific skills. This is more engaging than a static list.
        - Experience Section: Goal is to show career progression over time. A horizontal timeline built with HTML/Tailwind was chosen over a simple list. Interaction: Clicking on a company node reveals detailed information, keeping the interface clean. This tells a clearer story of professional growth.
        - General Text: All textual content from the resume is presented in clean, well-structured cards and sections for maximum readability. -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-color: #f8fafc; /* slate-50 */
        }
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 380px;
            margin-left: auto;
            margin-right: auto;
            height: 380px;
            max-height: 400px;
        }
        .timeline-item::before {
            content: '';
            position: absolute;
            left: 50%;
            top: -10px;
            transform: translateX(-50%);
            width: 20px;
            height: 20px;
            border-radius: 50%;
            background-color: #475569; /* slate-600 */
            border: 3px solid #f1f5f9; /* slate-100 */
            z-index: 10;
        }
        .timeline-item.active::before {
            background-color: #0ea5e9; /* sky-500 */
        }
    </style>
</head>
<body class="text-slate-700">

    <main class="container mx-auto p-4 sm:p-6 md:p-8 max-w-6xl">
        
        <!-- Hero Section -->
        <header class="text-center py-12">
            <h1 class="text-4xl md:text-5xl font-bold text-slate-800">MATHEUS PEREIRA</h1>
            <h2 class="mt-2 text-xl md:text-2xl text-sky-600 font-medium">Analista de Negócios | Analista de Requisitos | Gerente de Projetos</h2>
            <p class="mt-6 max-w-3xl mx-auto text-slate-600">
                Profissional com experiência consolidada em análise de requisitos, negócios e gestão de projetos, focado em implantar soluções inovadoras em tecnologia, fortalecer a comunicação entre áreas e garantir resultados consistentes.
            </p>
        </header>

        <!-- Skills Dashboard Section -->
        <section id="skills" class="py-12">
            <div class="text-center mb-12">
                <h3 class="text-3xl font-bold text-slate-800">Painel de Competências</h3>
                <p class="mt-2 text-slate-600">Explore minhas principais áreas de atuação. Clique em uma seção do gráfico para ver os detalhes.</p>
            </div>
            <div class="grid md:grid-cols-2 gap-8 lg:gap-12 items-center">
                <div class="chart-container">
                    <canvas id="skillsChart"></canvas>
                </div>
                <div id="skills-details" class="bg-white p-8 rounded-xl shadow-sm min-h-[380px] flex flex-col justify-center">
                    <h4 id="skill-category-title" class="text-2xl font-bold text-slate-800 mb-4">Minhas Habilidades</h4>
                    <ul id="skill-list" class="space-y-3 text-slate-600 list-none">
                        <li>Passe o mouse ou clique no gráfico para explorar.</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Professional Experience Section -->
        <section id="experience" class="py-12">
            <div class="text-center mb-16">
                <h3 class="text-3xl font-bold text-slate-800">Trajetória Profissional</h3>
                <p class="mt-2 text-slate-600">Navegue pela minha linha do tempo profissional. Clique em cada empresa para ver os detalhes da minha atuação.</p>
            </div>
            
            <!-- Timeline Navigation -->
            <div class="relative">
                <div class="border-t-4 border-slate-300 w-full absolute top-1.5"></div>
                <div class="flex justify-around">
                    <div id="timeline-nav-ahoy" class="timeline-item relative text-center cursor-pointer p-4 w-1/3 active" onclick="showExperience('ahoy')">
                        <span class="font-semibold block mt-4 text-sm sm:text-base">Ahoy by Belago</span>
                    </div>
                    <div id="timeline-nav-squadra" class="timeline-item relative text-center cursor-pointer p-4 w-1/3" onclick="showExperience('squadra')">
                        <span class="font-semibold block mt-4 text-sm sm:text-base">Squadra Digital</span>
                    </div>
                    <div id="timeline-nav-prodata" class="timeline-item relative text-center cursor-pointer p-4 w-1/3" onclick="showExperience('prodata')">
                        <span class="font-semibold block mt-4 text-sm sm:text-base">Prodata</span>
                    </div>
                </div>
            </div>

            <!-- Experience Details -->
            <div id="experience-details" class="mt-12">
                <div id="exp-ahoy" class="experience-card bg-white p-8 rounded-xl shadow-sm border-l-4 border-sky-500">
                    <h4 class="text-2xl font-bold text-slate-800">Analista de Negócios / Requisitos / Gerente de Projetos</h4>
                    <p class="text-slate-500 mt-1 mb-4">Ahoy by Belago (Cliente: Grupo Saga) | Jan/2025 – Nov/2025</p>
                    <ul class="space-y-3 text-slate-600 list-disc list-inside">
                        <li><b>Atuação Multifuncional:</b> Desempenho dos papéis de Gestão de Projetos, Análise de Negócios, Levantamento de Requisitos e implantação de soluções em projetos estratégicos.</li>
                        <li><b>Coordenação e Alinhamento:</b> Responsável pela coordenação de entregas, alinhamento estratégico entre áreas de negócio e TI, validação de fluxos e suporte em processos de adoção tecnológica.</li>
                        <li><b>Foco em Valor:</b> Garantia do cumprimento de prazos, integração entre stakeholders e geração de valor para o cliente.</li>
                    </ul>
                </div>
                <div id="exp-squadra" class="experience-card bg-white p-8 rounded-xl shadow-sm border-l-4 border-sky-500 hidden">
                    <h4 class="text-2xl font-bold text-slate-800">Analista de Negócios / Requisitos / Scrum Master / Product Owner (PO)</h4>
                    <p class="text-slate-500 mt-1 mb-4">Squadra Digital | Dez/2023 – Jan/2024</p>
                    <ul class="space-y-3 text-slate-600 list-disc list-inside">
                        <li><b>Agilidade e Multi-papel:</b> Experiência em conciliar múltiplos papéis (BA, Requisitos, SM e PO) com foco em agilidade, utilizando Scrum e Kanban.</li>
                        <li><b>Gestão de Produto (PO):</b> Atuação como Product Owner, priorizando o backlog, alinhando expectativas e garantindo a entrega de valor ao negócio.</li>
                        <li><b>Scrum Master (SM):</b> Condução de cerimônias ágeis, remoção de impedimentos e apoio ao time no cumprimento de sprints.</li>
                        <li><b>Requisitos:</b> Levantamento, documentação de requisitos, elaboração de histórias de usuário e definição de critérios de aceite.</li>
                    </ul>
                </div>
                <div id="exp-prodata" class="experience-card bg-white p-8 rounded-xl shadow-sm border-l-4 border-sky-500 hidden">
                    <h4 class="text-2xl font-bold text-slate-800">Analista de Negócios / Requisitos / Gerente de Projetos</h4>
                    <p class="text-slate-500 mt-1 mb-4">Prodata Gestão Estratégica | Set/2022 – Dez/2023</p>
                    <ul class="space-y-3 text-slate-600 list-disc list-inside">
                        <li><b>Especialização em ERP:</b> Levantamento, análise e documentação de requisitos para sistemas ERP.</li>
                        <li><b>Otimização de Processos:</b> Mapeamento e otimização de processos, alinhando fluxos de negócio a soluções tecnológicas.</li>
                        <li><b>Gestão de Implantação:</b> Acompanhamento de projetos de implantação, assegurando prazos, escopo e qualidade.</li>
                        <li><b>Integração e Qualidade:</b> Execução de testes funcionais, validação de entregas e integração de sistemas e documentação técnica para desenvolvimento.</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Education & Contact Section -->
        <section id="education-contact" class="py-12">
             <div class="grid md:grid-cols-2 gap-8">
                <div class="bg-white p-8 rounded-xl shadow-sm">
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">Formação Acadêmica</h3>
                    <div class="space-y-4">
                        <div>
                            <p class="font-semibold text-slate-700">Análise e Desenvolvimento de Sistemas (Cursando)</p>
                            <p class="text-slate-500">UNIFECAF - Conclusão em 2026</p>
                        </div>
                        <div>
                            <p class="font-semibold text-slate-700">Ensino Médio</p>
                            <p class="text-slate-500">Colégio Estadual Antônio Alves Fortes - Concluído em 2013</p>
                        </div>
                    </div>
                </div>
                <div class="bg-white p-8 rounded-xl shadow-sm">
                    <h3 class="text-2xl font-bold text-slate-800 mb-4">Contato</h3>
                    <div class="space-y-4 text-slate-600">
                        <p>
                            <span class="font-semibold">Celular:</span>
                            <a href="tel:+5562993371996" class="text-sky-600 hover:underline">(62) 99337-1996</a>
                        </p>
                        <p>
                            <span class="font-semibold">E-mail:</span>
                            <a href="mailto:mviniciusgg15@gmail.com" class="text-sky-600 hover:underline">mviniciusgg15@gmail.com</a>
                        </p>
                        <p>
                            <span class="font-semibold">Localização:</span> Aparecida de Goiânia, Goiás, Brasil
                        </p>
                    </div>
                </div>
             </div>
        </section>
        
    </main>
    
    <footer class="text-center py-6">
        <p class="text-slate-500 text-sm">Currículo Interativo desenvolvido para Matheus Pereira.</p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', function () {
            const skillsData = {
                labels: ['Análise e Requisitos', 'Gestão de Projetos e Produtos', 'Qualidade e Suporte'],
                datasets: [{
                    data: [4, 5, 4],
                    backgroundColor: ['#0ea5e9', '#0284c7', '#38bdf8'],
                    hoverBackgroundColor: ['#0369a1', '#075985', '#0ea5e9'],
                    borderColor: '#f8fafc',
                    borderWidth: 4,
                    hoverOffset: 15
                }]
            };

            const skillsDetails = {
                'Análise e Requisitos': [
                    'Levantamento de requisitos',
                    'Análise de negócios',
                    'Análise de sistemas',
                    'Prototipagem de baixa fidelidade (Figma)'
                ],
                'Gestão de Projetos e Produtos': [
                    'Gestão de projetos',
                    'Metodologias Ágeis (Scrum & KANBAN)',
                    'Gerenciar backlog de demandas',
                    'Desenvolver MVP',
                    'Garantir execução do projeto'
                ],
                'Qualidade e Suporte': [
                    'Garantir qualidade do produto',
                    'Métricas',
                    'Suporte aos desenvolvedores e helpdesk',
                    'Desenvolver documentação (manuais, vídeos e tutoriais)'
                ]
            };

            const ctx = document.getElementById('skillsChart').getContext('2d');
            const skillsChart = new Chart(ctx, {
                type: 'doughnut',
                data: skillsData,
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    cutout: '60%',
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                font: {
                                    size: 14,
                                    family: 'Inter, sans-serif'
                                }
                            }
                        },
                        tooltip: {
                            enabled: true
                        }
                    },
                    onClick: (event, elements) => {
                        if (elements.length > 0) {
                            const chartElement = elements[0];
                            const label = skillsData.labels[chartElement.index];
                            updateSkillsDetails(label);
                        }
                    },
                    onHover: (event, elements) => {
                         if (elements.length > 0) {
                            const chartElement = elements[0];
                            const label = skillsData.labels[chartElement.index];
                            updateSkillsDetails(label);
                            event.native.target.style.cursor = 'pointer';
                        } else {
                            event.native.target.style.cursor = 'default';
                        }
                    }
                }
            });

            const skillCategoryTitle = document.getElementById('skill-category-title');
            const skillList = document.getElementById('skill-list');

            function updateSkillsDetails(category) {
                skillCategoryTitle.textContent = category;
                const skills = skillsDetails[category] || [];
                skillList.innerHTML = skills.map(skill => `<li class="flex items-start"><span class="text-sky-500 mr-3 mt-1">✓</span>${skill}</li>`).join('');
            }
        });

        function showExperience(id) {
            const allCards = document.querySelectorAll('.experience-card');
            allCards.forEach(card => card.classList.add('hidden'));

            const selectedCard = document.getElementById(`exp-${id}`);
            if (selectedCard) {
                selectedCard.classList.remove('hidden');
            }
            
            const allNavItems = document.querySelectorAll('.timeline-item');
            allNavItems.forEach(item => item.classList.remove('active'));
            
            const selectedNavItem = document.getElementById(`timeline-nav-${id}`);
            if(selectedNavItem) {
                selectedNavItem.classList.add('active');
            }
        }
    </script>
</body>
</html>
