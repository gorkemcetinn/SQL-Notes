### LIKE

- 'WHERE' operatöründe kolonları filtrelemek için kullanılır.
#### '%'
- '%' işareti, bir veya birden fazla karakteri temsil eder.
- Eğer 'a%' şeklinde olursa a ile başlayan veri anlamına gelir.
- Eğer '%a' şeklinde olursa a ile biten veri anlamına gelir.
- Yani % işareti sonsuz sayıda karakter gelebilir demektir.

```sql
SELECT * FROM personnel WHERE first_name LIKE 'A%';
```

```sql
SELECT * FROM personnel WHERE first_name ILIKE 'A%';
```

* *'ILIKE' büyük-küçük harf duyarsız şekilde sorgu yapabilir.* 

```sql
SELECT * FROM personnel WHERE first_name LIKE '%a%';
```

- İçinde 'a' karakteri bulunan isimleri döndürür.

```sql
SELECT * FROM personnel WHERE first_name LIKE 'C%n';
```

- C ile başlayan n ile biten veriyi çağırır.
#### ' _ '

- **Sadece 1 karakterin** yerini tutar.

```sql
SELECT * FROM personnel WHERE first_name LIKE '_li';
```
- İkinci ve üçüncü harfi `li` olan ve toplamda **3 harfli** isimleri bulur. (örneğin: `Ali` eşleşir ama `Aslı` eşleşmez)
---
### IN

- 'OR' ifadesinin kısaltılmış halidir

```SQL
SELECT * FROM personnel 
WHERE department 
IN ('Marketing','HR');
```
- Departmanı Marketing ve HR olan verileri getirir.
---
### BETWEEN

- Belirli bir aralıktaki değerleri seçer. Değerler sayı, metin veya tarih olabilir.

```sql
SELECT _column_name(s)_  
FROM _table_name_  
WHERE _column_name_ BETWEEN _value1_ AND _value2;_
```

```sql
SELECT * FROM personnel 
WHERE salary BETWEEN 30000 AND 50000
ORDER BY salary;
```
- Maaşı 30000 ve 50000 arasında olan verileri getirip maaşa göre azalan düzeyde sırala.
- *NOT BETWEEN* arasında değil anlamı taşır.

```SQL
SELECT * FROM personnel 
WHERE salary BETWEEN 30000 AND 50000
AND department IN ('IT','HR')
```
- Aynı sorguyu sadece departmanı IT ve HR olanları getirir.

```sql
SELECT * FROM personnel 
WHERE first_name BETWEEN 'Cenan' AND 'Elif'
ORDER BY first_name
```
- Alfabetik olarak Cenan ve Elif arasındaki verileri getirir ve sıralar.
---
### AS 

* Kolon isimlerini istediğimiz gibi düzenlememize olanak sağlar.

```sql
SELECT _column_name_ AS _alias_name_  
FROM _table_name;_
```
---
### JOIN İşlemleri

- İki veya daha fazla tablodaki satırları, aralarındaki ilişkili bir sütuna göre birleştirmek için kullanılır.
- Tüm tablolarımız: 

| Tablo Adı  | Açıklaması          |
| ---------- | ------------------- |
| employee   | Çalışan bilgileri   |
| department | Departman bilgileri |
| dept_emp   | Departman No.'ları  |
| salary     | Maaş tablosu        |

-  Bu tablolar arasında kolonları birleştirerek yeni tablolar yaratma işlemidir.

<div style="display: flex; gap: 10px;">
  <img src="images/img_inner_join.png" alt="Inner Join" width="200">
  <img src="images/img_full_outer_join.png" alt="Full Outer Join" width="200">
  <img src="images/img_right_join.png" alt="Right Join" width="200">
  <img src="images/img_left_join.png" alt="Left Join" width="200">
</div>
<img width="861" height="158" alt="image" src="https://github.com/user-attachments/assets/bd36993c-7da2-43ba-9a94-527b144c8655" />


#### INNER JOIN

```SQL
SELECT tablo1.sütun, tablo2.sütun
FROM tablo1
JOIN tablo2
ON tablo1.ortak_sütun = tablo2.ortak_sütun;
```

```sql
SELECT e.first_name, e.last_name, d.dept_no, dp.dept_name from employee e 
join dept_emp d ON e.emp_no = d.emp_no
join department dp ON dp.dept_no = d.dept_no;
```
- Kullanıcının departman numarasını ve departman ismini getirir.

```sql
SELECT  e.first_name, e.last_name, s.amount from employee e
join salary s ON s.emp_no = e.emp_no
WHERE s.to_date = '9999-01-01'
ORDER BY s.amount DESC
```
* Kullanıcıların ad, soy-ad ve maaşını getirir ve maaşa sıralar.

```sql
SELECT dp.dept_name, ROUND(AVG(s.amount), 2) AS ort_maas
FROM employee e
JOIN salary s ON e.emp_no = s.emp_no
JOIN dept_emp d ON e.emp_no = d.emp_no
JOIN department dp ON d.dept_no = dp.dept_no
WHERE s.to_date = '9999-01-01'
GROUP BY dp.dept_name
ORDER BY avg_salary DESC;
```
- Departmanlara göre ortalama maaşı getirir.
#### LEFT JOIN

- **soldaki tablodaki tüm satırları alır**, sağdaki tabloyla **eşleşen varsa getirir**, **yoksa `NULL` döner**.

```sql
SELECT 
  e.first_name, 
  e.last_name, 
  s.amount
FROM employee e
LEFT JOIN salary s ON e.emp_no = s.emp_no
  AND s.to_date = '9999-01-01'
  ORDER BY s.amount DESC;
```
* İsim , soy-isim ve maaşı getirir ancak maaşı `NULL` olanlarıda getirir.

```sql
SELECT 
  e.first_name, 
  e.last_name, 
  dp.dept_name
FROM employee e
LEFT JOIN dept_emp d ON e.emp_no = d.emp_no
LEFT JOIN department dp ON d.dept_no = dp.dept_no;
```
* Kullanıcının adı, soy adı ve departmanını getirir ancak departmanı `NULL`olanlarıda getirir.
