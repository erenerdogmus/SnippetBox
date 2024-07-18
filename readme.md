# My Web Application

## Proje Hakkında
Bu proje, kullanıcıların `kod snippet'lerini oluşturmasına`, `görüntülemesine` ve `yönetmesine` olanak tanıyan bir web uygulamasıdır. Ayrıca, `kullanıcı kayıt` ve `giriş işlemleri` ile `kullanıcı oturum yönetimi` gibi özellikleri de içermektedir. Proje, temel `web uygulaması geliştirme`, `kullanıcı kimlik doğrulama`, `form doğrulama` ve `veritabanı işlemleri` gibi konuları ele alarak, geliştiricilere bu alanlarda pratik yapma fırsatı sunar.

## Projenin Amacı
Projenin temel amacı, geliştiricilere `web uygulaması geliştirme sürecinin` farklı yönlerini öğretmek ve bu alanda pratik yapmalarını sağlamaktır. `Kullanıcı kimlik doğrulama`, `form doğrulama`, `oturum yönetimi` ve `veritabanı işlemleri` gibi kritik konuları içeren bu proje, gerçek dünya senaryolarında karşılaşılabilecek sorunların çözümüne yönelik deneyim kazandırmayı hedefler.

## Özellikler
- **Ana Sayfa:** En son eklenen snippet'lerin listelenmesi.
- **Snippet Görüntüleme:** Belirli bir snippet'i görüntüleme.
- **Snippet Oluşturma:** Yeni snippet oluşturma.
- **Kullanıcı Kayıt:** Yeni kullanıcı kaydı oluşturma.
- **Kullanıcı Giriş:** Var olan kullanıcılar için giriş yapma.
- **Kullanıcı Çıkış:** Giriş yapmış kullanıcılar için çıkış yapma.
- **Form Doğrulama:** Kullanıcı giriş ve kayıt formları için veri doğrulama.
- **Oturum Yönetimi:** Kullanıcı oturumlarının yönetimi.

## Kullanılan Paketler
- `net/http`: HTTP sunucusu ve istemci uygulamaları için temel HTTP paketleri.
- `github.com/julienschmidt/httprouter`: Yönlendirme ve URL işleme için yüksek performanslı bir HTTP yönlendirici.
- `github.com/go-playground/form/v4`: Form verilerini ayrıştırmak ve doğrulamak için kullanılır.
- `github.com/justinas/nosurf`: CSRF saldırılarına karşı koruma sağlamak için kullanılan paket.
- `github.com/alexedwards/scs/v2`: Oturum yönetimi için kullanılan bir paket.
- `github.com/go-sql-driver/mysql`: MySQL veritabanı sürücüsü.
- `golang.org/x/crypto/bcrypt`: Şifrelerin güvenli bir şekilde saklanması için bcrypt algoritması.

## Kurulum

### Gereksinimler
- Go 1.18 veya üstü
- MySQL veritabanı

### Adımlar

1. Depoyu klonlayın:
    ```sh
    git clone https://github.com/erenerdogmus/SnippetBox.git
    ```

2. Bağımlılıkları yükleyin:
    ```sh
    go mod tidy
    ```

3. Veritabanını oluşturun ve gerekli tabloları ekleyin:
    ```sql
    CREATE DATABASE snippetbox;
    USE snippetbox;

    CREATE TABLE snippets (
        id INTEGER PRIMARY KEY AUTO_INCREMENT,
        title VARCHAR(100) NOT NULL,
        content TEXT NOT NULL,
        created DATETIME NOT NULL,
        expires DATETIME NOT NULL
    );

    CREATE TABLE users (
        id INTEGER PRIMARY KEY AUTO_INCREMENT,
        name VARCHAR(255) NOT NULL,
        email VARCHAR(255) NOT NULL,
        hashed_password CHAR(60) NOT NULL,
        created DATETIME NOT NULL
    );
    ```

4. `.env` dosyasını oluşturun ve veritabanı bilgilerini ekleyin:
    ```sh
    DB_DSN="kullanici_adi:sifre@tcp(127.0.0.1:3306)/snippetbox?parseTime=true"
    ```

5. Uygulamayı başlatın:
    ```sh
    go run ./cmd/web
    ```

## Kullanım

### Ana Sayfa
Ana sayfada en son eklenen snippet'ler listelenir.

### Snippet Görüntüleme
Belirli bir snippet'i görüntülemek için:

```bash
GET /snippet/view/:id
```

### Snippet Oluşturma
Yeni bir snippet oluşturmak için:


```bash
GET /snippet/create
POST /snippet/create
```

### Kullanıcı Kayıt
Yeni bir kullanıcı kaydı oluşturmak için:

```bash
GET /user/signup
POST /user/signup
```

### Kullanıcı Giriş
Var olan bir kullanıcı için giriş yap:

```bash
GET /user/login
POST /user/login
```

### Kullanıcı Çıkış
Giriş yapmış bir kullanıcı için çıkış yap:

```bash
POST /user/logout
```


### Proje Yapısı
- `cmd/web` - Ana uygulama kodu.
- `internal/models` - Veritabanı modelleri.
- `internal/validator` - Form doğrulama fonksiyonları.
- `ui/html` - HTML şablon dosyaları.
- `ui/static` - Statik dosyalar (CSS, JS).