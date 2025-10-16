BAŞLA
    // Sistem başlangıç ayarları
    sistemAktif = DOĞRU
    alarmDurumu = YANLIŞ
    tehditSeviyesi = 0
    
    // Sonsuz ana döngü
    DÖNGÜ DOĞRU
        // 1. Sistem aktif mi kontrolü
        EĞER sistemAktif == DOĞRU İSE
            
            // 2. Tüm sensörleri oku
            hareketVar = hareketSensörüOku()
            kapıAçık = kapıSensörüOku()
            pencereAçık = pencereSensörüOku()
            evSahibiEvde = evSahibiKontrolEt()
            
            // 3. Tehdit analizi
            EĞER alarmDurumu == YANLIŞ İSE
                // Alarm tetikleme kontrolleri
                EĞER hareketVar == DOĞRU VEYA kapıAçık == DOĞRU VEYA pencereAçık == DOĞRU İSE
                    
                    // Yanlış alarm kontrolü
                    EĞER evSahibiEvde == YANLIŞ İSE
                        // Alarm seviyesi belirleme
                        EĞER hareketVar == DOĞRU İSE
                            tehditSeviyesi = 3  // Yüksek
                        DEĞİLSE EĞER kapıAçık == DOĞRU İSE
                            tehditSeviyesi = 2  // Orta
                        DEĞİLSE
                            tehditSeviyesi = 1  // Düşük
                        EĞER_BİTTİ
                        
                        // Alarmı aktif et
                        alarmDurumu = DOĞRU
                        alarmSistemiAktifEt(tehditSeviyesi)
                        
                        // Bildirim gönderme
                        EĞER tehditSeviyesi >= 2 İSE
                            SMS_Gönder("Yüksek seviye güvenlik ihlali!")
                            Uygulama_Bildirimi_Gönder()
                        DEĞİLSE
                            Email_Gönder("Düşük seviye güvenlik uyarısı")
                        EĞER_BİTTİ
                    EĞER_BİTTİ
                EĞER_BİTTİ
                
            DEĞİLSE
                // Alarm aktif durumunda yapılacaklar
                // Kamera kaydı devam et
                kameraKaydıBaşlat()
                
                // Alarm sıfırlama kontrolü
                EĞER alarmSıfırlamaSinyali() == DOĞRU İSE
                    alarmDurumu = YANLIŞ
                    tehditSeviyesi = 0
                    alarmSistemiDurdur()
                    SMS_Gönder("Alarm sıfırlandı - Sistem normal modda")
                EĞER_BİTTİ
            EĞER_BİTTİ
            
            // 4. Bekleme ve sistem durumu kontrolü
            BEKLE(5000)  // 5 saniye bekle
            
        DEĞİLSE
            // Sistem pasif durumda
            BEKLE(10000)  // 10 saniye bekle
        EĞER_BİTTİ
        
        // 5. Sistem durumu değişiklik kontrolü
        EĞER uzaktanKomutVar() == DOĞRU İSE
            komut = uzaktanKomutOku()
            EĞER komut == "SISTEM_AKTIF" İSE
                sistemAktif = DOĞRU
            DEĞİLSE EĞER komut == "SISTEM_PASIF" İSE
                sistemAktif = YANLIŞ
                alarmDurumu = YANLIŞ
                alarmSistemiDurdur()
            EĞER_BİTTİ
        EĞER_BİTTİ
        
    DÖNGÜ_BİTTİ
SON
