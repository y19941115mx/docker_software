FROM sequenceiq/hadoop-docker:2.7.1

# Install Hive and configure Namenode
RUN curl -s https://downloads.apache.org/hive/hive-2.3.9/apache-hive-2.3.9-bin.tar.gz | tar -xz -C /usr/local/
RUN ln -s /usr/local/apache-hive-2.3.9-bin /usr/local/hive
ENV HIVE_HOME=/usr/local/hive
ENV PATH=$PATH:$HIVE_HOME/bin
RUN cp $HIVE_HOME/conf/hive-default.xml.template $HIVE_HOME/conf/hive-site.xml
RUN echo "export HADOOP_HOME=/usr/local/hadoop" >> $HIVE_HOME/conf/hive-env.sh

# Start Namenode and Hive Metastore
CMD ["bash", "-c", "/etc/bootstrap.sh && $HADOOP_HOME/sbin/start-dfs.sh && $HADOOP_HOME/sbin/start-yarn.sh && hive --service metastore"]