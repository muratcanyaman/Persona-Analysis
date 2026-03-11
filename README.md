# 🎯 Persona Analysis — Rule-Based Customer Classification

<div align="center">

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.x-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

*Kural tabanlı sınıflandırma yöntemiyle müşteri segmentasyonu ve potansiyel gelir tahmini*

</div>

---

## 📌 Proje Hakkında

Bu proje, bir oyun şirketinin müşterilerini **demografik ve davranışsal özelliklerine** göre segmentlere ayırarak, yeni gelen müşterilerin şirkete **ortalama ne kadar gelir getirebileceğini** tahmin etmeyi amaçlamaktadır.

Kural tabanlı sınıflandırma (Rule-Based Classification) yaklaşımı kullanılarak, müşteriler çeşitli kriterlere göre gruplandırılmış ve her grup için **persona**lar oluşturulmuştur.

## 📊 Veri Seti

`persona.csv` dosyası, bir oyun şirketinin uluslararası satış verilerini içermektedir.

| Değişken | Açıklama | Tip |
|----------|----------|-----|
| **PRICE** | Müşterinin harcama tutarı | `int` |
| **SOURCE** | Müşterinin bağlandığı cihaz türü (ios / android) | `object` |
| **SEX** | Müşterinin cinsiyeti (male / female) | `object` |
| **COUNTRY** | Müşterinin ülkesi (usa, bra, deu, tur, fra, can) | `object` |
| **AGE** | Müşterinin yaşı | `int` |

> 📏 **Boyut:** 5.000 satır × 5 sütun

## 🗂️ Proje Yapısı

```
Persona-Analysis/
│
├── persona.csv                         # Ham veri seti
├── persona_analysis.ipynb              # Ana analiz notebook'u
├── Kural_Tabanlı_Sınıflandırma.pdf     # Proje dökümanı ve görev tanımları
└── README.md                           # Proje açıklaması
```

## 🔬 Analiz Adımları

Projede aşağıdaki 8 görev sırasıyla gerçekleştirilmiştir:

### Görev 1 — Keşifçi Veri Analizi (EDA)
- Unique `SOURCE` sayısı ve frekansları incelendi → **android: 2974**, **ios: 2026**
- Unique `PRICE` değerleri belirlendi → **6 farklı fiyat** (9, 19, 29, 39, 49, 59)
- Ülke ve kaynak bazlı satış sayıları ve toplam gelirler hesaplandı
- Ülke ve kaynak kırılımında ortalama fiyatlar analiz edildi

### Görev 2 — Çoklu Kırılım Analizi
`COUNTRY`, `SOURCE`, `SEX` ve `AGE` kırılımında ortalama kazançlar hesaplandı.

### Görev 3 — Sıralama
Çıktı, `PRICE` değerine göre azalan şekilde sıralandı.

### Görev 4 — Index Dönüşümü
Multi-index yapısı, `reset_index()` ile düz bir DataFrame'e dönüştürüldü.

### Görev 5 — Yaş Kategorileri
`AGE` değişkeni kategorik hale getirildi:

| Kategori | Aralık |
|----------|--------|
| `0-18` | 0 – 18 yaş |
| `19-23` | 19 – 23 yaş |
| `24-30` | 24 – 30 yaş |
| `31-40` | 31 – 40 yaş |
| `41-66` | 41+ yaş |

### Görev 6 — Persona Tanımlama
Müşteri personaları, değişkenlerin birleştirilmesiyle oluşturuldu:

```
FORMAT: SOURCE_COUNTRY_SEX_AGE_CAT
ÖRNEK:  ANDROID_BRA_MALE_0-18
```

### Görev 7 — Segmentasyon
Personalar, `PRICE` değerine göre **4 segmente** (A, B, C, D) ayrıldı (`pd.qcut`).

### Görev 8 — Yeni Müşteri Tahmini
Yeni gelen müşteriler için segment ve tahmini gelir belirlendi:

| Müşteri Profili | Persona | Segment | Tahmini Gelir |
|-----------------|---------|---------|---------------|
| 33 yaş, Android, Türk, Kadın | `ANDROID_TUR_FEMALE_31-40` | **D** | ~27.5 |
| 35 yaş, iOS, Fransız, Kadın | `IOS_FRA_FEMALE_31-40` | **C** | ~33.0 |

## 🛠️ Kullanılan Teknolojiler

- **Python 3.12**
- **Pandas** — Veri manipülasyonu ve analiz
- **NumPy** — Sayısal hesaplamalar
- **Seaborn & Matplotlib** — Veri görselleştirme

## 🚀 Kurulum ve Çalıştırma

```bash
# Repoyu klonlayın
git clone https://github.com/muratcanyaman/Persona-Analysis.git
cd Persona-Analysis

# Gerekli kütüphaneleri yükleyin
pip install pandas numpy seaborn matplotlib jupyter

# Notebook'u açın
jupyter notebook persona_analysis.ipynb
```

## 📈 Temel Bulgular

- 🇺🇸 **USA** en yüksek satış hacmine sahip ülkedir (**2.065 satış**, toplam **$70.225**)
- 🇧🇷 **Brezilya** ikinci sırada yer almaktadır (**1.496 satış**, toplam **$51.354**)
- 📱 **Android** kullanıcıları iOS kullanıcılarına göre daha fazla satış oluşturmaktadır (**2.974 vs 2.026**)
- 💰 Ülke bazlı ortalama fiyatlar birbirine oldukça yakındır (~**$34**)
- 🇹🇷 **Türkiye**, Android platformunda en yüksek ortalama fiyata sahiptir (**$36.23**)





---

<div align="center">



</div>
