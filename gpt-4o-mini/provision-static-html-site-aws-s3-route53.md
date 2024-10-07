fileName: provision-static-html-site-aws-s3-route53.md  
# Provisioning a Static HTML Site using AWS S3 and Route 53
This tutorial will guide you through the steps to provision a static HTML site using AWS S3 for storage and Route 53 for domain management.

## Step 1
First, you will need to create an S3 bucket to store your static files. Make sure to choose a unique name for your bucket.

<field label="bucketName" description="Enter a unique name for your S3 bucket">my-static-site-bucket</field>

## Step 2
Now, let's configure the S3 bucket for static website hosting. You need to specify the index document and an error document.

<field label="indexDocument" description="Enter the name of your index document">index.html</field>
<field label="errorDocument" description="Enter the name of your error document">error.html</field>

## Step 3
Next, you should upload your static HTML files to the S3 bucket. You can use the AWS CLI or the AWS Management Console to perform this task.

<field label="localFilePath" description="Path to your local HTML files">/path/to/your/files</field>

## Step 4
You must set the bucket policy to make your S3 bucket public so that your site can be accessed by visitors.

<yaml label="bucketPolicy" description="Enter your S3 bucket new policy">
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::${bucketName}/*"
    }
  ]
}
</yaml>

## Step 5
Once your S3 bucket is set up, the next step is to configure Route 53 to manage your domain name. You will need to create a hosted zone in Route 53.

<field label="domainName" description="Enter your domain name">example.com</field>

## Step 6
Finally, you will need to create a record set in your hosted zone to route traffic to your S3 bucket. 

<field label="recordType" description="Enter the record type (A for address record)">A</field>
<field label="aliasTarget" description="Enter your S3 bucket endpoint">s3-website-us-east-1.amazonaws.com</field>

## Step 7
Now that you've entered all the required information, here is the bash script that sets up the S3 bucket, uploads your files, and configures Route 53.

<script>return `  
aws s3api create-bucket --bucket ${bucketName} --region us-east-1 --create-bucket-configuration LocationConstraint=us-east-1  
aws s3 website s3://${bucketName} --index-document ${indexDocument} --error-document ${errorDocument}  
aws s3 cp ${localFilePath} s3://${bucketName}/ --recursive  
aws s3api put-bucket-policy --bucket ${bucketName} --policy '${bucketPolicy}'  
aws route53 create-hosted-zone --name ${domainName} --caller-reference "my-zone-ref"  
aws route53 change-resource-record-sets --hosted-zone-id <your-hosted-zone-id> --change-batch '  
{  
  "Changes": [{  
      "Action": "CREATE",  
      "ResourceRecordSet": {  
          "Name": "${domainName}",  
          "Type": "${recordType}",  
          "AliasTarget": {  
              "HostedZoneId": "<your-s3-hosted-zone-id>",  
              "DNSName": "${aliasTarget}",  
              "EvaluateTargetHealth": false  
          }  
      }  
  }]  
}'  
`</script>  

## Conclusion
You have successfully set up a static HTML site using AWS S3 and Route 53. Your website is now live and accessible to visitors!
