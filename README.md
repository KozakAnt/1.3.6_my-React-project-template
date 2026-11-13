Добавление Vitest в проект

1. Добавление пакета Vitest через npm: yarn add -D vitest

2. Так как Vitest предоставляет нам только функции для тестирования, понадобятся дополнительные пакеты:
   для имитации браузера (взаимодействия с HTML и API браузера) добавляем пакет jsdom: yarn add -D jsdom
   для работы с React и имитации пользовательских действий нужно добавить следующие пакеты:
   yarn add -D @testing-library/jest-dom @testing-library/react @testing-library/user-event

3. Настройка конфигурации Vitest. Два способа:

создать отдельный файл с vitest.config.ts. Этот способ лучше использовать, если проект не на Vite:
export default defineConfig({
test: {
globals: true,
environment: 'jsdom',
}
})

или добавить настройки в конфиг-файл vite.config.ts. Этот способ лучше подходит для проекта на Vite. Нужно добавить в объект, который принимает параметром функция defineConfig, поле test. Но перед импотром defineConfig необходимо добавить строку “/// <reference types="vitest"/>”:

import { defineConfig } from 'vitest/config';
import react from '@vitejs/plugin-react';

export default defineConfig({
plugins: [react()],
test: {
globals: true,
environment: 'jsdom',
},
});

4.  Скрипт для запуска тестов в package.json:

    {
    "scripts": {
    "test": "vitest"
    }
    }
