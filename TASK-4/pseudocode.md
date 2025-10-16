BAŞLA
    // Giriş ve Kimlik Doğrulama
    YAZDIR "Üniversite Ders Kayıt Sistemine Hoş Geldiniz"
    
    // Giriş Kontrolü
    DOĞRU_ŞEKİLDE_GİRİŞ_YAP = YANLIŞ
    DENEME_SAYISI = 0
    MAKS_DENEME = 3
    
    DÖNGÜ DENEME_SAYISI < MAKS_DENEME VE DOĞRU_ŞEKİLDE_GİRİŞ_YAP == YANLIŞ
        OKU öğrenciNo
        OKU şifre
        
        EĞER kimlikDoğrula(öğrenciNo, şifre) == DOĞRU İSE
            DOĞRU_ŞEKİLDE_GİRİŞ_YAP = DOĞRU
            YAZDIR "Giriş başarılı!"
            ÖĞRENCİ_BİLGİ = getÖğrenciBilgileri(öğrenciNo)
        DEĞİLSE
            DENEME_SAYISI = DENEME_SAYISI + 1
            YAZDIR "Hatalı giriş! Kalan deneme: " + (MAKS_DENEME - DENEME_SAYISI)
        EĞER_BİTTİ
    DÖNGÜ_BİTTİ
    
    EĞER DOĞRU_ŞEKİLDE_GİRİŞ_YAP == YANLIŞ İSE
        YAZDIR "Çok fazla hatalı giriş. Sistemden çıkılıyor..."
        DURDUR
    EĞER_BİTTİ
    
    // Öğrenci bilgilerini al
    öğrenciID = ÖĞRENCİ_BİLGİ.id
    sınıf = ÖĞRENCİ_BİLGİ.sınıf
    danışmanID = ÖĞRENCİ_BİLGİ.danışmanID
    alınanKredi = ÖĞRENCİ_BİLGİ.toplamKredi
    
    // Genel kontroller
    EĞER kayıtEngeliKontrol(öğrenciID) == DOĞRU İSE
        YAZDIR "Kayıt engeliniz bulunuyor. İdari birime başvurun."
        DURDUR
    EĞER_BİTTİ
    
    EĞER kayıtDönemiKontrol() == YANLIŞ İSE
        YAZDIR "Kayıt dönemi dışındasınız."
        DURDUR
    EĞER_BİTTİ
    
    // Ders listesini getir
    DERS_LISTESİ = getUygunDersler(sınıf, öğrenciID)
    seçilenDersler = []
    toplamKredi = 0
    
    // Ders seçim döngüsü
    YAZDIR "Ders seçimine başlayabilirsiniz:"
    
    DÖNGÜ DOĞRU
        YAZDIR "Mevcut dersler:"
        I = 0 İKEN I < DERS_LISTESİ.uzunluk KADAR I = I + 1
            YAZDIR DERS_LISTESİ[I].kod + " - " + DERS_LISTESİ[I].ad + " (" + DERS_LISTESİ[I].kredi + " kredi)"
        DÖNGÜ_BİTTİ
        
        YAZDIR "İşlemler: [E]kle, [Ç]ıkar, [T]amam"
        OKU işlem
        
        EĞER işlem == "E" VEYA işlem == "e" İSE
            YAZDIR "Eklemek istediğiniz ders kodunu girin:"
            OKU dersKodu
            
            // Ders bulma
            ders = dersBul(DERS_LISTESİ, dersKodu)
            
            EĞER ders == BOŞ İSE
                YAZDIR "Geçersiz ders kodu!"
                DEVAM_ET
            EĞER_BİTTİ
            
            // Tüm kontrolleri yap
            hataVar = YANLIŞ
            
            // 1. Kontenjan kontrolü
            EĞER kontenjanKontrol(ders) == YANLIŞ İSE
                YAZDIR "Ders kontenjanı dolu!"
                hataVar = DOĞRU
            EĞER_BİTTİ
            
            // 2. Ön koşul kontrolü
            EĞER hataVar == YANLIŞ İSE
                EĞER önKoşulKontrol(öğrenciID, ders) == YANLIŞ İSE
                    YAZDIR "Ön koşul ders(ler)i tamamlamadınız!"
                    hataVar = DOĞRU
                EĞER_BİTTİ
            EĞER_BİTTİ
            
            // 3.
