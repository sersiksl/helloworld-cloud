FROM python:alpine3.7
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
RUN chmod 444 index.py
RUN chmod 444 requirements.txt
 
# Service must listen to $PORT environment variable.
# This default value facilitates local development.
ENV PORT 8080
CMD python ./index.py
