# 2-toby-kim-wordpress-resume
클라우드과정 1주차 과제 - LAMP 서버로 Wordpress 서비스를 만들어 이력서 작성하기

<br>

# 1. How to set?
- VirtualBox
- Ubuntu 24.04.1 LTS
- Apache/2.4.58

1. VirtualBox 네트워크 세팅 (NAT)
    - 포트포워딩
        - 22(SSH)
        - 80(Apache)
2. UFW 방화벽 설치
    ```bash
    ~$ sudo ufw enable          # ufw 방화벽 활성화
    ~$ sudo ufw allow ssh       # ssh 포트 허용
    ~$ sudo ufw allow 80        # 80(Apache) 포트 허용
    ~$ sudo ufw status          # 설정한 포트 상태 확인
    ```
3. Apache 설치 및 설정
    ```bash
    sudo apt install apache2        # 아파치 설치
    sudo systemctl enable apache2   # 서버 작동 시 아파치 서버 자동 실행 설정
    sudo systemctl start apach32    # 아파치 실행
    sudo systemctl status apache2   # 아차피 서버 상태 확인
    ```
4. MySQL 설치 및 DB 설정
    
    - MySQL 설치
    ```bash
    sudo apt install mysql-server   # mysql 설치
    sudo mysql -u root              # root 계정으로 mysql 접속
    ```
    
    - DB 사용자 생성 및 권한 설정 
    ```sql
    -- DB 이름
    mysql> CREATE DATABASE wordpress;    

    -- DB 사용자 생성
    mysql> CREATE USER '유저 이름'@'localhost' IDENTIFIED BY '비밀번호';        

    -- DB 사용자 권한 설정
    mysql> GRANT ALL PRIVILEGES ON wordpress.* TO '유저 이름'@'localhost';      

    -- DB 사용자 권한 적용
    mysql> FLUSH PRIVILEGES;       

    mysql> EXIT;
    ```

5. PHP 파일 실행 관련 설치
    ```bash
    sudo apt install php php-mysql php-curl php-gd php-mbstring php-xml php-xmlrpc
    ```

6. Wordpress 설치
    ```bash
    # Apache 디렉터리로 이동
    cd /var/www/html
    # Wordpress 다운로드
    wget https://wordpress.org/latest.tar.gz
    # 다운로드한 압축파일 압축해제
    tar -xzvf latest.tar.gz
    # wordpress 디렉터리 권한 변경
    sudo chmod 755 wordpress/
    ```

<br>

# 2. Wordpress 설정 및 사용
1. Wordpress에 DB 계정정보 입력
```bash
cd /var/www/html/wordpress/
cp wp-config-sample.php wp-config.php       # wp-config.php 파일 생성
vi wp-config.php                            # wp-config.php 파일 수정(아래 코드블럭 참고)
```

*wp-config.php*
```php
// ** Database settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'wp_db' );

/** Database username */
define( 'DB_USER', 'wp_user' );

/** Database password */
define( 'DB_PASSWORD', 'wp_user' );

/** Database hostname */
define( 'DB_HOST', 'localhost' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );
```
-> 위에서 생성한 DB 계정 정보에 맞게 입력

2. Wordpress 사용

    1) 브라우저를 통해 `http://localhost/wordpress/wp-admin/install.php` 접속

    2) `install` 버튼 클릭
    3) `http://localhost/wordpress/wp-login.ph` 접속
    4) wordpress 계정 생성
    5) wordpress 이용

<br>

# Result
![Image](https://github.com/user-attachments/assets/d91546e4-a846-4889-a53c-1a9db38d6b8e)

➡️ [Video Link](https://github.com/user-attachments/assets/51684ae3-0d48-4b7b-af48-350322adf973)