
.. meta::
    :description: ECS Compose-X and FireLens
    :keywords: AWS, ECS, FireLens, Compose-X

################################################
AWS ECS and FireLens with Compose-X
################################################

Examples of various configurations to illustrate how to define configurations to deploy
to ECS with FireLens logging configuration, using FluentBit, via Compose-X.

All the examples in this repository are used as tests for end-to-end testing when working on new features
and version of ECS Compose-X

Simple Examples
=================

* `Declare FireLens with cloudwatch plugin`_
* `Declare FireLens with firehose plugin`_
* `Replace awslogs with FireLens cloudwatch plugin`_


Advanced Examples
=======================

The following examples take things a step further and will use Compose-X Files Composer as a sidecar that will
load up the configuration for FireLens to include and use in final deployment.


* `Enable API HealthCheck and set grace period`_
* `Enable nginx parser using SourceFile`_

FireHose using x-kinesis_firehose
-------------------------------------

* `Using with options.delivery_name`_
* `Using with x-logging.Firelens.Advanced`_

Motivations for such module
=============================

A lot of examples available today, which are remarkable btw, in the `amazon-ecs-firelens-examples`_ GIT repository,
all involve adding a configuration file to the container when you want to use advanced configurations in `AWS Fargate`_.

On EC2 deployments, you can pull the configuration from S3. Which is great, if it never changes.

With the `x-logging.FireLens`_ extension, I really wanted to have something that would give users the agility to change
configuration quickly, dynamically, and without having to worry about where in AWS the configuration is stored.

And so, the current implementation allows to deploy to any ECS compute target (EC2, Fargate, ECS Anywhere) and never
have to make any changes.

Useful links
=================

* `Fluent Bit`_
* `amazon-ecs-firelens-examples`_

Compose Documentation
----------------------

* `x-kinesis_firehose`_
* `x-kinesis`_
* `services.x-logging`_

.. _Declare FireLens with cloudwatch plugin: ./examples/declare_firelens_with_cw_plugin/README.rst
.. _Declare FireLens with firehose plugin: ./examples/declare_firelens_with_firehose_plugin/README.rst
.. _Replace awslogs with FireLens cloudwatch plugin: ./examples/replace_awslogs/README/.rst
.. _Enable API HealthCheck and set grace period: ./examples/enable_api_healthcheck_and_set_grace_period/README.rst
.. _Enable nginx parser using SourceFile: ./examples/enable_nginx_parser_using_source_file/README.rst
.. _Using with options.delivery_name: ./examples/x_kinesis_firehose_with_options_delivery_name/README.rst
.. _Using with x-logging.Firelens.Advanced: ./examples/x_kinesis_firehose_with_firelens_advanced/README.rst


.. _amazon-ecs-firelens-examples: https://github.com/aws-samples/amazon-ecs-firelens-examples
.. _AWS Fargate:
.. _x-logging.FireLens:
.. _x-kinesis_firehose: https://docs.compose-x.io/syntax/compose_x/firehose.html
.. _x-kinesis: https://docs.compose-x.io/syntax/compose_x/kinesis.html
.. _services.x-logging: https://docs.compose-x.io/syntax/compose_x/ecs.details/logging.html

.. _Fluent Bit: https://docs.fluentbit.io/manual/
