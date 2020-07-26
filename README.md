Türkçe Açıklama
# TeshisDestekSistemi
Java and Rapidminer
Karar destek sistemleri(KDS), verilmesi gereken kararla ilgili veriyi daha iyi anlayarak, daha etkin karar seçenekleri oluşturma, alternatifleri belirleme ve değerlendirme işlevlerine destek sağlayan ve doğru karar verme olasılığını artıran sistemlerdir. En genel anlamıyla Karar Destek Sistemleri yönetici konumundaki karar vericilerin karar vermelerine yardımcı olan sistemlerdir.
KDS’nin temelleri 1960’lı yıllarda atılmaya başlamıştır. Bu konudaki ilk kavramlar 1971’de M. Scott Morton tarafından “Management Decision Systems (Yönetim Karar Sistemleri) başlıklı bir yazıda ele alınmıştır. Daha sonra gerek akademik, gerekse endüstriyel alanlarda araştırma-geliştirme ve uygulama çalışmaları hızla yayılmıştır.
KDS’ler, veritabanındaki modüller aracılığıyla, çok ölçütlü ve birbirleriyle çelişen kriterler altında karar vericinin optimum çözümü elde etmesinde karar vericiye yardımcı olan, problem çözümünü hızlandıran ve kullanıcıyla etkileşimli olarak çalışan bilgisayar destekli sistemler olarak tanımlanabilmektedir. KDS’ler, veritabanına girilen verileri özetlemede ve analiz etmede karar vericiye yardımcı olmaktadır. Kısaca KDS için bir tür tahminleme yazılımı da denilebilmektedir.
https://archive.ics.uci.edu/ml/datasets/Heart+failure+clinical+records linkinde yer alan, Türkçeye kalp yetmezliği klinik kayıtları olarak ta çevrilebilen bir veriseti kullanılmıştır. İlgili veriseti .csv(comma seperated value/virgülle ayrılmış değer) formatındadır. 
Veriseti; Faysalabad Hükümet Kolejinden (Pakistan) Tanvir Ahmad, Assia Munir, Sajjad Haider Bhatti, Muhammad Aftab, and Muhammad Ali Raza tarafından, makine öğrenmesi sistemi için hazırlanmıştır. 
299 hastaya ait veriler 13 farklı öznitelikte toplanmıştır
Bu 13 öznitelik şunlardır:
 yaş: hastanın yaşı (yıl)
anemi: kırmızı kan hücrelerinin veya hemoglobin (boolean) azalması, kansızlık var mı varsa 1 yoksa 0
yüksek tansiyon: hastanın hipertansiyonu (boolean) varsa 1, yoksa 0
kreatinin fosfokinaz (CPK): Kandaki CPK enziminin seviyesi (mcg / L)
diyabet: Hastada diyabet varsa (boolean) 1, yoksa 0
ejeksiyon fraksiyonu: her kasılmada kalbi terk eden kan yüzdesi (yüzde)
trombositler: kandaki trombositler (x 1000 trombosit / mL)
cinsiyet: kadın veya erkek (ikili) kadın 0, erkek 1
serum kreatinin: kandaki serum kreatinin seviyesi (mg / dL)
serum sodyum: kandaki serum sodyum seviyesi (mEq / L)
sigara içme: hasta sigara içerse 1 ya da değil 0 (boolean)
zaman: takip süresi (gün)
[hedef] ölüm olayı: hasta takip süresi içinde (boolean) ölmüşse 1 değilse 0
Verisetindeki 13 sütün, 299 satır yani 3887 hücrenin tamamı incelenmiş, tek bir hücrede dahi eksiklik bulunamamıştır.
Trombosit verisinin veri tipi real veri tipi olduğu için, bazı hastalara ait trombosit değerleri virgüllü gözükmektedir. 
Veriseti RapidMiner’e aktarılırken, Verisetinde trombosite ait real olan data type integer olarak düzenlenerek, virgüllü değer sorunu çözülmüştür.
Karar ağacının daha doğru yorumlanabilmesi için, verisetindeki özniteliklerin adları Türkçeye tercüme edilmiştir Örneğin orijinal verisetindeki age ibaresi yas olarak çevrilmiştir.
KDS tasarımında referans alınan veriseti; düzenlenmiş olan verisetidir.
Daha düzgün bir karar ağacı oluşturmak için, özniteliklerden yüksek tansiyon, sigara kullanımı, diyabet var mı, ölüm var mı, kansızlık var mı adlı özniteliklere verilen 1 değerleri Evet’e, 0 değerleri Hayır’a çevrilirken, 
Cinsiyet özniteliğindeki 1 değerleri Erkek’e, 0 değerleri ise Kadın’a çevrilmiştir. Böylece daha düzgün bir karar ağacı elde edilmiş ve ağacın performansı hakkında daha anlaşılabilir bilgi alınabilmiştir
CSV dosyasındaki verileri düzenlemek için excelden bağımsız bir csv düzenleyici program olan CSVed adlı bir program kullanılarak, veriler daha kolay ve güvenli bir şeklilde düzenlenmiştir.
Karar ağacını oluşturmadan önce, veriseti düzenlenmiştir.
Veriseti RapidMiner’e eklenmiştir. 
Karar Ağacının neyin kararını vereceği tanımlanmıştır. (Kalp yetmezliğinden dolayı ölümün olup olmayacağına karar veriyor)
Karara etki eden öznitelikler belirlenmiştir
Veriseti %41 eğitim, %59 test verisi olacak şekilde 2’ye bölünmüştür
Verisetinin eğitim verisindeki veriler karar ağacına input olarak tanımlanmıştır
Karar ağacı «gain ratio» ya göre, budama confidencesi 0.25, ön budama confidensi 0.1, maximal derinliği 20 olacak şekilde oluşturulmuştur
Karar ağacının sonucu ve test verisi ile mini bir model oluşturulmuş ve model, kendisini karar ağacıyla yani eğitim verisiyle eğiterek, test verilerinden bir karar çıkarmıştır.
Daha sonra ise modelin performansı ölçülmüş ve modelin çıkardığı tahmini kararlar, karar ağacı ve performans vektörü «gain ratio/kazanç oranı» algoritmasına göre elde edilmiştir.
RapidMiner daki başka algoritmalar (information gain, accuracy ve gini index) kullanıldığında, ağaç uzunluğu ve modelin performans değerleri değişkenlik gösterir.
Performans ve anlamlı ağaç açısından en uygun olan ağaç, gain index ile elde edilerek yazılımın arayüz tasarımı ağaçtan elde edilen değerlerden faydalanarak yapılmıştır.
Karar ağacının budanma miktarı arttıkça, Accuracy ve AUC yüzde değerleri artmaktadır ancak bir karar verme işi tek bir kıstasa göre verilemeyeceği için, karara en çok etki eden kıstasları barındıran bir karar ağacı oluşturulmuştur.
Doğruluk-Accuracy: %79,10
Kesinlik-Precision: %83.74
Hassasiyet-Recall: %85.83
AUC Değeri:
En iyi: 0.825
Ortalama: 0.713
Kötümser: 0.612
Pozitif Sınıfı: Hayır kararları
Negatif Sınıfı: Evet kararları

