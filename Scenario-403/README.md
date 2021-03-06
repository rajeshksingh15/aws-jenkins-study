Table of Contents
=================

   * [Requirements](#requirements)
   * [Procedures](#procedures)
   * [More Resources](#more-resources)

<a href="https://www.dennyzhang.com"><img src="https://raw.githubusercontent.com/DennyZhang/aws-jenkins-study/master/images/jenkins_ecs_2nodes.png"/> </a>

# Requirements
1. Start ECS with 2 node
2. Start Jenkins service within ECS. 1 Master and 3 Slaves
3. Enable ALB for Jenkins master

# Procedures
- Use CF to setup the env
```
    export STACK_NAME="docker-cf-jenkins"
    export TMP_FILE="file://cf-denny-jenkins-ecs-2nodes.yml"
    [ -n "$SSH_KEY_NAME" ] || export SSH_KEY_NAME="denny-ssh-key1"
    aws cloudformation create-stack --template-body "$TMP_FILE" \
        --stack-name "$STACK_NAME" --parameters \
        ParameterKey=JenkinsUser,ParameterValue=username \
        ParameterKey=JenkinsPassword,ParameterValue=mypassword \
        ParameterKey=KeyName,ParameterValue=$SSH_KEY_NAME

     aws cloudformation delete-stack --stack-name "$STACK_NAME"
```
<a href="https://www.dennyzhang.com"><img align="right" width="185" height="37" src="https://raw.githubusercontent.com/USDevOps/mywechat-slack-group/master/images/dns_small.png"></a>

- Verify Jenkins
curl -I http://$server_ip:8080

# More Resources
- https://shuaib.me/ecs-jenkins/
