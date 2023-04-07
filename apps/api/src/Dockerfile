#более легкая основа для образа, вместо обычной node:14
FROM node:14-alpine as build
WORKDIR /opt/app
#сначала добавляем только package.json, устанавливаем зависимости и только после этого
#вставляем все остальные файлы, чтобы при изменении кода зависимости не устанавливались заново а брались из кэша
ADD *.json ./ 
RUN npm install
ADD . .
RUN npm  run build api

# доп стадия, на которой создается финальный образ без всех ненужных файлов, атолько 
# зависимости node_modules и main.js
FROM node:14-alpine
WORKDIR /opt/app
ADD package.json ./
RUN npm install --only=prod
COPY --from=build /opt/app/dist/apps/api ./dist
CMD ["node", "./dist/main.js"]

