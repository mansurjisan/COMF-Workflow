```mermaid
flowchart TD
    A[jnos_ofs_prep.ecf] --> B[JNOS_OFS_PREP]
    B --> C[exnos_ofs_prep.sh]
    
    C --> D1[nos_ofs_launch.sh prep]
    C --> D2[nos_ofs_create_forcing_met.sh nowcast]
    C --> D3[nos_ofs_create_forcing_river.sh]
    C --> D4[nos_ofs_create_forcing_obc.sh]
    C --> D5[nos_ofs_create_forcing_met.sh forecast]
    
    C --> E{OCEAN_MODEL?}
    E -->|FVCOM| F1[nos_ofs_prep_fvcom_ctl.sh]
    E -->|ROMS| F2[nos_ofs_prep_roms_ctl.sh]
    E -->|SELFE| F3[nos_ofs_prep_selfe_ctl.sh]
    
    F1 & F2 & F3 --> G[nowcast control file]
    F1 & F2 & F3 --> H[forecast control file]

    classDef ecfNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef jobNode fill:#ffa,stroke:#333,stroke-width:2px;
    classDef scriptNode fill:#aef,stroke:#333,stroke-width:2px;
    classDef fileNode fill:#afa,stroke:#333,stroke-width:2px;
    class A ecfNode;
    class B jobNode;
    class C,D1,D2,D3,D4,D5,F1,F2,F3 scriptNode;
    class G,H fileNode;