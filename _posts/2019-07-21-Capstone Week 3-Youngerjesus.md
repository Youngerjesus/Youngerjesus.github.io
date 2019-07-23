---
layout: post
title:  "Week 3 capstone Identity "
date:   2019-07-09 11:36:36 +0530
tags: [identity, blockchain, Identity Management,uPort]
author: Youngerjesus
categories: blockchain sovrin blockstack jolocom shoCard capstone 
---

<h2 id="목차"> 목차 </h2>
<ul>
    <li> Sovrin  
        <ul> 
            <li> overview </li>
            <li> DID </li>
            <li> Evaluation </li>
        </ul>   
    </li>
    <li> jolocom 
        <ul> 
            <li> overview </li>
            <li> HD Key </li>
            <li> Evaluation </li>
        </ul>   
    </li>
    <li> shoCard
        <ul> 
            <li> overview </li>
            <li> The shoCard Archietecture </li>
            <li> Third-party Certification </li>
            <li> Evaluation </li>
        </ul>   
    </li>
    <li> Blockstack 
        <ul> 
            <li> overview </li>
            <li> gaia </li>
            <li> Evaluation </li>
        </ul>   
    </li>
</ul>
<pre style="white-space: pre;
    word-break: break-word;">
<h3> SOVRIN  </h3>
    Sovrin은 사용자가 a self-sovereign identity를 평생 동안 소유할 수 있도록 하고, 이를 저장하기 위해 중앙 당국에 의존하지 않는다는 것을 의미한다.
     <div class="no" style="display: none;" > 이 말은 사용자가 스스로 자기 신원을 관리할 수 있다는 말입니다  
    제3자가 확인한 데이터를 말합니다 은행 계좌 정보, 의료 데이터와 같은 개인 정보라고 생각하면 됩니다 
    </div>
    sovrin에서는 검증 가능한 클레임을 보다 쉽고 안전하게 표현, 교환 및 확인할 수 있고 그들이 어떤 정보를 공개하고 교환할것인지를 선택할 수 있다.

    Sovrin [21]은 Permissioned distributed ledger 기술을 기반으로 구축된 공공 오픈 소스 네트워크로입니다 
   <div class="no" style="display: none;" >  참여하기 위해서는 Sovrin Foundation의 허가를 받아야만 한다는 소리다  
    허가를 받기만 하면 sovrin에서는 누구든지 신분을 만들 수 있고 인터넷에 접속할 수 있는 사람은 신원을 확인할 수 있다. 
   </div>
    
    sovrin ID는 decentralized identifiers (DID)를 사용하여 ID를 활성화하고 asym-metric cryptography를 사용하여 사용자에게 바인딩한다.
    <div class="no" style="display: none;">
    DID를 사용하는 이유는 DID는  (IP 주소 또는 전화 번호와 달리) 중앙 권한을 통해 발행할 필요가 없으며 영구적이고, 식별자를 만들 수 있기 때문입니다 
    ID 소유자는 그러한 식별자에 대한 완전한 통제권을 유지한다. (IP 주소 또는 전화 번호와 달리) </div>
    DID는 개방형 표준이라서  모든 블록체인에서 DID를 등록하고 해결하는 방법을 정의하는 할 수 있다.
    이러한 DID는 ID 소유자의 각 공개 키(이 DID), ID 소유자가 공개하고자 하는 기타 정보 및 상호 작용에 필요한 네트워크 주소로 구성된 DID 문서 객체(DDO)로 블록체인(blockchain)에 배치된다.
    <div class="no" style="display: none;" > (ID 소유자가 공개키를 통해서 자신이 드러내고자하는 정보를 DDO로 블록체인에 배치한다) </div>
    
