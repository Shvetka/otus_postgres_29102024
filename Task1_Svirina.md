# SQL и реляционные СУБД. PostgreSQL в облаках 

## 1. Дефолтный уровень изоляции read committed 
 Во второй сессии изменений не увидим, т.к. прочитать можно только закомиченое
 Как только поставили комит смогли увидеть во второй сессии
## 2.REPEATABLE READ
 Смогли увидеть незакомиченные изменения в первой сессии, но во второй недоступны. После комита везде видно
## 3. SERIALIZABLE
 Откатил одну транзакцию