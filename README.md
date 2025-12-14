# TUGAS BESAR-UAS-KELOMPOK-1
(ismail)
        return df.sort_values("Tanggal", ascending=False).reset_index(drop=True)
    return pd.DataFrame(columns=["Tanggal", "Kategori", "Nominal", "Deskripsi"])

def save_data(df):
    df.to_csv(CSV_FILE, index=False)


st.title("💰 Aplikasi Pengeluaran Sederhana")

df = load_data()

tab1, tab2 = st.tabs(["📊 Data", "➕ Tambah"])

(gebby)
if st.button("Simpan"):
        if nominal > 0:
            baru = pd.DataFrame([{
                "Tanggal": tanggal,
                "Kategori": kategori,
                "Nominal": nominal,
                "Deskripsi": deskripsi
            }])
            df = pd.concat([baru, df], ignore_index=True)
            save_data(df)
            st.success("Data tersimpan!")
        else:
            st.error("Nominal harus lebih dari 0.")
