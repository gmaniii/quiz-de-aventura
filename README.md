import React, { useState } from "react";

// Quiz Interativo: Tribos Indígenas
// ⚠️ Observação: as imagens usam URLs públicas (Unsplash/Pexels) apenas como ilustração temática.
// Para uso offline/autorais, substitua os links por arquivos locais ou imagens com direitos garantidos.

const TRIBES = [
  {
    id: "guarani",
    name: "Guarani",
    coverImage:
      "https://images.unsplash.com/photo-1500530855697-b586d89ba3ee?q=80&w=1200&auto=format&fit=crop", // floresta
    questions: [
      {
        q: "Qual é um dos elementos centrais da espiritualidade Guarani?",
        options: [
          "Danças de guerra",
          "Canto sagrado e rezas (mborai)",
          "Caça de animais grandes",
          "Pinturas corporais vermelhas",
        ],
        correctIndex: 1,
        explanation:
          "Para os Guarani, o mborai (canto sagrado) conecta a comunidade ao mundo espiritual e é parte essencial das cerimônias religiosas.",
        image:
          "https://images.unsplash.com/photo-1501785888041-af3ef285b470?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Qual é a base da alimentação tradicional Guarani?",
        options: [
          "Milho e mandioca",
          "Arroz e feijão",
          "Batata e trigo",
          "Carne de caça apenas",
        ],
        correctIndex: 0,
        explanation:
          "O milho e a mandioca são cultivados há séculos e têm papel cultural e alimentar muito forte entre os Guarani.",
        image:
          "https://images.unsplash.com/photo-1560785496-3c9d1b3d5b38?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Os Guarani acreditam em uma 'Terra Sem Males'. O que isso significa?",
        options: [
          "Uma ilha sagrada no litoral",
          "Um lugar onde não há sofrimento",
          "Uma região cheia de caça",
          "Um templo subterrâneo",
        ],
        correctIndex: 1,
        explanation:
          "A Terra Sem Males é uma visão espiritual de um lugar perfeito, livre de doenças e fome, buscado por meio da fé e da prática ritual.",
        image:
          "https://images.unsplash.com/photo-1502082553048-f009c37129b9?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "O que representa o petyngua (cachimbo cerimonial) entre os Guarani?",
        options: [
          "Força do guerreiro",
          "Conexão com os ancestrais",
          "Símbolo de caça",
          "Arte decorativa",
        ],
        correctIndex: 1,
        explanation:
          "Fumar o petyngua é um ritual de ligação com os espíritos e uma prática coletiva importante.",
        image:
          "https://images.unsplash.com/photo-1497215728101-495f8e5b0f36?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Como os Guarani tradicionalmente transmitem seu conhecimento?",
        options: [
          "Em livros escritos",
          "Através de professores contratados",
          "Pela oralidade, histórias e cantos",
          "Por pinturas em cavernas",
        ],
        correctIndex: 2,
        explanation:
          "O conhecimento é repassado pelos mais velhos por meio da fala, cantos e narrativas sagradas, reforçando a memória coletiva.",
        image:
          "https://images.unsplash.com/photo-1526318472351-c75fcf070305?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Qual arte é muito presente entre os Guarani?",
        options: [
          "Esculturas em pedra",
          "Tecelagem de algodão",
          "Cestaria e artesanato em taquara",
          "Pinturas em tela",
        ],
        correctIndex: 2,
        explanation:
          "A cestaria em taquara é tradição transmitida por gerações, usada no cotidiano e em contextos rituais.",
        image:
          "https://images.unsplash.com/photo-1604335399105-20f86f5e39c4?q=80&w=1200&auto=format&fit=crop",
      },
    ],
  },
  {
    id: "yanomami",
    name: "Yanomami",
    coverImage:
      "https://images.unsplash.com/photo-1544739313-6fadad91d867?q=80&w=1200&auto=format&fit=crop", // Amazônia aérea
    questions: [
      {
        q: "Qual o tipo de habitação coletiva típica dos Yanomami?",
        options: [
          "Oca individual",
          "Maloca circular (yano)",
          "Tenda de palha portátil",
          "Casa subterrânea",
        ],
        correctIndex: 1,
        explanation:
          "As grandes malocas circulares, chamadas yano, abrigam várias famílias em uma estrutura comunal aberta no centro.",
        image:
          "https://images.unsplash.com/photo-1526318472351-c75fcf070305?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Qual prática espiritual é central entre os Yanomami?",
        options: [
          "Culto às pedras",
          "Xamanismo com os xapiri",
          "Adoração ao fogo apenas",
          "Meditação silenciosa coletiva",
        ],
        correctIndex: 1,
        explanation:
          "Os xamãs se comunicam com os xapiri (espíritos auxiliares) através de cantos e inalação de pó alucinógeno (yãkoana) em rituais de cura e proteção.",
        image:
          "https://images.unsplash.com/photo-1504208434309-cb69f4fe52b0?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Sobre a alimentação, os Yanomami são conhecidos por:",
        options: [
          "Pastoralismo de gado",
          "Horticultura e caça/pesca",
          "Monocultura de trigo",
          "Apenas coleta de frutos",
        ],
        correctIndex: 1,
        explanation:
          "Praticam horticultura itinerante (roça de mandioca, banana, cará), além de caça e pesca, compondo uma dieta diversa.",
        image:
          "https://images.unsplash.com/photo-1455731679969-0ef3a9e346ca?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Qual ritual funerário ficou conhecido na literatura etnográfica Yanomami?",
        options: [
          "Sepultamento em árvores",
          "Cremar e consumir as cinzas em mingau",
          "Múmias de fumaça",
          "Barco-rio para o além",
        ],
        correctIndex: 1,
        explanation:
          "No ritual reahu, as cinzas do falecido podem ser misturadas a um mingau de banana, gesto de incorporação e memória coletiva.",
        image:
          "https://images.unsplash.com/photo-1614258725662-6469a8e1b51c?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Um desafio contemporâneo crítico para os Yanomami é:",
        options: [
          "Secas do sertão",
          "Garimpo ilegal e doenças associadas",
          "Vulcanismo local",
          "Glaciações sazonais",
        ],
        correctIndex: 1,
        explanation:
          "A invasão por garimpo ilegal traz mercúrio, violência e doenças, impactando gravemente a saúde e o território Yanomami.",
        image:
          "https://images.unsplash.com/photo-1500390361284-88c6b1b36000?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Quanto à estética corporal, entre os Yanomami é comum:",
        options: [
          "Tatuagens com tinta industrial",
          "Pinturas com urucum e carvão",
          "Piercings de metal pesados",
          "Raspagem total de cabelos",
        ],
        correctIndex: 1,
        explanation:
          "A pintura corporal com urucum (vermelho) e carvão (preto) compõe marcações estéticas, rituais e identitárias.",
        image:
          "https://images.unsplash.com/photo-1497384401032-2182d2687715?q=80&w=1200&auto=format&fit=crop",
      },
    ],
  },
  {
    id: "xavante",
    name: "Xavante",
    coverImage:
      "https://images.unsplash.com/photo-1520975693416-35a1cb0b6091?q=80&w=1200&auto=format&fit=crop", // cerrado
    questions: [
      {
        q: "Qual prática esportivo-ritual é emblemática entre os Xavante?",
        options: [
          "Corrida de tora",
          "Luta de capoeira",
          "Arremesso de dardo",
          "Regata de canoas",
        ],
        correctIndex: 0,
        explanation:
          "A corrida de tora envolve carregar troncos pesados em equipes, fortalecendo corpo, disciplina e cooperação entre clãs.",
        image:
          "https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "A organização social Xavante se baseia fortemente em:",
        options: [
          "Moidades (dualismo clânico)",
          "Cidades-estado independentes",
          "Casta hereditária rígida",
          "Famílias isoladas",
        ],
        correctIndex: 0,
        explanation:
          "O dualismo em moidades regula casamento, cooperação e rituais, estruturando alianças e papéis sociais.",
        image:
          "https://images.unsplash.com/photo-1482192505345-5655af888cc4?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Entre os Xavante, um rito marcante de formação juvenil é:",
        options: [
          "Wai'a (iniciação) e educação formal de guerreiros",
          "Batismo em rio gelado",
          "Prova de salto sobre fogo",
          "Peregrinação anual urbana",
        ],
        correctIndex: 0,
        explanation:
          "O complexo de iniciação (como o Wai'a) marca a passagem de fases da vida, com ensinamentos, resguardo e orientações dos mais velhos.",
        image:
          "https://images.unsplash.com/photo-1483721310020-03333e577078?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Quanto à língua, os Xavante falam:",
        options: [
          "Uma língua da família Akwén (Jê)",
          "Tupi-Guarani",
          "Arawak",
          "Karib",
        ],
        correctIndex: 0,
        explanation:
          "O Xavante pertence ao tronco Macro-Jê, família Akwén, com rica tradição oral e cantos cerimoniais.",
        image:
          "https://images.unsplash.com/photo-1517541866997-4fdb4d716f00?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Uma característica marcante da estética Xavante é:",
        options: [
          "Corte de cabelo e pinturas geométricas",
          "Somente tatuagens faciais permanentes",
          "Máscaras de metal",
          "Uso exclusivo de branco",
        ],
        correctIndex: 0,
        explanation:
          "Cortes de cabelo específicos e pinturas geométricas corporais comunicam idade, status e participação ritual.",
        image:
          "https://images.unsplash.com/photo-1517842184081-39b8b67a97b0?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Qual relação do ambiente com o modo de vida Xavante?",
        options: [
          "Adaptação ao Cerrado com coleta, caça e roças",
          "Criação extensiva de gado bovino",
          "Agricultura mecanizada de larga escala",
          "Dependência exclusiva de comércio urbano",
        ],
        correctIndex: 0,
        explanation:
          "Vivem no bioma Cerrado, articulando roças, coleta de frutos nativos e caça, de forma sazonal e comunitária.",
        image:
          "https://images.unsplash.com/photo-1500534623283-312aade485b7?q=80&w=1200&auto=format&fit=crop",
      },
    ],
  },
  {
    id: "tikuna",
    name: "Tikuna",
    coverImage:
      "https://images.unsplash.com/photo-1584118624012-b237f2c2a6ee?q=80&w=1200&auto=format&fit=crop", // rio amazônico
    questions: [
      {
        q: "O 'ritual da moça nova' (pelazón) entre os Tikuna marca:",
        options: [
          "A colheita do milho",
          "A primeira menstruação e a passagem para a vida adulta",
          "A mudança de aldeia",
          "A adoção de um nome estrangeiro",
        ],
        correctIndex: 1,
        explanation:
          "A pelazón celebra a puberdade feminina com reclusão, pinturas e danças, reconhecendo a transição social da jovem.",
        image:
          "https://images.unsplash.com/photo-1543997385-22fe6c1f6d56?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "A estética corporal Tikuna utiliza com frequência:",
        options: [
          "Tinta de jenipapo e urucum",
          "Grafite spray",
          "Argila azul industrial",
          "Tintas acrílicas importadas",
        ],
        correctIndex: 0,
        explanation:
          "Jenipapo (preto-azulado) e urucum (vermelho) são usados em pinturas rituais e festivas de forte simbolismo.",
        image:
          "https://images.unsplash.com/photo-1495562569060-2eec283d3391?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "A principal região de ocupação Tikuna no Brasil é:",
        options: [
          "Alto Solimões, fronteira com Colômbia e Peru",
          "Serra do Mar, Sudeste",
          "Pampa Gaúcho",
          "Chapada Diamantina",
        ],
        correctIndex: 0,
        explanation:
          "Os Tikuna vivem majoritariamente ao longo do Alto Solimões (AM), em área transfronteiriça com Peru e Colômbia.",
        image:
          "https://images.unsplash.com/photo-1519681393784-d120267933ba?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Quanto à subsistência, os Tikuna praticam:",
        options: [
          "Pesca, roças e coleta na várzea",
          "Somente pecuária leiteira",
          "Mineração de carvão",
          "Plantio mecanizado de soja",
        ],
        correctIndex: 0,
        explanation:
          "A vida nas margens dos rios envolve pesca abundante, roçados (mandioca, milho, banana) e coleta de recursos da floresta.",
        image:
          "https://images.unsplash.com/photo-1544739313-6fadad91d867?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Um elemento artístico típico entre os Tikuna é:",
        options: [
          "Máscaras e ornamentos em festas",
          "Esculturas de mármore renascentistas",
          "Vitrais medievais",
          "Cerâmica esmaltada japonesa",
        ],
        correctIndex: 0,
        explanation:
          "Máscaras, coroas e adereços destacam personagens míticos em rituais e festas comunitárias.",
        image:
          "https://images.unsplash.com/photo-1520975693416-35a1cb0b6091?q=80&w=1200&auto=format&fit=crop",
      },
      {
        q: "Sobre demografia, os Tikuna são conhecidos por:",
        options: [
          "Ser um dos maiores povos indígenas do Brasil",
          "Ser o menor povo indígena do mundo",
          "Viver exclusivamente em cavernas",
          "Migrar sazonalmente para o Ártico",
        ],
        correctIndex: 0,
        explanation:
          "Os Tikuna figuram entre os povos indígenas com maior população no Brasil, com muitas comunidades no Amazonas.",
        image:
          "https://images.unsplash.com/photo-1528892952291-009c663ce843?q=80&w=1200&auto=format&fit=crop",
      },
    ],
  },
];

