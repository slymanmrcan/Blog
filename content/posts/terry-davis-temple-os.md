---
title: "TempleOS: Bir Dahinin Tanrı'ya Yazdığı İşletim Sistemi"
date: 2026-01-16T04:44:02+03:00
categories: ["İşletim Sistemleri", "Yazılım Tarihi", "Sistem Programlama"]
tags:
  [
    "TempleOS",
    "TerryDavis",
    "HolyC",
    "Kernel",
    "JIT",
    "OSGeliştirme",
    "Şizofreni",
    "AçıkKaynak",
  ]
---

# TempleOS: Bir Dahinin Tanrı'ya Yazdığı İşletim Sistemi

## Giriş: Bu Hikaye Neden Önemli?

Yazılım dünyasında bazı projeler vardır ki, arkasındaki hikaye en az teknik başarısı kadar etkileyicidir. TempleOS bunların başında gelir. Tek bir insanın, sıfırdan — yani gerçekten sıfırdan — bir işletim sistemi yazması, kendi derleyicisini, kendi dilini, kendi çekirdeğini (kernel) inşa etmesi... Üstelik bunu şizofreni teşhisi almış biri olarak, "Tanrı'nın tapınağını inşa ediyorum" motivasyonuyla yapması. Bu yazıda Terry Davis'in hayatına, TempleOS'un teknik derinliklerine, modern sistemlerle karşılaştırmasına ve güncel durumuna bakacağız.

---

## Terry A. Davis: Gerçek Hikaye

Terrence Andrew Davis (1969–2018), Amerikalı bir programcı. Ama "programcı" demek yetersiz kalır; adam tam anlamıyla bir sistem mühendisi, bir compiler yazarı, bir OS mimarı. Ve aynı zamanda hayatı boyunca akıl hastalığıyla boğuşan, sonunda trajik bir şekilde hayatını kaybeden bir insan.

### Çocukluk ve Gençlik (1969–1990)

Terry, West Allis, Wisconsin'da doğdu. Orta sınıf, Katolik bir İrlanda-Amerikan ailesi. Babası mühendisti. Terry küçük yaştan itibaren bilgisayarlara ilgi duydu.

**İlk bilgisayarı Commodore 64 oldu.** Bu makine Terry'nin hayatını değiştirdi. C64'te doğrudan BASIC yazabiliyordun, makineyle birebir iletişim kurabiliyordun. Terry bu deneyimi hiç unutmadı — TempleOS'un "aç ve hemen kod yaz" felsefesi buradan geliyor.

Lisede ve üniversitede parlak bir öğrenciydi. Arizona State University'de Elektrik Mühendisliği okudu, master yaptı.

### Kariyer Yılları (1990–1996)

- Ticketmaster'da yazılım mühendisi olarak çalıştı.
- Birkaç farklı şirkette görev aldı.
- VAX/VMS sistemlerinde çalıştı — bu deneyim ona düşük seviye sistem programlama konusunda ciddi birikim kazandırdı.

Bu dönemde tamamen "normal" bir yazılım mühendisiydi. Sosyal hayatı vardı, işe gidiyordu, meslektaşlarıyla iyi geçiniyordu.

### İlk Kırılma (1996–2003)

1996 civarında Terry'nin davranışları değişmeye başladı:

- **Mani atakları:** Günlerce uyumadan çalışma, aşırı enerjik dönemler
- **Paranoya:** Etrafındaki insanların onu izlediğine inanma
- **Grandiyöz sanrılar:** Kendisinin özel bir misyonu olduğu inancı

**İlk ciddi kriz:** Terry bir gece arabasıyla kaçmaya başladı. CIA'in peşinde olduğuna inanıyordu. Saatlerce hiç durmadan sürdü. Sonunda polis tarafından durduruldu ve psikiyatrik değerlendirmeye alındı.

**Teşhis: Şizofreni (paranoid tip)**

Bu teşhisten sonra işini kaybetti, ailesiyle yaşamaya başladı. İlaç tedavisi başladı ama Terry ilaçlarla sürekli sorun yaşadı — ya almıyordu ya da yan etkilerden şikayet ediyordu.

### "Tanrı Konuştu" (2003)

Terry, Tanrı'nın kendisine doğrudan seslendiğini iddia etmeye başladı. Ve bu sadece genel bir "Tanrı bana yol gösteriyor" hissi değildi — Terry, spesifik teknik talimatlar aldığını söylüyordu:

