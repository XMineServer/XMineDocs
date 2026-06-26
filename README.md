# XMine API Docs

Портал документации REST API для сервисов XMine. Публикуется автоматически через GitHub Pages.

## Структура

```
specs/
  index.json              # реестр сервисов (генерируется автоматически)
  identity-service/
    openapi.yaml
  economy-service/
    openapi.yaml
  ...
index.html                # Swagger UI портал
```

## Как добавить новый сервис

1. Скопируй `service-workflow-template.yml` в свой репозиторий:
   ```
   .github/workflows/publish-spec.yml
   ```

2. В настройках своего репозитория задай переменную:
   - `Settings → Secrets and variables → Actions → Variables`
   - Имя: `SERVICE_ID`
   - Значение: `my-service-name` (латиница, дефисы)

3. Убедись что в репозитории XMineDocs есть секрет `DOCS_DEPLOY_TOKEN`
   - `Settings → Secrets and variables → Actions → Secrets`
   - Это Personal Access Token с правом `repo` на XMineDocs

4. Запушь изменения в `api/openapi.yaml` — спека автоматически появится на портале.

## Настройка GitHub Pages (первый раз)

1. `Settings → Pages → Source` → выбери **GitHub Actions**
2. Запушь любое изменение в `main` — сработает `deploy-pages.yml`
3. Портал будет доступен по адресу: `https://xmineserver.github.io/XMineDocs`

## Personal Access Token

Токен нужен для того чтобы workflow из сервисных репозиториев могли писать в XMineDocs.

1. Перейди в `github.com → Settings → Developer settings → Personal access tokens → Fine-grained tokens`
2. Создай токен с доступом к репозиторию `XMineDocs`:
   - `Contents: Read and Write`
3. Добавь токен как секрет `DOCS_DEPLOY_TOKEN` в каждый сервисный репозиторий
   (или один раз на уровне организации: `Organization Settings → Secrets`)
