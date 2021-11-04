FROM python:3.7

RUN apt-get update
RUN apt-get install -y --no-install-recommends nginx

RUN rm /etc/nginx/nginx.conf
COPY conf/nginx.conf /etc/nginx/

WORKDIR /usr/deploy
COPY . /usr/deploy/

RUN /usr/local/bin/python -m pip install --upgrade pip
RUN pip3 install -r requirements.txt

EXPOSE 5000
EXPOSE 8080

CMD service nginx start && gunicorn -w 3 -b :5000 -t 360 --reload wsgi:app
