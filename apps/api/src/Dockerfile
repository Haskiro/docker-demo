#более легкая основа для образа, вместо обычной node:14
FROM node:14-alpine
WORKDIR /opt/app
#сначала добавляем только package.json, устанавливаем зависимости и только после этого
#вставляем все остальные файлы, чтобы при изменении кода зависимости не устанавливались заново а брались из кэша
ADD *.json ./ 
RUN npm install
ADD . .
RUN npm  run build api
CMD ["node", "./dist/apps/api/main.js"]