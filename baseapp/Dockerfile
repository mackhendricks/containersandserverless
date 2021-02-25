FROM python:3
RUN mkdir app
COPY . /app
RUN pip install -r ./app/requirements.txt
ENV SLACK_API_KEY=""
ENV DB_USER=""
ENV DB_PASS=""
CMD ["python", "./app/app.py"]
