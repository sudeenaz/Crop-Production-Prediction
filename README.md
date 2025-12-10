# Crop Production Prediction

Bu proje, tarımsal üretim tahmini üzerine hazırlanmış bir makine öğrenmesi çalışmasıdır. Hedefimiz, **Paddy yield (kg)** değerini tahmin ederek tarımsal üretim planlamasına katkı sağlamak ve verimlilik analizlerini kolaylaştırmaktır.

---

## Proje Amacı

Tarımda verim tahmini, kaynak yönetimi ve üretim planlaması açısından kritik öneme sahiptir. Bu proje ile amaçlananlar:

1. Geçmiş tarımsal verileri kullanarak verim tahmini yapmak  
2. Farklı makine öğrenmesi algoritmalarının performansını karşılaştırmak  
3. Üretimi etkileyen başlıca faktörleri ortaya koymak

Bu sayede çiftçiler ve tarım planlamacıları daha bilinçli kararlar alabilir.

---

## Veri Seti

Veri seti: [Predict Crop Production (Kaggle)](https://www.kaggle.com/datasets/stealthtechnologies/predict-crop-production)

Veri seti, farklı tarım alanları, toprak tipleri, gübreleme miktarları, iklim verileri ve sulama bilgilerini içermektedir.

Kolonlar:
- Hectares
- Agriblock
- Variety
- Soil Types
- Seedrate (in Kg)
- LP_Mainfield (in Tonnes)
- Nursery
- Nursery area (Cents)
- LP_nurseryarea (in Tonnes)
- DAP_20days
- Weed28D_thiobencarb
- Urea_40Days
- Potassh_50Days
- Micronutrients_70Days
- Pest_60Day (in ml)
- 30DRain (in mm)
- 30DAI (in mm)
- 30_50DRain (in mm)
- 30_50DAI (in mm)
- 51_70DRain (in mm)
- 51_70AI (in mm)
- 71_105DRain (in mm)
- 71_105DAI (in mm)
- Min temp_D1_D30
- Max temp_D1_D30
- Min temp_D31_D60
- Max temp_D31_D60
- Min temp_D61_D90
- Max temp_D61_D90
- Min temp_D91_D120
- Max temp_D91_D120
- Inst Wind Speed_D1_D30 (in Knots)
- Inst Wind Speed_D31_D60 (in Knots)
- Inst Wind Speed_D61_D90 (in Knots)
- Inst Wind Speed_D91_D120 (in Knots)
- Wind Direction_D1_D30
- Wind Direction_D31_D60
- Wind Direction_D61_D90
- Wind Direction_D91_D120
- Relative Humidity_D1_D30
- Relative Humidity_D31_D60
- Relative Humidity_D61_D90
- Relative Humidity_D91_D120
- Trash (in bundles)
- Paddy yield (in Kg) — Target variable

Hedef değişken: **Paddy yield(in Kg)**

---

## Model Performans

| Model | MAE | RMSE | R² Score |
|-------|-----:|------:|--------:|
| Linear Regression | 698.32 | 927.94 | 0.9894 |
| Random Forest | 512.34 | 678.45 | 0.9952 |
| SVR | 3685.245102 | 5262.527620 | 0.658560 |

---
## Sonuç ve Model Karşılaştırması
Bu çalışmada Paddy Yield (Kg) değerini tahmin etmek için üç farklı supervised (denetimli) makine öğrenimi modeli kullanılmıştır:

- **Linear Regression**  
- **Random Forest Regressor**  
- **Support Vector Regression (SVR)**

Her model aynı eğitim/test veri seti üzerinde değerlendirilmiş ve performansları MAE, RMSE ve R² Score metrikleriyle karşılaştırılmıştır.

## Genel Değerlendirme

Analiz sonuçlarına göre en başarılı model Random Forest Regressor olmuştur. Bunun temel sebepleri şunlardır:

Doğrusal olmayan ilişkileri iyi öğrenir.
Paddy verimi; toprak nemi, sıcaklık, gübre miktarı, çevresel faktörler gibi birçok değişkenin doğrusal olmayan kombinasyonlarından etkilenir. Linear Regression bu karmaşıklığı yakalayamazken, Random Forest yakalayabilir.

Aykırı değerlere karşı dayanıklıdır.
Tarımsal verilerde ölçüm hataları / uç değerler sık görülür. Random Forest bu tarz gürültülü verilerde daha stabil çalışır.

Özellikler arasında etkileşimleri otomatik öğrenir.
Random Forest, özellikler arasındaki karmaşık ilişkileri ağaç yapıları sayesinde doğal olarak yakalayabilir.

Overfitting’i azaltan bir topluluk yöntemidir.
Tek bir karar ağacı aşırı öğrenmeye meyilliyken, çoklu ağaçlardan oluşan Random Forest genel performansı iyileştirir.

## Model Performanslarının Yorumlanması

Aşağıdaki metriklerde daha düşük MAE/RMSE ve daha yüksek R² daha iyidir.

**Linear Regression**  
Basit bir doğrusal model olduğu için karmaşık değişken ilişkilerini tam olarak yakalayamamış ve en düşük performansı göstermiştir.

**Support Vector Regression (SVR)**
Orta seviyede performans göstermiştir. Küçük / orta büyüklükteki veri setlerinde etkili olsa da hiperparametre ayarı yapılmadığında doğruluğu sınırlı kalabilir.

**Random Forest Regressor**  
En yüksek R² ve en düşük RMSE değerini elde ederek en başarılı model olmuştur.

---

## Grafikler

### Model Karşılaştırması (R²)
![Model Karşılaştırması (R2)](model_comparison_r2.png)

### Random Forest — Gerçek vs Tahmin
![Random Forest - Gerçek vs Tahmin](rf_actual_vs_pred.png)

### Linear Regression - Residual Dağılımı
![Residual LR](residual_lr.png)

### Random Forest - Residual Dağılımı
![Residual RF](residual_rf.png)

### Random Forest - Feature Importance (Top 15)
![Feature Importance](feature_importance_rf.png)

### SVR - Hata Dağılımı
![SVR Errors](svr_errors.png)

---

## Açıklamalar

- Scatter plot gerçek ve tahmin edilen değerleri karşılaştırır; ideal doğrultu çizgisi gösterilmiştir.  
- Residual plot’lar model hatalarının dağılımını gösterir; simetrik ve dar dağılım iyi performansı işaret eder.  
- Feature importance grafiği, Random Forest modelinin hangi değişkenlere daha çok güvendiğini ortaya koyar.

---

## Nasıl Çalıştırılır

1. `paddydataset.csv` dosyasını Colab veya lokal ortama koy.  
2. `notebook.ipynb` dosyasını aç ve sırasıyla hücreleri çalıştır.  
3. Grafikler `*.png` olarak üretilecektir; README içindeki görüntülerin görüntülenmesi için PNG dosyalarını repo köküne yükleyin.

---

## Licence & Kaynak
Veri seti: Kaggle — Predict Crop Production
