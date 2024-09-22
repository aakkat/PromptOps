# PromptOps
I have used PromptOps and based on it code generated using Github copilot extension in Visual studio code

Problem Statement:
Write a prompts to generate webapp to arithmetic calculation and deploy code on AWS using AWS code build.

Prompt: Create a code in python for webapp to arithmetic calculation.

![Image1](https://github.com/user-attachments/assets/cd26384c-2d46-451a-a8df-456a1c89f8f1)

Image 1
Based on code generated using prompt will create a file named app.py and update code in it.
app.py code

![Image2](https://github.com/user-attachments/assets/70ce0c07-acda-44e1-a539-8e4d55ec2d73)
Image 2

 ![Image3](https://github.com/user-attachments/assets/6148a688-2e5b-4609-a2be-a7e4209505eb)
Image 3
Once code updated in file then executed python app.py

 ![Image4](https://github.com/user-attachments/assets/af13e0a0-7806-4675-b757-b96914515fcc)
Image 4
And once using URL in browser then getting below output in UI

 ![Image5](https://github.com/user-attachments/assets/58206500-2be8-46cb-9251-cc8dbe18f3b3)
Image 5
Now write a prompt to add CSS in index.html
Prompt: Add CSS in index.html

 ![Image6](https://github.com/user-attachments/assets/0041e78d-541e-4252-980c-7fa6a8e42409)
Image 6

Once CSS added then look and feel of browser will be updated as per below which is working absolutely fine.
 
 ![Image7](https://github.com/user-attachments/assets/63bdcdfb-dddf-4a23-90a0-ac19f53a4427)
Image 7

Prompt: Create dockerfile for app.py so that entire app copy in image

 ![Image8](https://github.com/user-attachments/assets/4147d79d-9e17-4288-84ad-1949aa87a9e0)
Image 8

Update code in Dockerfile in your project directory

 ![Image9](https://github.com/user-attachments/assets/a5acfbf9-f084-4022-b8ce-2ab21ea03362)
Image 9

Logged in to brainboard

 ![Image10](https://github.com/user-attachments/assets/754ffa43-ef4d-44fd-85cd-eb5017625a91)
Image 10

How to give access keys and secret key?
Click on profile  Cloud Providers  AWS  New Connection  Access Keys
Post giving access keys and secret keys connection becomes successful

 ![Image11](https://github.com/user-attachments/assets/730400c6-10d0-49c1-a49a-321512525b8c)
Image 11

Go to New architecture  Create using AI and give prompt Create ssm name tgsdockerpassword and put value aak2pass in Mumbai region
Note: Here value (ask2pass) will be used as actual working docker password 

 ![Image12](https://github.com/user-attachments/assets/8eb16035-8eef-4c74-89fc-5b2858e6f410)
Image 12

SSM credential created on AWS using brainboard

 ![Image13](https://github.com/user-attachments/assets/9840125a-1db3-4d06-a16e-85efa3095eb2)
Image 13

Here system manager updated detail in parameter store using brain board

 ![Image14](https://github.com/user-attachments/assets/d619a550-2449-4d31-9ce6-9ae14ba487b1)
Image 14

Buildspec.yml file is developed and updated in VS code 

 ![Image15](https://github.com/user-attachments/assets/7547ea15-71a0-4172-8f64-a875bfa45e8e)
Image 15

version: 0.2

phases:
  install:
    commands:
      - echo "Installing dependencies..."
      - pip install --upgrade awscli
      - aws --version
  pre_build:
    commands:
      - echo "Decrypting Docker password..."
      - DOCKER_PASSWORD=$(aws ssm get-parameter --name tgsdockerpassword --with-decryption --query 'Parameter.Value' --output text)
      - echo "Logging in to Docker Hub..."
      - docker login -u aakkat -p $DOCKER_PASSWORD
      - echo "Building Docker image..."
      - docker build -t aakkat/tgsweb .
  build:
    commands:
      - echo "Pushing Docker image to Docker Hub..."
      - docker push aakkat/tgsweb
  post_build:
    commands:
      - echo "Cleaning up..."
      - docker logout

artifacts:
  files:
    - '**/*'


Next Prompt on brainboard to setup code build setup code build named AKweb123 using aws service in mumbai region and get source code from github https://github.com/aakkat/PromptOps.git with artifact block and all possible roles with ssm parameter get role also

 ![Image16](https://github.com/user-attachments/assets/14846bf2-6747-4d1b-babe-b0df06c38f48)
Image 16

Here code build is ready 

 ![Image17](https://github.com/user-attachments/assets/208c443a-c262-4a87-8b8d-440d24ebf127)
Image 17

Next prompt Brainboard  search for latest amazon linux2 amiid and launch in Mumbai with ssh and port 5000 allow public in security group and install docker and run docker image aakkat/tgsweb:latest and export port 5000

 ![Image18](https://github.com/user-attachments/assets/3d5d7e43-ee96-43e8-8cfb-70edae614708)
Image 18

Here EC2 deployed

 ![Image19](https://github.com/user-attachments/assets/e82e1a2b-4e46-4cab-945f-3fa0ffedb963)
Image 19

Click on Start build so that it will pull from Github and build image on dockerhub

 ![Image20](https://github.com/user-attachments/assets/1753d5ab-b7ba-4f33-9698-814e53d26395)
Image 20

Here code build executed successfully and it deployed docker image in docker hub.

 ![Image21](https://github.com/user-attachments/assets/fd09f635-6c3a-4b9f-bbe8-99133c09a006)
Image 21

Below is the docker image build on docker hub

 ![Image22](https://github.com/user-attachments/assets/6966cd68-d566-4362-b37d-4d69c0034efd)
Image 22

Now Logged in to EC2 and deploying docker container based on newly build image i.e aakat/tgsweb:latest with container name as tgswebdeploy

 ![Image23](https://github.com/user-attachments/assets/49153231-3d73-42ad-96fd-c09b5d579880)
Image 23

But there is no ensurity that container will deploy as below error coming where missed some package

 ![Image24](https://github.com/user-attachments/assets/1c85ee63-b4e9-4ce2-b129-055148d0c225)
Image 24

Now I go to github copilot and ask it to provide requirement file you need to install above package also
Prompt to resolve above error
add package in requirements.txt file based on error ImportError: cannot import name 'url_quote' from 'werkzeug.urls' in python3.9 and flask=2.1.0

 ![Image25](https://github.com/user-attachments/assets/8b2cea13-fc75-4b11-8df9-f10e3bae3b05)
Image 25

Once code is updated then I will sync it with github.

 ![Image26](https://github.com/user-attachments/assets/31d7e328-fff0-4afd-bcbc-8b531d5bbae0)
Image 26

Code is updated successfully on Github

 ![Image27](https://github.com/user-attachments/assets/5ed48912-41b3-4876-bbca-f42c1f2b82e4)
Image 27

Now once code is updated on github then will start codebuild on AWS by clicking on retry build

 ![Image28](https://github.com/user-attachments/assets/b820c0eb-c101-4bcd-9bfc-28fc21ad3a16)
Image 28

Code build executed successfully 

 ![Image29](https://github.com/user-attachments/assets/55aff72d-1ba8-46df-b42d-d023994dc239)
Image 29

Now container deployed successfully

 ![Image30](https://github.com/user-attachments/assets/c470bed8-933b-4219-9ac0-263ec503b153)
Image 30

Updated container with 5000 port

 ![Image31](https://github.com/user-attachments/assets/d3d5f57e-8d6c-43af-87d3-9a7ee710d128)
Image 31

 ![Image32](https://github.com/user-attachments/assets/77e01091-8151-4464-8885-dc0f85ac5126)
Image 32

I logged in to Synk to check vulnerabilities

 ![Image33](https://github.com/user-attachments/assets/0275d91e-4764-443b-baa1-ef36b2e27efc)
Image 33
Here you can check all related vulnerabilities

 ![Image34](https://github.com/user-attachments/assets/16c5ea49-ab86-4767-ad96-7db015bee2a8)
Image 34

Now in case code deploy should be triggered automatically with try again ,for this we need Jenkins file and will write next prompt
Next Jenkins Prompt -> search for latest amazon linux 2 ami id and lauch ec2 instance with iam power user role attached without key pair with proper instance type to support in Mumbai with ssh and port 8080 allow public in security group and install git and install stable Jenkins with no gpg check with right java software for amazon linux java corretto and install latest kubectl and get kubeconfig from eks cluster name my-cluster from mumbai
Created new architecture

 ![Image35](https://github.com/user-attachments/assets/1e277820-af38-477d-912c-75075d7b67e8)
Image 35

Below architecture created
 ![Image36](https://github.com/user-attachments/assets/1f1cedb0-d3f2-4abe-bda9-d1cf5d34c2e3)
Image 36

