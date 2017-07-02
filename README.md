# aws_lambda_ortools
Google ortools binaries and their dependencies, processed for the Python 3.6 runtime on AWS Lambda

# Instructions to use as-is
Download as zip  
Upload to AWS Lambda  
Confirm the response equals  
    {
      "statusCode": "200",
      "body": "\"[0, 7, 2, 3, 4, 12, 6, 8, 1, 11, 10, 5, 9]\"",
      "headers": {
        "Content-Type": "application/json"
      }
    }  
Modify lambda_function.py code as desired.  

# Guidelines to recreate from scratch
  Launch an EC2 instance with Amazon's latest Linux image.  
  Install miniconda.  
  Create an environment running python 3.6  
  easy_install py3-ortools  
  Create a $folder to bundle your files in  
  Find and move the top level files from the .egg folders to $folder for:  
* protobuf  
* six  
* py3-ortools  

** Example: $mv /home/ec2-user/miniconda3/envs/py36/lib/python3.6/site-packages/six-1.10.0-py3.6.egg /home/ec2-user/lambda_libs/ort_binaries  **
  
Now you should have the same files as in the repo. Ortools will run on your ec2 instance, but not on lambda, due to permission restrictions.  
  
There are about 5 files you need to chmod. Zipping the $folder you made, uploading it to Lambda, and running the lambda_function.py should reveal which files require chmodding in the error messages.  
  
** Example: $sudo chmod o+r ortools/constraint_solver/solver_parameters_pb2.py  **
  
Once this is done, you should receive the response mentioned earlier. This means the tutorial code for ortools has been succesfully executed!  