Temel olarak; doktor, kalp hastası olduğundan şüphelenilen hastaya ait karara etki eden öznitelik değerlerini sisteme girer.
Sistem ise belli kurallara göre oluşturulmuş modele (model, rapidminerde oluşturulmuştur.) ve modelden referans alınan değerlere göre, girilen değerleri karşılaştırarak, hastanın mevcut durumu ve gelecekteki akıbeti hakkında tahmini olarak bir sonuç çıktısı verir. Buradan gelen sonuca göre doktor, hasta için gerekeni yerine getirir. 
Verilen karar, hastada kalp yetmezliğinin olup olmamasıdır.
Burada unutulmaması gereken; KDS yazılımının nihai karar verici olmadığı, sadece ilgili otoritelerce verilecek olan nihai karara destek verdiğidir. 
Yani karar verme yetkisi yazılıma değil ilgili otoriteye aittir.
KDS arayüz yazılımı Java® dili kullanılarak, Netbeans IDE programında Windows Form Uygulaması olarak yazılmıştır.
Arayüz yazılımı oluşturulurken, karar ağacındaki kıstaslar ve değerler dikkate alınmış ve bu değerler ile girilen değerler if-else şeklinde karşılaştırılarak, olası karar belirtilmiştir. 
Yaş ve gün değerleri haricindeki tüm sayısal değerler floattır.
Yaş ve gün integer dır.
Sisteme girmek için gerekli kullanıcı adı ve parolasının her ikisine de «admin» yazılması gerekmektedir.
Sisteme girildiğinde öncelikle hastanın takip süresinin gün olarak girilmesi gerekir.
Gün girildikten sonra istenilen değerlerin tamamı doldurulur ve sonuç için «Teşhis Koy» tuşuna basılır
Çıkan sonuç %79.13 doğruluk değerine sahiptir.




English Description
#DiagnosticSupportSystem

Decision support systems (DSS) are systems that support the functions of creating more effective decision options, determining alternatives and evaluating functions and increasing the probability of correct decision by better understanding the data about the decision to be made. In the most general sense, Decision Support Systems are systems that help decision makers in executive positions to make decisions.
The foundations of DSS started to be laid in the 1960s. The first concepts on this subject were discussed in 1971 by M. Scott Morton in an article titled "Management Decision Systems." Later, research-development and application studies in academic and industrial fields spread rapidly.
DSS' can be defined as computer-aided systems that help the decision maker, accelerate problem solving and interact with the user through the modules in the database, under multi-criteria and conflicting criteria. DSS' assist the decision maker in summarizing and analyzing the data entered in the database. Briefly, a kind of estimation software for KDS can also be called.
A dataset, which can be translated into Turkish as a clinical record of heart failure, has been used in the link https://archive.ics.uci.edu/ml/datasets/Heart+failure+clinical+records. The related dataset is in .csv (comma seperated value / comma separated value) format.
Data set; It was prepared for the machine learning system by Tanvir Ahmad, Assia Munir, Sajjad Haider Bhatti, Muhammad Aftab, and Muhammad Ali Raza from Faysalabad Government College (Pakistan).
Data for 299 patients were collected in 13 different attributes
These 13 attributes are:
 age: patient's age (years)
