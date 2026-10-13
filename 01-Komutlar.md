# Komut Referansı

## Giriş / Çıkış

| Komut | Açıklama |
|-------|----------|
| `get` | Klavyeden bir sayı oku → akümülatöre kaydet |
| `print` | Akümülatörün içeriğini çıktıya yaz |

## Bellek İşlemleri

| Komut | Açıklama |
|-------|----------|
| `load Val` | `Val` değerini akümülatöre yükle |
| `store M` | Akümülatörün içeriğini `M` bellek hücresine kaydet |

`Val` bir sayı (örn. `1`) veya bellek etiketi (örn. `taban`) olabilir.  
`M` her zaman bir bellek etiketidir.

## Aritmetik

| Komut | İşlem |
|-------|-------|
| `add Val` | akümülatör ← akümülatör + Val |
| `sub Val` | akümülatör ← akümülatör − Val |
| `mul Val` | akümülatör ← akümülatör × Val |
| `div Val` | akümülatör ← akümülatör ÷ Val |
| `mod Val` | akümülatör ← akümülatör mod Val |

## Akış Kontrolü

| Komut | Açıklama |
|-------|----------|
| `goto L` | `L` etiketli satıra git |
| `ifpos L` | akümülatör ≥ 0 ise `L`'ye git |
| `ifzero L` | akümülatör = 0 ise `L`'ye git |
| `ifneg L` | akümülatör < 0 ise `L`'ye git |
| `stop` | Programı durdur |

## Bellek Başlangıç Değeri

```
etiket   sayi
```

Program başlamadan önce bellek hücrelerine ilk değer atar. Satır etiketi **ilk sütundan** başlar, komutlar en az bir boşluk bırakılarak yazılır.

---

## Sözdizimi Kuralları

- Komutlar **ilk sütundan başlamaz**; önünde en az bir boşluk/sekme bulunmalıdır.
- Satır etiketleri (goto hedefleri ve bellek adları) **ilk sütundan** başlar.
- `#` ile başlayan satırlar yorum satırıdır, göz ardı edilir.
- Program `stop` komutuyla biter.

---

## Örnek: Basit Toplama

```
basla   get
        store a
        get
        add a
        print
        stop
```

> Klavyeden iki sayı alır, toplamını yazdırır.