<h3> DID Technology </h3>
    DID는 a unique identifier 와 an associated DID Document의 두 가지다
        The unique identifier looks something like 
        “did:example:123456789abcdefghi” 
         <div class="no" style="display: none;" > (DID Document를 조회하기 위한 고유 ID라고 생각하면 된다) </div>
        DID Document는 JSON-LD 객체로서, 검색이 용이하도록 어떤 중앙 위치에 저장되어 있다.
        json-LD는 json을 사용해서 linked data를 인코딩하는 방식이다 
         <div class="no" style="display: none;" > 
         (json과 유사한 방식으로 직렬화 하는게 가능하고 Linked-data가 웹상에 존재하는 데이터를 개별 URI로 식별하기 떄문에 JSON-LD를 사용한다)
        </div>
        JSON-LD 
        JSON is a useful data serialization and messaging format 
        <div class="example">
        {
            <span class="na"> "@context" : </span>  <span class="s2"> "https://w3id.org/did/v1",</span> 
            <span class="na">"id" :</span>   <span class="s2"> "did : example : 123456789abcdefghi", </span>
            <span class="na">"authentication" : </span>:  <span class="s2"> [{
                // 다음과 같이 인증하는 데 사용됩니다. ... ... 
                "id": "예 : 123456789abcdefghi # keys-1",
                "type": "RsaVerificationKey2018",
                "controller": "did : example : 123456789abcdefghi",
                "publicKeyPem": "----- 공개 키 시작 ... 최종 공개 키 ----- \ r \ n"
            }], </span>
            <span class="na">"service": </span>   <span class="s2"> [{
                // DID와 연결된 인증 가능한 자격 증명을 검색하는 데 사용됩니다.
                "type": "VerifiableCredentialService",
                "serviceEndpoint": "https://example.com/vc/"
            }] </span>
        }
        </div >

<h4> @context (Must) </h4>
        {
           "@context": "https://w3id.org/did/v1"
        }
        대화의 context를 정하는 부분이다 
         <div class="no" style="display: none;" > (두 소프트웨어 시스템이 데이터를 교환할떄 서로 이해하는 프로토콜을 사용해야한다 그 부분을 정하는 곳) </div>
<h4> @id </h4>
        {
          "id": "did:example:21tDAKCERh95uGgKbJNHYp"
        }
            did:” + <method> + “:” <method-specific-identifier>. 
            Above, my method was “example” and my method-specific-identifier was “123456789abcdefghi”.
            DID Document를 조회하기 위한 고유 ID다 id는 method와 method specific identifier로 나뉜다 
             <div class="no" style="display: none;" > (실제로 내가 DID 찾을 방법을 정하는 부분으로 현재는 비트코인, sovrin, IPFs, 등 9가지 등록방법이 정의되어있다) </div>

<h4> @public Keys </h4>
 <div class="example">
        <span class="na"> "publicKey": </span> <span class="s2"> [{
                "id": "did:example:123456789abcdefghi#keys-1",
                "type": "RsaVerificationKey2018",
                "controller": "did:example:123456789abcdefghi",
                "publicKeyPem": "-----BEGIN PUBLIC KEY...END PUBLIC KEY-----\r\n"
            }, {
                "id": "did:example:123456789abcdefghi#keys-2",
                "type": "Ed25519VerificationKey2018",
                "controller": "did:example:pqrstuvwxyz0987654321",
                "publicKeyBase58": "H3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
            }, {
                "id": "did:example:123456789abcdefghi#keys-3",
                "type": "Secp256k1VerificationKey2018",
                "controller": "did:example:123456789abcdefghi",
                "publicKeyHex": "02b97c30de767f084ce3080168ee293053ba33b235d7116a3263d29f1450936b71"
            }],  </span>
        ...
        } 
    </div>
            공개키는 디지털 서명, 암호화 및 기타 암호화 작업에 사용되며 Service end point와의 보안 통신 설정을 하는데 사용된다 
             <div class="no" style="display: none;" > 
             (publicKey property의 값은 공개 키의 배열로서 여러개 등록하는게 가능하다 대신에 중복항목을 포함해서는 안됩니다 
             여기서의 공개키는 인증에서 삽입되거나 참조 될 수 있습니다 )
             </div>