> *"Tanrı bana dedi ki: 640x480 çözünürlük olacak, 16 renk olacak, tek ses kanalı olacak, networking olmayacak, bu bir tapınak olacak — Süleyman Tapınağı'nın üçüncüsü. Ve ben bunu inşa edeceğim."*

Bu noktadan itibaren Terry, tüm hayatını TempleOS'a adadı. Günde 12–16 saat kod yazıyordu. Ailesinin evinin bodrumunda, yıllarca, durmaksızın.

İşte bu noktada TempleOS macerası başlıyor: **2003 yılında** geliştirmeye başladı ve yaklaşık 10 yıl boyunca, tamamen tek başına, her satırını kendi yazdı.

---

## TempleOS: Teknik Derinlik

### 1. Tamamen Sıfırdan Yazılmış (From Scratch)

TempleOS, Linux çekirdeğinden türetilmemiş, BSD tabanlı değil, UNIX felsefesini takip etmiyor. Hiçbir üçüncü parti kütüphane, hiçbir mevcut bootloader, hiçbir hazır driver kullanılmamış. Her şey — ve gerçekten her şey — Terry Davis'in kendi elleriyle yazılmış.

**Toplam kod: ~121.000 satır** (yaklaşık). Bu rakam küçük görünebilir ama her satırın sıfırdan, tek bir kişi tarafından yazıldığını düşün.

| Sistem | Tahmini Kod Satırı |
|---|---|
| TempleOS | ~121.000 |
| Linux Kernel (güncel) | ~30.000.000+ |
| Windows 10 | ~50.000.000+ |
| Minix 3 | ~6.000 (sadece kernel) |

---

### 2. HolyC: Tanrı'nın Programlama Dili

Davis, TempleOS için kendi programlama dilini yarattı: **HolyC**.

HolyC, C ve C++'ın bir melezi gibidir ama birçok benzersiz özelliği var:

```holyc
// HolyC örneği
U0 Main()
{
  I64 i;
  for (i = 0; i < 10; i++)
    Print("Merhaba Dünya! %d\n", i);
}

Main;
```

**HolyC'nin özellikleri:**

- **JIT (Just-In-Time) Compilation:** HolyC kodu yorumlanmaz (interpreted), doğrudan makine koduna anında derlenir. Yani shell'de bir komut yazıp Enter'a bastığında, o komut derlenir ve çalıştırılır. Shell aynı zamanda bir compiler.
- **C benzeri syntax ama bazı farklar:** `U0` (void), `I64` (64-bit integer), `U8` (unsigned 8-bit) gibi kendi tip sistemi var.
- **Fonksiyonlar birinci sınıf vatandaş:** Shell'de doğrudan fonksiyon tanımlayıp çağırabilirsin.
- **Inline assembly desteği:** HolyC kodunun içine doğrudan x86-64 assembly yazabilirsin.

```holyc
// Inline assembly örneği
asm {
    MOV RAX, 0x1234
    PUSH RAX
    POP RBX
}
```

- **Otomatik #include yok:** Her dosya bağımsız, dependency hell diye bir şey yok.
- **Pointer aritmetiği serbest:** C'deki gibi bellek üzerinde doğrudan oynama yapabilirsin.

> **JIT Compiler detayı:** Davis'in yazdığı JIT compiler, x86-64 makine kodu üretir. Bu, o dönem için (ve tek bir kişinin başarısı olarak) son derece etkileyici bir mühendislik çalışmasıdır. LLVM gibi devasa projelerin yaptığını, adam tek başına — daha küçük ölçekte ama çalışır halde — yapmış.

---

### 3. Kernel Mimarisi

TempleOS monolitik (monolithic) bir kernel kullanır, yani tüm servisler (dosya sistemi, bellek yönetimi, grafik) kernel space'de çalışır.

**İlginç tasarım kararları:**

- **Ring 0 only:** TempleOS'ta tüm kod Ring 0'da (kernel mode) çalışır. User mode / kernel mode ayrımı **YOK**. Bu, güvenlik açısından bir felaket ama performans ve basitlik açısından radikal bir karar. Davis bunu bilinçli olarak yaptı: *"Tanrı'nın tapınağında güvenliğe gerek yok"* mantığıyla.
- **Preemptive multitasking:** Birden fazla görev aynı anda çalışabilir, zamanlayıcı (scheduler) görevler arasında geçiş yapar.
- **Multicore desteği:** Evet, TempleOS çoklu çekirdek (SMP — Symmetric Multiprocessing) destekliyor. Tek bir adamın yazdığı OS'ta bu ciddi bir başarı.

