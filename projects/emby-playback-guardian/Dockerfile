FROM python:3.12-slim
COPY . /src
WORKDIR /src
RUN pip install --no-cache-dir -r requirements.txt
RUN python -m py_compile guardian.py && echo "guardian.py compiles"
