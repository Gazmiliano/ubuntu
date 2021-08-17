sudo systemctl stop mysql
sudo systemctl edit mysql

[Service]
ExecStart=
ExecStart=/usr/sbin/mysqld --skip-grant-tables --skip-networking

sudo systemctl daemon-reload

chown -R mysql:mysql /var/lib/mysql

sudo systemctl start mysql
sudo mysql -u root

mysql> FLUSH PRIVILEGES;
mysql> GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'Password';
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password';
mysql> exit
mysql> FLUSH PRIVILEGES;

sudo systemctl revert mysql
sudo systemctl daemon-reload
sudo systemctl restart mysql