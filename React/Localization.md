# Localization

Создание мультиязычности обычно достигается следующим путем:

1) Создаются файлы переводов, например в public/locales, следующего содержания:
```
locales/
    en/
        translation.json
    ru/
        translation.json
```
```json
{
    "notifications": {
        "not_empty": "It should not be empty",
        "success": "Success"
        ...
    },
    "errors": {...}
}
```
2) Настраивается локализация
```js
// src/i18n.ts
import i18n from 'i18next';
import LanguageDetector from 'i18next-browser-languagedetector';
import Backend from 'i18next-http-backend';
import { initReactI18next } from 'react-i18next';
import { ENV } from 'utils/constants/env';

i18n
  .use(Backend)
  .use(LanguageDetector)
  .use(initReactI18next)
  .init({
    compatibilityJSON: 'v3',
    fallbackLng: 'ru',
    debug: ENV === 'dev',
    detection: {
      order: ['localStorage'],
      caches: ['localStorage'],
    },
    interpolation: {
      escapeValue: false,
    },
  });

export default i18n;

```
3) Используется нужная строка с помощью useTranslate
```js
import { useTranslation } from 'react-i18next';
const Alert = () => {
    const t = useTranslate(); // для удобства
    return <div>{t('notification.success')}</div> // "Success" для en

```