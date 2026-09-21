# 🩺 COVID-19 Pasientləri Üzrə Kliniki Risk Analizi: Pnevmoniya və Yüksək Yaşın Ölüm Sıçrayışındakı Rolu

Bu layihə **25,000-dən çox COVID-19 pasient qeydini** ehtiva edən səhiyyə datası üzərində aparılmış hərtərəfli İlkin Məlumat Analizi (EDA) və kliniki risk qiymətləndirilməsidir. Tədqiqatın əsas məqsədi baza ölüm göstəricilərini təyin etmək, xroniki xəstəliklər üzrə Nisbi Riski (Relative Risk) hesablamaq, yaş qrupları üzrə pnevmoniyanın təsirini qiymətləndirmək və kliniki indikatorlar arasında multikollinearlığı aşkar etməkdir.

---

## 📌 Əsas İnsaytlar və Xülasə

* **Ümumi Baza Ölüm Faizi:** Dataset üzrə pasientlərin ümumi ölüm göstəricisi **16.2%** təşkil edir.
* **Əsas Ölüm Tətikləyicisi:** **Pnevmoniya** ölüm göstəricisi ilə ən yüksək xətti korelyasiyaya ($r = 0.47$) malikdir və təkbaşına ölüm riskini **~5.1 dəfə** artırır.
* **Xroniki Xəstəlik Sayının Təsiri (Comorbidity Multiplier):** 
  * **0 xroniki xəstəliyi** olan şəxslərdə ölüm faizi **~3.2%**-dir.
  * **2 xroniki xəstəliyi** olanlarda bu göstərici **~18.3%**-ə yüksəlir (**5.7 dəfə risk artımı**).
  * **3 və daha çox xroniki xəstəliyi** olanlarda isə risk baza göstəriciyə nəzərən **~8.0 dəfə** sıçrayır.
* **Yaş üzrə Stratifikasiya Paradoksu (Nisbi Risk Sıçrayışı):**
  * Pnevmoniyası olan **19–30 yaş qrupunda** mütləq ölüm faizi (**12.0%**), **81+ yaş qrupu** ilə (**59.7%**) müqayisədə xeyli aşağıdır.
  * Lakin tam sağlam gənclərlə (baza ölüm ~0.3%) müqayisədə, pnevmoniyaya yoluxan 19–30 yaşlı şəxslərdə **Nisbi Risk 37.3 dəfə sıçrayır**. Bu da pnevmoniyanın gənc orqanizm üçün kəskin risk yaradan əsas faktor olduğunu göstərir.

---

## 📊 Metodologiya və Analitik Çərçivə

1. **Datanın Hazırlanması və İmputasiya:**
   * Ötürülmüş (boş) kliniki dəyərlər kodlaşdırılaraq təhlilə yararlı hala gətirildi.
   * Şərti ehtimalları riyazi olaraq hesablamaq üçün binar hədəf dəyişəni `IS_DIED` ($1 = \text{Ölüb}, 0 = \text{Sağ qalıb}$) yaradıldı.
2. **Mütləq və Nisbi Risk Metrikaları:**
   * **Mütləq Ölüm Faizi** $\mathbb{E}[\text{IS\_DIED} \mid \text{Faktor}]$ düsturu ilə hesablandı.
   * **Nisbi Risk (RR)** aşağıdakı nisbətlə təyin edildi:
     $$\text{Nisbi Risk} = \frac{P(\text{Ölüb} \mid \text{Xəstəlik Var})}{P(\text{Ölüb} \mid \text{Xəstəlik Yoxdur})}$$
3. **Yaş Faktorunun İzolə Edilməsi (Age Control):**
   * Yaşın xalis təsirini xəstəliyin təsirindən ayırmaq üçün yaş qrupları üzrə kəsişmə matrisi (`pd.crosstab`) tətbiq olundu.
4. **Korelyasiya və Multikollinearlıq Təhlili:**
   * Dəyişənlər arası xətti asılılığı görmək və gələcək regressiya modellərində multikollinearlığın qarşısını almaq üçün Korelyasiya Xəritəsi (Heatmap) quruldu.

---
