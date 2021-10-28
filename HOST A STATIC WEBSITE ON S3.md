# HOST A STATIC WEBSITE ON S3

For this project, we are going to be hosting a random static website on AWS using S3.

## STEP 1 - DOWNLOAD THE CONTENTS OF THE STATIC WEBSITE

Go to this google drive [link](https://drive.google.com/drive/folders/1Odgbg6mR7zdJW9AFn_-xHNzQ9eWaFOyC) and download the `s3staticsitecode` folder.

Extract the files to a folder of your choice.

## STEP 2 - CREATE AN S3 BUCKET

Navigate to the S3 dashboard and click on create a bucket
![image](https://user-images.githubusercontent.com/22638955/139158812-006ad5a0-bd4d-4963-9a17-2c12bd3d5ba2.png)

**Please note that your bucket name must be unique, or else you won't be able to create a bucket**

Just for the purpose of this project, we would allow "public access" to this bucket as we want ut to be visible to the public and we want to use it for static website hosting.

![image](https://user-images.githubusercontent.com/22638955/139271995-2b502beb-5d34-4a06-b8de-8c305a10aaf9.png)

You can setup the rest of the options as shown below, then create the bucket - 

![image](https://user-images.githubusercontent.com/22638955/139275369-ac2fa1cc-9440-4549-b339-9b8b8020ca1f.png)

![image](https://user-images.githubusercontent.com/22638955/139275713-3b8fb6c4-8430-474f-98c1-b087fd0f88cc.png)

## STEP 3 - UPLOAD CONTENTS INTO YOUR BUCKET

Go into your created bucket and then upload the contents of `s3staticsitecode` (You can drag and drop) -

![image](https://user-images.githubusercontent.com/22638955/139276518-a7d29f67-76ab-4317-8d88-9e223a24eddc.png)

## STEP 4 - SETUP S3 FOR STATIC WEB HOSTING

Navigate to the properties tab and then lets look for `static website hosting`

Click on "Edit" and then enable it, specify your index document (index.html) and save these changes - 

![image](https://user-images.githubusercontent.com/22638955/139277988-14ac5875-0931-49e9-8f99-9d7c55ca9e25.png)

Clicking on the s3 bucket link that should bring up our website would bring up an error as we have not assigned permissions for our site to be publicly viewed - 

![image](https://user-images.githubusercontent.com/22638955/139278411-51e422dd-b944-497c-8624-d1ffde76cac9.png)

To mitigate the issue above, go to the "Permissions" tab, edit the "Bucket policy", paste the code below and save changes - 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}
```

The code above is used to grant read-only permission to public anonymous users. Here's the [link](https://docs.aws.amazon.com/AmazonS3/latest/userguide/example-bucket-policies.html#example-bucket-policies-use-case-2) to the document.

If you want to understand the best practices for securing files in your S3 bucket and risks involved in granting public access to your S3 bucket, have a look at this [link](https://aws.amazon.com/premiumsupport/knowledge-center/secure-s3-resources/)

Go back to the webpage we opened previously and refresh. You should be presented with exactly what we have below - 

![image](https://user-images.githubusercontent.com/22638955/139285972-a204d38f-236e-4c47-988b-006bae7c954c.png)

Thank You!!!
