# 📈 Complexia

> **ACM 2025 (To Appear)**  
> _**Complexia: Static Inference of Algorithmic Complexity and Execution Cost via JS/TS Graph Analysis**_  
> 📄 [Publication Link – Coming Soon]

---

## ✨ Overview

**Complexia** is a formal and deterministic static analysis tool for JavaScript and TypeScript that extracts:

- ✅ **Asymptotic Complexity (Big O)** via control flow analysis,  
- ✅ **Real Instruction Cost** via weighted instruction traversal,  
- ✅ **Estimated Memory Allocation**,  
- ✅ **Platform-specific CPU Time** based on IC × CPI / Clock Rate.

Complexia introduces two **original graph models** proposed by Héla Ben Khalfallah:

- 📊 **OFG** – *O Flow Graph*: estimates structural **time and memory complexity** (Big O).  
- 🧮 **IFG** – *Instruction Flow Graph*: computes weighted **instruction count** and **allocation cost**.

By combining graph semantics with classical CPU performance modeling, Complexia provides **pre-runtime performance estimation**, helpful for optimization, benchmarking, and code complexity regression.

---

## ⚙️ Architecture Summary

| Graph | Purpose | Captures | Output |
|-------|---------|----------|--------|
| **OFG** | Estimate asymptotic complexity | Loops, branches, recursion | `O(n)`, `O(n log n)`, etc. |
| **IFG** | Compute real execution cost | Instruction weights, function calls | `instructionCount`, `memoryBytes` |

Final CPU time is derived using:

```txt
CPU Time = IC × CPI / Clock Rate
```

---

## 📥 Installation

```bash
npm install -D complexia
```

### Prerequisites
- Node.js ≥ 18.x
- TypeScript or JavaScript project

---

## 🚦 CLI Usage

```bash
npx complexia analyze \
  --srcDir "./examples" \
  --outputDir "./reports" \
  --format html,json \
  --cpuProfile "./profiles/intel-i7.json"
```

### Output formats:
- `html`: Developer-friendly complexity dashboard
- `json`: Machine-readable for CI/CD or research

---

## 🔬 Example Analysis Output

```json
{
  "function": "sumSquares",
  "estimatedTimeComplexity": "O(n)",
  "estimatedMemoryComplexity": "O(1)",
  "instructionCount": "3n + 2",
  "memoryBytes": "8",
  "cpuModel": {
    "CPI": 2,
    "clockGHz": 2,
    "cpuTime": "3n ns"
  }
}
```

---

## 📐 CPU Performance Model

Complexia integrates the classical CPU performance equation:

```txt
CPU Time = Instruction Count × CPI / Clock Rate
```

You can specify target hardware using `--cpuProfile`:

```json
{
  "name": "Intel i7",
  "CPI": 1.5,
  "clockGHz": 3.2
}
```

---

## 💡 Use Cases

- ✅ Detect complexity regressions during CI
- ✅ Pre-runtime performance estimation
- ✅ Algorithm class verification for education
- ✅ Baseline analysis for green computing models (e.g., [emissia](https://github.com/helabenkhalfallah/emissia))

---

## 📦 Repository Structure

```
.
├── src/          # Graph builders and cost engine
├── cli/          # CLI interface and argument parsing
├── examples/     # Sample algorithms with known complexity
├── reports/      # HTML/JSON output
├── profiles/     # Hardware profiles (CPI, clock, memory)
```

---

## 🧠 Theory & Validation

### Formal Architecture:
- **OFG** = asymptotic structure graph (Big O via loop/call analysis) *(Proposed by Héla Ben Khalfallah)*
- **IFG** = instruction-weighted graph (IC + memory cost) *(Proposed by Héla Ben Khalfallah)*
- **Final Cost** = `IC × CPI / Clock Rate` (with optional memory footprint)

### Scientific Grounding:
- Based on static analysis, CFG/DFG theory, cost semantics
- Deterministic and platform-independent (but configurable)

---


---

## 💾 Memory Cost Model

In addition to time complexity and instruction count, **Complexia** estimates **real memory consumption** using instruction-level annotations from the IFG (Instruction Flow Graph).

### 📊 Memory Estimation Equation:

```txt
Total Memory = ∑(Static Allocations + Dynamic Allocations × Growth Rate)
             = ∑ (object_size + array_size(n) + return_structures + temp buffers)
```

### 📌 IFG-based Memory Tracking:

Each instruction is annotated with memory-relevant metadata:

- `allocatesMemory`: `true | false`
- `allocationSize`: e.g. `n * 8 bytes` for `new Array(n)`
- `mutationType`: e.g. `.push`, `.concat`, `.set`
- `inputDependent`: Indicates whether allocation scales with input size
- `scopeLifetime`: Helps estimate whether memory persists (`local`, `returned`, `global`)

### 🔍 Example Memory Estimate:

```json
{
  "function": "bufferedSum",
  "estimatedMemoryComplexity": "O(n)",
  "memoryBytes": "n * 8 + 64",
  "memoryNotes": [
    "Array of size n allocated",
    "8 bytes per element",
    "Temporary buffer: 64 bytes"
  ]
}
```

### 💡 Optional Memory Profiles

Just like CPU, users may define memory profiles (e.g., element sizes, object headers):

```json
{
  "defaultElementSize": 8,
  "objectHeader": 16,
  "stringOverhead": 40
}
```

Memory cost can then be modeled per platform or JS engine characteristics.

---
## 📚 Citation

```bibtex
@inproceedings{benkhalfallah2025complexia,
  author    = {Héla Ben Khalfallah},
  title     = {Complexia: Static Inference of Algorithmic Complexity and Execution Cost via JavaScript/TypeScript Graph Analysis},
  booktitle = {Proceedings of the ACM Conference on Programming Languages (ACM SIGPLAN)},
  year      = {2025},
  note      = {To appear},
}
```

---

## 🤝 Contributing

```bash
git clone https://github.com/helabenkhalfallah/complexia.git
cd complexia
npm install
```

Then run analysis with:

```bash
npm run analyze -- --srcDir "./examples" --outputDir "./reports" --format html,json
```

---

## 📜 License

MIT License — See [LICENSE](./LICENSE)
