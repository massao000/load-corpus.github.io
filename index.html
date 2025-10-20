import React, { useState, useEffect, useRef } from "react";

export default function ITACorpusViewer() {
  const [rows, setRows] = useState([]);
  const [index, setIndex] = useState(0);
  const fileInputRef = useRef(null);

  useEffect(() => {
    function onKey(e) {
      if (e.key === "ArrowRight") next();
      if (e.key === "ArrowLeft") prev();
    }
    window.addEventListener("keydown", onKey);
    return () => window.removeEventListener("keydown", onKey);
  }, [rows, index]);

  useEffect(() => {
    const example = `春の訪れを告げる鳥たちのさえずりは、希望に満ちている.,春<はる>の訪<おとず>れを告<つ>げる鳥<とり>たちのさえずりは、希望<きぼう>に満<み>ちている.,ハルノオトズレヲツゲルトリタチノサエズリハ、キボウニミチテイル.,\n夜の静けさに響く足音が、だれもいないはずの家から聞こえた.,夜<よる>の静<しず>けさに響<ひび>く足音<あしおと>が、だれもいないはずの家から聞こえた.,ヨルノシズケサニヒビクアシオトガ、ダレモイナイハズノイエカラキコエタ。,.`;
    const parsed = parseCSV(example);
    setRows(parsed.filter(r => r.length >= 3));
    setIndex(0);
  }, []);

  function parseCSV(text) {
    const lines = [];
    let cur = [];
    let field = "";
    let inQuotes = false;
    for (let i = 0; i < text.length; i++) {
      const ch = text[i];
      const next = text[i + 1];
      if (ch === '"') {
        if (inQuotes && next === '"') {
          field += '"';
          i++;
        } else {
          inQuotes = !inQuotes;
        }
      } else if (ch === ',' && !inQuotes) {
        cur.push(field);
        field = "";
      } else if ((ch === '\n' || ch === '\r') && !inQuotes) {
        if (ch === '\r' && text[i + 1] === '\n') continue;
        if (field !== '' || cur.length > 0) {
          cur.push(field);
          lines.push(cur);
        }
        cur = [];
        field = "";
      } else {
        field += ch;
      }
    }
    if (field !== '' || cur.length > 0) {
      cur.push(field);
      lines.push(cur);
    }
    return lines;
  }

  function handleFile(e) {
    const file = e.target.files?.[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = ev => {
      const text = ev.target.result;
      const parsed = parseCSV(text);
      const filtered = parsed.filter(r => r.length >= 3);
      setRows(filtered);
      setIndex(0);
    };
    reader.readAsText(file, "utf-8");
  }

  function annotatedToRubyHtml(annotated) {
    if (!annotated) return "";
    const escape = s => String(s)
      .replace(/&/g, "&amp;")
      .replace(/</g, "&lt;")
      .replace(/>/g, "&gt;")
      .replace(/＜/g, "&lt;")
      .replace(/＞/g, "&gt;");

    let out = "";
    let i = 0;
    while (i < annotated.length) {
      const ltHalf = annotated.indexOf("<", i);
      const ltFull = annotated.indexOf("＜", i);
      let lt = -1;
      let isFull = false;
      if (ltHalf === -1) lt = ltFull, isFull = ltFull !== -1;
      else if (ltFull === -1) lt = ltHalf, isFull = false;
      else if (ltHalf < ltFull) lt = ltHalf, isFull = false;
      else lt = ltFull, isFull = true;

      if (lt === -1) {
        out += escape(annotated.slice(i));
        break;
      }

      const gtChar = isFull ? '＞' : '>';
      const gt = annotated.indexOf(gtChar, lt);
      if (gt === -1) {
        out += escape(annotated.slice(i));
        break;
      }

      let baseStart = lt - 1;
      if (baseStart < 0) baseStart = 0;

      while (baseStart - 1 >= 0) {
        const prev = annotated[baseStart - 1];
        if (/[一-龯]/.test(prev)) {
          baseStart--;
        } else {
          break;
        }
      }

      const base = annotated.slice(baseStart, lt);
      const rubyText = annotated.slice(lt + 1, gt);

      out += escape(annotated.slice(i, baseStart));
      out += `<ruby>${escape(base)}<rt>${escape(rubyText)}</rt></ruby>`;
      i = gt + 1;
    }
    return out;
  }

  function next() {
    if (rows.length === 0) return;
    setIndex((idx) => Math.min(rows.length - 1, idx + 1));
  }
  function prev() {
    if (rows.length === 0) return;
    setIndex((idx) => Math.max(0, idx - 1));
  }

  const current = rows[index] || ["", "", ""];
  const main = current[0] || "";
  const annotated = current[1] || "";
  const katakana = current[2] || "";

  return (
    <div className="min-h-screen bg-gray-50 flex flex-col items-center p-6">
      <div className="w-full max-w-3xl bg-white rounded-2xl shadow-lg p-6 mb-2">
        <h1 className="text-2xl font-semibold mb-4">ITAコーパス 文ビューワ</h1>

        <div className="flex gap-3 items-center mb-4">
          <input
            ref={fileInputRef}
            type="file"
            accept=".csv,text/csv"
            onChange={handleFile}
            className=""
          />
          <button
            onClick={() => { if (fileInputRef.current) fileInputRef.current.click(); }}
            className="px-3 py-1 rounded bg-indigo-600 text-white"
          >
            CSVをアップロード
          </button>
          <div className="ml-auto text-sm text-gray-500">{rows.length} 件読み込み</div>
        </div>

        <div className="border rounded p-6 mb-12">
          <div className="text-lg leading-relaxed" style={{ fontSize: '1.6rem' }}>
            <div dangerouslySetInnerHTML={{ __html: annotatedToRubyHtml(annotated || main) }} />
          </div>
          <div className="mt-2 text-xs text-gray-500" style={{ fontSize: '0.9rem' }}>
            {katakana}
          </div>
        </div>
      </div>

      <div className="fixed bottom-0 left-0 right-0 w-full bg-white shadow p-4 flex items-center justify-between">
        <div className="flex gap-2">
          <button onClick={prev} className="px-4 py-2 rounded bg-gray-200">◀ 前へ</button>
          <button onClick={next} className="px-4 py-2 rounded bg-gray-200">次へ ▶</button>
        </div>
        <div className="text-sm text-gray-600">{rows.length ? `${index + 1} / ${rows.length}` : "0 件"}</div>
      </div>

      <div className="mt-4 text-xs text-gray-500 max-w-3xl text-center">
        {"ヒント: ← / → キーでも切替できます。CSVは1列目=本文、2列目=ルビ付き（例: 春<はる>よ来<こ>い）、3列目=カタカナの順にしてください。"}
      </div>
    </div>
  );
}