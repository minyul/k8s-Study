# 유튜브 따배쿠를 주기적을 들으면서 공부해보자. 총 35강의이고 하루에 한개씩만 해보자 

책은 쿠버네티스 입문 - 90가지 예제로 배우는 컨테인 관리 자동호 표준 <br>

시스템에서 하나의 프로그램을 실행시키려며 어떻게해야할까? Node오 같은 환경이 있어야한다.<br>
FROM node 를 통해 환경을 만든다음 Copy를 이용항 프로그램을 갖고오면 된다. <br>
이러한 dockerfile을 이용해서 컨테이너를 실행하시위해서는 도커 플랫폼이 필요하다.<br>

우선 hub와 같은 저장소에 이미지를 넣어주고 저장해준다.<br>
허브에는 수많은 이미지들이 존재한다.<br>

docker create ve docker run <br>
두 명령어 모두 이미지를 통해 컨테이너를 생성하는 명령어. <br>

즉, docker pull, docker create, docker start 하면 컨테이너가 실행된다. 이렇게 도커 플랫폼이 필요로한다. <br>

계속 얘기하는 거지만 가상머신 vs 컨테이너 차이점은 가장 중요한 것이 Hypervisor이 없다는 것이다. <br>

도커플랫폼이 실행이 된다는 것은 도커 엔진이며 도커 엔진이라함은 안에 서버인 도커 데몬이 실행된다는 것. <br>

가상머신 같은 경우에는 OS가 필요로한데.. 예를들면 Ngnix웹서버를 만들때, 100메가 뿐 필요없는데 ... OS가 1기가 정도가 든다. <br>
즉, 가상머신이 아닌 도커엔진을 쓰면 OS가 필요가없으니 용량에 훨 가벼움<br>

확장또한 가볍고 배포도 빠르지! 이게 도커가 나온 이유.. 가장 중요함. 배포를 위한 것이다. <br>

수평으로 확장이 가능하다. 용량이 적으니까 가볍자나. 그래서 웹어플리케이션, 웹서버를 여러대를 수평확장할수 있다. 장애일수도있기 때문에 <br>


3월 18일 

시스템 하나에다가마 만들며 불안하니 두개 세개 분산 운영할 수 있다. <br>
오케스트레이션 : 어플리케이션을 잘 배치해서 잘 운영이 될수 있도록 ! <br>

control plane을 두고 worker node 들을 두고 운영한다 <br>

쿠버네티스 : 컨테이너화된 애플리케이션을 자동으로 배포, 스케일링 및 관리해주는 오픈소스 시스템 <br>
장점중 큰것은 어디서나 실행가능 : 온프레미스, 퍼블릭 클라우드. <br>
온프레미스에 있었더 컨테이너들을 퍼블리 클라우드에 옮길수 있다. 야믈파일을 이용해서 갖고올수있지 <br>
선언적 API도 하나의 장점이다. 선언적 API : Control plane 이 있다고 하고 두개으 Node가 있다고하면  <br>
- 쿠버야 ㄴ 웹서버 3개가 필요해! 라고 하며 만들어주는! 그런게 선언적 API <br>

3월 19일

두개의 환경으로 연습 가능 <br>

카타코다 쿠버네티스 플레이 그라운드 <br>
플레이 윗 쿠버네티스 <br>

컨테이너 네트워크 인터페이스 : 컨테이터간 통신을 지원하는 VxLAN. Pod Network라고도 부름 <br>
컨테이너 기반으로 동작하는 어플리케이션 웹, 로그인컨테이너는 서로간의 통신을 해야한다. 서로 통신하기위한 인터페이스 즉, 소프트웨어가 있다 <br>
노드 안에 여러 파드들이 존재하지 <br>
컨테이너들은 자기만의 IP를 갖고있다. 파드와 파드간의 통신이 가능해야한다. 이러한 컨테이너들끼리 통신하기 위해서는 위브넷, 칼리코 등등이 있다. <br>
컨테이너 -> CNI -> 물리적 -> CNI -> 컨테이너 연결 <br>



-----

# k8s-Study
추석 - 인프런 쿠버 강의를 보며 공부해보자



# 컨테이너 오케스트레이션 (서버를 관리한다는 것)

VM
서버하나에 가상머신이 여러개!
조금 느리고 관리가 불편하지만 괜찮다.

