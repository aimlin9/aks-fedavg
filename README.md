# AKS-FedAvg

**Adaptive Key-Size Engineering for Latency-Efficient Paillier-Secured Federated Learning Aggregation in Resource-Constrained Networks**

Research codebase for a KNUST Department of Computer Science Research Methods proposal (2026). Extends the Project 12 federated learning system (cross-school student-progress tracking) with an engineered, adaptive Paillier key-size selection module — **AKS-FedAvg**.

## What this is

Paillier homomorphic encryption is the standard way to secure model-update aggregation in federated learning, but existing systems fix the key size once at design time (e.g. 1024 bits in Alqazzaz, 2025; 3072 bits in Du et al., 2023), regardless of how compute/bandwidth-constrained a given client is. This project engineers and benchmarks **AKS-FedAvg**: a [F]abricated adaptive key-size selection module that picks the smallest Paillier key satisfying a target security level, given each client's observed latency/bandwidth profile.

Full research proposal (problem statement, literature review, methodology, marking-scheme self-assessment) lives in [`docs/`](./docs).

## Status

🚧 **Proposal stage.** Phase 0 (environment setup) and Phase 1 (locked baseline) have not started yet. See [`docs/Research_Proposal.docx`](./docs) for the full work plan and timeline (Section 10).

## Planned structure

```
.
├── docs/                  # Research proposal, literature notes
├── src/
│   ├── baseline/          # Locked, unmodified fixed-key Paillier-FedAvg (Phase 1)
│   ├── aks_fedavg/         # Engineered adaptive key-size module (Phase 2)
│   └── instrumentation/    # Timing/bandwidth measurement layer
├── experiments/            # Run configs + logs (5 key sizes × 4 client counts × 3 network profiles)
├── notebooks/              # Analysis: Wilcoxon tests, Pareto-frontier plots
├── tests/
├── requirements.txt
└── README.md
```

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Baselines compared against

1. Unencrypted FedAvg (scientific control)
2. Fixed 2048-bit Paillier-FedAvg (NIST-minimum standard)
3. Fixed 3072-bit Paillier-FedAvg (Du et al., 2023)
4. Fixed 1024-bit Paillier-FedAvg (Alqazzaz, 2025)

## Key references

- Paillier, P. (1999). *Public-key cryptosystems based on composite degree residuosity classes.* EUROCRYPT '99. https://doi.org/10.1007/3-540-48910-X_16
- McMahan, H. B. et al. (2017). *Communication-efficient learning of deep networks from decentralized data.* AISTATS. https://doi.org/10.48550/arXiv.1602.05629
- Bonawitz, K. et al. (2017). *Practical secure aggregation for privacy-preserving machine learning.* ACM CCS. https://doi.org/10.1145/3133956.3133982
- Pan, Y. et al. (2024). *FedSHE: adaptive segmented CKKS homomorphic encryption.* Cybersecurity. https://doi.org/10.1186/s42400-024-00232-w
- Du, W. et al. (2023). *Privacy-preserving framework for cross-device federated learning.* Complex & Intelligent Systems. https://doi.org/10.1007/s40747-023-00978-9

(Full reference table with all DOIs in the proposal, Section 11.)

## License

MIT — see [LICENSE](./LICENSE).

## Author

Ramsey ([@aimlin9](https://github.com/aimlin9)) — Department of Computer Science, KNUST.
