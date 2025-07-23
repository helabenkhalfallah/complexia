# 📈 Complexia

> **ACM 2025 Publication**  
> _Complexia: Static Inference of Algorithmic Complexity and Resource Costs via JavaScript/TypeScript AST Analysis_  
> 📄 [ACM Publication Link – Coming Soon]

---

## ✨ Overview

**Complexia** is a formal and deterministic static analysis tool that estimates **algorithmic time complexity**, **memory allocation patterns**, and **approximate instruction counts** from JavaScript/TypeScript source code using AST traversal.

Designed for performance-aware development and pre-runtime feedback, Complexia translates raw source code into a reproducible **complexity signature** using structural program analysis.

The system computes:

- **Time Complexity (Big O)**: Detects O(1), O(n), O(n log n), O(n²), etc. via static pattern recognition.
- **Static Memory Estimation**: Infers allocation footprints from variable usage and data structures.
- **Instruction Count Estimation**: Converts AST-node cost heuristics into approximate op counts.
- **Code Block Profiling**: Identifies dominant functions, loops, and hotspots at dev time.

---

## 📥 Installation

```bash
npm install -D complexia
```

### Prerequisites

- Node.js ≥ 18.x
- TypeScript project or plain JS/TS files

---

## 🚦 CLI Usage

Run the tool with:

```bash
npx complexia analyze   --srcDir "./examples"   --outputDir "./reports"   --format html,json
```

### Supported formats:

- `html`: Human-readable performance dashboard
- `json`: Machine-readable output for pipeline integration

---

## 🔬 Reproducing Evaluation Results

To reproduce the experimental pipeline and complexity estimation on sample projects:

```bash
git clone https://github.com/helabenkhalfallah/complexia.git
cd complexia
npm install
npm run analyze -- --srcDir "./examples" --outputDir "./reports" --format html,json
```

### Output:

📂 `reports/`  
- `complexity-report/ComplexityOverview.json`  
- `complexity-report/ComplexityOverview.html`  
- `complexity-report/OpsEstimates.json`  
- Optional heatmaps, AST snapshots, and diagnostics

> **Note**: The included `examples/` folder demonstrates loop nesting, recursion, and branching constructs across common complexity classes. A full benchmarked dataset will be released in conjunction with the ACM publication.

---

## 📦 Repository Structure

- `src/` – Core AST traversal and complexity inference engine
- `cli/` – Command-line interface for batch analysis
- `examples/` – Reference programs with known complexity
- `reports/` – HTML/JSON output for review and inspection

---

## 📚 Citation

```bibtex
@inproceedings{benkhalfallah2025complexia,
  author    = {Héla Ben Khalfallah},
  title     = {Complexia: Static Inference of Algorithmic Complexity and Resource Costs via JavaScript/TypeScript AST Analysis},
  booktitle = {Proceedings of the ACM Conference on Programming Languages (ACM SIGPLAN)},
  year      = {2025},
  note      = {To appear},
}
```

---

## 🧠 Use Cases

- Developer feedback loop for performance at dev time
- Complexity regression detection in CI/CD
- Algorithm class verification for educational use
- Input to sustainability models (e.g., [`emissia`](https://github.com/helabenkhalfallah/emissia))

---

## 🤝 Contributing

```bash
git clone https://github.com/helabenkhalfallah/complexia.git
cd complexia
npm install
```

Run:

```bash
npm run analyze -- --srcDir "./examples" --outputDir "./reports" --format html,json
```

---

## 📜 License

Licensed under the MIT License. See the [LICENSE](./LICENSE) file.
