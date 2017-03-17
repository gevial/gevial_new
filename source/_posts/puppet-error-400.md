---
title: Puppet Error 400
description: "Что делать, если Puppet не видит модуль."
date: 2015-06-17
tags: [puppet, troubleshooting]
---
Сегодня добавил в репозиторий Puppet новый модуль, прописал его в манифесте ноды. На ноде puppet agent не мог получить каталог с сервера - сервер “не видел” модуль.

В консоли это выглядело так:

```
Error: Could not retrieve catalog from remote server:
Error 400 on SERVER: Puppet::Parser::AST::Resource failed with error ArgumentError:
Could not find declared class rclocal at
/var/git/puppet-main/production/manifests/service_nodes/redis.timeweb.net.pp:31
on node redis1.timeweb.net
Warning: Not using cache on failed catalog
Error: Could not retrieve catalog; skipping run
```

Модуль располагался в правильной директории, ошибки не должно было быть. Оказалось, что причиной являлось отсутствие некоторых обязательных полей в `metadata.json` этого модуля. После добавления всех обязательных полей из [https://docs.puppetlabs.com/puppet/latest/reference/modules_publishing.html#fields-in-metadatajson](https://docs.puppetlabs.com/puppet/latest/reference/modules_publishing.html#fields-in-metadatajson) ошибка исчезла.