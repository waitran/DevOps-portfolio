<div align="center">

<img src="https://img.shields.io/badge/WAITRAN-ENGINEERING%20PORTFOLIO-0f172a?style=for-the-badge&amp;labelColor=0f172a&amp;color=0f172a" alt="waitran · engineering portfolio">

<h1>Данил · DevOps / DevSecOps</h1>

<p><strong>Автоматизировать рутину. Понимать систему. Делать сбои объяснимыми.</strong></p>

<p>Ищу стажировку или junior-роль<br>Linux · контейнеры · CI · наблюдаемость · безопасность</p>

<a href="https://github.com/waitran"><img src="https://img.shields.io/badge/GitHub-waitran-e2e8f0?style=for-the-badge&amp;logo=github&amp;logoColor=white&amp;labelColor=0f172a" alt="GitHub waitran"></a>
<img src="https://img.shields.io/badge/Open%20to-Intern%20%2F%20Junior-34d399?style=for-the-badge&amp;labelColor=0f172a" alt="Открыт к стажировкам и junior-позициям">

<br><br>

<a href="#-проекты">Проекты</a> &nbsp;·&nbsp;
<a href="#-технологии-в-деле">Технологии</a> &nbsp;·&nbsp;
<a href="#-результаты-и-проверки">Результаты</a> &nbsp;·&nbsp;
<a href="#-контакт">Контакт</a>

</div>

---

### Обо мне

Развиваюсь в DevOps и DevSecOps через практические проекты: работаю с **Linux и Python**, собираю контейнерные стенды, настраиваю проверки и разбираюсь в поведении сервисов при сбоях.

Мне интересно всё, что связывает код с его эксплуатацией: **воспроизводимый запуск, понятные метрики, диагностика и ограничения доступа**. Здесь собраны учебные работы и pet-проекты с конкретными примерами того, что можно посмотреть в коде.

<table>
<tr>
<td width="33%" valign="top">

<strong>⚙️ Автоматизация</strong><br><br>
Python, CLI-инструменты, повторяемые команды запуска и проверки.

</td>
<td width="33%" valign="top">

<strong>📈 Надёжность</strong><br><br>
Метрики, алерты, SLI/SLO, контролируемые ошибки и диагностика по runbook.

</td>
<td width="33%" valign="top">

<strong>🛡️ Безопасность</strong><br><br>
Контейнер без root, ограничение привилегий и ресурсов, минимальные права CI.

</td>
</tr>
</table>

## 🚀 Проекты

### 01 &nbsp; Reliability Lab

> **От HTTP-запроса до метрики, алерта и восстановления.**

Учебный стенд для практики эксплуатации: HTTP-сервис на Python, Prometheus, Docker Compose и GitHub Actions. В сервисе можно явно включить ошибки и задержки, наблюдать последствия и пройти диагностику по инструкции.

<img src="https://img.shields.io/badge/Python-3.12-3776AB?style=flat-square&amp;logo=python&amp;logoColor=white" alt="Python 3.12"> <img src="https://img.shields.io/badge/Docker-Compose-2496ED?style=flat-square&amp;logo=docker&amp;logoColor=white" alt="Docker Compose"> <img src="https://img.shields.io/badge/Prometheus-metrics%20%26%20alerts-E6522C?style=flat-square&amp;logo=prometheus&amp;logoColor=white" alt="Prometheus"> <img src="https://img.shields.io/badge/GitHub_Actions-CI-2088FF?style=flat-square&amp;logo=githubactions&amp;logoColor=white" alt="GitHub Actions">

| Задача | Реализация | Посмотреть |
| :--- | :--- | :--- |
| Наблюдать поведение сервиса | Счётчики HTTP-ответов, histogram задержки, health/readiness endpoints | [Код сервиса][lab-app] |
| Воспроизводить среду | Compose, healthcheck, лимиты CPU/RAM/PID, постоянный том Prometheus | [Конфигурация][lab-compose] |
| Проверять изменения | Unit-тесты, валидация конфигурации, тесты правил, сборка и smoke-проверка | [CI workflow][lab-ci] |
| Обнаруживать деградацию | Алерты недоступности target, доли ошибок и p95 задержки | [Правила и тестовые ряды][lab-monitoring] |
| Восстанавливаться по инструкции | Сценарии ошибок и задержек, диагностика, проверка восстановления | [Runbook][lab-runbook] |
| Уточнять границы измерений | Определения SLI, цели SLO, бюджет ошибок и ограничения данных | [SLO][lab-slo] |

