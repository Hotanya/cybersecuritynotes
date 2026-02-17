# AWS



1.  Make profile using API creds for base account <br>

    <pre><code><strong>aws configure --profile clientname 
    </strong><strong> ID: A 
    </strong> Access Key: a 
     ap-southeast-2 
     jsonjs
    </code></pre>
2. Use the base account to use MFA&#x20;

```json
aws sts get-caller-identity --profile clientname 
aws sts get-session-token --token-code 262297 --serial-number arn:aws:iam::123456789012:mfa/email@email.com --profile clientname
```

&#x20;  3\. Make a profile with MFA credentials and session token&#x20;

```
aws configure --profile clientnameAuth 
aws configure set aws_session_token "" --profile clientnameAuth

```

&#x20;  4\. Use MFA profile to assume a role&#x20;

```
aws sts assume-role --role-arn arn:aws:iam::317000736746:role/clientSecurityAuditRole --role-session-name clientSecurityAuditRole --profile clientnameaAuth
```

&#x20;  5\. Make a new profile using role’s credentials and token {Use details from above request}&#x20;

```
aws configure --profile clientSecurityAuditRole 
aws configure set aws_session_token " " --profile clientSecurityAuditRole
```

&#x20;  6\. Test the connection with new profile \
`aws s3 ls --profile clientSecurityAuditRole`

