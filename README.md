<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Science 8 Unit A Topic 2 Study Guide Quiz</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- React & ReactDOM CDNs -->
    <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
    <!-- Babel for JSX -->
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
</head>
<body class="bg-slate-50 text-slate-800 font-sans min-h-screen flex flex-col items-center justify-start p-4 sm:p-8">

    <div id="root" class="w-full max-w-3xl"></div>

    <script type="text/babel">
        const { useState } = React;

        const quizData = [
            {
                id: 1,
                type: "single",
                question: "In the Classification of Matter chart, what term fills the box directly under 'More than one substance'?",
                options: [
                    "A pure substance",
                    "A mixture term",
                    "A liquid element",
                    "A chemical bond"
                ],
                correct: [1],
                explanation: "Matter containing more than one substance is classified as a mixture."
            },
            {
                id: 2,
                type: "multi",
                question: "Which of the following are examples of heterogeneous mixtures (mechanical mixtures or suspensions)? (Select all that apply)",
                options: [
                    "Fresh fruit salad",
                    "Orange pulp juice",
                    "Clear cup salt water",
                    "Pure oxygen gas"
                ],
                correct: [0, 1],
                explanation: "Fruit salad and orange juice with pulp have visible distinct parts (heterogeneous), whereas salt water is a solution and oxygen is a pure substance."
            },
            {
                id: 3,
                type: "multi",
                question: "Which of the following substances are classified as pure substances? (Select all that apply)",
                options: [
                    "Pure gold metal",
                    "Distilled water",
                    "Fresh ocean water",
                    "Granite rock chunk"
                ],
                correct: [0, 1],
                explanation: "Gold (element) and pure water (compound) have constant composition throughout, unlike ocean water or granite."
            },
            {
                id: 4,
                type: "single",
                question: "How do the particles in a solid move compared to the particles in a gas?",
                options: [
                    "Vibrate fixed spot",
                    "Move rapidly around",
                    "Slide past loosely",
                    "Expand container filled"
                ],
                correct: [0],
                explanation: "Solid particles are held tightly in place and vibrate, whereas gas particles move rapidly and randomly."
            },
            {
                id: 5,
                type: "single",
                question: "What is the key difference between a homogeneous mixture and a heterogeneous mixture?",
                options: [
                    "Looks same throughout",
                    "Has visible layers",
                    "Has solid particles",
                    "Contains one atom"
                ],
                correct: [0],
                explanation: "Homogeneous mixtures look completely uniform throughout, while heterogeneous mixtures show distinct visible parts."
            },
            {
                id: 6,
                type: "single",
                question: "If you mix hot chocolate powder into hot water, which component acts as the solute?",
                options: [
                    "Hot water fluid",
                    "Chocolate powder",
                    "The ceramic mug",
                    "The water steam"
                ],
                correct: [1],
                explanation: "The solute is the substance being dissolved (chocolate powder), while water is the solvent."
            },
            {
                id: 7,
                type: "single",
                question: "Which of the following two solutions is more concentrated?",
                options: [
                    "25g in 100mL water",
                    "10g in 50mL water",
                    "Both equal density",
                    "Neither forms salt"
                ],
                correct: [0],
                explanation: "25g/100mL = 0.25 g/mL, which is higher than 10g/50mL = 0.20 g/mL."
            },
            {
                id: 8,
                type: "single",
                question: "What happens when you add more solute to an already saturated solution at room temperature?",
                options: [
                    "Sinks to bottom",
                    "Dissolves quickly",
                    "Evaporates away",
                    "Turns into gas"
                ],
                correct: [0],
                explanation: "A saturated solution holds the maximum solute possible; any added solute will not dissolve and settles at the bottom."
            },
            {
                id: 9,
                type: "single",
                question: "Is the saturation point for sugar in water the same as the saturation point for salt in water?",
                options: [
                    "No different solubility",
                    "Yes identical amount",
                    "Yes both dissolve",
                    "No sugar floats"
                ],
                correct: [0],
                explanation: "Saturation points depend on the specific chemical properties of the solute; water can dissolve much more sugar than salt."
            },
            {
                id: 10,
                type: "multi",
                question: "Which of the following factors directly affect the maximum solubility limit of a solute in a solvent? (Select all that apply)",
                options: [
                    "Solvent temperature",
                    "Type of solute",
                    "System pressure",
                    "Stirring speed rate"
                ],
                correct: [0, 1, 2],
                explanation: "Temperature, solute/solvent type, and pressure determine solubility limit. Stirring speeds up dissolving rate, not maximum solubility."
            },
            {
                id: 11,
                type: "single",
                question: "What is water commonly called because it can dissolve so many different substances?",
                options: [
                    "Universal solvent",
                    "Aqueous solute",
                    "Pure mixture liquid",
                    "Thermal fluid state"
                ],
                correct: [0],
                explanation: "Water is widely known as the 'universal solvent' because it dissolves more substances than any other liquid."
            },
            {
                id: 12,
                type: "single",
                question: "How does an increase in water temperature affect the solubility of dissolved oxygen gas?",
                options: [
                    "Oxygen solubility drops",
                    "Oxygen solubility rises",
                    "Oxygen turns solid",
                    "Oxygen stays constant"
                ],
                correct: [0],
                explanation: "Gas solubility decreases as liquid temperature rises because gas molecules gain energy to escape into the air."
            },
            {
                id: 13,
                type: "multi",
                question: "Which techniques will increase the RATE at which a solid sugar cube dissolves in tea? (Select all that apply)",
                options: [
                    "Stirring tea briskly",
                    "Crushing sugar cube",
                    "Heating tea liquid",
                    "Cooling tea liquid"
                ],
                correct: [0, 1, 2],
                explanation: "Agitation, increased surface area (crushing), and higher temperature all increase the speed/rate of dissolving."
            }
        ];

        function App() {
            const [answers, setAnswers] = useState({});
            const [submitted, setSubmitted] = useState(false);
            const [score, setScore] = useState(0);

            const handleOptionChange = (qId, optionIdx, type) => {
                if (submitted) return;

                if (type === "single") {
                    setAnswers(prev => ({ ...prev, [qId]: [optionIdx] }));
                } else {
                    setAnswers(prev => {
                        const current = prev[qId] || [];
                        if (current.includes(optionIdx)) {
                            return { ...prev, [qId]: current.filter(i => i !== optionIdx) };
                        } else {
                            return { ...prev, [qId]: [...current, optionIdx].sort() };
                        }
                    });
                }
            };

            const handleSubmit = () => {
                let correctCount = 0;
                quizData.forEach(q => {
                    const userAns = (answers[q.id] || []).sort();
                    const correctAns = [...q.correct].sort();
                    if (JSON.stringify(userAns) === JSON.stringify(correctAns)) {
                        correctCount++;
                    }
                });
                setScore(correctCount);
                setSubmitted(true);
                window.scrollTo({ top: 0, behavior: 'smooth' });
            };

            const handleReset = () => {
                setAnswers({});
                setSubmitted(false);
                setScore(0);
                window.scrollTo({ top: 0, behavior: 'smooth' });
            };

            return (
                <div className="bg-white rounded-xl shadow-sm border border-slate-200 p-6 sm:p-10">
                    <header className="border-b border-slate-100 pb-6 mb-8">
                        <h1 className="text-2xl sm:text-3xl font-bold text-slate-900 tracking-tight">Science 8 Unit A Topic 2 Study Guide Quiz</h1>
                        <p className="text-slate-600 mt-2 text-sm sm:text-base">
                            Complete all 13 study guide questions below. Some questions require selecting more than one correct option.
                        </p>
                    </header>

                    {submitted && (
                        <div className="mb-8 p-6 bg-slate-100 rounded-lg border border-slate-200 text-center">
                            <h2 className="text-xl font-semibold text-slate-900">Quiz Submitted!</h2>
                            <p className="text-lg text-slate-700 mt-2">
                                Your Score: <span className="font-bold text-slate-900">{score}</span> / {quizData.length}
                            </p>
                            <button
                                onClick={handleReset}
                                className="mt-4 px-6 py-2 bg-slate-800 text-white text-sm font-medium rounded-md hover:bg-slate-700 transition"
                            >
                                Restart Quiz
                            </button>
                        </div>
                    )}

                    <div className="space-y-8">
                        {quizData.map((q, qIdx) => {
                            const userAns = answers[q.id] || [];
                            const correctAns = q.correct;
                            const isCorrect = submitted && JSON.stringify([...userAns].sort()) === JSON.stringify([...correctAns].sort());

                            return (
                                <div key={q.id} className={`p-6 rounded-lg border ${submitted ? (isCorrect ? 'border-emerald-200 bg-emerald-50/30' : 'border-rose-200 bg-rose-50/30') : 'border-slate-200 bg-white'}`}>
                                    <div className="flex items-start justify-between">
                                        <h3 className="font-medium text-slate-900 text-base sm:text-lg">
                                            <span className="text-slate-500 font-normal mr-2">Q{qIdx + 1}.</span>
                                            {q.question}
                                        </h3>
                                    </div>
                                    
                                    <p className="text-xs text-slate-500 mt-1 mb-4 italic">
                                        {q.type === 'multi' ? 'Select all correct choices.' : 'Select one choice.'}
                                    </p>

                                    <div className="space-y-2.5">
                                        {q.options.map((opt, oIdx) => {
                                            const isSelected = userAns.includes(oIdx);
                                            const isOptCorrect = correctAns.includes(oIdx);

                                            let optionStyling = "border-slate-200 hover:border-slate-300 bg-white";
                                            if (submitted) {
                                                if (isOptCorrect) {
                                                    optionStyling = "border-emerald-500 bg-emerald-50 text-emerald-900 font-medium";
                                                } else if (isSelected && !isOptCorrect) {
                                                    optionStyling = "border-rose-300 bg-rose-50 text-rose-900";
                                                }
                                            } else if (isSelected) {
                                                optionStyling = "border-slate-800 bg-slate-50 ring-1 ring-slate-800";
                                            }

                                            return (
                                                <label
                                                    key={oIdx}
                                                    className={`flex items-center p-3.5 rounded-md border text-sm sm:text-base cursor-pointer transition ${optionStyling}`}
                                                >
                                                    <input
                                                        type={q.type === 'single' ? 'radio' : 'checkbox'}
                                                        name={`question-${q.id}`}
                                                        checked={isSelected}
                                                        onChange={() => handleOptionChange(q.id, oIdx, q.type)}
                                                        disabled={submitted}
                                                        className="h-4 w-4 text-slate-800 focus:ring-slate-800 border-slate-300 mr-3"
                                                    />
                                                    <span>{opt}</span>
                                                </label>
                                            );
                                        })}
                                    </div>

                                    {submitted && (
                                        <div className="mt-4 pt-3 border-t border-slate-200/60 text-sm">
                                            <p className={`font-semibold ${isCorrect ? 'text-emerald-700' : 'text-rose-700'}`}>
                                                {isCorrect ? '✓ Correct' : '✕ Incorrect'}
                                            </p>
                                            <p className="text-slate-600 mt-1"><span className="font-medium">Explanation:</span> {q.explanation}</p>
                                        </div>
                                    )}
                                </div>
                            );
                        })}
                    </div>

                    {!submitted && (
                        <div className="mt-10 text-center">
                            <button
                                onClick={handleSubmit}
                                className="px-8 py-3 bg-slate-900 text-white font-medium rounded-md hover:bg-slate-800 transition shadow-sm"
                            >
                                Submit & Grade Quiz
                            </button>
                        </div>
                    )}
                </div>
            );
        }

        ReactDOM.render(<App />, document.getElementById('root'));
    </script>
</body>
</html>
