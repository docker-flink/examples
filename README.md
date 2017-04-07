Flink Docker Examples
=====================

Examples for how to use the Flink Docker images in a variety of ways.

Flink Helm Chart
----------------

Build the Helm archive:

    $ helm package helm/flink/

Deploy a non-HA Flink cluster with a single taskmanager:

    $ helm install --name my-cluster flink*.tgz

Deploy a non-HA Flink cluster with three taskmanagers:

    $ helm install --name my-cluster --set flink.num_taskmanagers=3 flink*.tgz

Deploy an HA Flink cluster with three taskmanagers:

    $ cat > values.yaml <<EOF
    flink:
      num_taskmanagers: 3
      highavailability:
        enabled: true
        zookeeper_quorum: <zookeeper quorum string>
        state_s3_bucket: <s3 bucket>
        aws_access_key_id: <aws access key>
        aws_secret_access_key: <aws secret key>
    EOF
    $ helm install --name my-cluster --values values.yaml flink*.tgz
