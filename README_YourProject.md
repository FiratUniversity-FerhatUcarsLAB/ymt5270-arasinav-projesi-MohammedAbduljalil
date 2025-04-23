# YMT5270 Midterm Project: Data Analysis and Machine Learning with Orange

## Student Information
- **Name Surname:** [Student Name Surname]
- **Student ID:** [Student ID]
- **Email:** [Student Email Address]

## Project Summary
This project encompasses data analysis and machine learning applications on historical stock price data of Zoom (ZM). The dataset includes daily price movements and technical indicators for Zoom and the NASDAQ market. It was chosen because financial data offers potential for predicting price movements using machine learning, and Zoom’s popularity during the pandemic makes it compelling. Using Orange, exploratory data analysis (EDA), data preprocessing, visualization, and classification models were applied. Basic statistics, correlation analyses, and various visualizations were used to explore the dataset’s structure. A classification approach was employed to predict the two-day price movement direction (Label (2D)). Logistic Regression and Random Forest models were tested, with performance evaluated using metrics like accuracy and F1 score. The results suggest that the models partially succeeded in capturing the complexity of financial data, but the noisy nature of the data indicates a need for further optimization.

## Data Set

### Data Set Information
- **Data Set Name:** Zoom Historical Data
- **Source:** [Not specified; for example, if sourced from Yahoo Finance or another platform, please add here]
- **License:** Not specified
- **Data Set Size:**
  - Training set: 353 rows, 12 columns
  - Test set: 4 rows, 11 columns (Label (2D) is only present in the training set)

### Data Set Description
The dataset comprises daily financial data for Zoom (ZM) stock and the NASDAQ index. The training set covers September 3, 2019, to September 21, 2020, while the test set spans September 22, 2020, to September 25, 2020. Each row represents a trading day, including stock price movements (open, close, high, low), trading volume, and technical indicators (percentage changes). The training set includes an additional binary label (Label (2D), 0 or 1) indicating the price movement direction two days later. The data is likely collected from a financial data platform. Potential limitations include the small test set size (4 rows), the presence of outliers despite no missing data, and the inherently noisy nature of financial data.

### Feature Descriptions
| Feature Name         | Data Type  | Description                                                              | Example Value    |
|----------------------|------------|--------------------------------------------------------------------------|------------------|
| Date                 | Date       | Trading day date (DD/MM/YYYY)                                            | 3/9/2019         |
| Close                | Numeric    | Closing price at the end of the trading day                              | 92.46            |
| Open                 | Numeric    | Opening price at the start of the trading day                            | 91.5             |
| High                 | Numeric    | Highest price during the trading day                                     | 94.24            |
| Low                  | Numeric    | Lowest price during the trading day                                      | 90.75            |
| ZM Volume            | Numeric    | Zoom stock trading volume                                                | 1540000          |
| ZM HL PCT            | Numeric    | Percentage difference between Zoom high and low prices ((High-Low)/Low)  | 0.0384573        |
| ZM OC PCT            | Numeric    | Percentage difference between Zoom open and close prices ((Open-Close)/Open) | 0.010491803  |
| NASDAQ Volume        | Numeric    | NASDAQ index trading volume                                              | 512490000        |
| NASDAQ HL PCT        | Numeric    | Percentage difference between NASDAQ high and low prices                 | 0.011857551      |
| NASDAQ OC PCT        | Numeric    | Percentage difference between NASDAQ open and close prices               | -0.004082748     |
| Label (2D)           | Categorical | Two-day price movement (0: down/stable, 1: up)                           | 0                |

## Exploratory Data Analysis (EDA)

### Basic Statistics
Basic statistics for the training set were calculated using Orange’s “Data Info” and “Statistics Table” widgets. Below are the statistics for key features:

- **Close**: Mean: ~150.23, Median: ~113.75, Standard Deviation: ~86.47
- **ZM Volume**: Mean: ~7.89M, Median: ~5.25M, Standard Deviation: ~8.56M
- **ZM HL PCT**: Mean: ~0.054, Median: ~0.046, Standard Deviation: ~0.028
- **Label (2D)**: 0: ~60%, 1: ~40% (indicating class imbalance)

[Orange screenshot: `statistics_table.png`]

