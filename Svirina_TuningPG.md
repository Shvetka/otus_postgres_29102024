# Тюнинг Постгреса

## Создаем бд

CREATE DATABASE benchmark;

## Заполняем данными

pgbench -h 127.0.0.1 -p 5432 -U postgres -i -s 150 benchmark

## Проводим тест

pgbench -h 127.0.0.1 -p 5432 -U postgres -c 50 -j 2 -P 60 -T 600 benchmark

transaction type: <builtin: TPC-B (sort of)>
scaling factor: 150
query mode: simple
number of clients: 50
number of threads: 2
duration: 600 s
number of transactions actually processed: 133209
latency average = 225.066 ms
latency stddev = 117.261 ms
initial connection time = 381.263 ms
tps = 222.062292 (without initial connection time)

Обработано 133209 транзакций с пропускной способностью 222 транзакций в секунду

## Настроила параметры ссайта https://www.pgconfig.org для OLTP систем

sudo nano /var/lib/postgresql/14/main/postgresql.conf

effective_cache_size = 3GB
work_mem = 14MB
maintenance_work_mem = 205MB
checkpoint_completion_target=0.9
wal_buffers=-1
listen_addresses='*'
random_page_cost=4.0
effective_io_concurrency=2
max_worker_processes=8
max_parallel_workers_per_gather=2
max_parallel_workers=2
min_wal_size =2GB
max_wal_size=3GB

## Проводим тест
pgbench -h 127.0.0.1 -p 5432 -U postgres -c 50 -j 2 -P 60 -T 600 benchmark

transaction type: <builtin: TPC-B (sort of)>
scaling factor: 150
query mode: simple
number of clients: 50
number of threads: 2
duration: 600 s
number of transactions actually processed: 219347
latency average = 136.664 ms
latency stddev = 165.826 ms
initial connection time = 385.322 ms
tps = 365.637492 (without initial connection time)
postgres@compute-vm-2-2-20-ssd-1736420818884:~$

Обработано 219347 транзакций с пропускной способностью 365 транзакций в секунду

# Производительность выросла