**Инженерный акцент:** проверки здоровья не увеличивают счётчик полезных операций; инъекции выключены по умолчанию в приложении; алерты ошибок и задержки учитывают минимальный трафик.

**[Исходники стенда →][lab]** &nbsp;·&nbsp; **[Отчёт о проверке →][lab-validation]** &nbsp;·&nbsp; **[Успешный CI →][lab-run]**

<details>
<summary><strong>Воспроизвести лабораторию</strong></summary>

<br>

Текущая ветка портфолио содержит только этот README. Полный стенд сохранён в истории на коммите `4e3681d`; все ссылки проекта закреплены за этой версией.

Нужны Git, Docker Engine с Compose v2+, make и Python 3.12+. Порты 8080 и 9090 должны быть свободны.

```bash
git clone https://github.com/waitran/DevOps-portfolio.git
cd DevOps-portfolio
git switch --detach 4e3681da63ffaa4e348e7701265964e3afbbe44a

make test
make check-config
make test-rules
make up
make smoke
make load
```

Сервис: [127.0.0.1:8080/healthz](http://127.0.0.1:8080/healthz) · Метрики: [127.0.0.1:8080/metrics](http://127.0.0.1:8080/metrics) · Prometheus: [127.0.0.1:9090](http://127.0.0.1:9090)

```bash
make chaos       # 180 секунд: каждый четвёртый запрос возвращает учебный HTTP 500
make recover     # 330 секунд успешного трафика, чтобы ошибки вышли из окна 5m
make latency     # отдельное упражнение с задержкой 600 ms
make recover
make down
```

Сценарии выполняются по одному. Порты Compose привязаны к loopback; инъекции предназначены для локальной лаборатории. Подробности и условия срабатывания алертов — в [runbook][lab-runbook].

</details>

<br>

### 02 &nbsp; IT Radar

> **Автоматизация поиска стажировок и IT-возможностей.**

Pet-проект на Python: сбор публикаций из публичных источников, фильтрация и дедупликация, хранение в SQLite, Telegram-интерфейс и контейнерный запуск.

**Статус:** исходники IT Radar сейчас закрыты. Проект упомянут как дополнительная работа; публичные исходники и результаты проверок доступны в разделе Reliability Lab.

## 🧰 Технологии в деле

<div align="center">

<img src="https://img.shields.io/badge/Linux-0f172a?style=for-the-badge&amp;logo=linux&amp;logoColor=FCC624" alt="Linux">
<img src="https://img.shields.io/badge/Bash-0f172a?style=for-the-badge&amp;logo=gnubash&amp;logoColor=4EAA25" alt="Bash">
<img src="https://img.shields.io/badge/Python-0f172a?style=for-the-badge&amp;logo=python&amp;logoColor=3776AB" alt="Python">
<img src="https://img.shields.io/badge/Git-0f172a?style=for-the-badge&amp;logo=git&amp;logoColor=F05032" alt="Git">
<br>
<img src="https://img.shields.io/badge/Docker-0f172a?style=for-the-badge&amp;logo=docker&amp;logoColor=2496ED" alt="Docker">
<img src="https://img.shields.io/badge/GitHub_Actions-0f172a?style=for-the-badge&amp;logo=githubactions&amp;logoColor=2088FF" alt="GitHub Actions">
<img src="https://img.shields.io/badge/Prometheus-0f172a?style=for-the-badge&amp;logo=prometheus&amp;logoColor=E6522C" alt="Prometheus">

</div>

<br>

| Область | Подтверждённая практика |
| :--- | :--- |
| **Linux & scripting** | Python-сервис и CLI-генератор трафика, HTTP/JSON, команды Make для запуска и диагностики |
| **Контейнеры** | Dockerfile, Docker Compose, healthcheck, volumes и ограничения ресурсов |
| **CI** | GitHub Actions: тесты → проверка конфигурации → сборка → запуск → smoke |
| **Observability** | Prometheus, PromQL, counters/histograms, recording rules и алерты |
| **Reliability** | Учебные SLI/SLO, инъекция ошибок/задержек, runbook |
| **Security** | Non-root приложение, read-only FS, drop capabilities, no-new-privileges, права CI `contents: read` |

**Следующий фокус — Kubernetes и CD:** probes, requests/limits, rolling update, проверяемое развёртывание и откат. Эти этапы пока не представлены здесь как завершённые проекты. Публичных исходников KubeOptimizer и отдельного стенда Chaos Mesh/k6 для включения в портфолио на момент оформления не найдено.

## ✅ Результаты и проверки

| Проверка Reliability Lab | Зафиксированный результат |
| :--- | :--- |
| Unit-тесты | **8 / 8** — GitHub Actions, 14 ноября 2026 |
| Правила Prometheus | **6 сценариев** на синтетических временных рядах |
| Контролируемые ошибки | **40 запросов → 30 × HTTP 200 + 10 × HTTP 500**, неожиданных ответов 0 |
| Контролируемая задержка | **8 запросов с 600 ms → 8 × HTTP 200**, неожиданных ответов 0 |
| Docker и HTTP | **Сборка и запуск успешны**, `/healthz`, `/readyz`, `/api/work`, `/metrics` прошли smoke-проверку |
| Prometheus | **Сбор метрик подтверждён:** `up{job="demo"}=1` |
| Удалённый CI для версии `4e3681d` | **[Успешное выполнение 14 ноября 2026][lab-run]** |

Результаты подтверждены логами [запуска GitHub Actions от 14 ноября 2026][lab-run] для закреплённой версии `4e3681d`. Правила алертов проверены на синтетических временных рядах; полный ручной цикл `pending → firing → inactive` этим запуском не подтверждён. Подробности предыдущей проверки — в [отчёте лаборатории][lab-validation]. Цель **99,5% успешных операций за 30 дней** описана в SLO как учебная цель; достигнутая доступность и production-опыт не заявляются. Доставка уведомлений, Kubernetes и автоматический deployment в эту версию лаборатории не входят.

<details>
<summary><strong>🇬🇧 English overview</strong></summary>

<br>

**Danil · DevOps / DevSecOps · seeking an internship or junior role**

I build learning projects around Linux automation, containerised services, CI and observability. My public work includes a Python reliability lab with Docker Compose, Prometheus metrics and alert tests.

- **Reliability Lab:** health checks, counters and latency histograms, controlled fault injection, CI validation, SLI/SLO definitions and an incident runbook.
- **Security practice:** a non-root application container, read-only filesystems, dropped capabilities, resource limits and read-only CI permissions.
- **Next:** Kubernetes deployment, delivery pipelines and verified rollback.

The lab passed GitHub Actions validation on 14 November 2026: 8 unit tests, Prometheus rule tests, container build/start, HTTP smoke checks, injected error/latency traffic and a successful Prometheus scrape. All metrics above describe this lab validation. They do not represent production availability. IT Radar source repositories are currently private.

**[Source snapshot][lab] · [Validation report][lab-validation] · [CI evidence][lab-run]**

</details>

---

<div align="center">

<h3 id="-контакт">🤝 Контакт</h3>

<p>Открыт к стажировкам и junior-позициям в DevOps / DevSecOps.<br>Готов обсудить проекты, технические решения и задачи команды.</p>

<a href="https://github.com/waitran"><img src="https://img.shields.io/badge/Посмотреть_профиль-@waitran-34d399?style=for-the-badge&amp;logo=github&amp;logoColor=white&amp;labelColor=0f172a" alt="Профиль waitran на GitHub"></a>

<br><br>

<sub>Учебные проекты · Проверяемые исходники · Понятные ограничения</sub>

</div>

[lab]: https://github.com/waitran/DevOps-portfolio/tree/4e3681da63ffaa4e348e7701265964e3afbbe44a
[lab-app]: https://github.com/waitran/DevOps-portfolio/blob/4e3681da63ffaa4e348e7701265964e3afbbe44a/app/server.py
[lab-compose]: https://github.com/waitran/DevOps-portfolio/blob/4e3681da63ffaa4e348e7701265964e3afbbe44a/compose.yaml
[lab-ci]: https://github.com/waitran/DevOps-portfolio/blob/4e3681da63ffaa4e348e7701265964e3afbbe44a/.github/workflows/ci.yml
[lab-monitoring]: https://github.com/waitran/DevOps-portfolio/tree/4e3681da63ffaa4e348e7701265964e3afbbe44a/monitoring
[lab-runbook]: https://github.com/waitran/DevOps-portfolio/blob/4e3681da63ffaa4e348e7701265964e3afbbe44a/docs/RUNBOOK.md
[lab-slo]: https://github.com/waitran/DevOps-portfolio/blob/4e3681da63ffaa4e348e7701265964e3afbbe44a/docs/SLO.md
[lab-validation]: https://github.com/waitran/DevOps-portfolio/blob/4e3681da63ffaa4e348e7701265964e3afbbe44a/docs/VALIDATION.md
[lab-run]: https://github.com/waitran/DevOps-portfolio/actions/runs/43627817612
