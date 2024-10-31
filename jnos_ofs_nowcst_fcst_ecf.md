```mermaid
flowchart TD
    A[jnos_ofs_nowcst_fcst.ecf] --> B[JNOS_OFS_NOWCST_FCST]
    B --> C[exnos_ofs_nowcast_forecast.sh]
    
    C --> D1[nos_ofs_launch.sh nowcast]
    D1 --> E1{Restart Available?}
    
    E1 -->|Yes| F1[Regular Run]
    E1 -->|No| F2[Cold Start]
    
    F1 & F2 --> G[nos_ofs_nowcast_forecast.sh nowcast]
    G --> H[Archive Nowcast]
    
    H --> I{LEN_FORECAST > 0?}
    I -->|Yes| J[nos_ofs_nowcast_forecast.sh forecast]
    J --> K[nos_ofs_archive.sh forecast]
    
    I -->|No| L[End]
    K --> L
    
    C -.->|If Interrupted| M[exnos_ofs_continue_forecast.sh]
    M --> N[Process Restart Files]
    N --> J

    classDef ecfNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef jobNode fill:#ffa,stroke:#333,stroke-width:2px;
    classDef scriptNode fill:#aef,stroke:#333,stroke-width:2px;
    classDef processNode fill:#afa,stroke:#333,stroke-width:2px;
    classDef decisionNode fill:#fda,stroke:#333,stroke-width:2px;
    class A ecfNode;
    class B jobNode;
    class C,D1,G,J,M scriptNode;
    class H,K,N processNode;
    class E1,I decisionNode;