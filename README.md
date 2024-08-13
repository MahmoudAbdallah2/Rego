# Rego
Example Rego Policies:
1. Detect Publicly Accessible S3 Buckets
s3_public_buckets => This policy checks if any S3 bucket has a public read or write policy.
Input Data: You need to pass the S3 bucket policies as input to this Rego script.
Output: The policy will detect and return any buckets that are publicly accessible

2. Detect Security Groups Allowing Unrestricted Inbound Traffic
ec2_open_SG => This policy checks if any security group allows inbound traffic from any IP address (0.0.0.0/0) on sensitive ports like 22 (SSH) or 3389 (RDP).
Input Data: This script requires security group configurations as input.
Output: It will flag any security group that allows unrestricted inbound access to sensitive ports.

Running the Policies with OPA:
Prepare the Input Data: Collect the AWS configuration data (S3 bucket policies, security group rules) and structure it in a JSON format.

Run the Policy:
Save the Rego policies to a file, e.g., aws_security.rego.
Use OPA to evaluate the policy against the input data:

opa eval --input input.json --data aws_security.rego 'data.aws.security.s3.deny'

The Results:
The evaluation will return the buckets or security groups that violate the defined policies.

Example Output:
If any buckets are found to be publicly accessible, OPA will output something like this:
{

    "result": [
        {
            "bucket": "my-public-bucket"
        }
    ]
    
}
