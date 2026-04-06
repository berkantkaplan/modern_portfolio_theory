# Markowitz Portföy Optimizasyonu

Modern Portföy Teorisi uygulanarak Sharpe Ratio maksimizasyonu ile optimal portföy oluşturulması üzerine temel bir uygulama. 2020 itibarıyla yfinance'den çekilen verilerin logaritmik getirileri hesaplanmış, ardından **Ledoit-Wolf metodu** ile varlıkların kovaryans matrisi bulunmuştur.

---

## Varlık Evreni

| Sektör | Varlıklar |
|--------|-----------|
| Teknoloji | AAPL, TSLA, AMZN, MSFT, GOOGL |
| Perakende | WMT, NKE |
| Enerji | BE |
| Büyüme | PLTR, LITE |
| Bitcoin | MSTR |
| Emtia | GLD (Ons Altın) |
| Tahvil | TLT (ABD Tahvili) |

---

## Optimizasyon

**Scipy SLSQP** optimizer'ı ile Sharpe Ratio maksimizasyonu yapıldı. Tek bir varlıkta yoğunlaşmayı önlemek için üst sınır **%25** olarak belirlendi.

| Varlık | Ağırlık |
|--------|---------|
| AMZN | %25.0 |
| WMT | %25.0 |
| GLD | %25.0 |
| MSTR | %14.8 |
| LITE | %10.2 |

> Üst sınır %25 olmasına rağmen optimizer, AMZN, WMT ve GLD'ye maksimum ağırlığı verdi. Portföyün %75'i bu 3 varlıktan oluştu.

---

## Backtest (2020-10-02 / 2026-04-02)

| Metrik | Değer |
|--------|-------|
| Yıllık Getiri | %27.92 |
| Max Drawdown | -%34.38 |
| Beta | 0.90 |
| Alpha | 0.15 |
| Sharpe Ratio | 1.34 |

2020-10-02 tarihinde oluşturulan bu portföy, SPY'den daha az volatil olmakla birlikte 2021 ilk çeyreğinden 2024 dördüncü çeyreğine kadar SPY'nin altında kalmış. 2021-11-05'te zirveye ulaşan portföyün -%34.38 düşerek 2024-05-16'ya kadar toparlanamamış olması psikolojik açıdan taşıması zor bir portföy olduğu yorumu yapılabilir. Son olarak, 2025 başından itibarense SPY'yi belirgin şekilde geride bırakıyor. Bu da portföy performansının büyük ölçüde varlık seçimine ve piyasa koşullarına bağlı olduğunu gösteriyor.

---

## Monte Carlo Simülasyonu (1000 Senaryo, 252 Gün)

| Metrik | Değer |
|--------|-------|
| Ortalama Getiri | %35 |
| En İyi %5 Senaryo | %82 |
| En Kötü %5 Senaryo | -%5 |
| Kayıp Olasılığı | %8.3 |

---

## Değerlendirme

Model %25 GLD önerse de 2025-2026 döneminde altının savaş ortamında dahi düşmesi ve fiyat hareketlerinde merkez bankası alımlarının belirleyici rol oynaması, altının klasik güvenli liman özelliğini her koşulda taşımadığını düşündürtüyor. Fiyat hareketlerinde merkez bankası alımlarının etkili olduğu göz önünde bulundurulduğunda, %25 GLD oranı portföy riski açısından yüksek olarak değerlendirilebilir.

ABD Başkanı Trump'ın yeni FED başkanının faizleri indirmesini talep etmesi ve savaş sonrası normalleşme döneminde faiz indirim beklentilerinin güçlenebileceği göz önünde bulundurulduğunda, modelin portföye eklemediği TLT'nin 2026 ortasından itibaren değer kazanabileceği düşünülmektedir.

Varlık kümesinde hem TLT hem BND test edilmiş olsa da her ikisi de optimizer tarafından seçilmemiştir. Bu durum, analiz dönemindeki faiz artış ortamının tahvil getirilerini olumsuz etkilemesinden kaynaklanıyor olabilir.

Model yalnızca geçmiş fiyat hareketlerine dayandığından makroekonomik değişkenleri, jeopolitik riskleri ve irrasyonel piyasa davranışlarını göz ardı etmektedir. Buna ek olarak, sunulan varlık kümesi sektör çeşitliliği açısından sınırlı kalmıştır. Daha geniş ve çeşitliliği yüksek bir varlık kümesi ve makro faktörlerin modele dahil edilmesi, daha dengeli bir portföy dağılımı üretebilir.
