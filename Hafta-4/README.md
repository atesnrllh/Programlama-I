# Oyuncak Makine — Lab Dersi

[Simülatör: toy.emrecan.dev](https://toy.emrecan.dev/)

Bu ders, bilgisayarın içinde kodun nasıl işlendiğini göstermek amacıyla tasarlanmış bir giriş laboratuvarıdır. Gerçek bir işlemcinin çalışma mantığını basitleştirilmiş bir simülatör üzerinde öğreniyoruz.

## İçerik

| Dosya | Konu |
|-------|------|
| [00-Kavramlar.md](00-Kavramlar.md) | İşlemci, RAM, akümülatör nedir? |
| [01-Komutlar.md](01-Komutlar.md) | Oyuncak Makine komut referansı |
| [02-Alistirmalar.md](02-Alistirmalar.md) | Alıştırmalar: Üs alma, Faktöriyel |

## Nasıl çalışılır?

1. [toy.emrecan.dev](https://toy.emrecan.dev/) adresini aç
2. Kaynak kod alanına programı yaz
3. **Çalıştır** ile direkt çalıştır, **Adımla** ile adım adım takip et
4. Bellek ve akümülatör değerlerini gözlemle

> **Adımla butonu tepki vermiyorsa** aşağıdaki "Bilinen sorun" bölümüne bak.

---

## Bilinen Sorun: Adımla butonu çalışmıyor

**Belirti:** **Çalıştır** ve **Baştan al** çalışıyor, ama **Adımla**'ya basınca hiçbir şey olmuyor. `get` komutunda sayı soran pencere de açılmıyor. Sorun Chrome'da da Firefox'ta da aynı.

**Neden:** Butonun kodu `onclick="step()"` şeklinde yazılmış. Tarayıcı bu ismi önce butonun kendi özelliklerinde arıyor. Güncel HTML'de her `<input>` elemanının `step` adında bir özelliği olduğu için sitedeki `step` fonksiyonu yerine bu boş özellik çağrılıyor. Konsolda şu hata görünür:

```
Uncaught TypeError: step is not a function
```

### Geçici çözüm (her öğrenci kendi tarayıcısında)

1. [toy.emrecan.dev](https://toy.emrecan.dev/) sayfasını aç.
2. Klavyede **F12**'ye bas. Sağda veya altta geliştirici araçları paneli açılır.
3. Panelin üstündeki sekmelerden **Console**'a tıkla (Elements sekmesinin hemen sağında). Firefox'ta bu sekmenin adı **Konsol**.
4. Panelin en altında `>` işaretli boş bir satır var. Oraya tıkla.
5. Şu satırı kopyalayıp yapıştır ve **Enter**'a bas:

   ```js
   document.querySelector('input[value="Adımla"]').onclick = () => window.step();
   ```

6. Tarayıcı yapıştırmaya izin vermeyip bir uyarı gösterirse, uyarıda yazmanı istediği ifadeyi yaz ve **Enter**'a bas. İngilizce arayüzde bu ifade `allow pasting`. Ardından 5. adımdaki satırı tekrar yapıştır.
7. Konsol panelini açık bırakabilir ya da **F12** ile kapatabilirsin.

### Adımla'yı kullanma

1. Kaynak kod alanına programını yaz.
2. **Baştan al**'a bir kez bas. **Sonraki komut** kutusunda ilk komut görünür (örneğin `1:basla get`).
3. Her **Adımla** tıklamasında tek bir komut çalışır. Her adımdan sonra **Sonraki komut**, **Akümülatör** ve **Bellek** alanlarını izle.
4. `get` komutunda sayı soran pencere açılır. Sayıyı yazıp **Tamam**'a bas. Pencereyi boş bırakır ya da **İptal**'e basarsan program durur.
5. Program `stop` komutuna ulaşınca biter. Sonra **Adımla**'ya basarsan çıktıda `no next step` yazar. Yeniden başlamak için **Baştan al**'a bas.

> **Dikkat:** Bu düzeltme sayfa yenilenene kadar geçerli. Sayfayı yenilersen (F5) veya yeniden açarsan 2–6. adımları tekrarla.

### Kalıcı çözüm (siteyi yöneten kişi için)

Sitenin `index.html` dosyasındaki Adımla butonunda `step()` çağrısını `window.step()` olarak değiştirmek yeterli:

```html
<input type="button" value="Adımla" onclick="window.step()">
```
