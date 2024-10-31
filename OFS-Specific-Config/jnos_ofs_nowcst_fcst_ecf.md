```mermaid
flowchart TD
    A[jnos_ofs_nowcst_fcst.ecf] --> B[JNOS_OFS_NOWCST_FCST]
    B --> C[exnos_ofs_nowcast_forecast.sh]
    
    C --> D[nos_ofs_launch.sh nowcast]
    C --> E[nos_ofs_nowcast_forecast.sh]
    
    E --> F{Run Type}
    F -->|nowcast| G1[Run Nowcast]
    F -->|forecast| G2[Run Forecast]
    
    G1 & G2 --> H{OCEAN_MODEL}
    H -->|ROMS| I1["$EXECnos/cbofs_roms_mpi"]
    H -->|FVCOM| I2["$EXECnos/fvcom_NGOFS"]
    
    I1 & I2 --> J[nos_ofs_archive.sh]

    classDef ecfNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef jobNode fill:#ffa,stroke:#333,stroke-width:2px;
    classDef scriptNode fill:#aef,stroke:#333,stroke-width:2px;
    classDef execNode fill:#afa,stroke:#333,stroke-width:2px;
    class A ecfNode;
    class B jobNode;
    class C,D,E,J scriptNode;
    class I1,I2 execNode;