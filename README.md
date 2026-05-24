<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Explorando la Sociología: Un Análisis Interactivo</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Chart.js -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

    <!-- Chosen Palette: Warm Neutral Harmony (Backgrounds: Slate-50, Slate-100; Text: Slate-800; Accents: Violet-600, Emerald-600) -->
    <!-- Application Structure Plan: A single-page dashboard/report layout. Starts with a high-level definition, moves through historical context (founders), explains core analytical frameworks (perspectives) via interactive tabs to avoid overwhelming text, and concludes with quantitative illustrative data on research methods and modern study areas using charts. This flow mirrors a logical introductory learning path. -->
    <!-- Visualization & Content Choices: 
         1. Founders: Grid layout for quick scanning of key figures.
         2. Perspectives: Interactive Tabs. Goal: organize dense theoretical text; Justification: allows user to focus on one theory at a time; Method: Vanilla JS + Tailwind.
         3. Methods: Doughnut Chart. Goal: Show proportion of methodological usage; Justification: standard way to show parts of a whole; Method: Chart.js.
         4. Topics: Bar Chart. Goal: Compare focus areas over time; Justification: easily compares discrete categories; Method: Chart.js.
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    colors: {
                        brand: {
                            light: '#ede9fe', // violet-100
                            DEFAULT: '#7c3aed', // violet-600
                            dark: '#5b21b6', // violet-800
                        },
                        accent: {
                            DEFAULT: '#059669', // emerald-600
                        }
                    },
                    fontFamily: {
                        sans: ['Inter', 'system-ui', 'sans-serif'],
                        serif: ['Merriweather', 'serif'],
                    }
                }
            }
        }
    </script>

    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=Merriweather:ital,wght@0,300;0,700;1,300&display=swap');

        body {
            background-color: #f8fafc; /* slate-50 */
            color: #1e293b; /* slate-800 */
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
        }

        h1, h2, h3, h4 {
            font-family: 'Merriweather', serif;
        }

        /* Mandatory Chart Container Styling */
        .chart-container {
            position: relative;
            width: 100%;
            max-width: 800px;
            margin-left: auto;
            margin-right: auto;
            height: 40vh;
            max-height: 400px;
            min-height: 300px;
        }

        /* Custom scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9; 
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8; 
        }

        .tab-content {
            display: none;
            animation: fadeIn 0.3s ease-in-out;
        }
        .tab-content.active {
            display: block;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(5px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="antialiased">

    <!-- Navigation -->
    <nav class="fixed w-full bg-white/90 backdrop-blur-md shadow-sm z-50 border-b border-slate-200">
        <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <span class="text-2xl mr-2">🌍</span>
                    <span class="font-bold text-xl tracking-tight text-brand-dark">SocioData</span>
                </div>
                <div class="hidden md:flex items-center space-x-8">
                    <a href="#intro" class="text-slate-600 hover:text-brand transition-colors text-sm font-medium">Introducción</a>
                    <a href="#fundadores" class="text-slate-600 hover:text-brand transition-colors text-sm font-medium">Fundadores</a>
                    <a href="#perspectivas" class="text-slate-600 hover:text-brand transition-colors text-sm font-medium">Perspectivas</a>
                    <a href="#datos" class="text-slate-600 hover:text-brand transition-colors text-sm font-medium">Análisis de Datos</a>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <main class="pt-24 pb-16">
        
        <!-- Section: Intro -->
        <section id="intro" class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 mb-20">
            <div class="bg-white rounded-3xl p-8 md:p-12 shadow-sm border border-slate-100 relative overflow-hidden">
                <div class="absolute top-0 right-0 -mt-16 -mr-16 text-9xl opacity-5">🏛️</div>
                <div class="max-w-3xl relative z-10">
                    <h1 class="text-4xl md:text-5xl font-bold text-slate-900 mb-6 leading-tight">Comprendiendo la Estructura de la Sociedad Humana</h1>
                    <p class="text-lg text-slate-600 mb-6 leading-relaxed">
                        La <strong>sociología</strong> es el estudio sistemático y científico de la sociedad, el comportamiento social y los grupos humanos. Se centra en cómo las relaciones sociales influyen en el comportamiento de las personas y cómo las sociedades evolucionan y cambian con el tiempo.
                    </p>
                    <div class="flex flex-wrap gap-3 mt-8">
                        <span class="px-4 py-2 bg-slate-100 text-slate-700 rounded-full text-sm font-semibold tracking-wide uppercase">Cultura</span>
                        <span class="px-4 py-2 bg-slate-100 text-slate-700 rounded-full text-sm font-semibold tracking-wide uppercase">Desigualdad</span>
                        <span class="px-4 py-2 bg-slate-100 text-slate-700 rounded-full text-sm font-semibold tracking-wide uppercase">Instituciones</span>
                        <span class="px-4 py-2 bg-slate-100 text-slate-700 rounded-full text-sm font-semibold tracking-wide uppercase">Cambio Social</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section: Fundadores -->
        <section id="fundadores" class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 mb-24">
            <div class="mb-12">
                <h2 class="text-3xl font-bold text-slate-900 mb-4">Los Pioneros de la Disciplina</h2>
                <p class="text-slate-600 max-w-2xl">
                    Esta sección presenta a los pensadores clásicos cuyas teorías sentaron las bases para el análisis sociológico moderno. Sus ideas siguen siendo fundamentales para entender las dinámicas sociales actuales.
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <!-- Card 1 -->
                <div class="bg-white p-8 rounded-2xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow group">
                    <div class="text-4xl mb-4 group-hover:scale-110 transition-transform origin-left">⚙️</div>
                    <h3 class="text-xl font-bold text-slate-800 mb-2">Karl Marx</h3>
                    <p class="text-sm text-brand font-semibold mb-4">El Conflicto de Clases</p>
                    <p class="text-slate-600 text-sm leading-relaxed">
                        Argumentó que la historia de la sociedad es la historia de la lucha de clases. Se centró en cómo el sistema capitalista crea desigualdades económicas y poder que estructuran la sociedad.
                    </p>
                </div>
                <!-- Card 2 -->
                <div class="bg-white p-8 rounded-2xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow group">
                    <div class="text-4xl mb-4 group-hover:scale-110 transition-transform origin-left">🧩</div>
                    <h3 class="text-xl font-bold text-slate-800 mb-2">Émile Durkheim</h3>
                    <p class="text-sm text-brand font-semibold mb-4">Cohesión Social</p>
                    <p class="text-slate-600 text-sm leading-relaxed">
                        Pionero en la investigación empírica. Se centró en cómo las sociedades se mantienen unidas a través de valores compartidos y la división del trabajo. Famoso por su estudio sobre el suicidio.
                    </p>
                </div>
                <!-- Card 3 -->
                <div class="bg-white p-8 rounded-2xl shadow-sm border border-slate-100 hover:shadow-md transition-shadow group">
                    <div class="text-4xl mb-4 group-hover:scale-110 transition-transform origin-left">💡</div>
                    <h3 class="text-xl font-bold text-slate-800 mb-2">Max Weber</h3>
                    <p class="text-sm text-brand font-semibold mb-4">Racionalización</p>
                    <p class="text-slate-600 text-sm leading-relaxed">
                        Enfatizó la importancia de comprender las motivaciones subjetivas detrás de la acción social. Analizó cómo la racionalidad y la burocracia modelan las sociedades modernas.
                    </p>
                </div>
            </div>
        </section>

        <!-- Section: Perspectivas Teóricas (Interactive Tabs) -->
        <section id="perspectivas" class="bg-slate-100 py-20 mb-24">
            <div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="mb-12 text-center max-w-3xl mx-auto">
                    <h2 class="text-3xl font-bold text-slate-900 mb-4">Paradigmas Sociológicos</h2>
                    <p class="text-slate-600">
                        Los sociólogos utilizan diferentes lentes teóricos para analizar el mundo social. Interactúa con las pestañas a continuación para explorar los tres paradigmas principales que guían la investigación.
                    </p>
                </div>

                <div class="bg-white rounded-2xl shadow-sm overflow-hidden border border-slate-200">
                    <!-- Tab Headers -->
                    <div class="flex flex-col sm:flex-row border-b border-slate-200" id="tab-buttons">
                        <button class="tab-btn flex-1 py-4 px-6 text-center font-semibold text-slate-500 hover:text-brand hover:bg-slate-50 transition-colors focus:outline-none" data-target="tab-funcionalismo">
                            Funcionalismo
                        </button>
                        <button class="tab-btn flex-1 py-4 px-6 text-center font-semibold text-slate-500 hover:text-brand hover:bg-slate-50 transition-colors focus:outline-none border-t sm:border-t-0 sm:border-l border-slate-200" data-target="tab-conflicto">
                            Teoría del Conflicto
                        </button>
                        <button class="tab-btn flex-1 py-4 px-6 text-center font-semibold text-slate-500 hover:text-brand hover:bg-slate-50 transition-colors focus:outline-none border-t sm:border-t-0 sm:border-l border-slate-200" data-target="tab-interaccionismo">
                            Interaccionismo Simbólico
                        </button>
                    </div>

                    <!-- Tab Contents -->
                    <div class="p-8 md:p-12">
                        <!-- Funcionalismo -->
                        <div id="tab-funcionalismo" class="tab-content">
                            <div class="flex flex-col md:flex-row gap-8 items-start">
                                <div class="text-6xl text-brand/20 hidden md:block">🏗️</div>
                                <div>
                                    <h3 class="text-2xl font-bold text-slate-800 mb-4">La Sociedad como un Organismo</h3>
                                    <p class="text-slate-600 mb-4 leading-relaxed">
                                        El paradigma macro-sociológico ve a la sociedad como un sistema complejo cuyas partes trabajan juntas para promover la solidaridad y la estabilidad. Nuestras vidas están guiadas por <strong>estructuras sociales</strong> (patrones relativamente estables de comportamiento).
                                    </p>
                                    <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
                                        <h4 class="font-semibold text-slate-800 mb-2">Conceptos Clave:</h4>
                                        <ul class="list-disc list-inside text-slate-600 space-y-1 text-sm">
                                            <li>Funciones manifiestas (consecuencias reconocidas).</li>
                                            <li>Funciones latentes (consecuencias no reconocidas).</li>
                                            <li>Disfunción social (patrones que interrumpen el funcionamiento).</li>
                                        </ul>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Conflicto -->
                        <div id="tab-conflicto" class="tab-content">
                             <div class="flex flex-col md:flex-row gap-8 items-start">
                                <div class="text-6xl text-brand/20 hidden md:block">⚖️</div>
                                <div>
                                    <h3 class="text-2xl font-bold text-slate-800 mb-4">Desigualdad y Cambio</h3>
                                    <p class="text-slate-600 mb-4 leading-relaxed">
                                        Un marco macro-sociológico que ve a la sociedad como una arena de desigualdad que genera conflicto y cambio social. Analiza cómo factores como la clase social, la raza, la etnia y el género están vinculados a la distribución desigual de dinero, poder y educación.
                                    </p>
                                    <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
                                        <h4 class="font-semibold text-slate-800 mb-2">Preguntas Centrales:</h4>
                                        <ul class="list-disc list-inside text-slate-600 space-y-1 text-sm">
                                            <li>¿Quién se beneficia de los patrones sociales actuales?</li>
                                            <li>¿Cómo mantienen el poder los grupos dominantes?</li>
                                        </ul>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <!-- Interaccionismo -->
                        <div id="tab-interaccionismo" class="tab-content">
                             <div class="flex flex-col md:flex-row gap-8 items-start">
                                <div class="text-6xl text-brand/20 hidden md:block">🗣️</div>
                                <div>
                                    <h3 class="text-2xl font-bold text-slate-800 mb-4">El Nivel Micro</h3>
                                    <p class="text-slate-600 mb-4 leading-relaxed">
                                        Un marco teórico que ve a la sociedad como el producto de las interacciones cotidianas de los individuos. Se centra en cómo las personas utilizan símbolos para crear significado, comunicarse y formar visiones del mundo.
                                    </p>
                                    <div class="bg-slate-50 p-4 rounded-lg border border-slate-100">
                                        <h4 class="font-semibold text-slate-800 mb-2">Ejemplos de Enfoque:</h4>
                                        <ul class="list-disc list-inside text-slate-600 space-y-1 text-sm">
                                            <li>El lenguaje corporal en diferentes culturas.</li>
                                            <li>Cómo las etiquetas sociales afectan el comportamiento individual.</li>
                                        </ul>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <!-- Section: Datos y Gráficos -->
        <section id="datos" class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="mb-12">
                <h2 class="text-3xl font-bold text-slate-900 mb-4">La Sociología en la Práctica Empírica</h2>
                <p class="text-slate-600 max-w-2xl">
                    La sociología no es solo teoría; depende de rigurosos métodos de investigación para analizar tendencias. Los siguientes gráficos interactivos ilustran (con datos representativos) cómo los sociólogos recopilan datos y hacia dónde se dirige el enfoque de la investigación actual.
                </p>
            </div>

            <div class="grid grid-cols-1 lg:grid-cols-2 gap-12">
                
                <!-- Chart 1: Methods -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100">
                    <h3 class="text-xl font-bold text-slate-800 mb-2 text-center">Métodos de Investigación Utilizados</h3>
                    <p class="text-sm text-slate-500 text-center mb-6">Distribución porcentual en publicaciones recientes (datos ilustrativos)</p>
                    
                    <!-- Mandatory Chart Container -->
                    <div class="chart-container">
                        <canvas id="methodsChart"></canvas>
                    </div>
                    
                    <div class="mt-6 text-sm text-slate-600 text-center">
                        <p>Los métodos cuantitativos (encuestas) a menudo se complementan con análisis cualitativos para obtener un contexto más profundo.</p>
                    </div>
                </div>

                <!-- Chart 2: Trends -->
                <div class="bg-white p-6 rounded-2xl shadow-sm border border-slate-100">
                    <h3 class="text-xl font-bold text-slate-800 mb-2 text-center">Evolución de Temas de Interés</h3>
                    <p class="text-sm text-slate-500 text-center mb-6">Índice de menciones académicas por década (base 100)</p>
                    
                    <!-- Mandatory Chart Container -->
                    <div class="chart-container">
                        <canvas id="trendsChart"></canvas>
                    </div>

                    <div class="mt-6 text-sm text-slate-600 text-center">
                        <p>Se observa un marcado aumento en el estudio de la tecnología y su impacto social en las últimas décadas.</p>
                    </div>
                </div>

            </div>
        </section>

    </main>

    <!-- Footer -->
    <footer class="bg-slate-900 text-slate-400 py-12 text-center">
        <div class="max-w-6xl mx-auto px-4">
            <p class="mb-2">Documento Interactivo Generado para Análisis Sociológico.</p>
            <p class="text-sm">&copy; 2024 SocioData. Diseño basado en principios de Information Architecture.</p>
        </div>
    </footer>

    <!-- Javascript Logic -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            
            // --- TAB LOGIC ---
            const tabBtns = document.querySelectorAll('.tab-btn');
            const tabContents = document.querySelectorAll('.tab-content');

            // Initialize first tab
            const initTabs = () => {
                if(tabBtns.length > 0) {
                    tabBtns[0].classList.add('text-brand', 'border-b-2', 'border-brand', 'bg-white');
                    tabContents[0].classList.add('active');
                }
            };

            tabBtns.forEach(btn => {
                btn.addEventListener('click', (e) => {
                    // Remove active state from all buttons
                    tabBtns.forEach(b => {
                        b.classList.remove('text-brand', 'border-b-2', 'border-brand', 'bg-white');
                        b.classList.add('text-slate-500');
                    });
                    // Hide all contents
                    tabContents.forEach(c => c.classList.remove('active'));

                    // Add active state to clicked button
                    const targetId = btn.getAttribute('data-target');
                    btn.classList.remove('text-slate-500');
                    btn.classList.add('text-brand', 'border-b-2', 'border-brand', 'bg-white');
                    
                    // Show target content
                    document.getElementById(targetId).classList.add('active');
                });
            });

            initTabs();


            // --- CHART.JS CONFIGURATION ---
            
            // Common Options for responsiveness and styling
            Chart.defaults.font.family = "'Inter', sans-serif";
            Chart.defaults.color = '#64748b'; // slate-500

            // 1. Methods Doughnut Chart
            const ctxMethods = document.getElementById('methodsChart').getContext('2d');
            new Chart(ctxMethods, {
                type: 'doughnut',
                data: {
                    labels: ['Encuestas Cuantitativas', 'Entrevistas en Profundidad', 'Análisis Secundario', 'Observación Participante'],
                    datasets: [{
                        data: [45, 25, 20, 10],
                        backgroundColor: [
                            '#7c3aed', // brand
                            '#059669', // accent emerald
                            '#3b82f6', // blue
                            '#f59e0b'  // amber
                        ],
                        borderWidth: 2,
                        borderColor: '#ffffff',
                        hoverOffset: 4
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false, // Critical for container to control height
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                usePointStyle: true,
                            }
                        },
                        tooltip: {
                            callbacks: {
                                label: function(context) {
                                    return ' ' + context.label + ': ' + context.parsed + '%';
                                }
                            }
                        }
                    },
                    cutout: '65%'
                }
            });

            // 2. Trends Bar Chart
            const ctxTrends = document.getElementById('trendsChart').getContext('2d');
            new Chart(ctxTrends, {
                type: 'bar',
                data: {
                    labels: ['1990s', '2000s', '2010s', '2020s'],
                    datasets: [
                        {
                            label: 'Desigualdad Económica',
                            data: [65, 75, 90, 110],
                            backgroundColor: '#94a3b8', // slate-400
                        },
                        {
                            label: 'Impacto de la Tecnología',
                            data: [30, 60, 120, 180],
                            backgroundColor: '#7c3aed', // brand
                        },
                        {
                            label: 'Globalización',
                            data: [80, 110, 100, 95],
                            backgroundColor: '#10b981', // emerald
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false, // Critical for container to control height
                    scales: {
                        y: {
                            beginAtZero: true,
                            grid: {
                                color: '#f1f5f9', // slate-100
                                drawBorder: false,
                            }
                        },
                        x: {
                            grid: {
                                display: false,
                                drawBorder: false,
                            }
                        }
                    },
                    plugins: {
                        legend: {
                            position: 'bottom',
                            labels: {
                                padding: 20,
                                usePointStyle: true,
                            }
                        },
                        tooltip: {
                            mode: 'index',
                            intersect: false,
                        }
                    },
                    interaction: {
                        mode: 'nearest',
                        axis: 'x',
                        intersect: false
                    }
                }
            });
        });
    </script>
</body>
</html>
