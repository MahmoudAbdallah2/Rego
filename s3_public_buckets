package aws.security.s3

default allow = false

public_buckets[bucket] {
    bucket := input.s3.buckets[_]
    is_public(bucket)
}

is_public(bucket) {
    # Check if the bucket has a policy that allows public access
    bucket.policy.Statement[_].Effect == "Allow"
    bucket.policy.Statement[_].Principal == "*"
    bucket.policy.Statement[_].Action == "s3:GetObject"
}

deny {
    public_buckets[_]
}
