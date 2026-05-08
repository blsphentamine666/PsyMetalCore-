# PsyMetalCore-
export default function AnimeTattooAIGenerator() { const styles = [ "Cyber Tribal", "Dark Anime", "Y2K Gothic", "Biomechanical", "Neo Tokyo", "Blackwork", "Magical Hacker", "Gore Princess", ];

const placements = [ "Forearm", "Leg", "Back", "Hand", "Neck", "Chest", "Sleeve", ];

return ( <div className="min-h-screen bg-black text-white p-6"> <div className="max-w-5xl mx-auto"> <div className="mb-8"> <h1 className="text-5xl font-bold tracking-tight mb-2"> PSYCORE Tattoo AI </h1> <p className="text-zinc-400 text-lg"> Generador IA de tattoos anime cyber góticos. </p> </div>

<div className="grid md:grid-cols-2 gap-6">
      <div className="bg-zinc-900 rounded-3xl p-6 shadow-2xl border border-zinc-800">
        <h2 className="text-2xl font-semibold mb-4">
          Crear diseño
        </h2>

        <div className="space-y-4">
          <div>
            <label className="block mb-2 text-sm text-zinc-400">
              Concepto principal
            </label>
            <textarea
              placeholder="anime girl, cyber tribal armor, red neon eyes, gothic tattoo..."
              className="w-full h-32 rounded-2xl bg-zinc-950 border border-zinc-700 p-4 resize-none"
            />
          </div>

          <div>
            <label className="block mb-2 text-sm text-zinc-400">
              Estilo
            </label>
            <div className="grid grid-cols-2 gap-2">
              {styles.map((style) => (
                <button
                  key={style}
                  className="rounded-2xl border border-zinc-700 bg-zinc-950 p-3 hover:bg-zinc-800 transition"
                >
                  {style}
                </button>
              ))}
            </div>
          </div>

          <div>
            <label className="block mb-2 text-sm text-zinc-400">
              Zona del cuerpo
            </label>
            <div className="flex flex-wrap gap-2">
              {placements.map((place) => (
                <button
                  key={place}
                  className="px-4 py-2 rounded-full bg-zinc-950 border border-zinc-700 hover:bg-zinc-800 transition"
                >
                  {place}
                </button>
              ))}
            </div>
          </div>

          <div>
            <label className="block mb-2 text-sm text-zinc-400">
              Nivel de detalle
            </label>
            <input type="range" className="w-full" />
          </div>

          <button className="w-full mt-4 rounded-2xl py-4 text-lg font-semibold bg-white text-black hover:scale-[1.01] transition">
            Generar Tattoo
          </button>
        </div>
      </div>

      <div className="bg-zinc-900 rounded-3xl p-6 border border-zinc-800 flex flex-col">
        <div className="flex items-center justify-between mb-4">
          <h2 className="text-2xl font-semibold">
            Resultado IA
          </h2>
          <div className="text-sm text-zinc-500">
            SDXL + LoRA
          </div>
        </div>

        <div className="flex-1 rounded-3xl border border-dashed border-zinc-700 flex items-center justify-center bg-zinc-950 overflow-hidden min-h-[500px]">
          <div className="text-center px-8">
            <div className="text-6xl mb-4">⛧</div>
            <p className="text-zinc-400 text-lg">
              Aquí aparecerá tu diseño anime tattoo generado por IA.
            </p>
          </div>
        </div>

        <div className="grid grid-cols-2 gap-3 mt-4">
          <button className="rounded-2xl border border-zinc-700 py-3 hover:bg-zinc-800 transition">
            Exportar PNG
          </button>
          <button className="rounded-2xl border border-zinc-700 py-3 hover:bg-zinc-800 transition">
            Crear Stencil
          </button>
        </div>
      </div>
    </div>

    <div className="mt-8 grid md:grid-cols-3 gap-4">
      <div className="bg-zinc-900 rounded-3xl p-5 border border-zinc-800">
        <h3 className="text-xl font-semibold mb-2">
          Anime Dark
        </h3>
        <p className="text-zinc-400 text-sm">
          Diseños inspirados en anime gótico, Y2K y horror japonés.
        </p>
      </div>

      <div className="bg-zinc-900 rounded-3xl p-5 border border-zinc-800">
        <h3 className="text-xl font-semibold mb-2">
          Cyber Tribal
        </h3>
        <p className="text-zinc-400 text-sm">
          Mezcla biomecánica, tribal futurista y neón cyberweb.
        </p>
      </div>

      <div className="bg-zinc-900 rounded-3xl p-5 border border-zinc-800">
        <h3 className="text-xl font-semibold mb-2">
          Tattoo Ready
        </h3>
        <p className="text-zinc-400 text-sm">
          Composición adaptada para tatuajes reales y stencil.
        </p>
      </div>
    </div>
  </div>
</div>

); }
