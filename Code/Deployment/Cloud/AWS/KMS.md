[Documentation](https://awscli.amazonaws.com/v2/documentation/api/latest/reference/kms/index.html#cli-aws-kms)
[Rotate AWS KMS keys](https://docs.aws.amazon.com/kms/latest/developerguide/rotate-keys.html)
## CLI examples

aws kms encrypt --key-id YOURKEYIDHERE --plaintext fileb://secret.txt --output text --query CiphertextBlob | base64 --decode > encryptedsecret.txt

aws kms decrypt --ciphertext-blob fileb://encryptedsecret.txt --output text --query Plaintext | base64 --decode > decryptedsecret.txt

aws kms re-encrypt --destination-key-id YOURKEYIDHERE --ciphertext-blob fileb://encryptedsecret.txt | base64 > newencryption.txt 

aws kms enable-key-rotation --key-id YOURKEYIDHERE

aws kms get-key-rotation-status --key-id YOURKEYIDHERE

aws kms generate-data-key --key-id YOURKEYIDHERE --key-spec AES_256