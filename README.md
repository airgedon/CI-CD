```yaml
#_________________________________
# Github Action Part-1 Basics
#
# Copyleft (c) by Me 2022
#_________________________________
name: My-GithubActions
env:
  APPLICATION_NAME    : "MyFlask"
  DEPLOY_PACKAGE_NAME : "flask-deploy-ver-${{ github.sha }}"


on:
  push:
    branches: 
      - master
      - main
  pull_request:
    branches: [ "main" ]


jobs:

  my_testing:
    runs-on: ubuntu-latest


    steps:
    - name: Print Hello Message
      run : echo "Hello World from Testing job"
    - name: Execute few commands
      run :
        echo "Hello Message1"   
        echo "Hello Message2"
        echo "Apllication name:${{ env.APPLICATION_NAME }}"
    - name: List current folder
      run : ls -la
      
    - name: Git clone my repo
      uses: actions/checkout@v1
      
    - name: List current folder
      run : ls -la  
        
  my_deploy:
    runs-on: ubuntu-latest
    needs: [my_testing]
    env  :
      VAR1 : "This is Job level Variable1"
      VAR2 : "This is Job level Variable2"
    
    
    steps:
    - name: Print Hello Message
      run : echo "Hello World from Deploy job"
       
    - name: Printing Deployment package
      run : echo "Deploy package name is ${{ env.DEPLOY_PACKAGE_NAME }}"
        
    - name: Print env vars
      run : |
        echo "VAR1 - ${{ env.VAR1 }}"
        echo "VAR2 - ${{ env.VAR2 }}"
        echo "LOCAL_VARS - $LOCAL_VARS "
      env :
        LOCAL_VARS: "That is local variable"
        
    - name: Lets test some packages if they are right here 1
      run : aws --version

    - name: Lets test some packages if they are right here 2
      run : zip --version
 ```
 ---
 ```yaml
 name: First-Pipeline
env:
  Var1: Dom

on:
  push:
    branches: [ "main" ]
    
    
jobs:
  my_build:
    runs-on: ubuntu-latest
    
    steps:
    - name: List folders
      run : ls -la
    
    - name: G C
      uses: actions/checkout@v1
    
    - name: Print first string
      run : |
        echo "I am ${{ env.Var1 }}"
        
    - name: Print all current files
      run : ls -la
  second_build:
    runs-on: ubuntu-latest
    needs: [my_build]
    
    steps:
    - name: To install zsh
      run : |
        sudo apt install zsh
        
    - name: git 
      run : git --version
 ```
# Steps
> Go to Settings in Github repo -> Runners -> Create own self-hosted runner -> and copy all to your server
> then in .yml file ,make changes from 'runs-on: something ' to 'runs-on: self-hosted'
>  to clone your repo use " uses: actions/checkout@v2"
>  you can find your repo in _work/ folder repo_name/repo_name directory 