anemia: reduction of red blood cells or hemoglobin (boolean), anemia if there is 1 or 0
high blood pressure: 1 if the patient has hypertension (boolean), 0 otherwise
creatinine phosphokinase (CPK): level of CPK enzyme in the blood (mcg / L)
diabetes: 1 if the patient has diabetes (boolean) or 0
ejection fraction: percentage of blood leaving the heart at each contraction (percent)
platelets: platelets in the blood (x 1000 platelets / mL)
gender: female or male (binary) female 0, male 1
serum creatinine: serum creatinine level in blood (mg / dL)
serum sodium: serum sodium level in the blood (mEq / L)
smoking: 1 or not 0 if the patient smokes (boolean)
time: follow-up time (days)
[target] death event: 0 if the patient died within the follow-up period (boolean) 0 if not
13 columns in the dataset, 299 rows, or 3887 cells, were examined, and there was no deficiency in a single cell.
Since the data type of platelet data is real data type, platelet values of some patients appear to be comma.
While transferring Veriseti to RapidMiner, the data type of the thrombocyte in Veriset was edited as integer and the comma value problem was solved.
In order to interpret the decision tree more accurately, the names of the attributes in the database have been translated into Turkish. For example, the age word in the original database has been translated as mourning.
Data set referenced in DSS design; is the dataset that has been edited.
In order to create a more accurate decision tree, 1 values given to attributes such as high blood pressure, smoking, diabetes, death or anemia are converted to Yes and 0 values to No,
The values of 1 in the gender attribute have been converted into Male and 0 values into Female. Thus, a smoother decision tree was obtained and more understandable information about the performance of the tree was obtained.
Using a program called CSVed, a CSV editor program independent of Excel, to edit the data in the CSV file, the data was organized more easily and securely.
Before creating the decision tree, the dataset was edited.
The dataset has been added to RapidMiner.
Decision Tree has been defined what will decide. (Decides whether there will be death due to heart failure)
Attributes affecting the decision have been identified
The data set is divided into 2 as 41% education and 59% test data.
Data in the dataset's training data is defined as an input to the decision tree
According to the decision ratio “gain ratio”, pruning confidency is 0.25, preliminary pruning confidency is 0.1 and maximal depth is 20.
A mini model was created with the result of the decision tree and test data, and the model made a decision from the test data by training itself with the decision tree, that is, education data.
Afterwards, the performance of the model was measured and the estimated decisions made by the model were made according to the decision tree and the performance vector “gain ratio” algorithm.
When other algorithms (information gain, accuracy and gini index) are used in RapidMiner, tree length and model performance values vary.
The most suitable tree in terms of performance and meaningful tree was obtained with gain index and the interface design of the software was made by using the values obtained from the tree.
As the pruning amount of the decision tree increases, Accuracy and AUC percentage values increase, but since a decision-making job cannot be made according to a single criterion, a decision tree that has the most impact on the decision was created.
Accuracy-Accuracy: 79.10%
Precision-Precision: 83.74%
Sensitivity-Recall: 85.83%
AUC Value:
Best: 0.825
Average: 0.713
Pessimist: 0.612
Positive Class: No decisions
Negative Class: Yes decisions

Basically; the doctor enters the attribute values that affect the decision of the patient suspected of having heart disease into the system.
The system, by comparing the entered values according to certain rules (the model was created in the rapidminer) and the values referenced from the model, gives an estimated result output about the patient's current status and future fate. According to the result, the doctor fulfills what is necessary for the patient.
The decision made is whether the patient has heart failure.
It should not be forgotten here; It is that the DSS software is not the ultimate decision maker, it only supports the final decision to be made by the relevant authorities.
So the decision-making authority belongs to the relevant authority, not to the software.
The DSS interface software was written as a Windows Form Application in the Netbeans IDE program using the Java® language.
While creating the interface software, the criteria and values in the decision tree were taken into consideration and the possible decision was specified by comparing the values entered with these values as if-else.
All numerical values except for age and day values are float.
Age and day are integer.
In order to log in to the system, “admin” must be written in both the username and password required.
When entering the system, the patient's follow-up period must first be entered in days.
After the day is entered, all of the desired values are filled in and the "Diagnose" button is pressed for the result.
The result is 79.13% accuracy.