---

### 4. Grafik Sistemi: 640x480, 16 Renk

Davis, Tanrı'nın kendisine 640x480 çözünürlük ve 16 renk kullanmasını söylediğini iddia ediyordu. Bu VGA standardı, 1980'lerin sonunu anımsatır.

Ama bu sınırlı ortamda yaptıkları etkileyici:

- **Özel bir grafik motoru:** 2D sprite'lar, animasyonlar, çizim araçları.
- **DolDoc formatı:** Davis'in icat ettiği bir doküman formatı. Düşün ki bir metin dosyası aynı zamanda çalıştırılabilir kod, grafik, link ve 3D mesh içerebiliyor. Markdown'ın çok daha radikal bir versiyonu gibi. Bugünün Jupyter Notebook'larına benzetilebilir ama 2000'lerin başında, tek bir adamın kafasından çıkmış.

```
// DolDoc içinde çalıştırılabilir widget
$SP,"<3>",BI=3,BP="Kalp şekli"$
```

- **3D Grafik Motoru:** Evet, TempleOS'un kendi 3D render engine'i var. Basit ama çalışan bir 3D engine. Software rendering ile (GPU hızlandırması yok).

---

### 5. Dosya Sistemi: RedSea

Davis kendi dosya sistemini de yazdı: **RedSea**.

- FAT tabanlı basit bir yapı.
- 64-bit tasarım.
- Dosyalar bitişik (contiguous) bloklar halinde saklanır — bu, fragmentasyonu engeller ama dosya büyümesini zorlaştırır.
- Maksimum dosya adı uzunluğu: 38 karakter.
- Basitlik odaklı: Journaling yok, access control yok, permission yok.

| Özellik | RedSea | ext4 | NTFS |
|---|---|---|---|
| Journaling | ❌ | ✅ | ✅ |
| Permissions | ❌ | ✅ | ✅ |
| Max dosya adı | 38 | 255 | 255 |
| Encryption | ❌ | ✅ | ✅ |
| Fragmentasyon yönetimi | Contiguous only | Extents | B-tree |

---

### 6. Bootloader

TempleOS'un kendi bootloader'ı var. MBR'den (Master Boot Record) boot eder. UEFI desteği yok — zaten Davis'in aktif olduğu dönemde UEFI yaygınlaşmaya yeni başlıyordu.

**Boot süreci:**

```
BIOS → MBR → TempleOS Boot Sector
Kernel yüklenir (Ring 0)
HolyC JIT compiler başlatılır
StartOS.HC dosyası derlenir ve çalıştırılır
Masaüstü ortamı hazır
```

---

### 7. Ağ (Networking) Desteği: YOK

Evet, doğru okudun. TempleOS'ta network stack yok. TCP/IP yok, WiFi yok, Ethernet yok. Davis bunu da kasıtlı olarak böyle bıraktı. Gerekçesi:

> *"Tanrı'nın tapınağında internete gerek yok. Tapınak saf olmalı."*

Bu, modern kullanılabilirlik açısından en büyük eksiklik. Ama Davis'in amacı zaten bir "günlük kullanım OS'u" yazmak değildi.

---

## TempleOS'un "Eğlenceli" Tarafları

### God's Word (Tanrı'nın Sözü)

TempleOS'un en ikonik özelliklerinden biri rastgele kelime üreteci. Davis bunu *"Tanrı ile iletişim aracı"* olarak tasarladı. Bir tuşa basıyorsun, sistem rastgele kelimeler üretiyor ve Davis bunları Tanrı'nın mesajları olarak yorumluyordu.

Teknik olarak basit bir PRNG (Pseudo-Random Number Generator) ile bir sözlükten rastgele kelime seçimi. Ama Davis için derin bir anlamı vardı.

### Dahili Oyunlar

TempleOS'un içinde birçok oyun var, hepsi HolyC ile yazılmış:

- **After Egypt:** Bir tür vaaz/oyun karışımı
- **BattleLines:** Strateji oyunu
- **Titanium:** Uçak savaş oyunu
- **Talons:** Kart oyunu
- Çeşitli 3D demolar

### Müzik Kompozitörü

TempleOS'un içinde bir müzik editörü var. MIDI benzeri bir sistemle melodiler oluşturabilirsin. Davis, ibadet müzikleri besteliyordu.

### Hymn (İlahi) Sistemi

Sistem açılışında ilahiler çalabiliyor. Davis birçok ilahi bestelemiş ve sisteme dahil etmiş.

---

