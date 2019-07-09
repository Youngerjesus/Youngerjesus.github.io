---
layout: post
title:  "Introduction Klaytn"
date:   2019-07-09 11:36:36 +0530
tags: [klaytn, blockchain]
author: Youngerjesus

---
<link href="https://fonts.googleapis.com/css?family=Roboto&display=swap" rel="stylesheet">
<pre style="white-space: pre-line;
    word-break: break-word;">
<p>클레이튼 기존 블록체인 플랫폼의 약점 
Scalability(확장성) - 얼마나 많은 일을 신속히 처리할 수 있는지가 확장성이다 
    확장성을 알아보기 위해서는 두가지 조건이 있다. 
    TPS + Block Interval    
    TPS: 초당 몇개의 거래를 처리할 수 있는    
    Block Interval: 블록 생성 간격 - 블록이 어느정도 시간을 기준으로 만들어지는가 

        TPS 
            Visa TPS: 1700 
            비트코인 TPS: 7 (현실적으로는 2개에서 3개) 
            이더리움 TPS: 20  
            Klaytn TPS: 3000 
           
        Block Interval
            비트코인: 10분 
            이더리움: 15초 ~ 20초
            Klaytn: 1초 
            
            이게 실제로 어떻게 작용하는지 예를 들어서보면 TPS가 10000, Block Interval이 10분이다라고 생각해보자 
            물론 뒤에온 트랜잭션이 앞에온 트랜잭션보다 수수료 gas 를 더 많이 지불한다면 우선순위가 높아지지만 우선순위를 따지지않고 생각해보면
            최대로 내가 대기하는 시간은 10분이 걸릴 수 있다. 내가 요청을 보냈는데 10분뒤에 처리해준다면 그 블록체인은 아마 쓰고 싶지 않을거다 
        
        그리고 기존의 블록체인 네트워크와 비교해보면 참여자가 많아질수록 요청을 보내는 트랜잭션의 수가 많아지고 참여하는 노드 중에 제일 느린 노드에 맞게 하향 평준화가 된다
        (모든 참여자가 합의를 도출해야하니까 정보의 검증은 가장 느린 노드의 속도에 맞출 수 밖에 없다)
        이런경우 네트워크는 점점 느려질 수 밖에 없늗데  일반 클라이언트-서버구조라면 서버를 여러대 두는걸로 해결하지만 블록체인은 그렇게 해결할 수가 없다. 
        klaytn 같은 경우는 합의를 담담하는 (여기서는 요청을 처리한다고 생각 할 수 있다)CN 노드의 스펙을 올려서 이 문제를 해결한다. 
        
        CN(합의 노드의 참여조건)
        - Physical core가 40개 이상 
        - 256GB RAM 
        - 1년치의 데이터 약 14TB 저장 
        - 10G 네트워크

    Finality - 변경 불가능한 최종적인 상태를 말하고 블록이 Final 하다라는건 블록에 담긴 거래가 바뀔 수 없다는 걸 보증한다.
        내가 어떤 상품을 살라고 결제를 헀는데 결제가 안 되었을수도 있다라는 말이다.  
         
        비트코인과 이더리움은 이 최종성 확정성이 부족하다.
            여기서의 최종성은 완벽한 보증이아니라 처리가 될거라는 확률론적 최종성만 제공한다.  

            비트코인 기준 Finality까지의 평균시간 60분 (6번의 검증던계)
            이더리움 기준 Finality까지의 평균시간 6분(25번의 검증단계) 

        궁금한게 비트코인과 이더리움에서 내가 요청한 트랜잭션이 블록에 담기게 되고 이 블록이 메이저 체인에 연결되었는지를 확인하는 방법이 없는건지 궁금하다
        (메이저 체인에 연결되었다라는건 최종성이 보장되었다 라는 뜻이니까)
       
    Fork - 블록들의 연결이 두개 이상으로 갈라지는 걸 말한다. 
        이더리움과 블록체인의 작업증명 방식(pow)
            블록체인에 경쟁적으로 블록을 추가하기 위해 문제를 푼다.(Hash 값을 찾기 위해서 )
            이렇게 독립적으로 개개인이 채굴이 가능하기 때문에 동시에 블록을 채굴할 수 있고 블록이 두개가 올라오게 되고 분기가 발생한다. 
            
            이렇게 분기가 일어날경우 갈라진 블록에 대해서 다시 재전송해서 하나의 체인으로 연결시켜주는 작업을 해야한다. 
            작업증명 방식은 어떠한 노드든지 블록을 만들고 전파할 수 있기때문에 정보를 얻기 위해서는 가능한 많은 연결을 해야하는 문제가 있다 
        
        클레이튼의 경우에서는 블록을 만드는 노드가 정해져있어서 fork가 일어날 수 없고  
        블록 생성을 알려주는 Proxy Node가 있어서 이 노드와 연결을 하면 바로 최신정보를 받을 수 있다  

