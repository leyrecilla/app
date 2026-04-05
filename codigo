import { useState, useRef, useEffect } from "react";

const Ic = ({ p, s = 16, sw = 1.6, fill = "none", stroke = "currentColor" }) => (
  <svg width={s} height={s} viewBox="0 0 24 24" fill={fill} stroke={stroke}
    strokeWidth={sw} strokeLinecap="round" strokeLinejoin="round" style={{ flexShrink: 0 }}>
    <path d={p} />
  </svg>
);
const I = {
  folder:    "M3 7a2 2 0 0 1 2-2h3.17a2 2 0 0 1 1.42.59l1.41 1.41H19a2 2 0 0 1 2 2v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V7z",
  folderPlus:"M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h5l2 3h9a2 2 0 0 1 2 2zM12 11v6M9 14h6",
  plus:      "M12 5v14M5 12h14",
  sparkle:   "M9.663 17h4.673M12 3v1m6.364 1.636-.707.707M21 12h-1M17.657 17.657l-.707.707M12 21v-1m-5.657-1.636.707-.707M4 12H3m3.343-5.657-.707-.707M12 8a4 4 0 1 0 0 8 4 4 0 0 0 0-8z",
  wand:      "M15 4V2m0 14v-2M8 9H2m14 0h-2M13.8 13.8l1.4 1.4M13.8 4.2l1.4-1.4M3.2 13.8l1.4-1.4M3.2 4.2 4.6 5.6M12 9a3 3 0 1 1-6 0 3 3 0 0 1 6 0zM19 15l-7 7",
  copy:      "M9 5H7a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7a2 2 0 0 0-2-2h-2M9 5a2 2 0 0 1 2-2h2a2 2 0 0 1 2 2M9 5a2 2 0 0 0 2 2h2a2 2 0 0 0 2-2",
  check:     "M20 6 9 17l-5-5",
  x:         "M18 6 6 18M6 6l12 12",
  edit:      "M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7m-1.414-9.414a2 2 0 1 1 2.828 2.828L11.828 15H9v-2.828l8.586-8.586z",
  trash:     "M3 6h18m-2 0v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a1 1 0 0 1 1-1h4a1 1 0 0 1 1 1v2",
  star:      "M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z",
  search:    "M21 21l-4.35-4.35M17 11A6 6 0 1 1 5 11a6 6 0 0 1 12 0z",
  grid:      "M3 3h7v7H3zM14 3h7v7h-7zM14 14h7v7h-7zM3 14h7v7H3z",
  list:      "M8 6h13M8 12h13M8 18h13M3 6h.01M3 12h.01M3 18h.01",
  info:      "M12 16v-4M12 8h.01M22 12A10 10 0 1 1 2 12a10 10 0 0 1 20 0z",
  pkg:       "M21 16V8a2 2 0 0 0-1-1.73l-7-4a2 2 0 0 0-2 0l-7 4A2 2 0 0 0 3 8v8a2 2 0 0 0 1 1.73l7 4a2 2 0 0 0 2 0l7-4A2 2 0 0 0 21 16z",
  similar:   "M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2M9 7a4 4 0 1 0 0-8 4 4 0 0 0 0 8zM23 21v-2a4 4 0 0 0-3-3.87M16 3.13a4 4 0 0 1 0 7.75",
};

const AI_MODELS = [
  { id: "claude",  label: "Claude",  color: "#c9854a" },
  { id: "gpt4",    label: "GPT-4",   color: "#10a37f" },
  { id: "gemini",  label: "Gemini",  color: "#4285f4" },
  { id: "llama",   label: "Llama",   color: "#5577ff" },
  { id: "mistral", label: "Mistral", color: "#f5825a" },
  { id: "general", label: "General", color: "#8a8a6a" },
];

const DEFAULT_FOLDERS = [
  { id: "f1", name: "Escritura",     emoji: "✍️", color: "#7eb8a4" },
  { id: "f2", name: "Código",        emoji: "💻", color: "#7a9cc4" },
  { id: "f3", name: "Análisis",      emoji: "🔍", color: "#b08fce" },
  { id: "f4", name: "Creativo",      emoji: "🎨", color: "#d4856a" },
  { id: "f5", name: "Negocios",      emoji: "💼", color: "#c4a96e" },
  { id: "f6", name: "Investigación", emoji: "📚", color: "#8eb87a" },
];