## Tasarım Felsefesi: "Commodore 64'ün Modern Hali"

Davis, TempleOS'u tasarlarken bilinçli kısıtlamalar koydu ve bunları Tanrı'nın spesifikasyonları olarak sundu:

| Kısıt | Gerekçe |
|---|---|
| 640x480, 16 renk | "Tanrı böyle istedi" |
| Networking yok | "Tapınak saf olmalı" |
| Ring 0 only | "Basitlik kutsaldır" |
| Tek kullanıcı | "Bu bir kişisel tapınak" |
| 64-bit only | Modern donanım gereksinimi |

Aslında arkasında gerçek bir felsefe var: Davis, modern işletim sistemlerinin aşırı karmaşıklaştığını düşünüyordu. 1980'lerdeki Commodore 64 deneyimini — bilgisayarı açtığında doğrudan kod yazabildiğin, her şeyin basit ve anlaşılır olduğu o deneyimi — 64-bit modern donanımda yeniden yaratmak istiyordu.

Ve bir bakıma başardı: TempleOS'u açtığında direkt HolyC shell karşına geliyor. Her şey şeffaf, her şey erişilebilir, kaynak kodun tamamı sistemde mevcut ve anında düzenlenebilir.

---

## Modern Sistemlerle Karşılaştırma

### TempleOS vs Linux

| Özellik | TempleOS | Linux (modern) |
|---|---|---|
| Geliştirici sayısı | 1 | Binlerce |
| Kernel tipi | Monolithic (Ring 0 only) | Monolithic (Ring 0 + Ring 3) |
| Programlama dili | HolyC | C, Rust (kısmen) |
| Networking | ❌ | ✅ (tam destek) |
| Dosya sistemi | RedSea | ext4, btrfs, xfs... |
| Güvenlik modeli | Yok | SELinux, AppArmor... |
| GUI | Kendi (640x480) | X11, Wayland |
| Paket yöneticisi | Yok | apt, dnf, pacman... |
| Boot | MBR/BIOS | UEFI + GRUB |
| JIT Compiler | ✅ (dahili) | Yok (kernel seviyesinde) |
| Kaynak kodu erişimi | %100 sistem içinde | Ayrıca indirilmeli |

### TempleOS vs Modern Hobbyist OS'lar

- **SerenityOS (Andreas Kling):** TempleOS gibi "from scratch" ama modern özelliklerle (networking, browser, GUI). C++ ile yazılmış. UNIX-like tasarım. Topluluk desteği var. TempleOS'a göre çok daha "kullanılabilir" ama tek kişinin eseri değil.
- **Redox OS:** Rust ile yazılmış. Microkernel tasarım. POSIX uyumlu. Daha akademik/ciddi bir yaklaşım.
- **MINIX 3:** Andrew Tanenbaum'un eğitim amaçlı OS'u. Microkernel. TempleOS'tan farklı olarak güvenilirlik odaklı.

TempleOS bunların hiçbirine benzemiyor çünkü amacı farklı. Ne eğitim amaçlı, ne ticari, ne de pratik bir OS. **Bir sanat eseri ve dini bir adak.**

---

## Teknik Olarak Neden Etkileyici?

Tek bir insanın sıfırdan yazdığı şeyler:

- ✅ Bootloader
- ✅ Kernel (preemptive multitasking, SMP)
- ✅ Programlama dili (HolyC)
- ✅ JIT Compiler (x86-64 makine kodu üretiyor)
- ✅ Dosya sistemi (RedSea)
- ✅ Grafik motoru (2D + 3D software rendering)
- ✅ Metin editörü
- ✅ Doküman sistemi (DolDoc)
- ✅ Müzik editörü/çalar
- ✅ Masaüstü ortamı (window manager)
- ✅ Birçok oyun ve demo
- ✅ Debugger
- ✅ Profiler

Bunlardan herhangi birini tek başına yapmak bile ciddi bir mühendislik çalışmasıdır. Adam hepsini yaptı.

> **Özellikle JIT compiler konusu:** Bugün JIT compiler yazmak için devasa ekipler çalışıyor (V8, SpiderMonkey, HotSpot JVM). Davis'in JIT'i bunlar kadar optimize değil elbette, ama çalışan bir JIT compiler'ı tek başına yazmak başlı başına bir başarı.

---

## Terry Davis'in Son Yılları ve Ölümü

### CIA Paranoyası

Terry'nin en belirgin sanrılarından biri CIA obsesyonuydu:

