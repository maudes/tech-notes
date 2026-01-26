# Maude's Technical Notes
Technical notes on IoT protocols (Matter, WiFi 7) and CPE software architectures (prpl, RDK-B, OpenSync).


## Structure
tech-notes/
├── .github/workflows/     # CI/CD GitHub Actions auto-deployment
├── docs/                  # All pages and assets
│   ├── index.md           # Landing page
│   ├── favicon.ico        # Browser icon
│   ├── blog/              # 技術隨筆與部落格文章
│   ├── wireless/          # WiFi & 3GPP 
│   ├── matter/            # Matter learnings
│   ├── cpe/               # CPE structures (OpenWRT, RDK-B, prpl, OpenSync/Plume etc.)
│   └── assets/            # Static assets of the site
│       ├── images/        
│       ├── pdfs/          
│       └── css/           
├── mkdocs.yml             # MkDocs core configuration file
└── README.md             

tech-notes/
├── docs/
│   ├── index.md           # Landing Page
│   ├── blog/
│   │   ├── posts/         # 所有的部落格文章都放這裡
│   │   │   ├── 2026-01-26-wifi7-mlo.md
│   │   │   └── 2025-12-20-matter-setup.md
│   │   └── archive.md     # (選擇性) 歸檔頁面
│   ├── wireless/          # 結構化文件 (非部落格)
│   ├── assets/            # 圖片與媒體
│   └── favicon.ico
├── mkdocs.yml
└── .github/workflows/deploy.yml