const INIT_PROMPTS = [
  { id: 1, folderId: "f3", title: "Análisis Crítico de Texto", model: "claude", starred: true, uses: 47, created: "2024-03-10",
    description: "Evalúa textos complejos desde múltiples perspectivas, identificando argumentos, falacias y valor retórico.",
    tags: ["análisis","literatura","crítica"],
    content: "Analiza el siguiente texto desde múltiples perspectivas:\n\n{{TEXTO}}\n\nProporciona:\n1. Argumento central y tesis principal\n2. Técnicas retóricas empleadas\n3. Puntos fuertes y débiles\n4. Contexto: {{CONTEXTO}}\n5. Evaluación crítica fundamentada",
  },
  { id: 2, folderId: "f2", title: "Refactoring de Código", model: "gpt4", starred: false, uses: 132, created: "2024-02-28",
    description: "Transforma código legacy en código limpio y mantenible aplicando principios SOLID.",
    tags: ["refactoring","SOLID","clean code"],
    content: "Actúa como senior developer experto en {{LENGUAJE}}.\n\nRevisa este código:\n```\n{{CÓDIGO}}\n```\n\nObjetivo: {{OBJETIVO}}\n\nAplica principios SOLID, manejo de errores y documentación.",
  },
  { id: 3, folderId: "f1", title: "Artículo de Blog SEO", model: "claude", starred: true, uses: 89, created: "2024-03-15",
    description: "Genera artículos optimizados para SEO con estructura narrativa persuasiva y CTAs efectivos.",
    tags: ["blog","SEO","copywriting"],
    content: "Escribe un artículo de {{PALABRAS}} palabras sobre:\n\nTema: {{TEMA}}\nAudiencia: {{AUDIENCIA}}\nTono: {{TONO}}\n\n- Título con keyword\n- Intro gancho en 3 líneas\n- 5 secciones H2\n- CTA al final",
  },
  { id: 4, folderId: "f4", title: "Brainstorming SCAMPER", model: "gemini", starred: false, uses: 23, created: "2024-03-20",
    description: "Genera ideas innovadoras usando SCAMPER combinado con pensamiento lateral.",
    tags: ["ideas","innovación","SCAMPER"],
    content: "Genera ideas para {{PROYECTO}} usando SCAMPER.\n\nContexto: {{CONTEXTO}}\nRestricciones: {{RESTRICCIONES}}\n\nS-Sustituir, C-Combinar, A-Adaptar, M-Modificar, P-Proponer, E-Eliminar, R-Reordenar\n\n2 ideas por letra con impacto y viabilidad.",
  },
  { id: 5, folderId: "f5", title: "Resumen Ejecutivo", model: "claude", starred: true, uses: 61, created: "2024-03-05",
    description: "Condensa documentos complejos en resúmenes de una página para directivos.",
    tags: ["ejecutivo","directivos","estrategia"],
    content: "Crea un resumen ejecutivo de:\n\n{{DOCUMENTO}}\n\nDestinatario: {{DESTINATARIO}}\n\nIncluye: objetivo (2 oraciones), hallazgos clave (5 bullets), recomendaciones accionables y próximos pasos.\n\nMáx. 1 página, tono formal.",
  },
  { id: 6, folderId: "f6", title: "Revisión Bibliográfica", model: "gpt4", starred: false, uses: 38, created: "2024-03-18",
    description: "Estructura revisiones científicas identificando corrientes teóricas y tendencias.",
    tags: ["academia","bibliografía","APA"],
    content: "Revisión bibliográfica sobre:\n\nTema: {{TEMA}}\nPeríodo: {{PERÍODO}}\nBases: {{BASES_DE_DATOS}}\n\n1. Estado del arte\n2. Corrientes teóricas\n3. Metodologías\n4. Gaps de investigación\n5. Tendencias emergentes\n6. Referencias APA 7",
  },
];

const uid  = () => Math.random().toString(36).slice(2, 10);
const getVars = (text) => [...new Set((text.match(/\{\{([^}]+)\}\}/g) || []).map(m => m.replace(/\{\{|\}\}/g, "")))];
const modelOf = (id) => AI_MODELS.find(m => m.id === id) || AI_MODELS[5];

async function callClaude(messages, system = "") {
  const body = { model: "claude-sonnet-4-20250514", max_tokens: 1000, messages };
  if (system) body.system = system;
  const r = await fetch("https://api.anthropic.com/v1/messages", {
    method: "POST", headers: { "Content-Type": "application/json" },
    body: JSON.stringify(body),
  });
  const d = await r.json();
  return d.content?.map(b => b.text || "").join("") || "";
}

