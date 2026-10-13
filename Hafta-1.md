[Oyuncak Makine](https://toy.emrecan.dev/)

## 1. Üs alma — $a^b$

Klavyeden önce taban, sonra üs alınır. Çarpma işlemi döngü içerisinde tekrarlanır. Üs negatif olmayan bir tam sayı olmalıdır.

```
basla   get
        store taban
        get
        store us
        load us
        ifneg hata
        load 1
        store sonuc

dongu   load us
        ifzero bitir
        load sonuc
        mul taban
        store sonuc
        load us
        sub 1
        store us
        goto dongu

bitir   load sonuc
        print
        stop

hata    load 0
        print
        stop
```

**Adım adım izle:**
- `taban = 3`, `us = 4` gir → beklenen çıktı: `81`
- `taban = 2`, `us = 0` gir → beklenen çıktı: `1`
- `taban = 5`, `us = 1` gir → beklenen çıktı: `5`

---

## 2. Faktöriyel — $n!$

Klavyeden negatif olmayan bir tam sayı alınır ve $n \times (n-1) \times \cdots \times 1$ hesaplanır.

```
basla   get
        store n
        load n
        ifneg hata
        load 1
        store sonuc

dongu   load n
        ifzero bitir
        load sonuc
        mul n
        store sonuc
        load n
        sub 1
        store n
        goto dongu

bitir   load sonuc
        print
        stop

hata    load 0
        print
        stop
```

**Adım adım izle:**
- `n = 5` gir → beklenen çıktı: `120`
- `n = 0` gir → beklenen çıktı: `1`
- `n = 1` gir → beklenen çıktı: `1`

---

## Sorular

1. Üs alma programında `sonuc` neden `1` ile başlatılıyor? `0` ile başlatsaydık ne olurdu?
2. Faktöriyel programında döngü kaç kez dönüyor? `n = 5` için adımla çalıştırarak say.
3. İki program arasındaki yapısal benzerlik nedir?