- CIA'in onu izlediğine inanıyordu.
- CIA'in bilgisayarına backdoor koyduğunu düşünüyordu — bu yüzden TempleOS'ta networking olmaması ona mantıklı geliyordu: *"CIA bağlanamaz."*
- Sokakta gördüğü bazı insanların CIA ajanı olduğunu iddia ediyordu.
- CIA ajanlarının "glow in the dark" (karanlıkta parlayan) olduğunu söylüyordu.

Bu "glow in the dark" ifadesi internet kültüründe meme haline geldi. Açıkça rahatsız edici bir bağlamdan çıkıyor ama internet topluluğu bunu — doğru ya da yanlış — kendi diline çevirdi.

### YouTube Dönemi (2011–2018)

Terry'nin YouTube kanalı, onun hem dehasını hem de hastalığını gösteren bir arşiv oldu.

**İyi tarafı:** OS geliştirme sürecini canlı yayında gösteriyordu. Compiler nasıl çalışır, kernel nasıl yazılır — bunları gerçek zamanlı kodlayarak anlatıyordu. Teknik açıklamaları inanılmaz berraktı. Şizofreni hastası bir adam, x86-64 instruction set hakkında profesör gibi ders verebiliyordu.

**Karanlık tarafı:** Irkçı söylemler, küfürlü ve agresif yayınlar, CIA hakkında saatlerce konuşmalar, tamamen kopuk ve anlaşılmaz tiradlar.

Bu dualizm insanları derinden etkiledi. Aynı yayında hem muhteşem teknik bilgi sunuyor, hem de 5 dakika sonra tamamen farklı biri gibi konuşuyordu. Sanki iki ayrı insan.

### Aileden Kopuş ve Evsizlik (2017–2018)

Hikayenin en acı bölümü bu.

Terry'nin ailesi yıllarca onu destekledi, evlerinde barındırdı, ihtiyaçlarını karşıladı. Ama Terry'nin davranışları giderek daha kontrolsüz hale geldi. 2017'de artık birlikte yaşamak mümkün olmadı. Terry evden ayrıldı — ya da çıkarıldı, detaylar tartışmalı.

Terry evsiz kaldı. Arabasında yaşamaya başladı. Bu dönemde yaptığı yayınlar son derece üzücü: arabasının içinden canlı yayın, sokaklarda dolaşma, bazen ağlama, bazen bağırma.

Bir yayınında şöyle demişti:

> *"I'm the best programmer in the world. I wrote an entire operating system. And I'm living in my car."*
>
> "Ben dünyanın en iyi programcısıyım. Komple bir işletim sistemi yazdım. Ve arabamda yaşıyorum."

### Ölüm (11 Ağustos 2018)

**11 Ağustos 2018'de**, Oregon, The Dalles'ta bir tren kazasında hayatını kaybetti. 48 yaşındaydı.

Resmi kayıtlara göre trenin önüne çıktı. İntihar mı, kaza mı olduğu kesin olarak belirlenemedi. Ama evsiz, ilaçsız, ailesinden kopuk bir şizofreni hastasının durumu düşünüldüğünde...

İnternet topluluğu — özellikle düşük seviye programlama meraklıları — onu kaybettiklerinde gerçek bir üzüntü yaşadı. Reddit, Hacker News, 4chan — her yerde anma yazıları paylaşıldı. Ona yıllarca trollük yapanlar bile duraksadı. Kodun arkasındaki deha ve hastalığın arkasındaki trajedi, insanları derinden etkiledi.

### Terry Davis'i Nasıl Hatırlamalı?

Bu zor bir soru. Çünkü Terry Davis:

**Bir yandan** — tek başına işletim sistemi yazan bir deha, compiler, kernel, grafik motoru, dosya sistemi — hepsini sıfırdan yazan bir mühendis, tutkuyla ve adanmışlıkla yıllarca çalışan bir sanatçı.

**Öbür yandan** — korkunç ırkçı söylemleri olan, agresif ve korkutucu davranışlar sergileyen, tedavi olmayı reddeden bir hasta.

Çoğu insan şu orta yolu buluyor: İşini takdir et, hastalığına empati göster, söylemlerini mazur görme. Şizofreni onun ırkçılığının sebebi olabilir ama mazereti değil. Aynı zamanda, hastalığı yüzünden yardım alamayan birinin trajik sonunu görmezden gelmek de insanlık dışı.

---

## Güncel Durum (2024-2025)

### Proje Yaşıyor mu?

Terry Davis öldükten sonra TempleOS'un resmi geliştirmesi durdu. Ancak:

