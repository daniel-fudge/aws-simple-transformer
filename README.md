# aws-simple-transformer
The is a simple transformer to demo parallel serverless processing.

## Basic Components
### S3 with Lambda Trigger
To start the transformer, a package (zip file) is uploaded to a S3 bucket from a users workstaion using the CLI. A soon as the package lands in the bucket, a Lambda function is triggered.

### Step Function
The S3 Lambda launches a Step function to transform the package. This step function performs the following tasks.    
1. Python Lambda function to process the package.    
1. Parallel C++ Lambda functions to transform the data.   
1. Python Lambda function to summarize the parallel results.   
1. Lambda function to send the results to the desired email distribution.

## Compiling a C++ Lambda Function 
The basic steps for generating C++ Lambda function are described in the following references.
- [Introducing the C Lambda Runtime](https://aws.amazon.com/blogs/compute/introducing-the-c-lambda-runtime/)
- [C++ Sample Lab](https://github.com/awslabs/aws-lambda-cpp)

 ## Install som dependencies
 ```bash
sudo apt install cmake
sudo apt install make
sudo apt install zip
sudo apt install libcurl-devel
sudo apt install libcurl4-openssl-dev
sudo apt-get install libssl-dev
```

## Build the AWS C++ SDK
```bash
mkdir ~/install
git clone https://github.com/aws/aws-sdk-cpp.git
cd aws-sdk-cpp
mkdir build
cd build
cmake .. -DBUILD_ONLY="core" \
  -DCMAKE_BUILD_TYPE=Release \
  -DBUILD_SHARED_LIBS=OFF \
  -DENABLE_UNITY_BUILD=ON \
  -DCUSTOM_MEMORY_MANAGEMENT=OFF \
  -DCMAKE_INSTALL_PREFIX=~/install \
  -DENABLE_UNITY_BUILD=ON
make
make install
```

## Build the Runtime
```bash
$ git clone https://github.com/awslabs/aws-lambda-cpp-runtime.git
$ cd aws-lambda-cpp-runtime
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_BUILD_TYPE=Release \
  -DBUILD_SHARED_LIBS=OFF \
  -DCMAKE_INSTALL_PREFIX=~/install \
$ make
$ make install
```