<h4> Authentication </h4>
 <div class="example">
            {
                <span class="na"> "@context": </span> <span class="s2"> "https://w3id.org/did/v1",</span>
                "id": "did:example:123456789abcdefghi",
                ...
                <span class="na"> "authentication": </span >  <span class="s2">[
                    // this method can be used to authenticate as did:...fghi
                    "did:example:123456789abcdefghi#keys-1",
                    // this method can be used to authenticate as did:...fghi
                    "did:example:123456789abcdefghi#biometric-1",
                    // this method is *only* authorized for authentication, it may not
                    // be used for any other proof purpose, so its full description is
                    // embedded here rather than using only a reference
                    {
                    "id": "did:example:123456789abcdefghi#keys-2",
                    "type": "Ed25519VerificationKey2018",
                    "controller": "did:example:123456789abcdefghi",
                    "publicKeyBase58": "H3C2AVvLMv6gmMNam3uVAjZpfkcJCwDwnZn6z3wXmqPV"
                    }
                ],</span>
                ...
            }
        </div>
            인증은 DID subject(사용자)가 DID와 관련되어 있다는 것을 암호로 증명하는 매커니즘이다 
    <h4> Service Endpoint </h4>
    <div class="example">
            {
                <span class="na"> "service":</span> <span class="s2">[{
                    "id": "did:example:123456789abcdefghi#openid",
                    "type": "OpenIdConnectVersion1.0Service",
                    "serviceEndpoint": "https://openid.example.com/"
                }, {
                    "id": "did:example:123456789abcdefghi#vcr",
                    "type": "CredentialRepositoryService",
                    "serviceEndpoint": "https://repository.example.com/service/8377464"
                }, {
                    "id": "did:example:123456789abcdefghi#xdi",
                    "type": "XdiService",
                    "serviceEndpoint": "https://xdi.example.com/8377464"
                }, {
                    "id": "did:example:123456789abcdefghi#agent",
                    "type": "AgentService",
                    "serviceEndpoint": "https://agent.example.com/8377464"
                }, {
                    "id": "did:example:123456789abcdefghi#hub",
                    "type": "HubService",
                    "serviceEndpoint": "https://hub.example.com/.identity/did:example:0123456789abcdef/"
                }, {
                    "id": "did:example:123456789abcdefghi#messages",
                    "type": "MessagingService",
                    "serviceEndpoint": "https://example.com/messages/8377464"
                }, {
                    "id": "did:example:123456789abcdefghi#inbox",
                    "type": "SocialWebInboxService",
                    "serviceEndpoint": "https://social.example.com/83hfh37dj",
                    "description": "My public social inbox",
                    "spamCost": {
                    "amount": "0.50",
                    "currency": "USD"
                    }
                }, {
                    "id": "did:example:123456789abcdefghi#authpush",
                    "type": "DidAuthPushModeVersion1",
                    "serviceEndpoint": "http://auth.example.com/did:example:123456789abcdefg"
                }]</span>
            }
        </div>
            service end point는 해당 사용자에대한 service end point의 검색을 가능하게 하는것 

<h3> Evaluation </h3>
    sovrin identity를 사용하면 transaction cost를 줄일 수 있고 개인정보보호, 사이버 범죄의 제한, 간단한 신원인증을 할 수 있다 
     <div class="no" style="display: none;" >
    (transaction cost를 줄인다는 말은 판매자가 고객에 대한 더 많은 정보를 얻을 수 있다라는 것 내가 차량을 렌트하는데 
    이 사람의 신원정보중에 차량 경력이 많고, 사고 경력이 없다라고 판단이 되면 더 낮은 가격을 제시해도 된다 
    
    사이버 범죄를 제한한다라는건 판매를 할때 판매자와 구매자 모두 자신의 신분을 증명하고 검증받아야만 팔 수 있기 떄문에 사이버 버모지가 줄어들 수 있다는 취지다
    
    신원을 간단하게 한다라는건 일상생활의 다양한 분야에서 sovrin 신원 하나로 적용이 될 거라는 말이다. 근데 이건 sovrin 신원을 사용하는 사람의 양에 따라 달려있다 
    sovrin신원을 많이 사용하는 곳에서는 sovrin신원을 포함하는게 적합해지지만 사용자가 상대적으로 적다면 sovrin 신원을 도입할라고 하지 않을것이다. 즉 전적으로 사용자의 수에따라 달려있다)
    
    Jolocom과 uPort같은 경우는 Ethereum blockchain을 사용해 모든 노드가 참여하고 보상을 받는 반면에 
    ) 
    </div>
    sovrin은 permissioned blockchain으로 합의를 담당하는 노드는 sovrin foundation에서 정해져있다 
    이 경우 블록체인 실행 노드가 악의적으로 축소될 위험이 있다 



