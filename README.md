PsyMetalCore AI
"use client";

import { useState } from "react";
import {
  Sparkles,
  Download,
  Wand2,
  Skull,
  Cpu,
  Flame,
} from "lucide-react";

export default function MeatcoreTattooAI() {
  const [concept, setConcept] = useState("");
  const [generatedPrompt, setGeneratedPrompt] = useState("");
  const [generatedImage, setGeneratedImage] = useState("");
  const [isGenerating, setIsGenerating] = useState(false);

  const [selectedStyle, setSelectedStyle] =
    useState("Meatcore Giger");

  const [selectedPlacement, setSelectedPlacement] =
    useState("Full Sleeve");

  const styles = [
    "Meatcore Giger",
    "Biomechanical Flesh",
    "Cyber Gore",
    "Necro Anime",
    "Blood Cathedral",
    "Chrome Horror",
  ];

  const placements = [
    "Full Sleeve",
    "Forearm",
    "Leg",
    "Back",
    "Chest",
    "Neck",
  ];

  const generateTattoo = async () => {
    setIsGenerating(true);
    setGeneratedImage("");

    const prompt = `
masterpiece,
${selectedStyle},
anime biomechanical tattoo,
${selectedPlacement} tattoo composition,
${concept},
hr giger inspired flesh textures,
exposed tendons,
cybernetic veins,
dark organic tubes,
blood red glow,
black chrome biomechanical armor,
gothic horror atmosphere,
sharp tattoo linework,
tattoo stencil readability,
meatcore aesthetic,
dark web horror,
ultra detailed,
high contrast,
black background
`;

    setGeneratedPrompt(prompt);

    try {
      const response = await fetch("/api/generate", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({
          prompt,
        }),
      });

      const data = await response.json();

      if (data.image) {
        setGeneratedImage(data.image);
      }
    } catch (error) {
      console.error("Generation Error:", error);
    }

    setIsGenerating(false);
  };

  const downloadImage = async () => {
    if (!generatedImage) return;

    const response = await fetch(generatedImage);
    const blob = await response.blob();

    const url = window.URL.createObjectURL(blob);

    const a = document.createElement("a");
    a.href = url;
    a.download = "psymetalcore-tattoo.png";
    a.click();

    window.URL.revokeObjectURL(url);
  };

  return (
    <div className="min-h-screen bg-black text-white overflow-hidden">
      {/* BACKGROUND */}
      <div className="absolute inset-0 bg-[radial-gradient(circle_at_top,rgba(120,0,0,0.4),transparent_60%)]" />

      {/* LOADING */}
      {isGenerating && (
        <div className="fixed inset-0 z-50 bg-black/90 flex items-center justify-center">
          <div className="text-center">
            <div className="text-red-600 text-6xl animate-pulse mb-6">
              ⛧
            </div>

            <h2 className="text-3xl font-black tracking-widest text-red-500">
              MUTATING FLESH...
            </h2>
          </div>
        </div>
      )}

      <div className="relative z-10 max-w-7xl mx-auto px-6 py-10">
        {/* HEADER */}
        <div className="mb-10 flex items-center justify-between border-b border-red-950 pb-6">
          <div>
            <div className="flex items-center gap-3 mb-3">
              <Skull className="text-red-600" size={38} />

              <h1 className="text-5xl md:text-7xl font-black tracking-tight">
                PSYMETALCORE AI
              </h1>
            </div>

            <p className="text-zinc-500 text-lg max-w-2xl leading-relaxed">
              Generador IA de tattoos biomecánicos anime inspirado
              en horror industrial, carne sintética, biomech anime
              y estética cyber necromántica.
            </p>
          </div>

          <div className="hidden md:flex items-center gap-3 text-red-700">
            <Cpu />
            <Flame />
            <Wand2 />
          </div>
        </div>

        {/* MAIN GRID */}
        <div className="grid lg:grid-cols-2 gap-8">
          {/* LEFT PANEL */}
          <div className="bg-zinc-950/70 backdrop-blur rounded-[32px] border border-red-950 p-6 shadow-2xl shadow-red-950/20">
            <div className="mb-6">
              <h2 className="text-3xl font-bold mb-2">
                Create Flesh Design
              </h2>

              <p className="text-zinc-500">
                Diseña tattoos biomecánicos anime listos para
                stencil.
              </p>
            </div>

            <div className="space-y-6">
              {/* CONCEPT */}
              <div>
                <label className="block mb-2 text-sm text-zinc-500 uppercase tracking-[0.2em]">
                  Main Concept
                </label>

                <textarea
                  value={concept}
                  onChange={(e) =>
                    setConcept(e.target.value)
                  }
                  placeholder="anime biomechanical queen, chrome skull halo, exposed flesh tubes, cyber veins..."
                  className="w-full h-40 rounded-3xl bg-black border border-red-950 p-5 resize-none focus:outline-none focus:border-red-700 transition"
                />
              </div>

              {/* STYLE */}
              <div>
                <label className="block mb-3 text-sm text-zinc-500 uppercase tracking-[0.2em]">
                  Style Mutation
                </label>

                <div className="grid grid-cols-2 gap-3">
                  {styles.map((style) => (
                    <button
                      key={style}
                      onClick={() =>
                        setSelectedStyle(style)
                      }
                      className={`rounded-2xl p-4 text-sm border transition-all duration-300 ${
                        selectedStyle === style
                          ? "bg-red-700 text-white border-red-500 shadow-lg shadow-red-900/40"
                          : "bg-black border-red-950 hover:border-red-700 text-zinc-400"
                      }`}
                    >
                      {style}
                    </button>
                  ))}
                </div>
              </div>

              {/* PLACEMENT */}
              <div>
                <label className="block mb-3 text-sm text-zinc-500 uppercase tracking-[0.2em]">
                  Body Placement
                </label>

                <div className="flex flex-wrap gap-3">
                  {placements.map((placement) => (
                    <button
                      key={placement}
                      onClick={() =>
                        setSelectedPlacement(
                          placement
                        )
                      }
                      className={`px-5 py-3 rounded-full border transition-all ${
                        selectedPlacement === placement
                          ? "bg-red-700 border-red-500"
                          : "bg-black border-red-950 hover:border-red-700"
                      }`}
                    >
                      {placement}
                    </button>
                  ))}
                </div>
              </div>

              {/* BUTTON */}
              <button
                onClick={generateTattoo}
                className="w-full py-5 rounded-3xl bg-gradient-to-r from-red-950 via-red-700 to-red-950 hover:scale-[1.01] transition-all duration-300 flex items-center justify-center gap-3 text-lg font-bold tracking-wide"
              >
                <Sparkles />

                {isGenerating
                  ? "Mutating Flesh..."
                  : "Generate Meatcore Tattoo"}
              </button>
            </div>
          </div>

          {/* RIGHT PANEL */}
          <div className="bg-zinc-950/70 backdrop-blur rounded-[32px] border border-red-950 p-6 shadow-2xl shadow-red-950/20 flex flex-col">
            <div className="flex items-center justify-between mb-5">
              <div>
                <h2 className="text-3xl font-bold">
                  Neural Output
                </h2>

                <p className="text-zinc-500 text-sm mt-1">
                  Flux + SDXL + PsyMetalCore
                </p>
              </div>

              <div className="w-4 h-4 rounded-full bg-red-600 animate-pulse" />
            </div>

            <div className="flex-1 rounded-[32px] border border-red-950 bg-black overflow-hidden relative min-h-[580px]">
              <div className="absolute inset-0 opacity-20 bg-[radial-gradient(circle_at_center,rgba(255,0,0,0.25),transparent_70%)]" />

              <div className="relative h-full flex items-center justify-center p-4">
                {generatedImage ? (
                  <img
                    src={generatedImage}
                    alt="Generated Tattoo"
                    className="w-full h-full object-cover rounded-3xl"
                  />
                ) : generatedPrompt ? (
                  <div className="w-full bg-black/80 border border-red-950 rounded-3xl p-6 backdrop-blur">
                    <div className="flex items-center gap-3 mb-4 text-red-500">
                      <Cpu />

                      <span className="uppercase tracking-[0.3em] text-xs">
                        Generated Prompt
                      </span>
                    </div>

                    <p className="text-zinc-300 leading-relaxed text-sm whitespace-pre-wrap break-words">
                      {generatedPrompt}
                    </p>
                  </div>
                ) : (
                  <div className="text-center">
                    <div className="text-8xl text-red-900 mb-6">
                      ⛧
                    </div>

                    <h3 className="text-2xl font-bold mb-3">
                      Flesh Engine Ready
                    </h3>

                    <p className="text-zinc-500 max-w-md leading-relaxed">
                      Tu generación biomecánica aparecerá aquí.
                    </p>
                  </div>
                )}
              </div>
            </div>

            {/* ACTIONS */}
            <div className="grid grid-cols-2 gap-4 mt-5">
              <button
                onClick={downloadImage}
                className="rounded-2xl border border-red-950 py-4 hover:bg-red-950/30 transition flex items-center justify-center gap-2"
              >
                <Download size={18} />
                Export PNG
              </button>

              <button className="rounded-2xl border border-red-950 py-4 hover:bg-red-950/30 transition flex items-center justify-center gap-2">
                <Wand2 size={18} />
                Generate Stencil
              </button>
            </div>
          </div>
        </div>

        {/* FEATURES */}
        <div className="grid md:grid-cols-3 gap-6 mt-10">
          <div className="bg-zinc-950/70 rounded-[28px] border border-red-950 p-6">
            <div className="text-red-600 mb-4">
              <Skull size={32} />
            </div>

            <h3 className="text-2xl font-bold mb-3">
              Organic Horror
            </h3>

            <p className="text-zinc-500 leading-relaxed">
              Carne sintética, biomecánica visceral y horror
              industrial inspirado en biomech anime.
            </p>
          </div>

          <div className="bg-zinc-950/70 rounded-[28px] border border-red-950 p-6">
            <div className="text-red-600 mb-4">
              <Cpu size={32} />
            </div>

            <h3 className="text-2xl font-bold mb-3">
              Cyber Necromancy
            </h3>

            <p className="text-zinc-500 leading-relaxed">
              Estética dark web, mutación digital y tecnología
              corrupta.
            </p>
          </div>

          <div className="bg-zinc-950/70 rounded-[28px] border border-red-950 p-6">
            <div className="text-red-600 mb-4">
              <Flame size={32} />
            </div>

            <h3 className="text-2xl font-bold mb-3">
              Tattoo Ready
            </h3>

            <p className="text-zinc-500 leading-relaxed">
              Composición optimizada para stencil, sleeves y
              tatuajes reales.
            </p>
          </div>
        </div>
      </div>
    </div>
  );
}
export default function MeatcoreGeneratorPage() { return ( <div className="min-h-screen bg-black text-white overflow-hidden relative"> {/* Background */} <div className="absolute inset-0 bg-[radial-gradient(circle_at_top,rgba(120,0,0,0.35),transparent_40%)]" /> <div className="absolute inset-0 opacity-20 bg-[linear-gradient(rgba(255,0,0,0.08)_1px,transparent_1px),linear-gradient(90deg,rgba(255,0,0,0.08)_1px,transparent_1px)] bg-[size:40px_40px]" />

{/* Header */}
  <header className="relative z-10 border-b border-red-900/40 backdrop-blur-md bg-black/40">
    <div className="max-w-7xl mx-auto px-6 py-5 flex items-center justify-between">
      <div>
        <h1 className="text-4xl font-black tracking-[0.3em] uppercase text-red-500 drop-shadow-[0_0_12px_rgba(255,0,0,0.8)]">
          MeatCore AI
        </h1>
        <p className="text-red-200/60 mt-2 text-sm tracking-widest uppercase">
          Anime • Gore • Cyber • Tattoo Generator
        </p>
      </div>

      <button className="border border-red-700 px-5 py-2 rounded-full bg-red-950/40 hover:bg-red-700/20 transition-all duration-300 text-sm uppercase tracking-widest shadow-[0_0_20px_rgba(255,0,0,0.25)]">
        Github Deploy
      </button>
    </div>
  </header>

  {/* Hero */}
  <section className="relative z-10 max-w-7xl mx-auto px-6 py-16 grid lg:grid-cols-2 gap-10 items-center">
    <div>
      <div className="inline-flex items-center gap-2 border border-red-800/50 bg-red-950/20 px-4 py-2 rounded-full text-xs uppercase tracking-[0.3em] text-red-300 mb-6">
        PsyMetalCore Visual Engine
      </div>

      <h2 className="text-6xl md:text-7xl font-black leading-none uppercase">
        Generate
        <span className="block text-red-500 drop-shadow-[0_0_25px_rgba(255,0,0,0.7)]">
          Meatcore
        </span>
        Visions
      </h2>

      <p className="mt-8 text-zinc-400 text-lg leading-relaxed max-w-xl">
        Create brutal anime tattoo concepts, biomechanical horrors, gothic cyber girls,
        matrix demons, and hyper detailed underground visuals with an AI interface
        inspired by deathcore aesthetics and H.R. Giger textures.
      </p>

      <div className="flex flex-wrap gap-4 mt-10">
        <button className="px-7 py-4 rounded-2xl bg-red-600 hover:bg-red-500 transition-all duration-300 uppercase tracking-[0.2em] font-bold shadow-[0_0_30px_rgba(255,0,0,0.5)]">
          Start Generating
        </button>

        <button className="px-7 py-4 rounded-2xl border border-red-700/60 hover:border-red-500 hover:bg-red-900/20 transition-all duration-300 uppercase tracking-[0.2em] font-bold">
          Explore Gallery
        </button>
      </div>
    </div>

    {/* Generator UI */}
    <div className="relative">
      <div className="absolute inset-0 blur-3xl bg-red-700/20 rounded-full" />

      <div className="relative border border-red-900/50 bg-zinc-950/80 backdrop-blur-xl rounded-[32px] p-6 shadow-[0_0_50px_rgba(255,0,0,0.15)]">
        <div className="flex items-center justify-between mb-6">
          <div>
            <h3 className="text-2xl font-black uppercase tracking-wider text-red-400">
              Image Generator
            </h3>
            <p className="text-zinc-500 text-sm mt-1">
              Prompt driven visual engine
            </p>
          </div>

          <div className="h-3 w-3 rounded-full bg-red-500 animate-pulse" />
        </div>

        <textarea
          placeholder="Describe your nightmare...\n\nExample: biomechanical anime priestess with transparent skull, cyber tribal tattoos, red chrome armor, matrix symbols, gothic cathedral flesh textures"
          className="w-full h-48 bg-black/60 border border-red-900/40 rounded-2xl p-5 resize-none text-zinc-200 placeholder:text-zinc-600 focus:outline-none focus:border-red-500 transition-all duration-300"
        />

        <div className="grid grid-cols-2 gap-4 mt-5">
          <select className="bg-black/60 border border-red-900/40 rounded-xl p-4 text-zinc-300 focus:outline-none focus:border-red-500">
            <option>Anime Gore</option>
            <option>Cyber Tribal</option>
            <option>Biomechanical</option>
            <option>Dark Fantasy</option>
            <option>Y2K Matrix</option>
          </select>

          <select className="bg-black/60 border border-red-900/40 rounded-xl p-4 text-zinc-300 focus:outline-none focus:border-red-500">
            <option>1024x1024</option>
            <option>Portrait</option>
            <option>Tattoo Stencil</option>
            <option>Album Cover</option>
          </select>
        </div>

        <button className="mt-6 w-full py-5 rounded-2xl bg-red-600 hover:bg-red-500 transition-all duration-300 uppercase tracking-[0.3em] font-black text-lg shadow-[0_0_30px_rgba(255,0,0,0.45)]">
          Generate Image
        </button>

        {/* Fake Preview */}
        <div className="mt-8 border border-red-900/40 rounded-3xl overflow-hidden bg-black/70">
          <div className="aspect-square relative bg-[radial-gradient(circle_at_center,rgba(120,0,0,0.5),black)] flex items-center justify-center">
            <div className="absolute inset-0 opacity-20 bg-[url('https://images.unsplash.com/photo-1518770660439-4636190af475?q=80&w=1200&auto=format&fit=crop')] bg-cover bg-center" />

            <div className="relative z-10 text-center px-8">
              <p className="uppercase tracking-[0.4em] text-red-400 text-sm mb-4">
                Preview Output
              </p>

              <h4 className="text-3xl font-black uppercase leading-tight">
                Cyber Flesh Oracle
              </h4>

              <p className="text-zinc-500 mt-4 text-sm leading-relaxed">
                Generated visuals appear here after processing prompts.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  {/* Features */}
  <section className="relative z-10 max-w-7xl mx-auto px-6 pb-24">
    <div className="grid md:grid-cols-3 gap-6">
      {[
        {
          title: 'Tattoo Ready',
          text: 'Generate linework adapted for real skin and stencil conversion.',
        },
        {
          title: 'Anime Horror',
          text: 'Blend cyberpunk, gothic anime, biomechanical textures and gore.',
        },
        {
          title: 'Github Deploy',
          text: 'Perfect starter interface for Vercel, Github Pages or React apps.',
        },
      ].map((item, index) => (
        <div
          key={index}
          className="border border-red-900/40 bg-zinc-950/70 rounded-3xl p-7 hover:border-red-500/60 transition-all duration-300"
        >
          <div className="w-14 h-14 rounded-2xl bg-red-900/20 border border-red-800/40 flex items-center justify-center mb-5 text-red-400 font-black text-xl">
            0{index + 1}
          </div>

          <h3 className="text-2xl font-black uppercase mb-3 text-red-300">
            {item.title}
          </h3>

          <p className="text-zinc-500 leading-relaxed">
            {item.text}
          </p>
        </div>
      ))}
    </div>
  </section>

  {/* Footer */}
  <footer className="relative z-10 border-t border-red-900/30 py-8 text-center text-zinc-600 uppercase tracking-[0.2em] text-xs">
    MeatCore AI • Built for underground visual culture
  </footer>
</div>

) }
