# TUGAS BESAR-UAS-KELOMPOK-1
(Radit)
import streamlit as st
import pandas as pd
import os

CSV_FILE = "pengeluaran.csv"

# LOAD & SAVES
def load_data():
    if os.path.exists(CSV_FILE):
        df = pd.read_csv(CSV_FILE)
        df["Tanggal"] = pd.to_datetime(df["Tanggal"], format="mixed").dt.date 


(ismail)
        return df.sort_values("Tanggal", ascending=False).reset_index(drop=True)
    return pd.DataFrame(columns=["Tanggal", "Kategori", "Nominal", "Deskripsi"])

def save_data(df):
    df.to_csv(CSV_FILE, index=False)


st.title("💰 Aplikasi Pengeluaran Sederhana")

df = load_data()

tab1, tab2 = st.tabs(["📊 Data", "➕ Tambah"])

(Samuel Rizaldi Manalu)
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


