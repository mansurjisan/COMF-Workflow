```mermaid
flowchart TD
    A[jnos_ofs_obs.ecf] --> B[JNOS_OFS_OBS]
    B --> C[exnos_ofs_obs.sh]
    
    C --> D[nos_ofs_adjust_tides]
    D --> E[SST Processing]
    E --> E1[sst_cutout_multiSat.py]
    E --> E2[timeave_granules.py]
    E --> E3[d_sst_multiSat.py]
    
    E3 --> F[HF Radar Processing]
    F --> F1[d_hf.py]
    
    F1 --> G[SSH Processing]
    G --> G1[d_ssh.py]
    
    G1 --> H[Merge Observations]
    H --> H1[merge_obs.py]
    
    H1 --> I[Output Files]
    I --> I1[sst_super_obs]
    I --> I2[hf_obs]
    I --> I3[adt_obs]
    I --> I4[merged obs file]

    classDef ecfNode fill:#f9f,stroke:#333,stroke-width:2px;
    classDef jobNode fill:#ffa,stroke:#333,stroke-width:2px;
    classDef scriptNode fill:#aef,stroke:#333,stroke-width:2px;
    classDef processNode fill:#afa,stroke:#333,stroke-width:2px;
    class A ecfNode;
    class B jobNode;
    class C,E1,E2,E3,F1,G1,H1 scriptNode;
    class D,E,F,G,H,I processNode;