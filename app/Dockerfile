FROM ubuntu
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update -y --fix-missing
RUN apt-get install -y indelible
RUN apt-get install -y mafft
RUN apt-get install -y python3-pip python-dev build-essential

RUN pip3 install --upgrade pip

COPY requirements.txt /requirements.txt
RUN pip3 install --no-cache-dir -r requirements.txt

COPY . /app/
WORKDIR /app/

ADD . /app/

RUN cd /app/cpp_code && make all

ENV DEBUG=0

ENTRYPOINT ["python3", "pipeline_click.py"]  # execution command prefix. cannot be overidden unless done here.
#CMD python3 pipeline_click.py --path example_run/ --msaf msa.fasta --trf tree.txt
