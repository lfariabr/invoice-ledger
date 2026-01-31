## 📐 Module Breakdown (For Engineers)

### **`app.py` — Main Entry Point**
```python
def main():
    st.set_page_config(page_title="Invoice Ledger Analytics", layout="wide")
    
    # File upload
    uploaded_file = st.file_uploader("Upload Ledger Excel File", type=["xlsx"])
    
    # Load data (multi-sheet support)
    ledger_data = load_ledger(uploaded_file)
    
    # Building selector
    selected_sheet = st.sidebar.selectbox("Select Building:", ["All"] + sheet_names)
    
    # Apply filters
    df = apply_filters(df)
    
    # Show analytics
    show_summary_metrics(df)
    show_analytics(df)
```

**Responsibilities:**
- UI flow orchestration
- File upload handling
- Calls functions from specialized modules

---

### **`data_loader.py` — Smart Data Ingestion**
```python
@st.cache_data  # Caches loaded data for performance
def load_ledger(file_path):
    # Load all sheets
    df = pd.read_excel(file_path, sheet_name=None)
    
    for sheet_name, data in df.items():
        # Normalize column names (remove newlines, extra spaces)
        data.columns = data.columns.str.replace('\n', ' ').str.strip()
        
        # Convert dates intelligently
        data['Date'] = pd.to_datetime(data['Date'], errors='coerce')
        
        # Parse amounts as numeric
        data['Amount inc GST'] = pd.to_numeric(data['Amount inc GST'], errors='coerce')
        
        # Standardize contractor names (title case)
        data['Contractor'] = data['Contractor'].str.title()
    
    return df
```

**Key features:**
- **Multi-sheet parsing** (each building = separate sheet)
- **Data normalization** (consistent formatting)
- **Type conversion** (dates, amounts)
- **Caching** (load once, use everywhere)

---

### **`filters.py` �� Real-Time Interactions**
```python
def apply_filters(df):
    # Year filter (multi-select)
    years = st.sidebar.multiselect("Year(s):", sorted(df['Year'].unique()))
    if years:
        df = df[df['Year'].isin(years)]
    
    # Contractor filter
    contractors = st.sidebar.multiselect("Contractor(s):", sorted(df['Contractor'].unique()))
    if contractors:
        df = df[df['Contractor'].isin(contractors)]
    
    # Amount range slider
    min_amt, max_amt = float(df['Amount inc GST'].min()), float(df['Amount inc GST'].max())
    amount_range = st.sidebar.slider("Amount Range:", min_amt, max_amt, (min_amt, max_amt))
    df = df[(df['Amount inc GST'] >= amount_range[0]) & (df['Amount inc GST'] <= amount_range[1])]
    
    return df
```

**Design decision:**  
**No "Apply" button** — filters update instantly as users interact (Streamlit's reactive model)

---

### **`analytics.py` — Visualizations**
```python
def show_summary_metrics(df):
    """4-card KPI dashboard"""
    col1, col2, col3, col4 = st.columns(4)
    
    with col1:
        st.metric("Total Records", len(df))
    with col2:
        st.metric("Total Amount", f"${df['Amount inc GST'].sum():,.2f}")
    with col3:
        st.metric("Contractors", df['Contractor'].nunique())
    with col4:
        st.metric("Services", df['Service'].nunique())

def show_contractor_spending(df):
    """Bar chart + heatmap table"""
    contractor_spending = df.groupby('Contractor')['Amount inc GST'].sum().sort_values(ascending=False)
    
    # Bar chart
    st.bar_chart(contractor_spending)
    
    # Heatmap table (red = high spend, green = low)
    styled_df = contractor_df.style.format({'Total Spent': '${:,.2f}'}).background_gradient(
        subset=['Total Spent'],
        cmap='RdYlGn_r'  # Red → Yellow → Green
    )
    st.dataframe(styled_df)

def show_spending_over_time(df):
    """Monthly timeline chart"""
    monthly = df.set_index('Date').resample('ME')['Amount inc GST'].sum()
    st.line_chart(monthly)
```