// ─── STYLES ───────────────────────────────────────────────
const S = {
  lbl: { display: "block", color: "#5a5032", fontSize: 10, fontWeight: 800,
    letterSpacing: "0.12em", textTransform: "uppercase", marginBottom: 6 },
  sel: { width: "100%", background: "#15120a", border: "1px solid #2a2212",
    borderRadius: 8, color: "#c8b870", padding: "9px 12px", fontSize: 12,
    cursor: "pointer", outline: "none", fontFamily: "inherit" },
  inp: { width: "100%", background: "#15120a", border: "1px solid #2a2212",
    borderRadius: 8, color: "#e0d4b8", padding: "9px 12px", fontSize: 13,
    outline: "none", fontFamily: "inherit", lineHeight: 1.65, boxSizing: "border-box" },
};

// ─── ATOMS ────────────────────────────────────────────────
const Tag = ({ children, color = "#7a6a42" }) => (
  <span style={{ padding: "2px 9px", borderRadius: 20, fontSize: 10, fontWeight: 700,
    letterSpacing: "0.05em", textTransform: "uppercase",
    background: color + "22", color, border: `1px solid ${color}44` }}>
    {children}
  </span>
);

const Spin = ({ size = 14 }) => (
  <span style={{ width: size, height: size, border: `2px solid #3a3020`,
    borderTop: `2px solid #d4a853`, borderRadius: "50%",
    display: "inline-block", animation: "spin .6s linear infinite", flexShrink: 0 }} />
);

// ─── MODAL SHELL ──────────────────────────────────────────
function Modal({ title, subtitle, onClose, children, width = 580 }) {
  return (
    <div style={{ position: "fixed", inset: 0, zIndex: 300, background: "rgba(8,6,2,.9)",
      backdropFilter: "blur(6px)", display: "flex", alignItems: "center", justifyContent: "center", padding: 16 }}>
      <div style={{ width, maxWidth: "100%", maxHeight: "92vh", display: "flex", flexDirection: "column",
        background: "#1a1610", border: "1px solid #352e1c", borderRadius: 16,
        boxShadow: "0 32px 80px rgba(0,0,0,.75)" }}>
        <div style={{ padding: "18px 22px", borderBottom: "1px solid #2a2212",
          display: "flex", justifyContent: "space-between", alignItems: "flex-start", flexShrink: 0 }}>
          <div>
            <div style={{ color: "#e8d8b0", fontSize: 16, fontWeight: 800 }}>{title}</div>
            {subtitle && <div style={{ color: "#5a5038", fontSize: 12, marginTop: 2, maxWidth: 420 }}>{subtitle}</div>}
          </div>
          <button onClick={onClose} style={{ background: "none", border: "none", cursor: "pointer",
            color: "#5a5038", padding: 4, borderRadius: 6, marginTop: 2 }}>
            <Ic p={I.x} s={16} />
          </button>
        </div>
        <div style={{ flex: 1, overflow: "auto", padding: "20px 22px" }}>{children}</div>
      </div>
    </div>
  );
}

// ─── FOLDER MODAL ─────────────────────────────────────────
function FolderModal({ folder, onClose, onSave }) {
  const EMOJIS = ["📁","✍️","💻","🔍","🎨","💼","📚","🚀","🔬","🎯","💡","🌐","📊","🎓","⚡","🔧","🌿","🎵","📝","🏆","🧠","💎"];
  const COLORS = ["#7eb8a4","#7a9cc4","#b08fce","#d4856a","#c4a96e","#8eb87a","#c06080","#60a0c0","#d4a853","#a87050","#6080a0","#a06080"];
  const [name,  setName]  = useState(folder?.name  || "");
  const [emoji, setEmoji] = useState(folder?.emoji || "📁");
  const [color, setColor] = useState(folder?.color || "#7eb8a4");

  return (
    <Modal title={folder ? "Editar carpeta" : "Nueva carpeta"} onClose={onClose} width={420}>
      <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
        <div>
          <label style={S.lbl}>Nombre</label>
          <input value={name} onChange={e => setName(e.target.value)} placeholder="Nombre de la carpeta…" style={S.inp} />
        </div>
        <div>
          <label style={S.lbl}>Emoji</label>
          <div style={{ display: "flex", flexWrap: "wrap", gap: 5, marginTop: 5 }}>
            {EMOJIS.map(e => (
              <button key={e} onClick={() => setEmoji(e)} style={{
                width: 36, height: 36, borderRadius: 8,
                border: `2px solid ${emoji === e ? color : "#2a2212"}`,
                background: emoji === e ? color + "22" : "#15120a",
                cursor: "pointer", fontSize: 17,
              }}>{e}</button>
            ))}
          </div>
        </div>
        <div>
          <label style={S.lbl}>Color</label>
          <div style={{ display: "flex", gap: 6, marginTop: 5, flexWrap: "wrap" }}>
            {COLORS.map(c => (
              <button key={c} onClick={() => setColor(c)} style={{
                width: 26, height: 26, borderRadius: "50%", background: c,
                border: `3px solid ${color === c ? "#e8d8b0" : "transparent"}`,
                cursor: "pointer",
              }} />
            ))}
          </div>
        </div>
        {/* preview */}
        <div style={{ background: "#12100a", border: "1px solid #2a2212", borderRadius: 10, padding: "12px 16px",
          display: "flex", alignItems: "center", gap: 10 }}>
          <span style={{ fontSize: 24 }}>{emoji}</span>
          <div style={{ color: color, fontWeight: 700, fontSize: 14 }}>{name || "Nombre de la carpeta"}</div>
        </div>
        <div style={{ display: "flex", gap: 8 }}>
          <button onClick={() => { if (name.trim()) onSave({ name: name.trim(), emoji, color }); }}
            style={{ flex: 1, padding: "10px", background: "#d4a853", color: "#1a1108",
              border: "none", borderRadius: 9, cursor: "pointer", fontWeight: 800, fontSize: 13, fontFamily: "inherit" }}>
            {folder ? "Guardar cambios" : "Crear carpeta"}
          </button>
          <button onClick={onClose} style={{ padding: "10px 16px", background: "transparent", color: "#5a5032",
            border: "1px solid #2a2212", borderRadius: 9, cursor: "pointer", fontSize: 13, fontFamily: "inherit" }}>
            Cancelar
          </button>
        </div>
      </div>
    </Modal>
  );
}

