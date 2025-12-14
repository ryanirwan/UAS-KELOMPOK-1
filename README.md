# TUGAS BESAR-UAS-KELOMPOK-1
        return df.sort_values("Tanggal", ascending=False).reset_index(drop=True)
    return pd.DataFrame(columns=["Tanggal", "Kategori", "Nominal", "Deskripsi"])

def save_data(df):
    df.to_csv(CSV_FILE, index=False)

# APLIKASI
st.title("💰 Aplikasi Pengeluaran Sederhana")

df = load_data()

tab1, tab2 = st.tabs(["📊 Data", "➕ Tambah"])
