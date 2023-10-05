# Use an official Debian-based Python image
FROM python:3.8-slim-buster

# Set environment variables for PySpark
ENV SPARK_HOME=/usr/spark-3.3.0-bin-hadoop3
ENV PYTHONPATH=$SPARK_HOME/python:$PYTHONPATH

# Install dependencies
RUN apt-get update && apt-get install -y wget

# Install OpenJDK manually
RUN mkdir -p /usr/lib/jvm && \
    wget -q https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz -O /tmp/openjdk.tar.gz && \
    tar xzf /tmp/openjdk.tar.gz -C /usr/lib/jvm && \
    rm /tmp/openjdk.tar.gz && \
    update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.2/bin/java 100 && \
    update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.2/bin/javac 100

# Install Spark (adjust Spark version as needed)
RUN wget -q https://archive.apache.org/dist/spark/spark-3.3.0/spark-3.3.0-bin-hadoop3.tgz && \
    tar xf spark-3.3.0-bin-hadoop3.tgz -C /usr/ && \
    rm spark-3.3.0-bin-hadoop3.tgz

# Install Python packages
RUN pip install jupyter pandas pyspark findspark matplotlib seaborn scipy

# Expose Jupyter port
EXPOSE 8888

# Start Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