// ─── EDIT MODAL ───────────────────────────────────────────
function EditModal({ prompt, folders, onClose, onSave }) {
  const [f, setF] = useState(prompt || {
    title: "", description: "", folderId: folders[0]?.id || "",
    model: "claude", content: "", tags: [], starred: false,
  });
  const [tagIn, setTagIn] = useState("");
  const [improving, setImp] = useState(false);
  const set = (k, v) => setF(p => ({ ...p, [k]: v }));

  const addTag = () => {
    const t = tagIn.trim().toLowerCase();
    if (t && !f.tags.includes(t)) set("tags", [...f.tags, t]);
    setTagIn("");
  };

  const improve = async () => {
    if (!f.content) return;
    setImp(true);
    const res = await callClaude([{ role: "user", content:
      `Mejora este prompt de IA para ${modelOf(f.model).label}. Hazlo más específico, estructurado y efectivo. Mantén variables {{VARIABLE}} existentes. Devuelve SOLO el prompt mejorado sin explicaciones:\n\n${f.content}` }]);
    if (res) set("content", res.trim());
    setImp(false);
  };

  const v = getVars(f.content);

  return (
    <Modal title={prompt ? "Editar prompt" : "Nuevo prompt"} onClose={onClose} width={590}>
      <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
        <div>
          <label style={S.lbl}>Título</label>
          <input value={f.title} onChange={e => set("title", e.target.value)} placeholder="Nombre descriptivo…" style={S.inp} />
        </div>
        <div>
          <label style={S.lbl}>Descripción <span style={{ color: "#3a3018", fontWeight: 400 }}>(para la IA y para ti)</span></label>
          <textarea value={f.description} onChange={e => set("description", e.target.value)} rows={2}
            placeholder="¿Para qué sirve? ¿Quién lo usa? ¿Qué produce?"
            style={{ ...S.inp, resize: "vertical" }} />
        </div>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 10 }}>
          <div>
            <label style={S.lbl}>Carpeta</label>
            <select value={f.folderId} onChange={e => set("folderId", e.target.value)} style={S.sel}>
              {folders.map(fo => <option key={fo.id} value={fo.id}>{fo.emoji} {fo.name}</option>)}
            </select>
          </div>
          <div>
            <label style={S.lbl}>Modelo objetivo</label>
            <select value={f.model} onChange={e => set("model", e.target.value)} style={S.sel}>
              {AI_MODELS.map(m => <option key={m.id} value={m.id}>{m.label}</option>)}
            </select>
          </div>
        </div>
        <div>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 6 }}>
            <label style={{ ...S.lbl, marginBottom: 0 }}>
              Contenido {v.length > 0 && <span style={{ color: "#b08fce" }}>· {v.length} variables</span>}
            </label>
            <button onClick={improve} disabled={!f.content || improving}
              style={{ display: "flex", alignItems: "center", gap: 5, padding: "4px 10px",
                background: improving ? "#1a1810" : "#7b4db522", color: improving ? "#4a4040" : "#a887d4",
                border: `1px solid ${improving ? "#2a2020" : "#7b4db544"}`, borderRadius: 6,
                cursor: improving ? "wait" : "pointer", fontSize: 11, fontWeight: 700, fontFamily: "inherit" }}>
              {improving ? <Spin size={11} /> : <Ic p={I.wand} s={12} stroke="#a887d4" />}
              {improving ? "Mejorando…" : "Mejorar con IA"}
            </button>
          </div>
          <textarea value={f.content} onChange={e => set("content", e.target.value)} rows={7}
            placeholder={"Escribe el prompt. Usa {{VARIABLE}} para partes personalizables.\n\nEj: Actúa como experto en {{ÁREA}}. Analiza {{TEXTO}}..."}
            style={{ ...S.inp, resize: "vertical", fontFamily: "'JetBrains Mono', monospace", fontSize: 12 }} />
        </div>
        <div>
          <label style={S.lbl}>Etiquetas</label>
          <div style={{ display: "flex", flexWrap: "wrap", gap: 5, marginBottom: 6 }}>
            {f.tags.map(t => (
              <span key={t} style={{ display: "flex", alignItems: "center", gap: 4,
                padding: "3px 9px", background: "#221d10", borderRadius: 20, color: "#b8a870", fontSize: 11 }}>
                #{t}
                <button onClick={() => set("tags", f.tags.filter(x => x !== t))}
                  style={{ background: "none", border: "none", cursor: "pointer", color: "#5a4a28", lineHeight: 1, padding: 0, fontSize: 13 }}>×</button>
              </span>
            ))}
          </div>
          <div style={{ display: "flex", gap: 8 }}>
            <input value={tagIn} onChange={e => setTagIn(e.target.value)}
              onKeyDown={e => { if (e.key === "Enter") { e.preventDefault(); addTag(); }}}
              placeholder="Añadir etiqueta y pulsar Enter…" style={{ ...S.inp, flex: 1 }} />
            <button onClick={addTag} style={{ padding: "9px 14px", background: "#221d10", border: "1px solid #2a2212",
              borderRadius: 8, color: "#c8b870", cursor: "pointer", fontSize: 14, fontFamily: "inherit" }}>+</button>
          </div>
        </div>
        <div style={{ borderTop: "1px solid #2a2212", paddingTop: 14, display: "flex", gap: 8 }}>
          <button onClick={() => { if (f.title && f.content) onSave(f); }}
            style={{ flex: 1, padding: "11px", background: "#d4a853", color: "#1a1108",
              border: "none", borderRadius: 9, cursor: "pointer", fontWeight: 800, fontSize: 13, fontFamily: "inherit" }}>
            {prompt ? "Guardar cambios" : "Crear prompt"}
          </button>
          <button onClick={onClose} style={{ padding: "11px 18px", background: "transparent", color: "#5a5032",
            border: "1px solid #2a2212", borderRadius: 9, cursor: "pointer", fontSize: 13, fontFamily: "inherit" }}>
            Cancelar
          </button>
        </div>
      </div>
    </Modal>
  );
}

