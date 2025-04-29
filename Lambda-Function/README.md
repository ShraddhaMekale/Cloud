import json
import boto3

def lambda_handler(event, context):
    # Initialize the S3 client
    s3 = boto3.client('s3')

    # Extract the bucket name and file name from the event
    bucket_name = event['Records'][0]['s3']['bucket']['name']
    file_name = event['Records'][0]['s3']['object']['key']

    # Log the bucket name and file name (for debugging)
    print(f"Bucket: {bucket_name}")
    print(f"File: {file_name}")

    try:
        # Retrieve the S3 object (file)
        file_obj = s3.get_object(Bucket=bucket_name, Key=file_name)

        # Read and decode the content of the file
        file_content = file_obj['Body'].read().decode('utf-8')

        # Print the content of the file (for debugging)
        print(f"File content:\n{file_content}")

        # Optionally, you could perform additional processing on the file content
        # For example, save the content elsewhere, trigger another process, etc.

    except Exception as e:
        # Log any errors that occur during the process
        print(f"Error: {str(e)}")
        raise e  # Re-raise the exception for further logging if needed
