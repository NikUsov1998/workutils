If you encountered 504 Outdated Optimize Dep error after docker build then

From repo root:

```
docker compose down -v
```

Then remove all frontend caches on HOST too:

```
sudo find . -name node_modules -type d -prune -exec rm -rf {} +
```

```
sudo find . -name .vite -type d -prune -exec rm -rf {} +
```

```
sudo find . -name dist -type d -prune -exec rm -rf {} +
```

Then rebuild:

```
docker compose build --no-cache
```

```
docker compose up
```

---
if you encountered 301 

In `.env` file you must replace `http` with `https`:

```
VITE_APP_API_ROOT=https://127.0.0.1
```

```
CSRF_TRUSTED_ORIGINS='["https://127.0.0.1","https://localhost"]'
```

Then rebuild updated container
```
docker compose up -d --build
```
And advice you to clear cookies for localhost
```
https://127.0.0.1
```