<h3> JOLOCOM </h3>
    JOLOCOM은 사용자에게 decentrailized identity를 제공하기 위해서 hierarchical deterministic keys (HD keys)를 사용한다 
    HD 키는 시드에서 생성되고 사용자가 제어권을 가지고 있으며 부모 키로부터 자식 키를 추가적으로 생성하는게 가능하다 
    시드만 알고 있다면 언제든지 복구가 가능하며 이를 통해 사용자는 익명성을 제공하기 위한 하위 신분을 여러개 생성할 수 있다
     <div class="no" style="display: none;" >
    HD KEY가 아닌 여러개의 공개키 개인키를 가지고 있는것은 복구하는 과정에 비용이 많이 든다고 합니다 
    </div>

    HD 자식 키의 프로비저닝을 통해 통합 된I oT 장치의 소유권 모델링을 가능하게하여 Jolocom 신원 사용자에게 진정으로 모든 속성을 반영한 본격적인 분산 형 디지털 신원을 구축 할 수있는 방법을 제공합니다
<div class="no" style="display: none;" >
     (HD KEY를 통해 하위 자식 키를 여러개 만들 수 있고 이것들을 각각 IOT기기의 소유권과 매핑시킬 수 있다)

     마스터 시드로부터 마스터 키쌍을만들고 이거로부터 자식키가 유도되는 모습
</div>

    HD 키를 사용한다면 identity Management system에서는 사용적합성의 문제가 있다. 
    DID에서 사용자의 public key는 DDO의 IPFS 헤시에대해 매핑된다  
    이건 Ethereum smart contract에 의해 저장되어지는데 워낙 많이 공개키가 있을 수 있으니까 얘가 어디에 매핑되어있는지를 알고 있어야한다. 

<img src="{{ "/assets/img/HDKEY.png" | relative_url }}" alt="">
<h3> Hierarchical Deterministic Key Derivation </h3>
        Path Levels - 마스터 키 쌍은 BIP0032에 따라 개인키를 계층적으로 생성하고 관리할 수 있도록 한다 
        
        Identity path syntax: {m / purpose’ / context’ / entity’}
        
        ex) Path definition: {m / 73’ / signing-key’ / global’}

        Purpose - 신원 키 생성을 목적으로 했기 때문에 상수 73으로 설정된다 

        context - 컨텍스트 필드는 키가 사용되는 컨텍스트를 말한다 
