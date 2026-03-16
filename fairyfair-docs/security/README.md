# Безопасность платформы

## Содержание

- [Аутентификация и управление сессиями](./authentication.md)
- [Двухфакторная аутентификация](./2fa.md)
- [Защита от веб-атак](./web-security.md)
- [Инфраструктурная изоляция](./infrastructure.md)
- [Мониторинг и обнаружение атак](./monitoring.md)

---

## Краткий обзор

| Компонент | Решение |
|-----------|---------|
| Хеширование паролей | Argon2 (memory-hard) |
| Токены сессий | JWT HS256 с JTI, привязка к IP + User-Agent + fingerprint |
| Refresh-токены | SHA-256 хеш в БД, ротация при каждом обновлении |
| Cookie | HttpOnly + Secure + SameSite=Lax |
| 2FA | TOTP (Google Authenticator / Яндекс.Ключ), обязателен для admin |
| CSRF | HMAC-SHA256 nonce, constant-time сравнение |
| Rate limiting | Redis, гранулярные лимиты по эндпоинтам |
| SQL-инъекции | ORM + параметризованные запросы, no raw SQL |
| Валидация | Pydantic v2 на всех API-эндпоинтах |
| Платёжные вебхуки | IP-whitelist + HMAC + Pydantic |
| Admin-доступ | VPN / именной сертификат + 2FA |
| SSH | Только по ключам, fail2ban |
| Секреты 2FA | Fernet (AES-128-CBC) в БД |
