---
  title: "node-sass 오류"
  categories:

    - Tech
  tags: 
    - node-sass 오류"
    - aws
    - jenkins
    - node_versino
  toc: true
  toc_sticky: true
  toc_label: 목차
  popular: true
---



# node-sass install error

## 1. 원인은 간단하다.

> node 버전 문제이다.

> npm install node-sass 명령어를 로컬과 aws의 ec2-user는 정상적으로 수행 되었다.
> aws에 설치한 jenkins에서는 오류가 아래와 같은 오류가 발생했다.

```
npm WARN deprecated core-js@2.6.12: core-js@<3.3 is no longer maintained and not recommended for usage due to the number of issues. Because of the V8 engine whims, feature detection in old core-js versions could cause a slowdown up to 100x even if nothing is polyfilled. Please, upgrade your dependencies to the actual version of core-js.
npm ERR! code 1
npm ERR! path /var/lib/jenkins/workspace/gardener-FE/node_modules/node-sass
npm ERR! command failed
npm ERR! command sh -c node scripts/build.js
npm ERR! Building: /var/lib/jenkins/tools/jenkins.plugins.nodejs.tools.NodeJSInstallation/16.0.0/bin/node /var/lib/jenkins/workspace/gardener-FE/node_modules/node-gyp/bin/node-gyp.js rebuild --verbose --libsass_ext= --libsass_cflags= --libsass_ldflags= --libsass_library=
npm ERR! make: Entering directory `/var/lib/jenkins/workspace/gardener-FE/node_modules/node-sass/build'
npm ERR!   g++ -o Release/obj.target/libsass/src/libsass/src/ast.o ../src/libsass/src/ast.cpp '-DNODE_GYP_MODULE_NAME=libsass' '-DUSING_UV_SHARED=1' '-DUSING_V8_SHARED=1' '-DV8_DEPRECATION_WARNINGS=1' '-DV8_DEPRECATION_WARNINGS' '-DV8_IMMINENT_DEPRECATION_WARNINGS' '-D_GLIBCXX_USE_CXX11_ABI=1' '-D_LARGEFILE_SOURCE' '-D_FILE_OFFSET_BITS=64' '-D__STDC_FORMAT_MACROS' '-DOPENSSL_NO_PINSHARED' '-DOPENSSL_THREADS' '-DLIBSASS_VERSION="3.5.5"' -I/var/lib/jenkins/.cache/node-gyp/16.0.0/include/node -I/var/lib/jenkins/.cache/node-gyp/16.0.0/src -I/var/lib/jenkins/.cache/node-gyp/16.0.0/deps/openssl/config -I/var/lib/jenkins/.cache/node-gyp/16.0.0/deps/openssl/openssl/include -I/var/lib/jenkins/.cache/node-gyp/16.0.0/deps/uv/include -I/var/lib/jenkins/.cache/node-gyp/16.0.0/deps/zlib -I/var/lib/jenkins/.cache/node-gyp/16.0.0/deps/v8/include -I../src/libsass/include  -fPIC -pthread -Wall -Wextra -Wno-unused-parameter -m64 -O3 -fno-omit-frame-pointer -std=gnu++1y -std=c++0x -fexceptions -frtti -MMD -MF ./Release/.deps/Release/obj.target/libsass/src/libsass/src/ast.o.d.raw   -c
npm ERR! make: Leaving directory `/var/lib/jenkins/workspace/gardener-FE/node_modules/node-sass/build'
npm ERR! gyp info it worked if it ends with ok
npm ERR! gyp verb cli [
npm ERR! gyp verb cli   '/var/lib/jenkins/tools/jenkins.plugins.nodejs.tools.NodeJSInstallation/16.0.0/bin/node',
npm ERR! gyp verb cli   '/var/lib/jenkins/workspace/gardener-FE/node_modules/node-gyp/bin/node-gyp.js',
npm ERR! gyp verb cli   'rebuild',
```
> 그래서 각 버전을 확인해 봤다.
## 1 로컬
  ```bash
  D:\git\gardener-fe>node -v
  v14.16.0

  D:\git\gardener-fe>npm -v
  6.14.11
  ```
## 2 aws ec2-user 
  ```bash
  [ec2-user@ip-172-31-15-85 workspace]$ npm -v
  6.13.4
  [ec2-user@ip-172-31-15-85 workspace]$ node -v
  v12.16.0
  ```
## 3 jenkins는 build영역에 shell 명령어를 작성해 보았다.
  
![image](https://user-images.githubusercontent.com/7609848/117032627-9850b080-ad3c-11eb-9080-e0839e47d1f9.png)
   
 >  결과는 
![image](https://user-images.githubusercontent.com/7609848/117032822-c504c800-ad3c-11eb-90ea-e94e9ffb49bf.png)
   + npm -v
    7.10.0
    + node -v
    v16.0.0
   
## 4 jenkins 관리화면에서 nodejs 버전을 낮춰보았다.
  ![image](https://user-images.githubusercontent.com/7609848/117033214-1d3bca00-ad3d-11eb-8c17-d4ab6f5f6b60.png)
![image](https://user-images.githubusercontent.com/7609848/117033491-5f650b80-ad3d-11eb-99db-2e7cf1fdcb71.png)
![image](https://user-images.githubusercontent.com/7609848/117033569-73a90880-ad3d-11eb-9f0e-aa10ce6a3dcb.png)
![image](https://user-images.githubusercontent.com/7609848/117033621-81f72480-ad3d-11eb-943d-bb6d0026802c.png)

## 5 결과는 성공
 ![image](https://user-images.githubusercontent.com/7609848/117033744-a521d400-ad3d-11eb-9225-c56503ec8816.png)
 ![image](https://user-images.githubusercontent.com/7609848/117033802-b1a62c80-ad3d-11eb-911b-a07983d46300.png)

## 6 결론은 node-sass install error는 nodeJS 버전문제다.
   버전을 낮춰서 build 해보시길 바란다.