<div class="no" style="display: none;" > 
        (기본적으로 하나의 컨택스트만 정의되며 여기서는 서명 키 컨택스트로 간주된다 )
        </div>
        entity - entity는 키가 더 차별화 될 수 있는 다음 경로 깊이를 정의한다 
            {m / 73’ / signing-key’ / social-media’}

            or:

            {m / 73’ / signing-key’ / gaming’
 
<div class="no" style="display: none;" > 
    (Private verified credentials은 엑세스제어가 필요하고 지속적으로 사용할떄는 자체 호스팅된 서버에 저장되어야하니까 
    지속적인 가용성을 가진 public verified credentials같은 경우에는  IPFS와 같은 분산 스토로지에 저장해야한다. ) 
    </div>

<h3> Evalutaion  </h3>
Jolocom의 미래목표는 오픈소스릴리즈에 관한 기존의 기술 표준을 계속 사용하면서 모든 사람에게 단순하고 전세계적으로 self-sovereign을 제공하는게 목표이다 
그러므로 Identity attribute를 private verified credentials로 저장하고 싶을떄는 적합하지 않다고한다.  



<h3> shoCard </h3>
shoCard는 블록체인 상의 신분관리와 여권이나 운전면허와 같은 이미 신뢰된 정보들과 결합해서 사용한다 
shoCard는 다른 Identity management 시스템과는 달리 자체 서버를 사용해서 관련 정보들을 저장한다 
 <div class="no" style="display: none;" >
(   한번 내가 여행사에서 내 신원 정보를 제공해서 인증과정을 마쳤다면 그 과정을 매번 하지않고 인증했었다라는걸 자체 서버에 저장해둔다 
    그 사람들만이 알 수 있는 정보인 a new symmetric key로 암호화 되기 때문에 자기 서버에 저장한다고 해서 shoCard가 이 정보들을 알 수 있는 방법은 없다) 
</div>
ShoCard의 장점은 여러 블록 체인을 동시에 사용할 수 있고 필요할 경우 새 블록 체인을 추가할 수 있다는 것이다

 <div class="no" style="display: none;" >
(기존의 블록체인 시스템이 중단되거나 공격을받아서 쓸모 없어지는 경우에 다른 블록체인을 사용하는게 가능하다 )
블록체인 가술이면서 블록체인 네트워크에 의존성을 낮췄다 한 public blockchain만 사용한다면 이 블록체인 네트워크 상황에 따라서 traffic이 증가하거나 transaction fee가 증가하는 문제가 생길 수 있다 (실제로 예전에 이런 문제가 있었다고 들었다)
이러한 문제를 대비해 shoCard는 더 좋은 블록체인을 사용할 준비하는것 
이렇게 해도 상관없는게 기존의 블록체인에 쓴 데이터는 영구적으로 실행이 가능하고 레코드는 불변한다 
</div>

<img src="{{ "/assets/img/SHOCARD.png" | relative_url }}" alt="">
<h3> The shoCard Architecture 
• ShoCard SDKs 
• ShoCard Service layer
• ShoCard SideChain
• blockchain caches
• ShoCard Blockchain Adaptor 
</h3>

<h4> ShoCard SDKs </h4>
ShoCard SDK는 다른 서비스를 신뢰하지 않도록 자신의 서버 또는 장치에서 로컬로 모든 검증 검사를 수행한다. 또 블록체인 레코드를 독립적으로 검색하여 검증에 사용할 수 있다.

<h4>ShoCard Service layer </h4>
블록체인뿐만 아니라 서로 다른 애플리케이션과 서버 간의 안전한 통신 파이프라인으로 사용된다.
 <div class="no" style="display: none;" >
(안전한 통신 파이프라인 이라는 의미는 모든 메시지는 클라이언트에서 서명되고 다른 사람의 공개키로 암호화되서 shoCard 서비스는 절대로 데이터를 해독할 수 없다라는 걸 말한다) 
</div>

<h4> ShoCard SideChain </h4>
public 블록체인은 storage가 제한적이고 확장성이 부족한 문제가 있다
이러한 문제 때문에 shoCard에서 사이드 체인을 사용하는데 
사이드 체인은 블록체인에 작성된 다양한 인증에대한 검증 코드를 저장하기 위한 수단으로 제공된다 
 <div class="no" style="display: none;" >
(각각의 기록들은 해쉬되고 그 해시들은 20분 정도마다 작업증거로 블록체인에 쓰여진다.) 
</div>

<h4> blockchain caches </h4>
블록체인 로컬 복사본을 보관해서 더 빠르게 읽을수 있도록 캐쉬를 제공한다

<h4> ShoCard Blockchain Adaptor </h4>
The ShoCard Blockchain Adaptor abstracts the interface to the blockchain that maintains the proof of work, 
so the ShoCard Service layer can remain efficient
블록체인 인터페이스를 추상화해서 여러 블록체인을 사용하기 위한 것 

<img src="{{ "/assets/img/HASH.png" | relative_url }}" alt="">
<h4> Self-certification - 블록체인 상에 자기 신원을 저장하고 이게 나라는 걸 증명하는 것 </h4>
사용자는 shoCard mobile application이 필요하며 asymmetric key pair을 만들어준다 
대부분 일반적인 경우 사용자의 identity는 스마트폰과 같은 모바일 기기에 유지된다
사용자의 신원은 먼저 정부 ID, 운전면허 또는 여권을 스캔하거나 얼굴 이미지, 홍채 스캔 또는 오디오와 같은 생체 인식 정보를 캡처하여 수집한다 
이런 수집된 데이터는 개개인의 name/value fields로 분류되고 사용자의 개인키로 암호화 되어서 스마트폰에 유지된다.
이 과정 후 각각의 name/value fields는 signature hash로 변하고 전체 레코드로 정리된다 그 후 The resulting hash는 사용자의 private key로 서명된 후
블록체인에 저장된다 이걸 self-certification이라고 한다

자신의 스마트폰에 있는  the clear-text value field and code와 a pointer to the self-certification records를 제공함으로써 블록체인 상에 저장된 
record와 내가 가진 신원이 일치한다라는 걸 증명하고 public key를 제공함으로써 이게 내 것임을 보여준다 


<h4> Third-party Certification - 제3자가 개인의 신분과 자격을 증명하고 검증하는 것 </h4>
사용자는 자신의 Identity와 other information을 제3자와 공유할 수 있다 
사용자는 일반적으로 공유하기로 선택한 데이터를 공개 키와 함께 전달하고 블록체인 자체 인증에 대한 포인터를 전달하고 제3자가 다음 중 하나를 통해서 정보를 얻는다 
# an App that can scan her data
# QR 코드를 통해서 공유할 수 있는 웹 사이트 
# Bluetooth 장치 
그 다음 정보를 받은 The verifying entity는 사용자가 그 특정 정보를 소유하고 있는지 검사한다 검사가 완료되면 제3자는 사용자를 인증해준다 
 <div class="no" style="display: none;" >
(이게 뭐냐면 검증 프로세스가 이뤄졌다라는걸 문서화해놓는걸 말한다 전체 프로세스를 반복할 필요 없이 향후에 참조할 수 있도록 하는 것 )
</div>

<h3> Evaluation </h3>
ShoCard website에서는 shoCard를 이렇게 말한다.  
”It’s the one identity verification system that works the way consumers and businesses need it to for security, privacy,
 and always-on fraud protection”
 소비자와 기업을 위한 보안과 프라이버시를 위해서 blockchain identity management 시스템을 사용한다라고 

단점은 ShoCard 시스템에서의 기업은 모든 사용자에 대한 정보를 인증할 수 있기 때문에 이 기업을 사용자가 신뢰할 필요가 있다. 우리가 잘 알고 있는 기업의 경우에는
신뢰하는게 가능하지만 들어보지 못한 곳에 신뢰하기는 어렵다  

shoStore이라는 자체서버를 두기 때문에 서버가 다운되면 인증을 하지 못하는 문제가 있다.

장점은 블록체인을 여러개 사용하는게 가능하고 추가하는게 가능하다 




<h3> Blockstack </h3>
    블록스택은 탈중앙화 컴퓨터 네트워크다
    클라우드 컴퓨팅의 대안(alternative)이라고 생각하면 이해하기 편하다. 
    대개 개발자는 클라우드 서버에 애플리케이션을 개발하거나 그 안에 사용자 데이터를 저장하는데, 블록스택은 이 기능을 대체한다. 
    어떻게 대체하냐면 사용자 개별로 데이터 라커(Locker)를 가집니다 
    <div class="no" style="display: none;" >
    (애초에 데이터를 호스팅하지 않고 자기가 데이터를 가지고 있다가 필요할떄 공유하는 것을 말한다 )
    이런 데이터 라커는 대기업이 사용자로부터 데이터를 뽑아갈 필요 없이 앱과 데이터는 그 사용자의 소유물이 되는 것이다
    </div>
    블록스택에서의 ID는 ID를 등록할 때 유니버셜 ID, 일반 사용자 명(Universal User Name)을 얻는다. 블록스택에 있는 모든 앱에 이 사용자 명으로 로그인할 수 있다. 
     <div class="no" style="display: none;" >
    (새 앱을 사용할 때마다 회원가입을 하지 않고, 동일한 사용자 ID가 블록스택의 모든 앱에 적용된다.) 
    </div>
     <div class="no" style="display: none;" >
    (여타 블록체인들은 대부분 무거운(heavy) 블록체인)
    (체인에 상당량의 데이터를 저장해야 하고, 프로세스를 위한 로직(코드)을 담아야 하는 식이다. 
    </div>

    블록스택은 중요한 정보만 블록체인에 담고, 블록체인상에 퍼블리시하지 않고 대부분은 오프체인으로 구성해 사용자 데이터 라커에 전송된다

    Blockstack은 어떠한 블록체인에서도 작업할 수 있으며, 블록스택 ID라고 하는 블록체인에 대한 ID기능도 제공한다.
    Blockstack ID는 profile과  globally unique names으로 구성되며 사람, 회사, 웹 사이트, 소프트웨어 패키지 등에 등록할 수 있다. 
    각 profile은 public information뿐만 아니라 private information도 포함할 수 있으며, 둘 다 ID owner가 입력한다. 
    다른 동료 및 선택된 기관에서 이 정보를 검증할 수 있음

    블록스택은 애플리케이션이 개인 데이터 잠금 장치와 상호 작용할 수 있도록 하는 사용자 제어 스토리지 시스템인 가이아(Gaia) 스토리지 시스템을 사용하여 
    사용자의 데이터를 제어할 수 있도록 하고있다. 
    사용자는 이러한 데이터 라커를 클라우드 제공자 또는 프라이빗 호스팅과 같은 기타 데이터 스토리지 옵션에 호스팅할 수 있다. 
<div class="no" style="display: none;" >
    (가이아의 데이터는 사용자가 제어하는 암호키에 의해 암호화되고 서명된다. 중요한 것은 사용자가 사용할 제공자를 제어한다는 것이다.)
    </div>
    소프트웨어는 사용자의 데이터 라커가 어디에 위치하든 필요에 따라 접근해 읽어 들인다.
     <div class="no" style="display: none;" >
    (이론상으로는 하드 드라이브로 간주할 수 있지만, 꼭 스마트폰 기기는 아니다. 노트북도 되고, 각자 쓰는 서버든 드롭박스와 같은 서버 제공자든 데이터 라커를 놓을 수 있다. 
    물론 드롭박스나 구글 드라이브 등의 서버 제공자가 데이터 라커 속 프라이버시 정보를 들여다볼 순 없다. 완전히 암호화하기 때문이다)
    </div>
    <img src="{{ "/assets/img/GAIA.png" | relative_url }}" alt="">
    <div class="no" style="display: none;" >
    (gaia 찾기 내가 어떤 이름에 대한 파일을 가져오고 싶다면 블록스택 코어에대한 단일 호출로 내가 찾을 파일에 대해서 라우팅 정보 파일을 가져오고 
    이 라우팅 파일에서 gaia URL을 가져와 스토로지 백엔드에 연결한다 엑세스 권한이 있는경우 파일을 가져오는게 가능하다)
    </div>
    블록스택은 DNS를 대체하기 위해 블록체인 이름 시스템(BNS)이라는 블록체인 기반의 새로운 시스템을 제안한다
    BNS는 DNS와 유사한 기능을 제공하지만 중앙 루트 서버는 없다. BNS의 명명 시스템은 블록체인 및 각각의 private key의 암호화된 주소에 의해 소유되는 이름에 의존한다
    블록스택은 7만개 이상의 도메인 이름이 등록되어 있다고 한. 

Blockstack 목표
블록스택은 개발자들이 쉽게 디앱을 개발할 수 있는 블록체인 플랫폼을 만들고자 한다. 
 <div class="no" style="display: none;" > (ID관리는 블록스택의 목표가 아니라서 구현은 설명될 수 없다)  블록스택은 The identity management system 이상의 것을 시스템이 제공할 수 있다</div>
블록스택의 CEO인 무니브 알리는 컴퓨팅의 다음 시대를 개척하는 게 블록스택의 최대 목표라고 말했다. 
IBM이 개인용 컴퓨터를 개발하면서 컴퓨터 개발의 시대가 시작됐으며 이후 마이크로소프트의 데스크탑 시대와 구글의 클라우드 시대가 이어졌다고 덧붙여 말했다.
그는 다음 시대는 탈중앙화 시대가 될 것이고 그 시대를 위한 플랫폼을 개발하는 게 블록스택이 하는 일이라고 설명했다. 
블록스택 어스는 사용자가 앱에 로그인할 때 블록체인 기반 디앱인지 일반 앱인지 구분할 수 없을 정도로 편리하게 데이터를 입력하게끔 한 신원증명 방식”이라며 
“다만 사용자 데이터에 대한 통제권은 블록스택이 아닌 사용자 개인에게 있다”

<h3> Evaluation </h3>
블록스택이 어떤 블록체인이라도 사용할 수 있다는 사실은 더 이상의 성공을 위해 매우 중요하다. 
왜냐하면 블록스택은 어떤 식으로든 블록체인(blockchain)이 불안정해지는 경우, 예를 들어, 악성 행위자가 51%의 공격을 할 수 있게 하는 시스템에 해시율이 충분하지 않은 경우 등, 
블록체인(blockchain)이 어떤 식으로든 불안정해지는 경우 다른 블록체인을 쓰면되니까
 <div class="no" style="display: none;" >
(그러나 여러 블록체인(blockchain)을 동시에 지원하는 쇼카드의 접근 방식만큼 안전하지 않다.)
</div>

블록스택은 다른 동료와 선택된 당국이 이 정보를 확인할 수 있지만 특정 프로세스가 따로 정의되지는 않는다  <div class="no" style="display: none;" > (D-app에 따라 다르다) </div>
또 다른 큰 장점은 이미 등록된 신분들이 많다는 것이다. 현재 블록스택은 80,000개의 등록 ID[4]를 가지고 있으며, 따라서 블록체인에서 ID 관리를 하는 가장 큰 시스템 중 하나이다.

<div class="no" style="display: none;" >
(구현을 어떻게 하느냐에따라서)
</div>

Reference: https://sovrin.org/wp-content/uploads/Sovrin-Protocol-and-Token-White-Paper.pdf 
	https://medium.com/@adam_14796/understanding-decentralized-ids-dids-839798b91809
	identity Management on the blockchain pdf 
	https://w3c-ccg.github.io/did-spec/
    https://translate.googleusercontent.com/translate_c?depth=1&hl=ko&prev=search&rurl=translate.google.com&sl=en&sp=nmt4&u=https://github.com/jolocom/jolocom-lib/wiki/Jolocom-Whitepaper&xid=17259,15700023,15700186,15700190,15700256,15700259,15700262&usg=ALkJrhhKWgGd7b7jusyyRLC76WPGdtuh3g
    https://github.com/jolocom/jolocom-lib/wiki/Jolocom-Whitepaper
    https://jolocom.io/wp-content/uploads/2018/07/Jolocom-Technical-WP-_-Self-Sovereign-and-Decentralised-Identity-By-Design-2018-03-09.pdf
    http://wiki.hash.kr/index.php/%EB%B8%94%EB%A1%9D%EC%8A%A4%ED%83%9D
    https://blockstack.org/whitepaper.pdf
<pre>