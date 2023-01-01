FROM php
RUN mkdir template
RUN mkdir content
COPY website/ ./
COPY website/content/* ./content
COPY website/template/* ./template
EXPOSE 80
CMD ["php","-s","0.0.0.0:80"]