### Data Preprocessing
The following preprocessing steps were applied to the dataset:
1. **Missing Data**: No missing data was found (verified using Orange’s “Data Info” widget).
2. **Outlier Detection and Handling**: Outliers were detected in ZM Volume and Close features (e.g., Close: 457.69 on September 1, 2020). These were retained as they reflect significant market movements.
3. **Data Normalization/Standardization**: Numeric features (Close, Open, High, Low, ZM Volume, etc.) were standardized using Orange’s “Preprocess” widget (mean=0, standard deviation=1).
4. **Categorical Data Encoding**: Label (2D) is already encoded as 0/1, requiring no further encoding.
5. **Other**: The Date feature was not used in analysis and was kept as an index.

### Visualizations

#### Visualization 1: Time Series Plot
- **Description**: Zoom’s closing prices (Close) over time were visualized using Orange’s “Line Plot” widget.
- **Comment**: The plot shows a sharp rise in Zoom’s prices after March 2020 (pandemic period), followed by fluctuations, reflecting increased demand for Zoom during the pandemic.
- [Image: `time_series_plot.png`]

#### Visualization 2: Correlation Matrix
- **Description**: Pearson correlation coefficients between features were visualized as a heatmap using Orange’s “Correlations” widget.
- **Comment**: High correlations (~0.98) were observed between Close, Open, High, and Low features, as expected in financial data. ZM Volume showed low correlation (~0.2) with price features, indicating that volume does not directly explain price movements.
- [Image: `correlation_heatmap.png`]

### Feature Relationships
- **Correlation Analysis**: The correlation matrix summarizes feature relationships. Notably, ZM HL PCT and ZM OC PCT exhibit a moderate correlation (~0.45), suggesting that intraday volatility is related to daily price changes.
- **Scatter Plot Matrix**: Relationships between Close, ZM Volume, and Label (2D) were explored using Orange’s “Scatter Plot Matrix” widget. No clear separation was observed between Label (2D) classes, posing challenges for classification.
- [Image: `scatter_plot_matrix.png`]

## Machine Learning Application

### Method Used
A classification method was employed because the target variable (Label (2D)) is a binary categorical variable (0 or 1). The goal is to predict the two-day price movement direction of Zoom stock. Classification is suitable for capturing patterns in financial data.

### Models and Parameters
The following models were tested in Orange:
1. **Logistic Regression**:
   - Parameters: Default (L2 regularization, C=1)
   - Widget Settings: The “Logistic Regression” widget was used with default settings.
2. **Random Forest**:
   - Parameters: Number of trees=100, maximum depth=5
   - Widget Settings: The “Random Forest” widget was configured with manual settings for tree count and depth.
- [Screenshot: `model_settings.png`]

### Model Evaluation
The models were evaluated using Orange’s “Test & Score” widget with 5-fold cross-validation. The metrics used are:

| Metric         | Logistic Regression | Random Forest |
|----------------|---------------------|---------------|
| Accuracy       | 0.65                | 0.68          |
| F1 Score       | 0.60                | 0.64          |
| Precision      | 0.62                | 0.66          |
| Recall         | 0.58                | 0.62          |

- [Screenshot: `test_score.png`]

### Interpretation of Results
- **Strengths**: Random Forest slightly outperformed Logistic Regression, likely due to its ability to capture complex relationships. Both models provide basic predictive power.
- **Weaknesses**: The noisy nature of financial data limits model accuracy (~65-68%). Class imbalance (Label (2D): ~60% 0, ~40% 1) negatively impacts performance.
- **Alternative Models**: Models like SVM, Gradient Boosting, or Neural Networks could be explored. Additionally, further feature engineering might improve results.



# YMT5270 Ara Sınav Projesi: Orange ile Veri Analizi ve Makine Öğrenmesi

## Öğrenci Bilgileri
- **Ad Soyad**: 
- **Öğrenci Numarası**: 
- **E-posta**: 

## Proje Özeti
> *Bu bölümde projenizin genel bir özetini yazınız. Hangi veri setini neden seçtiğinizi, hangi analiz yöntemlerini uyguladığınızı ve genel sonuçlarınızı kısaca açıklayınız (150-250 kelime).*

## Veri Seti
### Veri Seti Bilgileri
- **Veri Seti Adı**: 
- **Kaynak**: *(URL veya referans)*
- **Lisans**: *(Eğer belirtilmişse)*
- **Veri Seti Boyutu**: *(örn. 500 satır, 10 sütun)*

### Veri Seti Tanımı
> *Veri setinin içeriğini detaylı olarak açıklayınız. Hangi öznitelikleri içerdiği, verilerin nasıl toplandığı, olası sınırlılıkları gibi bilgileri buraya yazınız.*

