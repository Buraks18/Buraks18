import sqlite3
from tkinter import *
from tkinter import messagebox

# Veritabanı oluşturma ve bağlanma
conn = sqlite3.connect("ilgaz_tesisat.db")
cursor = conn.cursor()

# Tablo oluşturma
cursor.execute("""
CREATE TABLE IF NOT EXISTS randevular (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    musteri_adi TEXT,
    telefon TEXT,
    tarih TEXT,
    saat TEXT,
    yapilan_isler TEXT
)
""")
conn.commit()

# Randevu ekleme fonksiyonu
def randevu_ekle():
    musteri_adi = entry_musteri.get()
    telefon = entry_telefon.get()
    tarih = entry_tarih.get()
    saat = entry_saat.get()
    yapilan_isler = text_isler.get("1.0", END)

    if musteri_adi and telefon and tarih and saat:
        cursor.execute("INSERT INTO randevular (musteri_adi, telefon, tarih, saat, yapilan_isler) VALUES (?, ?, ?, ?, ?)", 
                       (musteri_adi, telefon, tarih, saat, yapilan_isler))
        conn.commit()
        messagebox.showinfo("Başarılı", "Randevu başarıyla eklendi.")
        temizle()
    else:
        messagebox.showwarning("Uyarı", "Lütfen tüm alanları doldurun.")

# Kayıtları listeleme fonksiyonu
def randevulari_listele():
    cursor.execute("SELECT * FROM randevular")
    kayitlar = cursor.fetchall()
    listbox.delete(0, END)
    for kayit in kayitlar:
        listbox.insert(END, f"ID: {kayit[0]}, Adı: {kayit[1]}, Tarih: {kayit[3]} {kayit[4]}")

# Temizleme fonksiyonu
def temizle():
    entry_musteri.delete(0, END)
    entry_telefon.delete(0, END)
    entry_tarih.delete(0, END)
    entry_saat.delete(0, END)
    text_isler.delete("1.0", END)

# GUI
root = Tk()
root.title("Ilgaz Tesisat Randevu Sistemi")

Label(root, text="Müşteri Adı:").grid(row=0, column=0)
entry_musteri = Entry(root)
entry_musteri.grid(row=0, column=1)

Label(root, text="Telefon:").grid(row=1, column=0)
entry_telefon = Entry(root)
entry_telefon.grid(row=1, column=1)

Label(root, text="Tarih (YYYY-MM-DD):").grid(row=2, column=0)
entry_tarih = Entry(root)
entry_tarih.grid(row=2, column=1)

Label(root, text="Saat (HH:MM):").grid(row=3, column=0)
entry_saat = Entry(root)
entry_saat.grid(row=3, column=1)

Label(root, text="Yapılan İşler:").grid(row=4, column=0)
text_isler = Text(root, height=5, width=40)
text_isler.grid(row=4, column=1)

Button(root, text="Randevu Ekle", command=randevu_ekle).grid(row=5, column=0, pady=10)
Button(root, text="Randevuları Listele", command=randevulari_listele).grid(row=5, column=1, pady=10)

listbox = Listbox(root, width=70)
listbox.grid(row=6, column=0, columnspan=2)

root.mainloop()