클레이튼 블록체인 
    합의 
        어떤 합의알고리즘을 사용해서 문제점을 해결하는지를 보겠다
        합의 알고리즘은 여러개가 있고 Public , Private에 따라서 다르다 
        Public 블록체인     
            Pow, Pos 

        Privae 블록체인 
            pBFT, Raft 
        클레이튼의 경우 이런 문제를 해결하는 IBFT 알고리즘(이스탄불 비잔티움 결함 허용)
        BFT기반의 알고리즘은 이더리움의 Pow와는 다르게 암호해독을 위한 에너지를 낭비하지 않고 
            참여 노드 수를 제한시켜서 성능 높임
            하지만 참여 노드 수가 제한된다라는건 분산화를 약화시키고, 합의 결과가 소규모집단에서만 공개되므로 투명성이 저하되고 블록체인을 효율적으로 사용하는게 아니게된다. 
        
        클레이튼은 이러한 BFT기반 성능이점을 살리고 public 블록체인읮 장점과 합쳐서 단점을 개선시켜서 IBFT를 합의 알고리즘으로 선택한다. 
        IBFT는 공개를 통한 개인적인 합의 신뢰 모델로서 합의를 달성하는 소수 private 노드와 바깥에서 블록 생성 결과를 공개적으로 접근 및 검증하는 노드 이렇게 구성돠어있다. 
        
        블록 생성 사이클
            클레이튼의 블록생성주기는 라운드라고한다. 
            새로운 블록을 생성하고 끝내는 즉시 새로운 라운드가 시작된다. 
            블록의 생성시간은 약 1초정도가 된다. 

        IBFT 크게 세단계의 합의 과정이 있다. 
            pre-prepare - prepare - commit
            라운드 로빈 방식을 사용해서 매 라운드마다 합의 노드들 중에 Proposer(제안자)를 뽑는다. 그리고 나머지 합의 노드들은 Validator 검증을 하는 노드가 된다. 
            Propser Validator1 Validator2 Validator3이렇게 다 같은 합의 노드들이다. 
            이 중에 Validator3에 x가 되있다라는건 fault인 상태로 합의에 참여하지 못하는 상태를 말한다 이유로는 네트워크가 끊어졌거나, 악의적인 행동을 해서이다. 
            
            합의는 라운드 로빈 방식으로 진행된다. 
            Propose 단계
                합의 노드 중 하나가 Propser로 선택을한다. 
                (제안자를 구별하는 방법은 각각의 합의 노드가 가장 최근의 블록헤더에서 파생된 난수를 사용해서 자기가 라운드에 선택되었는지를 증명한다고 알려져있는데 이게 정확히 무슨소린진 잘 모르겠다.)
                (하여튼 합의 노드가 자신이 제안자라는 걸 알게되면 자신의 공개키를 통해서 Validator들에게 내가 제안자라고 알리게 된다. )
                (그리고 Validator도 자신이 Validator라는 사실을 Propser에게 알린다)

                여기서 Validator와 Propser가 누군지 서로 알게된다. 
            pre-prepare 
                Proposer가 트랜잭션 풀에서 트랜잭션을 선택하고 정렬해서 블록을 만들고 모든 Validator들에게 제안을 하게 된다. 
            prepare
                Validator는 Proposer에게 메시지를 받게되면 자신을 제외한 다른 노드들에게 잘 받았다고 메시지를 보낸다 
                여기서 Validator3은 fault가 일어난 상태이므로 어떠한 메시지 전송도 하지못한다. 
                이렇게 함으로써 몇개의 노드가 지금 합의에 참여하는지를 알 수 있게 된다. 
            commit 
                Proposer들에게 받은 제안을 수락할건지 다른 노드들과 통신하며 결정한다. 
                3분의2이상이 승락을 하면 블록 승인을한다 결국 이 commit 단계에서 결정이되고 비트코인과 이더리움과는 다르게 finality 부재가 없고 변경 불가능한 데이터가 이 stage에 저장된다.   

            블록 생성 전파                 
                제안된 블록은 Validator가 3분의 2이상이 승락을해서 성공적으로 완료되었다면 모든 블록들에게 알리고 그 합의 라운드는 끝이나게된다 
                모든 블록들에게 알리기 위해서 프록시 노드를 통해 엔드 포인트 노드들에게 전달이 된다. 이렇게 되면 모두가 동기화 되는 것이다. 

            이 방식의 문제점이라고하면 합의 노드가 많아질수록 통신의량은 기하 급수적으로 많아진다 라는 문제점이 있다. 
            그래서 연구에따르면 합의를 실행하는 노드가 16개 이상이되면 컨센서스가 크게 지연되는 즉 블록 생성이 지연되는 문제가 있다고 한다.
            그렇지만 데이터를 분산시키고 신뢰를 높이기 위해서는 합의에 참여하는 노드의 수가 많을 수록 좋다 
            이 두가지 요구사항을 고려했을떄 클레이튼은 각 합의 라운드마다 CN의 전체 집합중에서 서브 세트를 무작위로 선택함으로써 신뢰성도 높이고 처리하는 속도도 빠르게 한다  
    
    네트워크 구조 
        이 클레이튼 네트워크 축소판을 보면 
        전체 네트워크안에 Core Cell Newtork가 존재하고 Core Cell을 둘러싸는 Endpoint Node Network가 존재한다. 이렇게 클레이튼은 단일 네트워크가 아닌 two Layer Architecture로 이뤄져있다.
         
        Core Cell 네트워크를 보면 
            CNN: Consensus Node Network
            PNN: Proxy Node Network 로 구성되어있다 
            CN이 합의를 담당하는 노드고 PN은 생성된 블록을 EN에게 알려주는 역할을 하거나 EN이 제안한 트랜잭션을 CNN에게 알려주는 역할을한다. 

            하나의 Core Cell을 보면 한명의 참여자가 운영하게 되고 한개의 CN과 CN과 연결되어있느 여러개의 PN으로 구성한다 
            CN으로 참여하기 위해서는 조건이 있었었다. 성능이 종아야한다고 한개만 느려도 하향평준화가 되니까 
            CN은 자기들끼리 계속 소통 수 있고 빠르게 통신할 수 있도록 연결되어 있다 
            CN은 외부와 직접적으로 접촉할 수 없고 굉장히 Private환 환경에 놓여있게된다.  
                왜 이런 구조를 가지고 있냐면 CN이 EN과 직접적 연결이 된다고 가정할 경우에 커넥션이 계속적으로 늘어나면 성능이 떨어지니까 합의속도가 느려지는 상황이 생기기 때문에 
                CN은 자신이 믿을 수 있는 PN과만 연결한다. 
    
        바깥의 Endpont Node Network를 보면 
            EN은 Core Cell Network와 연결되어있다. 
            물론 EN끼리도 연결해서 정보를 주고받는것도 가능하다. 

            EN가 되기위한 특별한 조건이 없고 아무나 가능하고 d-app이나 web 클라이언트 들에게 정보를 제공하는게 가능하다 
        
        CN BootNode, PN BootNode EN BootNode들은 새로 들어온 노드들이 등록을 하는곳이고 
        또 다른 노드들과 연결할 수 있도록 도움을 주는 곳이다. 클레이튼에서 운영하느 노드들이다. 
             
    서비스 체인 
        클레이튼의 서비스 체인은 메인넷과 연결되는 독립적으로 운영되는 블록체인이다 
        확장성을 기반으로 나온 아이디어인데  독립된 서비스 공간을 구축하고 필요할 때 메인 네트워크에 신뢰를 얻는다라고 알려져있다  
        언제 서비스 체인이 쓰이냐면 
            B-app이 특별한 노드환경에서 설정되거나 
            Private 블록체인으로 쓰고싶을때 보안수준을 맞추기 위해서 
            많은 처리량을 요구해서 메인넷 배포하기에는 적합하지 않은 경우 (이더리움 같은 경우에 크립토 키리라는 d-app이 인기가 엄청날때 이더리움 네트워크 전체가 느려지는 일이 있었었다 )

        메인넷과 서비스 체인의 연결이 자유로운것은 아니다. 오직 제한된 트랜잭션만을 사용하는게 가능하다. (klay전송이 어느 조건을 만족할때만 가능하다고 알고있다) 

        클레이튼의 서비스체인안에서는 트랜잭션 수수료를 안받게 할 수 있고 자기가 원하는 환경을 구축하는게 가능하다.      
        
 

</p>
Reference: 
https://m.blog.naver.com/PostView.nhn?blogId=ehdtmdcouple&logNo=221183650560&proxyReferer=https%3A%2F%2Fwww.google.com%2F

https://baobab.wallet.klaytn.com/

https://ide.klaytn.com/

https://baobab.scope.klaytn.com/

</pre>