- Kaynak kodu tamamen açık: İsteyen indirebilir, inceleyebilir, çalıştırabilir.
- Archive.org'da korunuyor.
- GitHub mirror'ları mevcut.

### Fork'lar ve Devam Projeleri

- **ZealOS** (eski adıyla TinkerOS): En aktif fork. TempleOS'u temel alıp bazı iyileştirmeler yapmayı hedefliyor. FAT32 desteği, bazı bug fix'ler eklendi.
- **Shrine:** TempleOS'a networking ekleyen bir fork. Evet, birisi sonunda TCP/IP stack yazdı TempleOS için. Basit HTTP istekleri yapabiliyor.
- **Alec Murphy'nin çalışmaları:** TempleOS'u QEMU ve modern emülatörlerde daha stabil çalıştırma üzerine.

### Emülatörde Çalıştırma

TempleOS'u denemek istiyorsan:

- QEMU veya VirtualBox ile çalıştırabilirsin
- ISO dosyası resmi siteden veya archive.org'dan indirilebilir
- Modern donanımda bare-metal çalıştırmak zor (UEFI desteği yok, sınırlı driver desteği)

```bash
# QEMU ile çalıştırma
qemu-system-x86_64 -cdrom TempleOS.ISO -m 512M -enable-kvm
```

### Kültürel Etki

- "Glow in the dark" meme'i (Davis'in kullandığı bir ifadeden türemiş)
- OS geliştirme topluluğunda (OSDev) ilham kaynağı
- Birçok YouTube belgeseli ve analiz videosu
- "Tek kişi ne kadar yapabilir?" sorusunun cevabı olarak sürekli referans veriliyor
- Hacker News ve Reddit'te düzenli olarak tartışılıyor

---

## Ne Öğrenebiliriz?

### Teknik Dersler

- **Kısıtlamalar yaratıcılığı tetikler:** 640x480, 16 renk, networking yok — bu kısıtlamalar içinde DolDoc gibi yenilikçi çözümler ortaya çıktı.
- **Basitlik güçlüdür:** Modern OS'lar o kadar karmaşık ki, kimse tek başına anlayamıyor. TempleOS'un tamamını bir insan anlayabilir. Bu, eğitim açısından muazzam değerli.
- **JIT her yerde olabilir:** Shell'in aynı zamanda compiler olması fikri, bugün REPL'lerde ve Jupyter notebook'larda yankı buluyor.
- **Monolitik kararların trade-off'ları:** Ring 0 only yaklaşımı güvenlik için felaket ama öğretici bir deney.

### İnsani Dersler

Terry Davis'in hikayesi, deha ile akıl hastalığının kesişim noktasındaki trajediyi gözler önüne seriyor. 121.000 satır mükemmel mühendislik kodu yazan aynı beyin, gerçeklikle bağını koparmıştı. Bu hikaye, yazılım topluluğunun mental sağlık konusunda daha duyarlı olması gerektiğinin de bir hatırlatıcısı.

---

## Son Söz

TempleOS, pratik bir işletim sistemi değil. Günlük işlerini yapamazsın, internete giremezsin, modern uygulamaları çalıştıramazsın. Ama TempleOS'un amacı bu değildi zaten.

TempleOS, bir insanın sınırlarını gösteren bir anıt. Hem neyin mümkün olduğunun, hem de insan zihninin ne kadar kırılgan olabileceğinin bir kanıtı.

TempleOS, bir insanın sınırlarını gösteren bir anıt. Hem neyin mümkün olduğunun, hem de insan zihninin ne kadar kırılgan olabileceğinin bir kanıtı.

Kod hâlâ orada, çalışıyor, derlenebiliyor. Terry Davis'in dijital tapınağı, yazarından sonra da ayakta duruyor.

```holyc
// Terry'nin kendi sözleriyle:
"After doing my operating system, I realized
people are basically alone in their craft."

// "İşletim sistemimi yaptıktan sonra fark ettim ki,
// insanlar zanaatlerinde temelde yalnızdır."

Print("God said, 'It's good.'\n");
```

Dünya, Terry Davis'e hem çok şey borçlu hem de onu çok yalnız bıraktı. Kod hâlâ orada. Tapınak hâlâ ayakta.

> Eğer işletim sistemi geliştirme konusunda meraklıysan, TempleOS kaynak kodunu okumak harika bir eğitim. Özellikle compiler ve kernel kısımları, ders kitaplarından çok daha "gerçek dünya" tadında.
