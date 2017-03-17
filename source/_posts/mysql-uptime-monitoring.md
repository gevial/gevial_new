---
title: Мониторинг аптайма MySQL
date: 2017-02-20 15:13:45
tags: [mysql, monitoring]
---
Любая система мониторинга доступности сервиса выполняет проверки с определённым интервалом.
Зачастую он составляет 60 секунд. В таком случае кратковременные перебои в работе сервиса (например, перезапуски) обнаружены не будут.
Чтобы обойти эту неприятную ситуацию, можно мониторить аптайм демона. Для MySQL он выводится командой
```sql
SHOW GLOBAL STATUS LIKE "UPTIME";
```
В отсутствие перезапусков (т.е. в штатной работе) эта метрика должна только возрастать. Если обнаружена отрицательная динамика - демон был перезапущен.