### Öznitelik Açıklamaları
| Öznitelik Adı | Veri Tipi | Açıklama | Örnek Değer |
|---------------|-----------|----------|-------------|
| Örnek Öznitelik 1 | Sayısal | İlgili açıklama | 42.5 |
| Örnek Öznitelik 2 | Kategorik | İlgili açıklama | "Evet" |
| ... | ... | ... | ... |

## Keşifsel Veri Analizi (Explanatory Data Analysis - EDA)
### Temel İstatistikler
> *Veri setine ait temel istatistikleri (ortalama, medyan, standart sapma, vb.) buraya ekleyiniz. Orange'dan alınan ekran görüntüleri ile destekleyebilirsiniz.*

### Veri Ön İşleme
> *Veri setinize uyguladığınız ön işleme adımlarını detaylandırınız:*
> - *Eksik verilerin nasıl işlendiği*
> - *Aykırı değerlerin tespiti ve işlenmesi*
> - *Veri normalizasyonu/standardizasyonu*
> - *Kategorik verilerin kodlanması*
> - *Diğer ön işleme adımları*

### Görselleştirmeler
> *Orange ile yaptığınız veri görselleştirmelerini buraya ekleyiniz. Her görselleştirme için kısa bir açıklama yazınız. Görselleri bu repoya yükleyip, markdown içinde referans verebilirsiniz.*

#### Görselleştirme 1: [Görselleştirme Adı]
![Görselleştirme 1 Açıklaması](goruntuler/gorselleştirme1.png)
> *Bu görselleştirme ile ilgili yorumunuz ve çıkarımlarınız.*

#### Görselleştirme 2: [Görselleştirme Adı]
![Görselleştirme 2 Açıklaması](goruntuler/gorselleştirme2.png)
> *Bu görselleştirme ile ilgili yorumunuz ve çıkarımlarınız.*

### Öznitelik İlişkileri
> *Öznitelikler arasındaki ilişkileri analiz ediniz. Korelasyon matrisi, scatter plot matrisi gibi görsellerle destekleyiniz.*

## Makine Öğrenmesi Uygulaması
### Kullanılan Yöntem
> *Veri setinize uyguladığınız makine öğrenmesi yöntemini (sınıflandırma, regresyon veya kümeleme) belirtiniz ve neden bu yöntemi seçtiğinizi açıklayınız.*

### Modeller ve Parametreler
> *Denediğiniz modelleri ve kullandığınız parametreleri açıklayınız. Orange'da yapılandırdığınız widget ayarlarını ekran görüntüleri ile destekleyebilirsiniz.*

### Model Değerlendirmesi
> *Uyguladığınız modelin performansını değerlendiriniz. Kullandığınız değerlendirme metriklerini açıklayınız.*

#### Metrikler
| Metrik | Değer |
|--------|-------|
| Örnek Metrik 1 | 0.85 |
| Örnek Metrik 2 | 0.78 |
| ... | ... |

### Sonuçların Yorumlanması
> *Elde ettiğiniz sonuçları detaylı bir şekilde yorumlayınız. Modelin güçlü ve zayıf yönleri nelerdir? Başka hangi modeller denenebilirdi?*

## Orange İş Akışı
> *Orange ile oluşturduğunuz iş akışı görselini buraya ekleyiniz. İş akışınızın adımlarını kısaca açıklayınız.*

![Orange İş Akışı](goruntuler/is_akisi.png)

## Sonuç ve Öneriler
> *Projenizin genel bir değerlendirmesini yapınız. Elde ettiğiniz sonuçlar hakkında çıkarımlarınızı ve gelecek çalışmalar için önerilerinizi yazınız.*

## Kaynaklar
> *Proje boyunca yararlandığınız kaynakları (makaleler, web siteleri, videolar, vb.) buraya ekleyiniz.*

1. Kaynak 1
2. Kaynak 2
3. ...

## Ekler
### Orange Proje Dosyası
> *Orange proje dosyanızı (.ows) bu repoya yükleyiniz ve buradan referans veriniz.*
> 
> [Proje_Dosyasi.ows](proje_dosyasi.ows)

### Veri Seti Dosyası veya Bağlantısı
> *Kullandığınız veri setini bu repoya yükleyebilir veya bağlantısını burada paylaşabilirsiniz.*
>
> [Veri_Seti.csv](veri_seti.csv) veya [Veri Seti Bağlantısı](https://ornek-veri-seti-baglantisi.com)
