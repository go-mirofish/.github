<div align="center">

<img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/go-mirofish-thumbnail.png" alt="go-mirofish logo" width="55%"/>

**Go-MiroFish, lightweight and local-first**

[![GitHub Stars](https://img.shields.io/github/stars/go-mirofish/go-mirofish?style=flat-square&color=DAA520)](https://github.com/go-mirofish/go-mirofish/stargazers)
[![License: AGPL-3.0](https://img.shields.io/badge/License-AGPL--3.0-blue.svg?style=flat-square)](./LICENSE)
[![Go Version](https://img.shields.io/badge/Go-1.21+-blue.svg?style=flat-square)](https://go.dev/)
[![Python Version](https://img.shields.io/badge/Python-3.11+-blue.svg?style=flat-square)](https://www.python.org/)
[![GitHub Sponsors](https://img.shields.io/github/sponsors/justinedevs?style=flat-square&logo=github&label=Sponsor)](https://github.com/sponsors/go-mirofish)
[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-ffdd00?style=flat-square&logo=buy-me-a-coffee&logoColor=black)](https://www.buymeacoffee.com/justinedevs)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=flat-square&logo=discord&logoColor=white)](http://discord.gg/ePf5aPaHnA)
[![X](https://img.shields.io/badge/X-Follow-000000?style=flat-square&logo=x&logoColor=white)](https://x.com/mirofish_ai)

</div>

<div align="center">
   
Upload documents, describe what you want to predict, and get a full simulation report **on your laptop**.

</div>

## Quick start

**Canonical development:** Go gateway **in Docker** on :3000; Vue **locally** via Vite on :5173. You need **Docker**, **Node 18+**, and a one-time **`npm run setup`**.

1. **Clone**

   ```bash
   git clone https://github.com/go-mirofish/go-mirofish.git
   cd go-mirofish
   ```

2. **Configure and install**

   ```bash
   cp .env.example .env
   npm run setup
   ```

   Edit `.env` and set **`LLM_API_KEY`** and **`ZEP_API_KEY`**.

3. **Start the API (Docker)**

   ```bash
   make up
   ```

   - API / health: [http://127.0.0.1:3000/health](http://127.0.0.1:3000/health)

4. **Start the UI (local — second terminal)**

   ```bash
   npm run dev
   ```

   - App: [http://127.0.0.1:5173](http://127.0.0.1:5173) (Vite proxies `/api` to the gateway on :3000)
  

## What go-mirofish vs MiroFish

| | MiroFish (upstream) | go-mirofish (this repo) |
| --- | --- | --- |
| Control plane | Python / Flask (plus JS frontend) | **Go** (`gateway/`) — all `/api/*` routes |
| Local dev | Python venv, Flask, often multi-service | **Docker** gateway + **local** Vite (`make up` + `npm run dev`) |
| Simulation worker | Python-side integration | **Go-native** worker in the gateway process |
| Benchmarks & examples | Mixed scripts | **Go** `go-mirofish-examples` + bench tools + `mirofish-hybrid` helpers |
| Product Python | Required on the hot path | **Removed** (no `backend/.venv` in this tree) |
| Design goal | Full MiroFish upstream feature set | **Local-first**: lower moving parts, one gateway binary, fewer host dependencies |

> [!NOTE]
> RAM/startup “targets” depend on model provider, graph size, and simulation profile. For supported setup, see [Installation](docs/getting-started/installation.md).

## 🌐 Live Demo

- Static playground (zero-cost replay): [https://go-mirofish.vercel.app](https://go-mirofish.vercel.app)

## 📸 Screenshots

<div align="center">
  <table>
    <tr>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(1).png" width="520" />
        <br />
        <sub><b>Home / entry</b></sub>
      </td>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(2).png" width="520" />
        <br />
        <sub><b>Simulation run</b></sub>
      </td>
    </tr>
    <tr>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(3).png" width="520" />
        <br />
        <sub><b>Report generation</b></sub>
      </td>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(4).png" width="520" />
        <br />
        <sub><b>Report timeline / tools</b></sub>
      </td>
    </tr>
    <tr>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(5).png" width="520" />
        <br />
        <sub><b>Simulation history</b></sub>
      </td>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(6).png" width="520" />
        <br />
        <sub><b>Deep interaction</b></sub>
      </td>
    </tr>
    <tr>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(7).png" width="520" />
        <br />
        <sub><b>Split: graph, workbench &amp; system terminal</b></sub>
      </td>
      <td align="center">
        <img src="https://github.com/go-mirofish/go-mirofish/blob/main/static/image/Screenshot/Screenshot(8).png" width="520" />
        <br />
        <sub><b>Graph view &amp; node details</b></sub>
      </td>
    </tr>
  </table>
</div>


## Hardware compatibility

| Device | RAM | Works? |
| --- | ---: | --- |
| Desktop / laptop | 8GB | Yes |
| Desktop / laptop | 4GB | Yes (smaller simulations) |
| Raspberry Pi 5 | 4GB | Yes (light workloads; validate locally) |
| Raspberry Pi 4 | 4GB | Limited (expect tight headroom) |

> [!WARNING]
> Large graphs, long simulations, or heavy models can exceed **4GB** systems. Start with short runs and smaller seeds.

## Contributing

Issues and PRs are welcome. Use this repo for **go-mirofish** changes; upstream product discussion stays with [MiroFish](https://github.com/666ghj/MiroFish). Longer guides for contributors and the Phase 1–6 roadmap will live on **[go.mirofish.ai](https://go.mirofish.ai)** as the docs site grows.

## License

[AGPL-3.0](./LICENSE).

## Acknowledgments

Derived from **[MiroFish](https://github.com/666ghj/MiroFish)**. Simulation is powered by **[OASIS](https://github.com/camel-ai/oasis)**—thanks to the CAMEL-AI team.
