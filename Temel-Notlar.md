PGAdmin üzerinden PostgreSQL notları.

---
### SELECT

	Bir tablodaki tüm verileri çeker.

```sql
SELECT * FROM 'table'
```
	
```sql
SELECT * FROM personnel
```
---
### DISTINCT

	 Bir tablodaki benzersiz veriyi getirmek için kullanılır.

```sql
SELECT DISTINCT _column1_, _column2, 
FROM _table_name_;
```
	
```sql
SELECT DISTINCT department FROM personnel
```

---
### WHERE

	Veriyi belli bir koşulda filtrelemek için kullanılır.

```sql
SELECT _column1_, _column2, ..._  
FROM _table_name_  
WHERE _condition_;
```
	
```sql
SELECT * FROM personnel WHERE department = 'IT'
```
	
```sql
SELECT * FROM personnel where salary > 60000
```
	
```sql
SELECT first_name, position, salary FROM personnel where salary < 60000
```

| Sembol  |       Açıklama       |
| :-----: | :------------------: |
|    =    |       Eşittir        |
|    >    |       Büyüktür       |
|    <    |       Küçüktür       |
|   >=    |    Büyük Eşittir     |
|   <=    |    Küçük Eşittir     |
| != , <> |    Eşit Değildir     |
| BETWEEN | Belirli bir aralıkta |
|  LIKE   |     eşleştirmek      |
|   IN    | Liste yapısı gibi... |
|   NOT   |        Değil         |

```sql
SELECT first_name, position, salary FROM personnel WHERE first_name LIKE 'A%'
```
	
- Adı a ile başlayan kişiler.

```sql
SELECT first_name, position, salary FROM personnel WHERE salary BETWEEN 35000 AND 50000
```
	
- Maaşı 35000 ve 50000 aralığındaki kişileri getirir.

```sql
SELECT * FROM personnel WHERE department IN ('IT', 'HR', 'Sales');
```
	
- Departmanı belirtilen veriyi getirir.

```sql
SELECT * FROM personnel
WHERE salary BETWEEN 40000 AND 80000
AND department IN ('IT', 'HR');
```
	
- Maaş aralığı ve belirtilen departmanı getirir.

```sql
SELECT * FROM personnel WHERE salary > 50000 AND first_name LIKE 'A%'
```
	
- Maaşı 50000'den fazla olanı ve adı 'A' ile başlayanı getirir.

```sql
SELECT * FROM personnel 
WHERE salary > 50000 
AND (first_name LIKE 'A%' OR first_name LIKE 'E%')
```
	
- Maaşı 50000'den fazla olanı ve ismi A veya E ile başlayan veriyi getirir.

```sql
SELECT * FROM personnel  
WHERE salary NOT BETWEEN 10000 AND 60000;
```
	
- Maaşı 10000 ve 6000 arasında olmayan verileri getirir.

---
### ORDER BY

	Veriyi artan veya azalan düzeyde sıralamaya yarar. 
- ASC : Azalan
- DESC : Artan
	
```sql
SELECT * FROM personnel ORDER BY salary DESC
```

- Birden fazla kolon ile de sıralama yapılabilir. 
- Örnek: Departmana göre alfabetik bir sıralama yapar ancak departmanı aynı olan kişiler için maaşı da göz önünde bulundurarak değerlendirme yapar. 
	
```sql
SELECT * FROM personnel ORDER BY department, salary ASC
```
---
### NULL

	 Bir tabloda boşv eri aramak için kullanılır.
	
```sql
SELECT * from personnel WHERE first_name IS NULL;
```
	
```sql
SELECT * from personnel WHERE first_name IS NOT NULL;
```
---
### INSERT INTO

	Bir tabloya veri eklememizi sağlar.
	
```sql
INSERT INTO _table_name_ (_column1_, _column2_, _column3_, ...)  
VALUES (_value1_, _value2_, _value3_, ...);
```
---
### UPDATE

	 Bir tablodaki verileri güncellemek için kullanılır.

```sql
UPDATE _table_name_  
SET _column1_ = _value1_, _column2_ = _value2_, ...  
WHERE _condition_;
```

```sql
UPDATE personnel SET first_name = 'Görkem', last_name = 'Çetin' Where first_name = 'Muktedir'
```
	
- İsmi Muktedir olan verinin adını ve soy adını güncelle.
	
- 'Update' komutunu kullanmak zorunlu.
---
### DELETE

	 Bir tablodaki verileri silmek için kullanılır.

```SQL
DELETE FROM _table_name_ WHERE _condition_;
```
 
```sql
DELETE FROM personnel WHERE id=50;
```
	
- İd'si 50 olan veriyi sil.
	
- Where olmadan kullanırsak tablodaki tüm veriyi siler !!
- **DROP TABLE table_name** tabloyu siler
---
### LIMIT

	 Bir tablodaki verilerin belli sayıda getirilmesini sağlar.

```sql
SELECT * FROM tablo
WHERE koşul
ORDER BY sıralama_kriteri
LIMIT sayı;
```

```sql
SELECT * FROM personnel 
WHERE salary <60000
ORDER BY department, salary DESC
LIMIT 10;
```
	
* 'personnel' tablosundaki maaşı 60000 olan ilk 10 veriyi getir ve departmant, salary göre sırala.
	`OFFSET` komutu da ilk n veriyi atalyıp sonraki verileri almamızı sağlar.  **Sayfalama Yöntemi**
---
### SQL Fonksiyonlar

#### MIN() - MAX()

	Tablodaki verilerin minimum ve maksimum verilerini getirmesini sağlar.

```sql
SELECT MIN(_column_name_)  
FROM _table_name_  
WHERE _condition_;
```

```sql
SELECT MIN(salary) FROM personnel where salary > 50000
```

#### COUNT()

	 Bir kritere uyan satır sayısını getirir.

```sql
SELECT COUNT(_column_name_)  
FROM _table_name_  
WHERE _condition_;
```

```SQL
SELECT COUNT(*) FROM personnel where salary > 80000
```

#### SUM()

	Sayısal bir sütunun toplamını döndürür.

```sql
SELECT SUM(_column_name_)  
FROM _table_name_  
WHERE _condition_;
```

```SQL
SELECT SUM(SALARY) AS TOPLAM_MAAS FROM personnel WHERE SALARY < 45000
```


#### AVG()

	Sayısal bir sütunun ortalamasını alır.

```sql
SELECT AVG(_column_name_)  
FROM _table_name_  
WHERE _condition_;
```

```sql
SELECT AVG(SALARY) AS AVG_MAAS FROM personnel
```
