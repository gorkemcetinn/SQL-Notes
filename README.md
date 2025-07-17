# SQL Notları 🇹🇷

Bu repoda, PostgreSQL temelli SQL öğrenimim sırasında oluşturduğum temel SQL notları yer almaktadır. Notlar `pgAdmin` üzerinden yapılan pratikler ve sık kullanılan sorgulara dayanmaktadır. Reponun amacı hem kendi öğrenim sürecimi belgelemek hem de SQL'e yeni başlayanlar için sade bir kaynak sunmaktır.

---

## ✏️ İçerik Düzeyleri

### 🔵 Temel Seviye (Bu repo içerisinde)
- `SELECT`, `DISTINCT`, `WHERE`
- Koşul operatörleri: `=`, `>`, `<`, `BETWEEN`, `IN`, `LIKE`, `NOT`
- Sıralama: `ORDER BY`, `ASC`, `DESC`
- Veri Ekleme: `INSERT INTO`
- Güncelleme: `UPDATE`
- Silme: `DELETE`
- Boş veri kontrolü: `IS NULL`, `IS NOT NULL`
- Sınırlama ve sayfalama: `LIMIT`, `OFFSET`
- Fonksiyonlar: `MIN()`, `MAX()`, `COUNT()`, `SUM()`, `AVG()`

### 🟡 Orta Seviye
- JOIN türleri: INNER JOIN, LEFT JOIN
- GROUP BY, HAVING (yakında)
- Alt sorgular (Subqueries) (yakında)
- CASE ifadeleri (yakında)
- Temel çok tablolu sorgular
- Basit veri analizleri: maaş ortalaması, departman eşleşmeleri
- Alias kullanımı (AS)
- VIEW kullanımı: current_dept_emp gibi

### 🔴 İleri Seviye (Planlama aşamasında)
- View’lar, Index’ler
- Stored Procedures ve Functions
- Performance tuning ve execution plan analizi
- CTE (Common Table Expressions)
- JSON/Array veri tipi ile çalışma

---

## 🧰 Nasıl Kullanılır?

Bu depo bir **cheatsheet** veya **kişisel not defteri** gibi kullanılabilir. Özellikle SQL öğrenmeye yeni başlayan öğrenciler veya pratik yapmak isteyenler için uygundur. Markdown formatında düzenlenmiştir ve düzenli olarak güncellenmektedir.

---

## 🐳 Docker ile Çalıştırma

Bu repoda yer alan PostgreSQL notlarını deneyimlemek için Docker ile hızlıca bir veritabanı ortamı kurabilirsiniz.

### 🔧 Gerekli Araçlar
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

### ⚙️ Kurulum

Bu repodaki `docker-compose.yaml` dosyası PostgreSQL ve pgAdmin4 bileşenlerini çalıştırır. Başlamak için terminalde aşağıdaki komutu çalıştırmanız yeterlidir:

```bash
docker-compose up -d
```

### 📥 Servisler

| Servis     | Port | Açıklama                                                    |
| ---------- | ---- | ----------------------------------------------------------- |
| PostgreSQL | 5432 | Veritabanı sunucusu                                         |
| pgAdmin4   | 8080 | Web arayüz ([http://localhost:8080](http://localhost:8080)) |

### 🔐 Varsayılan Giriş Bilgileri
#### PostgreSQL:
- Veritabanı Adı: Deneme

- Kullanıcı Adı: postgres

- Şifre: 123456

#### pgAdmin4:
- E-posta: me@de.com

- Şifre: 123456

### 🧠 Not
pgAdmin'e giriş yaptıktan sonra, “Add New Server” diyerek host kısmına db, kullanıcı adı ve şifre kısmına yukarıdaki bilgileri girerek bağlantı kurabilirsiniz.


Tüm veriler pgdata adlı volume'da saklanır, container silinse bile veriler kaybolmaz.

---

## 📄 Lisans

Bu proje [MIT Lisansı](LICENSE) ile lisanslanmıştır. Kişisel veya eğitim amaçlı kullanabilirsiniz.

