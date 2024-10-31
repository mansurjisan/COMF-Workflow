```mermaid
flowchart TD
    A[Model Execution] --> B{Check OCEAN_MODEL}
    
    B -->|FVCOM| C1[FVCOM Settings]
    B -->|ROMS| C2[ROMS Settings]
    B -->|SELFE| C3[SELFE Settings]
    
    C1 --> D1[Load FVCOM Grid<br/>Set NPROC<br/>Set MPIOPTS]
    C2 --> D2[Load ROMS Grid<br/>Set Tiles<br/>Set MPIOPTS]
    C3 --> D3[Load SELFE Grid<br/>Set NPROC<br/>Set MPIOPTS]
    
    D1 & D2 & D3 --> E[Execute Model]

    classDef modelNode fill:#fda,stroke:#333,stroke-width:2px;
    classDef settingNode fill:#aef,stroke:#333,stroke-width:2px;
    classDef processNode fill:#afa,stroke:#333,stroke-width:2px;
    class A,B modelNode;
    class C1,C2,C3,D1,D2,D3 settingNode;
    class E processNode;