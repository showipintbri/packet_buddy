FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive
ARG PIP_BREAK_SYSTEM_PACKAGES=1

RUN echo "==> Upgrading apk and installing system utilities ...." \
 && apt -y update \
 && apt-get install -y wget \
 && apt-get -y install sudo

RUN echo "==> Installing Python3 and pip ...." \  
 && apt-get install python3 -y \
 && apt install python3-pip -y

RUN echo "==> Install dos2unix..." \
  && sudo apt-get install dos2unix -y 

RUN echo "==> Install langchain requirements.." \
  && pip install -U --quiet langchain_experimental langchain langchain-community \
  && pip install chromadb \
  && pip install tiktoken

RUN echo "==> Install jq.." \
  && pip install jq

RUN echo "==> Install streamlit.." \
  && pip install streamlit --upgrade

# Install tshark
RUN apt-get update && apt-get install -y tshark

RUN echo "==> Adding pyshark ..." \
  && pip install pyshark

RUN echo "==> Adding requests ..." \
  && pip install requests

RUN echo "==> Adding InstructorEmbedding ..." \
  && pip install -U sentence-transformers==2.2.2 \
  && pip install InstructorEmbedding

COPY /packet_buddy /packet_buddy/
COPY /scripts /scripts/

RUN echo "==> Convert script..." \
  && dos2unix /scripts/startup.sh

CMD ["/bin/bash", "/scripts/startup.sh"]
