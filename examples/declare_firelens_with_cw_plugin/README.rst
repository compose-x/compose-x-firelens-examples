
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X

################################################
Declare FireLens with CloudWatch group
################################################

Very simple example where you set the driver to ``awsfirelens`` and the `CloudWatch plugin`_ options.
Compose-X will automatically deal with IAM permissions to enable everything for the plugin to work properly.

.. literalinclude:: docker-compose.yaml

.. _CloudWatch plugin: https://docs.fluentbit.io/manual/pipeline/outputs/cloudwatch/
