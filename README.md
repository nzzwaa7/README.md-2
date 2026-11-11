```mermaid
flowchart LR
    subgraph Alat ["Alat & Gerbang Mutu"]
        direction LR
        GH["GitHub Issues & PR"] --> P1["1. Push / PR"]
        P1 --> P2["2. Build & Package<br><small>Docker & GitHub Actions</small>"]
        P2 --> P3["3. Automated Testing<br><small>SonarQube & Trivy</small>"]
        P3 --> P4["4. Release Artifact<br><small>Container Registry GHCR</small>"]
        P4 --> P5["5. Deploy Staging & Prod<br><small>Terraform & Helm</small>"]
        P5 --> P6["6. Monitoring & Feedback<br><small>Prometheus & Grafana</small>"]
        
        P6 -.->|"Umpan Balik Bug"| GH
    end
