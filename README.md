PsyMetalCore AI
import { useState } from "react"; import { Sparkles, Download, Wand2, Skull, Cpu, Flame, } from "lucide-react";

export default function MeatcoreTattooAI() { const [concept, setConcept] = useState(""); const [generatedPrompt, setGeneratedPrompt] = useState(""); const [isGenerating, setIsGenerating] = useState(false); const [selectedStyle, setSelectedStyle] = useState("Meatcore Giger"); const [selectedPlacement, setSelectedPlacement] = useState("Full Sleeve");

const styles = [ "Meatcore Giger", "Biomechanical Flesh", "Cyber Gore", "Necro Anime", "Blood Cathedral", "Chrome Horror", ];

const placements = [ "Full Sleeve", "Forearm", "Leg", "Back", "Chest", "Neck", ];

const generatePrompt = () => { setIsGenerating(true);

const prompt = `masterpiece, ${selectedStyle}, anime biomechanical tattoo, ${selectedPlacement} tattoo composition, ${concept}, hr giger inspired flesh textures, exposed tendons, cybernetic veins, dark organic tubes, blood red glow, black chrome biomechanical armor, gothic horror atmosphere, sharp tattoo linework, tattoo stencil readability, meatcore aesthetic, dark web horror, ultra detailed, high contrast, black background`;

setTimeout(() => {
  setGeneratedPrompt(prompt);
  setIsGenerating(false);
}, 1200);

};

return ( <div className="min-h-screen bg-black text-white overflow-hidden"> <div className="absolute inset-0 bg-[radial-gradient(circle_at_top,rgba(120,0,0,0.4),transparent_60%)]" />

<div className="relative z-10 max-w-7xl mx-auto px-6 py-10">
    <div className="mb-10 flex items-center justify-between border-b border-red-950 pb-6">
      <div>
        <div className="flex items-center gap-3 mb-3">
          <Skull className="text-red-600" size={38} />

          <h1 className="text-5xl md:text-7xl font-black tracking-tight">
            MEATCORE AI
          </h1>
        </div>

        <p className="text-zinc-500 text-lg max-w-2xl leading-relaxed">
          Generador IA de tattoos biomecánicos anime inspirado en
          horror industrial, H.R. Giger, carne sintética y estética
          cyber necromántica.
        </p>
      </div>

      <div className="hidden md:flex items-center gap-3 text-red-700">
        <Cpu />
        <Flame />
        <Wand2 />
      </div>
    </div>

    <div className="grid lg:grid-cols-2 gap-8">
      <div className="bg-zinc-950/70 backdrop-blur rounded-[32px] border border-red-950 p-6 shadow-2xl shadow-red-950/20">
        <div className="mb-6">
          <h2 className="text-3xl font-bold mb-2">
            Create Flesh Design
          </h2>

          <p className="text-zinc-500">
            Diseña tattoos biomecánicos anime listos para stencil.
          </p>
        </div>

        <div className="space-y-6">
          <div>
            <label className="block mb-2 text-sm text-zinc-500 uppercase tracking-[0.2em]">
              Main Concept
            </label>

            <textarea
              value={concept}
              onChange={(e) => setConcept(e.target.value)}
              placeholder="anime biomechanical queen, exposed flesh tubes, chrome skull halo, cyber veins, meat cathedral..."
              className="w-full h-40 rounded-3xl bg-black border border-red-950 p-5 resize-none focus:outline-none focus:border-red-700 transition"
            />
          </div>

          <div>
            <label className="block mb-3 text-sm text-zinc-500 uppercase tracking-[0.2em]">
              Style Mutation
            </label>

            <div className="grid grid-cols-2 gap-3">
              {styles.map((style) => (
                <button
                  key={style}
                  onClick={() => setSelectedStyle(style)}
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

          <div>
            <label className="block mb-3 text-sm text-zinc-500 uppercase tracking-[0.2em]">
              Body Placement
            </label>

            <div className="flex flex-wrap gap-3">
              {placements.map((placement) => (
                <button
                  key={placement}
                  onClick={() => setSelectedPlacement(placement)}
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

          <button
            onClick={generatePrompt}
            className="w-full py-5 rounded-3xl bg-gradient-to-r from-red-950 via-red-700 to-red-950 hover:scale-[1.01] transition-all duration-300 flex items-center justify-center gap-3 text-lg font-bold tracking-wide"
          >
            <Sparkles />
            {isGenerating ? "Mutating Flesh..." : "Generate Meatcore Tattoo"}
          </button>
        </div>
      </div>

      <div className="bg-zinc-950/70 backdrop-blur rounded-[32px] border border-red-950 p-6 shadow-2xl shadow-red-950/20 flex flex-col">
        <div className="flex items-center justify-between mb-5">
          <div>
            <h2 className="text-3xl font-bold">
              Neural Output
            </h2>

            <p className="text-zinc-500 text-sm mt-1">
              Flux + SDXL + Custom LoRA
            </p>
          </div>

          <div className="w-4 h-4 rounded-full bg-red-600 animate-pulse" />
        </div>

        <div className="flex-1 rounded-[32px] border border-red-950 bg-black overflow-hidden relative min-h-[580px]">
          <div className="absolute inset-0 opacity-20 bg-[radial-gradient(circle_at_center,rgba(255,0,0,0.25),transparent_70%)]" />

          <div className="relative h-full flex items-center justify-center p-8">
            {generatedPrompt ? (
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
                  Tu generación biomecánica aparecerá aquí. Diseños
                  preparados para tattoo anime, biomech horror y
                  estética meatcore.
                </p>
              </div>
            )}
          </div>
        </div>

        <div className="grid grid-cols-2 gap-4 mt-5">
          <button className="rounded-2xl border border-red-950 py-4 hover:bg-red-950/30 transition flex items-center justify-center gap-2">
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

    <div className="grid md:grid-cols-3 gap-6 mt-10">
      <div className="bg-zinc-950/70 rounded-[28px] border border-red-950 p-6">
        <div className="text-red-600 mb-4">
          <Skull size={32} />
        </div>

        <h3 className="text-2xl font-bold mb-3">
          Organic Horror
        </h3>

        <p className="text-zinc-500 leading-relaxed">
          Carne sintética, biomecánica visceral y horror industrial
          inspirado en H.R. Giger.
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
          Estética dark web, mutación digital y tecnología corrupta.
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
          Composición optimizada para stencil, sleeves y tatuajes
          reales de alto contraste.
        </p>
      </div>
    </div>
  </div>
</div>

); }
