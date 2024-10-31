```mermaid
flowchart TD
    %% ECF and Job initialization with OFS setting
    A[jnos_ofs_prep.ecf] -->|Sets OFS & CYC| B[JNOS_OFS_PREP]
    B -->|Exports OFS variable| C[exnos_ofs_prep.sh]

    %% Configuration loading
    C --> D[Load OFS Config]
    D --> D1["Check ${FIXofs}/${PREFIXNOS}.ctl"]
    D1 -->|"e.g. nos.tbofs.ctl"| D2[Load OFS-specific settings]
    D2 --> D3["Set domain bounds<br/>Set grid specs<br/>Set model params"]
    
    %% Main workflow branches with OFS context
    D3 --> E1[nos_ofs_launch.sh]
    E1 -->|"Uses OFS grid/params"| F1[Setup working dirs]
    
    D3 --> E2[nos_ofs_create_forcing_met.sh]
    E2 -->|"OFS domain bounds"| F2[Generate met forcing]
    
    D3 --> E3[nos_ofs_create_forcing_river.sh]
    E3 -->|"OFS river points"| F3[Generate river forcing]
    
    D3 --> E4[nos_ofs_create_forcing_obc.sh]
    E4 -->|"OFS boundaries"| F4[Generate boundary conditions]
    
    %% Model specific control file generation
    D3 --> G{Check OCEAN_MODEL}
    G -->|"FVCOM+OFS config"| H1[nos_ofs_prep_fvcom_ctl.sh]
    G -->|"ROMS+OFS config"| H2[nos_ofs_prep_roms_ctl.sh]
    G -->|"SELFE+OFS config"| H3[nos_ofs_prep_selfe_ctl.sh]

    classDef ecfNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef jobNode fill:#ffa,stroke:#333,stroke-width:2px;
    classDef scriptNode fill:#aef,stroke:#333,stroke-width:2px;
    classDef configNode fill:#fda,stroke:#333,stroke-width:2px;
    classDef processNode fill:#afa,stroke:#333,stroke-width:2px;
    class A ecfNode;
    class B jobNode;
    class C,E1,E2,E3,E4,H1,H2,H3 scriptNode;
    class D,D1,D2,D3 configNode;
    class F1,F2,F3,F4 processNode;
