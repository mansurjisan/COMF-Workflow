```mermaid
flowchart TD
    A[jnos_ofs_prep.ecf] --> B[JNOS_OFS_PREP]
    B --> C{Check OFS Type}
    C -->|Great Lakes<br/>LSOFS/LOOFS| D1[Skip OBC Generation]
    C -->|Other OFS| D2[Generate Open<br/>Boundary Conditions]
    C -->|WCOFS| D3[Set WCOFS Specific<br/>Restart & Paths]
    
    D2 --> E1[Run nos_ofs_create_forcing_obc.sh]
    D3 --> E2[export OFS_NF='wcofs'<br/>Set COMrst path]

    classDef ecfNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef jobNode fill:#ffa,stroke:#333,stroke-width:2px;
    classDef conditionNode fill:#fda,stroke:#333,stroke-width:2px;
    classDef processNode fill:#afa,stroke:#333,stroke-width:2px;
    class A ecfNode;
    class B jobNode;
    class C conditionNode;
    class D1,D2,D3,E1,E2 processNode;