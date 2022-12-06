## Инициализация проекта
##### Создаем файл package.json
```
npm init -y
```
##### Устанавливаем typescript
```
npm i -D typescript npm install @types/node --save-dev
```
## Настройка TypeScript компилятора
##### Создаем файл tsconfig.json
```
npx tsc -init
```
##### Оставляем эти настройки
```
{
  "compilerOptions": {
    "target": "ES2018",
    "lib": ["ES6"],
    "module": "NodeNext",
    "rootDir": "./src",
    "resolveJsonModule": true,
    "allowJs": true,
    "sourceMap": true,
    "outDir": "./build",
    "removeComments": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "noImplicitAny": true,
    "skipLibCheck": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules"],
  "lib": ["esnext"],
  "ts-node": {
    "esm": true
  }
}
```

##### Добавляем в package.json поддержку синтаксиса модулей для Node.js
```
"type": "module"
```
##### Создаем папку src, где хранится весь исходный код

## Настройка для режима разработки
##### Устанавливаем пакеты
```
npm install --save-dev ts-node nodemon
```
##### Добавляем в корень настройку для nodemon в файле nodemon.json
```
{
  "watch": ["src"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "npx ts-node ./src/main.ts"
}
```
##### Добавляем скрипт в package.json
```
"dev": "npx nodemon"
```
## Настройка для режима публикации
##### Ставим пакет для очистки папок
```
npm install --save-dev rimraf
```
##### Добавляем 2 скрипта в package.json
```
"start": "npm run build && node build/main",
"build": "rimraf ./build && npx tsc"
```
## Настройка ESlint
##### Ставим пакеты
```
npm i -D eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser
```
##### Создаем в корне .eslintrc
```
{
  "parser": "@typescript-eslint/parser",
  "extends": ["plugin:@typescript-eslint/recommended"],
  "parserOptions": { "ecmaVersion": 2018, "sourceType": "module" },
  "rules": {
    "@typescript-eslint/no-inferrable-types": "off"
  }
}
```
##### Добавляем 2 скрипта в package.json
```
"lint": "npx eslint ./src",
"format": "npx eslint ./src --fix"
```
## Настройка Prettier
##### Ставим пакет
```
npm i -D prettier
```
##### В корне добавляем файл .prettierrc
```
{
  "semi": true,
  "trailingComma": "all",
  "singleQuote": true,
  "printWidth": 120,
  "tabWidth": 2
}
```
## Настройка Husky
##### Ставим пакет
```
npm i -D husky
```
##### Добавляем настройку в корень package.json
```
"husky": {
  "hooks": {
    "pre-commit": "npm run lint"
  }
}
```