# Bilgisayar Nasıl Çalışır?

---

## 1. Genel Tablo

Bir bilgisayarın dört ana parçası vardır:

```
┌─────────────┐     komut & veri      ┌─────────────────────────┐
│   GİRİŞ     │ ───────────────────►  │        İŞLEMCİ (CPU)    │
│  (klavye)   │                       │                         │
└─────────────┘                       │  ┌──────────┐           │
                                      │  │  Kontrol │           │
┌─────────────┐     sonuç             │  │  Birimi  │           │
│   ÇIKIŞ     │ ◄───────────────────  │  └────┬─────┘           │
│  (ekran)    │                       │       │                 │
└─────────────┘                       │  ┌────▼─────┐           │
                                      │  │   ALU    │           │
┌─────────────┐     oku / yaz         │  └────┬─────┘           │
│    RAM      │ ◄──────────────────►  │       │                 │
│  (bellek)   │                       │  ┌────▼─────┐           │
└─────────────┘                       │  │Akümülatör│           │
                                      │  └──────────┘           │
                                      └─────────────────────────┘
```

---

## 2. RAM — Bellek

RAM, numaralı kutulardan oluşur. Her kutunun bir **adresi** (ismi) ve bir **değeri** vardır.

```
┌────────┬───────┐
│ Adres  │ Değer │
├────────┼───────┤
│ toplam │   0   │
│ taban  │   5   │
│ us     │   3   │
│ sonuc  │   1   │
└────────┴───────┘
```

- RAM sadece **saklar** — hesap yapmaz
- İşlemci istediği zaman okur veya yazar
- Program kapanınca içerik silinir

---

## 3. ALU — Hesap Makinesi

ALU (Arithmetic Logic Unit), işlemcinin hesap yapan birimidir. Yapabildiği işlemler:

```
┌────────────────────────────────────────┐
│               ALU                      │
│                                        │
│  Giriş A ──►                           │
│               [ + - × ÷ mod ]  ──► Sonuç
│  Giriş B ──►                           │
│                                        │
│  Karşılaştırma: sıfır mı? negatif mi? │
└────────────────────────────────────────┘
```

ALU sadece **iki sayıyla** çalışır ve sonucu üretir. Nerede saklanacağını bilmez — o iş akümülatörün.

---

## 4. Akümülatör — Geçici Kalem

Akümülatör, işlemcinin içindeki **tek yazmaçtır** (register). RAM'den farklıdır:

```
         RAM                    İşlemci
  ┌──────┬───────┐         ┌────────────────┐
  │taban │   5   │         │                │
  │us    │   3   │  ◄───►  │  Akümülatör: 5 │◄──► ALU
  │sonuc │   1   │         │                │
  └──────┴───────┘         └────────────────┘
  Uzakta, yavaş              Yanı başında, hızlı
```

- RAM'e ulaşmak için `load` / `store` komutu gerekir
- Akümülatör zaten ALU'nun yanındadır — her işlemde oradadır
- Tüm aritmetik işlemlerin sonucu akümülatöre düşer

---

## 5. Kontrol Birimi — Yönetici

Kontrol birimi programı **sırayla okur** ve her komut için doğru birimi çalıştırır:

```
  Program (RAM'de)
  ─────────────────
  1: load taban      ◄── Kontrol birimi burayı okur
  2: mul us              "load komutu → RAM'den oku, akümülatöre yaz"
  3: store sonuc
  4: stop
```

Her adımda şunu yapar:

```
Getir ──► Çözümle ──► Çalıştır ──► Getir ──► ...
```

`stop` komutuna gelince durur.

---

## 6. Oyuncak Makine'de Bunlar Nerede?

```
┌──────────────────────────────────────────────────────┐
│                  toy.emrecan.dev                     │
│                                                      │
│  Kaynak Kod         ←── programın RAM'deki hali      │
│                                                      │
│  Bellek tablosu     ←── RAM (adres + değer)          │
│                                                      │
│  Akümülatör kutusu  ←── işlemci içi yazmaç           │
│                                                      │
│  Sonraki komut      ←── kontrol biriminin baktığı yer│
│                                                      │
│  Adımla butonu      ←── bir "Getir→Çalıştır" turu   │
└──────────────────────────────────────────────────────┘
```

---

## 7. İlk Program: İki Sayı Topla

Artık kodu okuyalım:

```
basla   get         # klavyeden sayı al → akümülatöre yaz
        store a     # akümülatördeki değeri RAM'e (a hücresine) kaydet
        get         # ikinci sayıyı al → akümülatöre yaz
        add a       # ALU: akümülatör + a → akümülatöre yaz
        print       # akümülatördeki sonucu ekrana yaz
        stop
a   0               # a hücresini tanımla, başlangıç değeri 0
```

Adım adım bellek ve akümülatör:

| Adım | Komut | Akümülatör | RAM (a) |
|------|-------|-----------|---------|
| 1 | `get` (girdi: 4) | **4** | — |
| 2 | `store a` | 4 | **4** |
| 3 | `get` (girdi: 7) | **7** | 4 |
| 4 | `add a` | **11** | 4 |
| 5 | `print` | 11 | 4 → ekran: **11** |
| 6 | `stop` | — | — |

> Neden `store a` gerekti? Çünkü ikinci `get` akümülatörü **ezer** — ilk sayıyı RAM'e koymazsak kaybolur.

---

## Not: `a 0` en altta ama neden ilk hazır oluyor?

Simülatör programı çalıştırmadan önce iki aşamadan geçirir:

**Aşama 1 — Yükleme (parse):** Kod tamamıyla taranır.
- Hangi etiketler var? → `basla`, `a`
- Bellek tanımları (`a 0` gibi) RAM'e yazılır
- Komutlar nereden başlıyor? → `basla` etiketinden

Bu aşamada `a = 0` RAM'e yazılır. Henüz hiçbir komut çalışmamıştır.

**Aşama 2 — Çalıştırma:** `basla` etiketinden itibaren komutlar sırayla işlenir. `a 0` bir komut değildir, çalıştırılacak bir şey yoktur — zaten hazırdır.

```
Kod                     Ne zaman işlenir?
──────────────────────────────────────────
basla   get           ← Çalıştırma aşamasında (sırayla)
        store a       ← Çalıştırma aşamasında
        ...
        stop          ← Çalıştırma aşamasında
a   0                 ← Yükleme aşamasında (başlamadan önce)
```

Gerçek işlemcilerde de aynı mantık geçerlidir: program belleğe yüklenir, veri alanları hazırlanır, **sonra** ilk komuta atlanır.