function ProgressBar({ value, total }) {
  const pct = Math.round(((value + 1) / total) * 100);
  return (
    <div className="w-full bg-gray-200 rounded-2xl h-3 overflow-hidden">
      <div
        className="h-3 bg-emerald-600 transition-all"
        style={{ width: `${pct}%` }}
        aria-label={`Progresso ${pct}%`}
      />
    </div>
  );
}

export default function IndigenousQuizApp() {
  const [selectedTribe, setSelectedTribe] = useState(null);
  const [index, setIndex] = useState(0);
  const [score, setScore] = useState(0);
  const [showExplanation, setShowExplanation] = useState(false);
  const [chosen, setChosen] = useState(null);
  const [answers, setAnswers] = useState([]); // {q, correct, chosen}

  const tribe = TRIBES.find((t) => t.id === selectedTribe);
  const total = tribe ? tribe.questions.length : 0;

  const reset = () => {
    setSelectedTribe(null);
    setIndex(0);
    setScore(0);
    setShowExplanation(false);
    setChosen(null);
    setAnswers([]);
  };

  const handleChooseTribe = (id) => {
    setSelectedTribe(id);
    setIndex(0);
    setScore(0);
    setAnswers([]);
    setShowExplanation(false);
  };

  const handleAnswer = (i) => {
    if (!tribe) return;
    if (showExplanation) return;

    const question = tribe.questions[index];
    const correct = i === question.correctIndex;
    setChosen(i);
    setShowExplanation(true);
    setAnswers((prev) => [
      ...prev,
      { q: question.q, chosen: question.options[i], correct: correct, correctText: question.options[question.correctIndex], explanation: question.explanation },
    ]);
    if (correct) setScore((s) => s + 1);
  };

  const next = () => {
    setShowExplanation(false);
    setChosen(null);
    if (!tribe) return;
    if (index + 1 < tribe.questions.length) {
      setIndex((i) => i + 1);
    } else {
      // finished
    }
  };

  return (
    <div className="min-h-screen w-full bg-gradient-to-b from-emerald-50 to-white text-gray-900">
      <div className="max-w-4xl mx-auto p-6">
        <header className="flex items-center justify-between mb-6">
          <h1 className="text-2xl sm:text-3xl font-bold">🌿 Quiz das Tribos Indígenas</h1>
          <button
            onClick={reset}
            className="text-sm px-3 py-2 rounded-xl bg-gray-100 hover:bg-gray-200"
          >
            Reiniciar
          </button>
        </header>

        {!tribe && (
          <section>
            <p className="mb-4 text-gray-700">
              Escolha uma tribo para iniciar. As perguntas e curiosidades serão específicas da sua escolha.
            </p>
            <div className="grid sm:grid-cols-2 gap-4">
              {TRIBES.map((t) => (
                <button
                  key={t.id}
                  onClick={() => handleChooseTribe(t.id)}
                  className="group rounded-2xl overflow-hidden bg-white shadow hover:shadow-lg transition"
                >
                  <div className="h-40 w-full overflow-hidden">
                    <img
                      src={t.coverImage}
                      alt={`Imagem representativa de ${t.name}`}
                      className="w-full h-full object-cover group-hover:scale-105 transition"
                    />
                  </div>
                  <div className="p-4 text-left">
                    <h2 className="text-xl font-semibold">{t.name}</h2>
                    <p className="text-sm text-gray-600">6 perguntas com múltipla escolha + explicações detalhadas.</p>
                  </div>
                </button>
              ))}
            </div>
          </section>
        )}

        {tribe && index < total && (
          <section className="bg-white rounded-2xl shadow p-4 sm:p-6">
            <div className="flex items-center gap-3 mb-4">
              <span className="text-sm px-2 py-1 rounded-full bg-emerald-100 text-emerald-800">{tribe.name}</span>
              <span className="text-sm text-gray-600">Pergunta {index + 1} de {total}</span>
            </div>
            <ProgressBar value={index} total={total} />

            <div className="mt-4 grid md:grid-cols-2 gap-4">
              <div className="order-2 md:order-1">
                <h3 className="text-lg sm:text-xl font-semibold mb-3">{tribe.questions[index].q}</h3>
                <div className="space-y-2">
                  {tribe.questions[index].options.map((opt, i) => {
                    const isCorrect = i === tribe.questions[index].correctIndex;
                    const isChosen = chosen === i;
                    let styles = "border-gray-200 hover:border-emerald-300 hover:bg-emerald-50";
                    if (showExplanation && isChosen && isCorrect) styles = "border-emerald-500 bg-emerald-50";
                    if (showExplanation && isChosen && !isCorrect) styles = "border-red-400 bg-red-50";
                    if (showExplanation && !isChosen && isCorrect) styles += " border-emerald-300";

                    return (
                      <button
                        key={i}
                        onClick={() => handleAnswer(i)}
                        className={`w-full text-left border rounded-xl px-3 py-2 transition ${styles}`}
                        disabled={showExplanation}
                      >
                        <span className="font-medium">{String.fromCharCode(97 + i)})</span> {opt}
                      </button>
                    );
                  })}
                </div>

                {showExplanation && (
                  <div className="mt-4 p-3 border rounded-xl bg-gray-50">
                    <p className="font-semibold mb-1">
                      {chosen === tribe.questions[index].correctIndex ? "✅ Resposta correta!" : "❌ Resposta incorreta."}
                    </p>
                    <p className="text-sm text-gray-700 mb-1">
                      Correto: <strong>{tribe.questions[index].options[tribe.questions[index].correctIndex]}</strong>
                    </p>
                    <p className="text-sm text-gray-700">{tribe.questions[index].explanation}</p>
                    <div className="mt-3">
                      <button
                        onClick={next}
                        className="px-3 py-2 rounded-xl bg-emerald-600 text-white hover:bg-emerald-700"
                      >
                        {index + 1 < total ? "Próxima" : "Finalizar"}
                      </button>
                    </div>
                  </div>
                )}
              </div>

              <div className="order-1 md:order-2">
                <div className="rounded-2xl overflow-hidden h-56 sm:h-64 md:h-full bg-gray-100">
                  <img
                    src={tribe.questions[index].image}
                    alt="Ilustração da pergunta"
                    className="w-full h-full object-cover"
                  />
                </div>
              </div>
            </div>
          </section>
        )}

        {tribe && index >= total && (
          <section className="bg-white rounded-2xl shadow p-6">
            <div className="flex items-center justify-between">
              <h2 className="text-xl font-semibold">Resultado — {tribe.name}</h2>
              <span className="text-sm px-3 py-1 rounded-full bg-emerald-100 text-emerald-800">Pontuação: {score} / {total}</span>
            </div>
            <p className="text-gray-700 mt-2">Revise suas respostas e explicações abaixo. Você pode reiniciar ou escolher outra tribo.</p>

            <ol className="mt-4 space-y-3 list-decimal list-inside">
              {answers.map((a, i) => (
                <li key={i} className="p-3 border rounded-xl">
                  <p className="font-medium">{a.q}</p>
                  <p className="text-sm mt-1">
                    Sua resposta: <span className={a.correct ? "text-emerald-700" : "text-red-700"}>{a.chosen}</span> — Correto: <strong>{a.correctText}</strong>
                  </p>
                  <p className="text-sm text-gray-700 mt-1">{a.explanation}</p>
                </li>
              ))}
            </ol>

            <div className="mt-6 flex flex-wrap gap-3">
              <button
                onClick={() => handleChooseTribe(tribe.id)}
                className="px-4 py-2 rounded-xl bg-emerald-600 text-white hover:bg-emerald-700"
              >
                Refazer {tribe.name}
              </button>
              <button
                onClick={reset}
                className="px-4 py-2 rounded-xl bg-gray-100 hover:bg-gray-200"
              >
                Escolher outra tribo
              </button>
            </div>
          </section>
        )}

        <footer className="mt-10 text-xs text-gray-500">
          <p>
            Este quiz é educativo e apresenta curiosidades culturais. Para uso em sala de aula, complemente com fontes e materiais didáticos locais.
          </p>
        </footer>
      </div>
    </div>
  );
}