클라우드, 특정 벤더의 의존성이 생기기 때문에 사용하기 어렵고
기본적으로 하이퍼바이저가 있기에 성능이 느리다.

이때 !
도커가 나온다.

모든 실행환경을 도커로 !

특정 클라우드 벤더에 종송적이지 않고, 언어, 프레임워크에 상관없이
애플리케이션을 동일한 방식으로 관리 ( 오픈소스 )

aws -> gcp 

Developer 가 코드를 짜고 -> Build ( 도커 이미지를 만들고 ) -> 만든이미지를 도커허브, 저장소에 저장하고 
-> 그 도커이미지를 컨테이너를 실행

이 과정이 도커를 도입하고 나서 이 일련의 프로세스가 똑같아진다. 원래는 플랫폼이 다를때 이게 어려웟지만 이게 이롷게 된거지..


이제 이렇게 도커 컨테이너 여러개를 만들어서 사용하다보니까! 불편함이 있는거야. 너무많은 컨테이너가 있기 때문에
이렇게 많은 수천개 수만개! 의 컨테이너로 인해 관리가쫌..............


dcoker stop app && docker run .. : server 1
dcoker stop app && docker run .. : server 2
dcoker stop app && docker run .. : server 3

또한 서버가 여러개가 있는데 여기 중에서 컨테이너가 실행되고 있는지 모르겠어! 즉, 각 컨테이너가 실행중인 서버를
모니터링해주고 관리해야돼!


롤아웃, 롤백 ( 버전업하고 싶거나 )

Proxy { web : "192.168.0.200"  }
LoadBalancer { 10.0.0.100 , 10.0.0.101 }

web container 1
web container 2


서비스 이상, 부하 모니터링 은 어떻게할까?

복잡한 컨테이너 환경을 효과적으로 관리하기 위한 도구 : 컨테이너 오케스트레이션

서버관리자가 하는일을 대신해주는 프로그램을 만드는것 !

클러스터 : 클러스터 단위로 컨테이너 여러개를 하나로 합쳐서 추상화해서 관리를 한다 
마스터 서버를 앞에다가 두고 ! 클러스터 단위의 여러개의 도커 컨테이너를 관리한다 
즉, 마스터한테 명령을 잘해주면된다. !

복제를 3개 해주는 상태관리도 있다.
{
  image : "app1"
  replicas : 3
}

배포 버전관리도 있다!
서비스 디스커버리도 있고!
불륨설정도 가능하다! Node 1에는 aws , Node 2에는 GCP 등!


# 어떤것을 공부할까?

일련의 프로세스는

1.개발자가 코드를 작성
2. git merge request or push!
3. Build Test, Create Container Image, Push Container Image - Docker Registry 
4. Deploy : New or Update 
5. Kubernates 
6. Scale Out 

도커 컨테이너 실행하기  - 도커와 도커컴포즈를 이요한 멀티 컨테이너 
쿠버네티스에 컨테이너 배포하기 
외부 접속 설정하기
스케일 아웃하기 - 부하에 따른 컨테이너 관리 
그외 고급기능 소개



# 쿠버네티스 소개

컨테이너화된 애플리케이션을 자동으로 배포, 스케일링 및 그룹화
컨테이너를 쉽게 관리하고 연결하기 위해서 논리적은 단위로 그룹화


클라우드 환경에서 어떻게 애플리케이션을 배포하는게 좋은걸까?

! 잠깐!! 내가 궁금해서 방금 찾아본 것 

'Pod'란 쿠버네티스에서 최소 배포 단위로 하나 이상의 컨테이너를 포함한다. Docker를 사용해본 사용자라면 알듯 Docker에서는 최소의 배포 단위가 컨테이너이다. 하지만 쿠버네티스는 하나의 컨테이너가 아닌 컨테이너 및 네트워크, 스토리지가 포함된 Pod로 배포한다.

JAR는 여러개의 자바 클래스 파일과, 클래스들이 이용하는 관련 리소스 및 메타데이터를 하나의 파일로 모아서 자바 플랫폼에 응용 소프트웨어나 라이브러리를 배포하기 위한 소프트웨어 패키지 파일 포맷이다.


# 쿠버네티스 배포 데모

kubectl get node
kubectl get namesapce 
kubectl get po -n monitroting



# 쿠버네티스 아키텍처 

