FROM mariadb:latest

COPY . .

EXPOSE 3306

ADD card.sql /docker-entrypoint-initdb.d

CMD ["mariadbd"]
