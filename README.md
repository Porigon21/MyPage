> [!NOTE]
> [setup.sh](setup.sh)はsudoを使用します。
> あと、作業用ディレクトリで行ってください。

```
#!/bin/bash

# Node.jsとnpmの準備
sudo bash
apt install nodejs npm -y
npm install

# MariaDBのインストール
sudo apt update
sudo apt install -y mariadb-server

# MariaDBサービスの起動と有効化
sudo systemctl start mariadb
sudo systemctl enable mariadb

# MariaDBの初期設定 (rootパスワードの設定など)
sudo mysql_secure_installation

# MariaDBに接続してデータベースとテーブルを作成
echo "Creating database and table..."
sudo mysql -u root -p <<EOF
CREATE DATABASE IF NOT EXISTS mydb;
USE mydb;
CREATE TABLE IF NOT EXISTS posts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    content TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
EOF

echo "Database and table creation complete."

```