// ─── CREATE FROM DESCRIPTION ──────────────────────────────
function CreateDescModal({ folders, onClose, onCreate }) {
  const [desc,     setDesc]    = useState("");
  const [folderId, setFId]     = useState(folders[0]?.id || "");
  const [model,    setModel]   = useState("claude");
  const [loading,  setLoading] = useState(false);
  const [preview,  setPreview] = useState(null);
  const [step,     setStep]    = useState(1);

  const generate = async () => {
    if (!desc.trim()) return;
    setLoading(true);
    try {
      const raw = await callClaude([{ role: "user", content:
        `Genera un prompt profesional de IA basado en esta descripción: "${desc}"\n\nDevuelve SOLO JSON válido sin markdown:\n{"title":"título del prompt","description":"descripción del caso de uso en 1-2 oraciones","content":"el prompt completo con variables {{VARIABLE}} donde aplique","tags":["etiqueta1","etiqueta2","etiqueta3"]}\n\nEl content debe ser un prompt listo para usar, específico y con estructura clara.` }]);
      const clean = raw.replace(/```json|```/g, "").trim();
      setPreview(JSON.parse(clean));
      setStep(2);
    } catch {
      setPreview({ title: "Prompt generado", description: desc, content: desc, tags: ["general"] });
      setStep(2);
    }
    setLoading(false);
  };

  const accept = () => onCreate({
    ...preview, folderId, model,
    id: uid(), uses: 0, starred: false, created: new Date().toISOString().slice(0, 10),
  });

  return (
    <Modal title="Crear prompt con