누군가 컨테이너 1개를 띄어줘!! 라고 할수있지.
컨테이너 1개 생성!? 하고 메모를 한다.
그리고 계속 확인을 해봐야한다. 컨테이너가 계속 떠있는지 !

원하는 상태 컨테이너 1개 : 실제 떠있는 상태 1개 - 안정적인 상태
현재상태 == 원하는 상태  : Current State == Desired State
만약 다르면 조치를 해줘야한다! 

Disired State : 쿠버네티스느 이러한 루프를 계속 돈다.
상태체크 (Observe) -> 차이점발견 (Diff) -> 조치 (Act)
이러한 Loop 를 계속 돈다.!!


음 또 요청이들어왔다. 음... 새 컨테이너는 어디에(1번서버 또는 2번서버) 어디에!! 배포하지 ?
근데 이렇게 매일 어디에 배포하는지 확인하고 하는게 귀찮을 수 있다!

그래서 Scheduler 를 뽑을 수 있어!! ( 두번째 서버에 넣으면될것같은데!? 라는 생각)
또 컨테이너 상태를 체크할 사람을 뽑자! Controller를 뽑자!!
또 여러가지 부가적인것도 확인하는 것을 뽑을 사람이 필요해! 뽑아!!그게 전부 다 컨트롤러 입니다.


Desired State : Replication Controller , Endpoint Controller, Namespace Controller 등등 
이렇게 체크하는 컨트롤러를 만들 수 있다 ! ! ! ! 

