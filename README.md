# 📊 Invoice Ledger Analytics

**From static Excel rows to interactive insights—turning construction ledgers into an actionable analytics dashboard.**

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.29+-red.svg)](https://streamlit.io)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 🎯 The Problem

Managing construction or facility management finances often means wrestling with massive Excel files:

| Pain Point | Impact |
|------------|--------|
| **Manual filtering** | 5-10 minutes per query |
| **No visualizations** | Insights buried in numbers |
| **Version control nightmare** | "Which file is the latest?" |
| **Zero accountability** | No audit trail |

Every time you need to answer "How much did we spend with Contractor X in Q3?" you're stuck opening Excel, finding the right sheet, manually filtering columns, creating pivot tables, and repeating the process over and over.

**There had to be a better way.**

---

## ✨ The Solution

**Invoice Ledger Analytics** transforms financial spreadsheets from a chore into an insight-generation machine. Built with Python and Streamlit, this lightweight web app delivers:

- ⚡ **2-minute workflow** from upload to insights (down from 10 minutes)
- 🎨 **Interactive filtering** with real-time updates
- 📈 **Visual analytics** with heatmaps and charts
- 📥 **One-click CSV export** for reports and audits

---

## 🏗️ Architecture

The app follows clean software engineering principles—modular, maintainable, and production-ready:

```
invoice-ledger/
├── app.py              # Main entry point & UI orchestration
├── data_loader.py      # Excel loading, normalization & cleaning
├── filters.py          # Interactive filter components
├── analytics.py        # Metrics, charts & visualizations
└── requirements.txt    # Project dependencies
```

### Why Modular?
Each module has a **single responsibility**, making the codebase:
- ✅ **Maintainable** — Know exactly where to make changes
- ✅ **Testable** — Independently unit test each component
- ✅ **Reusable** — Port components to other projects
- ✅ **Collaborative** — Multiple developers can work in parallel

---

## 🔧 Key Features

### 1. Smart Data Processing
No more "Contractor" vs "contractor" headaches. The app automatically:
- Normalizes column names
- Parses dates intelligently
- Converts amounts to proper numeric types
- Strips whitespace from text fields

### 2. Interactive Filtering
Real-time filters with no "Apply" button needed:
- 📅 Year selector with auto-detection
- 🗓️ Date range picker for granular queries
- 🏢 Multi-select for contractors and services
- 🔍 Invoice search for quick lookups
- 💰 Amount range slider for budget-based filtering
- 🏗️ **"All Buildings/Locations"** option to view consolidated data across sheets

### 3. Visual Analytics
Instant insights through:
- **Summary metrics**: Total records, spending, contractors, services
- **Contractor breakdown**: Bar chart + color-coded table
- **Monthly timeline**: Line chart tracking expenses over time
- **Heatmaps**: High-spending contractors highlighted in red, low-spending in green

### 4. One-Click Export
Download filtered datasets as CSV with a single click—perfect for reports, audits, or stakeholder sharing.

---

## 🚀 Quick Start

### Prerequisites
- Python 3.10 or higher
- pip package manager

### Installation

```bash
# Clone the repository
git clone https://github.com/lfariabr/invoice-ledger.git
cd invoice-ledger

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run the app
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

### Usage

1. **Upload** your Excel ledger file
2. **Select** building/location (or choose "All" for consolidated view)
3. **Apply filters** in the sidebar
4. **Explore** analytics and charts
5. **Download** filtered data as needed

---

## 📦 Tech Stack

- **[Python 3.10+](https://www.python.org/)** — Core programming language
- **[Streamlit](https://streamlit.io)** — Web UI framework
- **[Pandas](https://pandas.pydata.org/)** — Data processing & analysis
- **[openpyxl](https://openpyxl.readthedocs.io/)** — Excel file integration

---

## 📐 Module Overview

### `app.py`
Main application entry point that orchestrates the UI flow and handles file uploads.

### `data_loader.py`
**Key function**: `load_ledger(file)`
- Loads Excel files with multi-sheet support
- Normalizes column names and data types
- Cleans and validates data

### `filters.py`
**Key function**: `apply_filters(df, sheet_name)`
- Renders sidebar filter components
- Applies filters in real-time
- Returns filtered dataframe

### `analytics.py`
**Key functions**:
- `show_summary_metrics()` — Display KPIs
- `show_contractor_spending()` — Contractor breakdown
- `show_spending_over_time()` — Monthly timeline
- `show_analytics()` — Main analytics orchestration

---

## 📊 Impact

### Before vs After

| Metric | Before | After |
|--------|--------|-------|
| Query time | 10-15 min | 2 min |
| Visualizations | None | Interactive charts |
| Reproducibility | Manual | One-click |
| Export | Copy-paste | CSV download |

---

## 🛣️ Roadmap

- [ ] Unit testing with pytest
- [ ] User authentication for multi-user access
- [ ] Database integration for historical tracking
- [ ] Predictive analytics using machine learning
- [ ] API endpoints for programmatic access

---

## 🎓 About This Project

Built as part of my **Master's in Software Engineering / AI** journey—blending academic rigor with industry practicality. This project demonstrates:
- Production-ready code structure
- Real-world problem solving
- Clean architecture principles
- User-centric design

---

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests

---

## 📄 License

This project is licensed under the MIT License.

---

## 👤 Author

**Luis Faria**

- 🌐 Portfolio: [luisfaria.dev](https://luisfaria.dev)
- 💼 LinkedIn: [linkedin.com/in/lfariabr](https://linkedin.com/in/lfariabr)
- 🐙 GitHub: [github.com/lfariabr](https://github.com/lfariabr)

---

> *"The best code is the code that makes work feel like play."*

Built with ❤️ and ☕ by [Luis Faria](https://github.com/lfariabr)