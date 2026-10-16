# Field Notes on Compression

Public research essays for the effort to build a smaller, complete, exactly decodable Hutter or LTCB package.

Read the journal at <https://jerecoder.github.io/entropy-forge-field-notes/>. A research review is due every ten elapsed wall-clock hours, covering experiments, analysis, literature, CPU work, engineering, negative findings, coordination, and research decisions. GPU time is reported separately as a cost metric.

The existing essays are a historical retrospective. The GPU ledger begins with an inherited 80.216691312-hour compute-cost total; it cannot be converted into an elapsed research timeline. The current UTC reporting window and next deadline are recorded in `_data/publication.json`. Publication can be delayed while the coordinator host is unavailable; a subsequent review covers the gap explicitly.

Post source paths and SHA-256 digests identify the private research records behind each account. This public repository contains the readable notes only, not reports, checkpoints, raw logs, or project code. Execution completion remains separate from scientific acceptance.

## Writing and theme

The essays use an argument-led structure: question, prediction or competing explanations, evidence, uncertainty, and implications for the research plan. They assume technical literacy without knowledge of internal execution machinery.

The site uses Jekyll’s stock Minima theme with standard home, page, and post layouts. No custom CSS, JavaScript, or layout overrides are used. The existing Pages workflow builds and deploys it; post URLs remain unchanged.

Use figures where they clarify evidence: learning curves, model-storage tradeoffs, and mechanism diagrams. Scientific plots include numerical sources, labeled units and scope, a caption, and alt text. The model-storage essay now includes a data-backed comparison and a downloadable vector figure.
