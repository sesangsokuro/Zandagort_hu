Zandagort admin
===============

다음은 모두`www/admin` 디렉토리에 적용됩니다.

이 PHP는 `$zanda_private_key`를 지정하여 콘솔에서만 실행할 수 있습니다 :

	php -f valami.php $zanda_private_key


## 서버 리셋

Ha fejlesztesz, és utána akarsz új szervert indítani, ezeken kell végigmenned.
업그레이드 중이고 새 서버를 시작하려면이 서버를 거쳐야합니다.

### Táblák kiürítése

Nézd meg az `egyeb_telepito.php`-ban a táblák listáját, hogy van-e ami kimaradt (ez csak akkor fontos, ha fejlesztettél, és van új tábla). Utána futtasd le.

### 행성 만들기

Nézd meg a `galaxis_telepito.php` elején a leírást, aztán futtasd le egyesével a blokkokat. (Nem minden esetben kell mindegyiket.)

### 생태계 및 농장 설치

Futtasd le az `okoszfera_es_gazdasag_telepito.php`-t. Hogy mi van egy bolygón induláskor, azt a `csatlak.php`-ban található `bolygo_reset()` függvény határozza meg.

### NPC 차량 설치

Futtasd le az `npc_telepito.php`-t.

### 관리자 및 일부 기본 사용자 만들기

A következőkben mindig csekkold le, hogy a `userek` és a `szovetsegek` táblában jó ID-kat kaptál-e, és hogy azok passzolnak a `config.php`-ban leírtakhoz.

1. Regisztrálj a normál regisztráló oldalon egy admin usert.

2. Alapíts vele egy admin szövit.

3. `UPDATE userek SET admin=1 WHERE id=1;`

4. Futtasd le a `user_telepito.php`-t.

5. `ALTER TABLE `zanda`.`szovetsegek` AUTO_INCREMENT = 3;` (egy slot meghagyása a kalóz szövinek: `config.php/KALOZOK_HADA_SZOV_ID`)

6. `ALTER TABLE `zanda`.`userek` AUTO_INCREMENT = 6;` (egy slot meghagyása a Zandagortnak: `config.php/ZANDAGORT_TULAJ_SZOV`)


## 새로운 은하 생성

A `galaxis` könyvtárban találsz néhány fájlt. Ezek nincsenek dokumentálva, szóval magadnak kell rájönnöd a működésükre, leszámítva a következő pár infót.

s7에서 은하계는 두 단계로 이루어졌고, s8에서는 하나의 단계로 이루어졌다. 파일은 오래된 유적으로 가득합니다. 예를 들어 s7에서 은하는 JPG 이미지 (실제 왜건 휠 은하의 우주 사진)로 만들어졌지만 s6의 알고리즘 적 잔해 (바디, 인테리어, 꼬리, 지느러미, 입)가 포함되어 있습니다.

원래 이들은 ZandaNet이있는 별도의 서버에서 실행되었습니다. 따라서 모든 은하들은 원래의 처녀 형태로 남아있다. `galaxis_telepito.php`의`block0 ()`함수는 여기에서 해당 서버로 복사합니다.

Ha ezeket használni szeretnéd, hozz létre egy `szuz_bolygok` vagy hasonló nevű táblát (ez simán lehet `MyISAM` is), módosítsd úgy a kódot, hogy a `galaxis_generator_....php` oda generálja a bolygókat, és a `galaxis_telepito.php` onnan másolja be őket a tényleges `bolygok` táblába.


## 다른

Ha bármi van, pl változik a `config.php/$rendszer_so`, akkor a `reset_admin_pw.php`-val tudod újra beállítani az admin user jelszavát.
