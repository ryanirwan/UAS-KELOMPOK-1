# TUGAS BESAR-UAS-KELOMPOK-1
import streamlit as st
import pandas as pd
import os

CSV_FILE = "pengeluaran.csv"

def load_data():
    if os.path.exists(CSV_FILE):
        df = pd.read_csv(CSV_FILE)
        df["Tanggal"] = pd.to_datetime(df["Tanggal"], format="mixed").dt.date 
        return df.sort_values("Tanggal", ascending=False).reset_index(drop=True)
    return pd.DataFrame(columns=["Tanggal", "Kategori", "Nominal", "Deskripsi"])
    
def save_data(df):
    df.to_csv(CSV_FILE, index=False)

st.title("💰 Aplikasi Pengeluaran Sederhana")
df = load_data()
tab1, tab2 = st.tabs(["📊 Data", "➕ Tambah"])

with tab2:
    st.header("Tambah Pengeluaran")
    tanggal = st.date_input("Tanggal")
    kategori = st.selectbox("Kategori", ["Makanan", "Transportasi", "Belanja", "Tagihan", "Lain-lain"])
    nominal = st.number_input("Nominal (Rp)", min_value=0)
    deskripsi = st.text_input("Deskripsi (opsional)")

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
with tab1:
    st.header("Data Pengeluaran")
    if df.empty:
        st.info("Belum ada data.")
    else:
        st.write("### Total Pengeluaran")
        st.metric("Total", f"Rp {df['Nominal'].sum():,}")
        st.write("### Tabel Data")
        st.dataframe(df)
        st.write("### Grafik Per Kategori")
        st.bar_chart(df.groupby("Kategori")["Nominal"].sum())
        st.write("---")
        st.write("### Hapus Data")
        idx = st.number_input("Hapus baris ke:", 
                              min_value=0, 
                              max_value=len(df)-1, 
                              step=1)
        if st.button("Hapus Baris"):
            df = df.drop(idx).reset_index(drop=True)
            save_data(df)
            st.success(f"Baris ke-{idx} dihapus!")
        if st.button("Hapus Semua Data"):
            df = df.iloc[0:0]
            save_data(df)
            st.success("Semua data terhapus!")

            