![image](https://user-images.githubusercontent.com/86240112/133997340-320b99c6-c1ee-4855-9668-fb80aaef6bed.png)

etcd : 데이터베이스? 같은느낌 - 모든 상태와 데이터를 저장, key -value 형태로 데이터저장 
현재 상태를 전부 저장하기 때문에 중요해에! 백업은 필수다 

Master 상세 - API server : 상태를 바꾸거나 조회 , etcd 와 유일하게 통신하는 모듈 , Rest api 형태로 제공!
권한을 체크하여 적절한 권한이 없을 경우 요청을 차단 ! 조회나 요청을 이 Api Server 를 통해서 ! ! ! ! !

Master 상세 - Scheduler : 새로 생성된 Pod를 감지하고 실행할 노드를 선택, 노드의 현재상태와 Pod 요구사항 체크
노드에 라벨을 부여


Master 상세 - Controller : 복제컨트롤러 노드 컨트롤러 엔드포인트컨트롤러 등등 많다. 끊임없이 상태를 체크하고 원하는 상태를 유지한다. 단일 프로세스로 실행 ! ! ! ! ! 


조회흐름 ! ! ! Controller 가 ApiServer 에게 정보를 조회할게요! 하면 이제 API Server 는 권한 체크를 하고 etcd 에 그 상태를 조회하고 보내준다 ! 그리고 지금 원하는 상태가 변경되었다 ! 이런것도 알려준다. 
그럼 Controller 을 그 변경사항을 알고나서 변경을 해주고! API Server에 변경한 것을 알려줌 . 갱싱 권한 체크하고 etcd 에 변화함


그럼 이제 Node 를 보자!

하나는 Proxy 하나는 Kublete (큐블릿) 이 뜬다.
마스터와 통신할때 API Server랑만 통신을 한다!

큐블릿이 !! Pod 이랑 통신을 한다 !!
각 노드에서 실행!
큐블릿은 각 노드에 꼭 떠있어야한다. 이 큐블릿이 Pod을 실행하고 중지하기 때문에!! 

프록시 !! 네트워크 프록시와 부하분산 역할, 실제로 하는 역할은 설정! 

![image](https://user-images.githubusercontent.com/86240112/133998321-ef07d63b-472b-45a2-bffb-0a26118929e9.png)


-- 흐름

어떤 관리자가 요청을 하는거지 Pod을 추가해줘!
API Server에 요청을 하는거지!
요청을 받은 API Server는 etcd에 Pod - 생성 요청이 왔다고 적어놓는다.
Controller 가 계속 체크를 한다. 새 Pod 확인을 계속하다가 요청을 보고! 할당하는 요청을 한다!
Api Server는 Pod 할당요청을 해라! 라고 etcd에요청 !
스케줄러는 이제 그 요청을 계속 보다가 어디에 어떤 node에 Pod를 할당할까.. 생각하다가 APi Server에 요청!

Api server는 특정 노드에 할당하는데 실행되기 전이다! 라고 etcd에 상태변화!
이제 '큐블릿'이 실행이 안된 pod이인나 확인하다가! 확인하고 pod를 생성한다! 큐블릿이!

이제 다시 API Sever에서는 그 정보를 보고 Etcd에 pod 할당되어있고 실행되어있따고 업데이트를 한다!!

그래서 계속 Controller Kubelete Api Server Etcd 는 계속~~~~ 실행되고있어 항상 체크하면서 업데이트하고!


# 쿠버네티스 아키텍처 - 2 ( 오브젝트 )

Pod : 가장 작은 배포 단위 - Container를 배포하는 것이 아니라 Pod를 배포함
그리고 고유 IP를 갖고있따.

여러개의 컨테이너가 하나의 Pod에 속할 수 있어. 보통은 1개의 Container가 존재하지!
이 여러개 컨테이너가 하나의 Pod에서 자원을 공유할수도있어 

ReplicaSet : 여러개의 Pod를 관리! 
만약 이걸 3 -> 4 로 바꾸면 이걸 ReplicaSet이 하나의 Pod를 생성해줌! 삭제도 가능

Deployment 버전 1 , 버전 2로 무중단 배포를 해야할때 Replicas 를 이용한다! 
내부적인 무언가 없고 Depolyment는 Replicaset을 이용해서 무중단 배포를 한다!

Service - ClusterIp : 클러스터 내부에서 사용하는 프록시 
Pod는 동적이지만 서비스는 고유 IP를 가짐
Pod는 죽고 새로 생성되고 하는데! 만약 여기서 IP를 없어지거나할텐데 그러면 .. 문제가생겨
그래서 Pod가 줄던 IP가 바뀌던 생서되던 앞에 Service가 있음 !!

![image](https://user-images.githubusercontent.com/86240112/134001436-cec092db-9ba8-42d1-af46-dbd6c92187e7.png)

근데 여기서 조금 의아한건 Cluster Ip는 내부에서만 접근가능하다! 그래서 nodePort가 있따!


![image](https://user-images.githubusercontent.com/86240112/134001820-0138f282-b0ef-4078-b07e-65b54eea8e69.png)

즉슨, Node1, 2 든 아무대나 보내도 알아서 찾아간다! 
근데 여기서 문제는.. 1번 노드가 만약 죽으면 어떻게 될까 !?

2번 노드로 붙어야하는데.. NodePort는 어떻게 ... 움??

그래서 여기서 또!! Service (LoadBalancer ) 가 생겼다!


![image](https://user-images.githubusercontent.com/86240112/134002083-349435c6-6e01-4c3e-a2c7-42200ff626a2.png)

Ingress ! 그 또 LoadBalnacer를 여러개 만들다기보다 또 앞단에 한개 따악! 도메인 또는 경로별 라우팅!
즉슨 Delpoyment를 생성하고 그러면 ReplicaSet이 자동으로 생성하고 이게 Pod를 생성하는거지!

또 이걸 외부에 노출해야하니까 Service(ClusterIp)가 생긴거지 그리고 NodePort! 그리고 LoadBalancer ! 
그리고 마지막으로 Ingress !!

그 외 기본 오브젝트 : Volume : EBS, NFS와 같은 Storage도 있고.. ConfigMap - 설정 !


# API 호출! 

Pod이라는 오브젝트가 있었고 이제 이걸 띄우고싶다 하면! 
yml 에 key value를 사용해서 표현을 한다

```java
apiVersion : 1
kind: Pod
metadata:
  name: example
spec:
  containers:     # 컨테이너가 여러개니까!
  - name: busybox
    image : busybox :1.25
```
api 가 이 명세를 보고 etcd에 넣으면 이제 각 오브젝트(스케줄러, 컨트롤 등등) 이 실행이되기 시작한다!

ArgoCd (Custom Resource) 


중요!!!!!       (조립된 사진)      (레고 자원) (설명서)        (조립)
API 호출하기 -> 원하는 상태를 다양한 오브젝트로 정의 하고 API 서버에 yaml 형식으로 전달!

# 돼지용

컨트롤러 플레인이 곧 마스터 == 마스터 노드이다. 컨트롤러 플레인에는 api server, 스케줄러, 컨트롤러 매니저, etcd가 있다. 






참고할 만한 자료 :

https://ikcoo.tistory.com/147
https://brunch.co.kr/@topasvga/1814


















































































