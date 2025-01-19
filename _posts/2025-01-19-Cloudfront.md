---
title: Serving Static Site from S3 Bucket over HTTPS with Cloudfront
description: 
date: 2026-01-19 09:36:00 +0000
categories: [Software, Projects]
tags: [aws, projects]
author: daniel
---
# Configuring for HTTPS

![Create cloudfront distribution](/assets/img/Cloudfront/cloudfront_createdistribution.jpg)

![Set cloudfront domain](/assets/img/Cloudfront/cloudfront_domain.jpg)

Click the use website endpoint. This will change it to `www.danielspyros.com.s3-website.eu-west-2.amazonaws.com`.

Leave it on "HTTP Only" and HTTP port 80


![Set cloudfront viewer protocol policy](/assets/img/Cloudfront/cloudfront_protocol.jpg)


![Set cloudfront certificate and alternate domain name](/assets/img/Cloudfront/cloudfront_certificate.jpg)

Request a public certificate, then click Next.

![Request certificate](/assets/img/Cloudfront/cloudfront_requestcertificate.jpg)

![Request Records](/assets/img/Cloudfront/cloudfront_createrecords.jpg)

Once the records are created in Route53, wait a couple minutes and refresh the certificate page. You should see that it is now issued.


![Certificate Issued](/assets/img/Cloudfront/cloudfront_certificate_issue.jpg)

Now that the certificate is issued. Select it in the cloudfront distribution that we were creating.

![Certificate Selected](/assets/img/Cloudfront/cloudfront_certificate_selected.jpg)

Click Create Distribution. The distribution should now start deploying, this can take a few minutes. You can see its status here:

![Distribution Status](/assets/img/Cloudfront/cloudfront_distribution_deploying.jpg)

It will change to a date once it has finished.




![Route 53 - Create record](/assets/img/Cloudfront/route53_createrecord.jpg)

![Route 53 - Create Alias](/assets/img/Cloudfront/route53_creatingalias.jpg)

Leave the Routing Policy on Simple Routing.


# CICD


Add permissions to S3 Bucket to allow uploading to bucket and cache invalidations of cloudfront. Not sure if this is for cache invalidations actually. might be configrued in IAM.
```json
{
    "Version": "2008-10-17",
    "Id": "PolicyForCloudFrontPrivateContent",
    "Statement": [
        {
            "Sid": "AllowCloudFrontServicePrincipal",
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudfront.amazonaws.com"
            },
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::www.danielspyros.com/*",
            "Condition": {
                "StringEquals": {
                    "AWS:SourceArn": "arn:aws:cloudfront::296062577759:distribution/E3OSAEDN2J894S"
                }
            }
        },
        {
            "Sid": "AllowPublicReadAccess",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::www.danielspyros.com/*"
        },
        {
            "Sid": "AllowJekyllGithubAction",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::296062577759:user/DanielBlogGithubActions"
            },
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:ListBucket",
                "s3:DeleteObject"
            ],
            "Resource": [
                "arn:aws:s3:::www.danielspyros.com",
                "arn:aws:s3:::www.danielspyros.com/*"
            ]
        }
    ]
}
```


