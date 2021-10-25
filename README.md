# devops-netology edited

# Настройки .gitignore в terraform

# Local .terraform directories
# Игнорировать локальные директории вида .terraform
**/.terraform/*

# .tfstate files
# Игнорировать файлы с расширением .tfstate и .tfstate.*
*.tfstate
*.tfstate.*

# Crash log files
# Игнорировать файл crash.log
crash.log

# Exclude all .tfvars files, which are likely to contain sentitive data, such as
# password, private keys, and other secrets. These should not be part of version
# control as they are data points which are potentially sensitive and subject
# to change depending on the environment.
# Игнорировать файлы с расширением .tfvars
*.tfvars

# Ignore override files as they are usually used to override resources locally and so
# are not checked in
# Игнорировать файлы override.tf, override.tf.json 
# и файлы вида *_override.tf, *_override.tf.json
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Include override files you do wish to add to version control using negated pattern
#
# !example_override.tf

# Include tfplan files to ignore the plan output of command: terraform plan -out=tfplan
# example: *tfplan*

# Ignore CLI configuration files
# Игнорировать файлы конфигураций .terraformrc и terraform.rc 
.terraformrc
terraform.rc