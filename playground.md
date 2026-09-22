graph LR
    subgraph Signal_In [タブレット / 信号入力]
        out[Headphone Out L]
        gnd[GND]
    end

    subgraph SW_Select [素子切り替えセクション]
        SW1[ジャンパー SW1: L/C切り替え]
        SW2[ジャンパー SW2: R切り替え]
    end

    subgraph LC_Pairs [LC組み合わせ]
        LC1["パターンA/B/C: L=10mH, C=0.1uF (f0 ≈ 5.0kHz)"]
        LC2["パターンD: L=1mH, C=1.0uF (f0 ≈ 5.0kHz)"]
    end

    subgraph R_Values [抵抗R]
        R1["R = 10 Ω (高Q)"]
        R2["R = 100 Ω (標準)"]
        R3["R = 470 Ω (低Q)"]
    end

    subgraph Protection [入力保護・アッテネータ]
        R_att1[分圧抵抗 10kΩ]
        R_att2[分圧抵抗 1kΩ]
        D1[保護ダイオード 1N5819 ×2]
        mic[Mic In]
    end

    out --> SW1
    SW1 -->|選択| LC1
    SW1 -->|選択| LC2
    LC1 --> SW2
    LC2 --> SW2

    SW2 -->|選択| R1
    SW2 -->|選択| R2
    SW2 -->|選択| R3

    R1 --> gnd
    R2 --> gnd
    R3 --> gnd

    SW2 --> R_att1
    R_att1 --> mic
    mic --> R_att2
    R_att2 --> gnd
    mic --> D1
    D1 --> gnd
