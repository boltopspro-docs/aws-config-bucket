<!-- note marker start -->
**NOTE**: This repo contains only the documentation for the private BoltsOps Pro repo code.
Original file: https://github.com/boltopspro/aws-config-bucket/blob/master/README.md
The docs are publish so they are available for interested customers.
For access to the source code, you must be a paying BoltOps Pro subscriber.
If are interested, you can contact us at contact@boltops.com or https://www.boltops.com

<!-- note marker end -->

# AWS Config Bucket CloudFormation Blueprint

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

The AWS CloudFormation StackSet example template helps you enable AWS Config in every region for compliance. The template creates an S3 Bucket in every region. This can be a little messy if you prefer to have S3 buckets in a limited number of regions. Particularly, if you do not really use the regions and have only enabled AWS Config for compliance reasons. This blueprint creates an S3 Bucket that can be used by AWS Config in different regions.

It works with the [boltopspro/enable-aws-config](https://github.com/boltopspro-docs/enable-aws-config) blueprint, which has a `BucketName` parameter that can be an existing bucket.

Related Blueprints:

* [boltopspro/aws-config-aggregator](https://github.com/boltopspro-docs/aws-config-aggregator)
* [boltopspro/aws-config-bucket](https://github.com/boltopspro-docs/aws-config-bucket)
* [boltopspro/enable-aws-cloudtrail](https://github.com/boltopspro-docs/enable-aws-cloudtrail)
* [boltopspro/enable-aws-config](https://github.com/boltopspro-docs/enable-aws-config)
* [boltopspro/enable-aws-guardduty](https://github.com/boltopspro-docs/enable-guardduty)

## Usage

1. Add blueprint to Gemfile
2. Configure: configs/aws-config-bucket values
3. Deploy

## Add

Add the blueprint to your lono project's `Gemfile`.

```ruby
gem "aws-config-bucket", git: "git@github.com:boltopspro/aws-config-bucket.git"
```

## Configure

First you want to configure the [configs](https://lono.cloud/docs/core/configs/) files. Use [lono seed](https://lono.cloud/reference/lono-seed/) to configure starter values quickly.

    LONO_ENV=development lono seed aws-config-bucket

To deploy to additional environments:

    LONO_ENV=production  lono seed aws-config-bucket

The generated files in `config/aws-config-bucket` folder look something like this:

    configs/aws-config-bucket/
    └── variables
        ├── development.rb
        └── production.rb

configs/aws-config-bucket/

```ruby
# The @accounts variable allows you to set a Bucket Policy that allow additional account access.
# Provide it with additional AWS account ids. The current AWS account is already automatically added.
@accounts = ["111111111", "22222222"]
```

Any bucket properties can also be set with `@bucket_properties:`

```ruby
@bucket_properties = {
  BucketName: "my-bucket",
}
```

## Deploy

Use the [lono cfn deploy](http://lono.cloud/reference/lono-cfn-deploy/) command to deploy. Example:

    LONO_ENV=development lono cfn deploy aws-config-bucket
    LONO_ENV=production  lono cfn deploy aws-config-bucket
