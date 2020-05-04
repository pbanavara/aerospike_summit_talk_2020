FROM python:3
WORKDIR /
RUN pip install --no-cache-dir flask requests aerospike
copy . .
EXPOSE 5000
CMD ["python", "./src/python_client.py"] 
