# Hafta 5

## Sınıf notları — Örnek ekran çıktıları

Program sırasıyla **geçen öğrenci sayısını**, **kalan öğrenci sayısını** ve **not ortalamasını** yazdırır.

### Örnek 1

Girdi: `85, 40, 50, 0, 75, 50, -1`

Ekran çıktısı:

```text
4
2
50
```

### Örnek 2

Girdi: `90, 30, -1`

Ekran çıktısı:

```text
1
1
60
```

### Örnek 3

Girdi: `0, -1`

Ekran çıktısı:

```text
0
1
0
```

`-1` hesaplamaya katılmaz. `0` geçerli bir nottur; `50` alan öğrenci geçer.

## Ruby ile Merhaba Dünya

Ruby kodu iki işletim sisteminde de aynıdır. Dosya oluşturma komutu ve masaüstü yolu farklıdır. Ruby'nin yüklü olduğunu `ruby --version` ile kontrol edebilirsiniz.

## Ubuntu

1. Terminalde masaüstünde boş dosya oluşturun:

```bash
touch ~/Masaüstü/Hello.rb
```

Masaüstü klasörünüzün adı İngilizceyse `Masaüstü` yerine `Desktop` yazın.

2. `Hello.rb` dosyasını bir metin düzenleyicide açın, aşağıdaki kodu yazıp kaydedin:

```ruby
puts "Merhaba dünya"
```

3. Terminalden çalıştırın:

```bash
ruby ~/Masaüstü/Hello.rb
```

## Windows (PowerShell)

Windows Terminal içinde PowerShell sekmesini açın.

1. Masaüstüne geçip dosyayı Not Defteri ile açın:

```powershell
cd ~/Desktop
notepad Hello.rb
```

Dosyayı oluşturmak için sorarsa **Evet** deyin. Masaüstünüz OneDrive içindeyse ilk komut olarak `cd ~/OneDrive/Desktop` kullanın.

2. Aşağıdaki kodu yazıp UTF-8 kodlamasıyla kaydedin:

```ruby
puts "Merhaba dünya"
```

3. Aynı PowerShell penceresinde çalıştırın:

```powershell
ruby Hello.rb
```

`ruby` komutu tanınmıyorsa Ruby kurulu olmayabilir veya PATH'e eklenmemiş olabilir.

## Beklenen çıktı

```text
Merhaba dünya
```

Bu örnek metni terminale yazdırır. Örnek kod bu klasördeki [Hello.rb](Hello.rb) dosyasında da bulunur.
