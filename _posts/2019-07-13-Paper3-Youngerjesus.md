---
layout: post
title:  "Identity Management on the Blockchain"
date:   2019-07-09 11:36:36 +0530
tags: [identity, blockchain, Identity Management]
author: Youngerjesus

---

<pre style="white-space: pre;
    word-break: break-word;">
ABSTRACT
    This paper gives an overview over six of the most promis-ing identity management systems that use the blockchain: Sovrin, Jolocom, uPort, ShoCard, Blockstack and Name- coin
    It shortly introduces them, briefly explains their de- sign, evaluates them, assesses in how far they fulfill the promises they make and lastly lists their current work and future goals. In the end, all systems are compared with each other regarding some of their properties


1. INTRODUCTION
    Identity management can be defined as a system to identify, authenticate and authorize individuals or - more generally - identities
    
    Nevertheless, most of those new identity management tech- niques offer a variety of use-cases and can be used for gov- ernments, managing accounts on websites or a new domain name system.
    For example, they can be used to verify a user’s age on multiple websites, without the user having to send each website a photo of his passport.
    Each identity management system is described in its own section and is introduced by a short overview and some of its properties. Then we explain its design in the next subsection. The last subsection begins with an evalu- ation whether the technology fulfills its promises if it listed some, followed by problems and advantages the technology has and lastly lists their current work as well as their future goals (again only if they are listed).



2. SOVRIN
    Self-sovereign 
    Sovrin [21] is a public open source identity network that is built on permissioned distributed ledger technology (DLT).
    Additionally, the identity is private which means they can manage it them- selves and can choose to whom they reveal what information (and to whom not) [3] [1].
    Sovrin enables its users to have a self-sovereign identity [22], which means that the users have lifelong full ownership of their identity and do not rely on any central authority to store it

2.1 Design
    A Sovrin identity uses decentralized identifiers (DID) [6] to enable the identity and binds them to a user by using asym- metric cryptography.
    The DIDs require no central authority to be issued and enable users to create identifiers that are permanent, globally unique and cryptographically verified while the identity owner maintains full control over those identifiers. 

2.2 Evaluation
    On their website the Sovrin Foundation claims that ”Sovrin identities will lower transaction costs, protect people’s per- sonal information, limit opportunity for cybercrime, simplify identity challenges in fields from healthcare to bank- ing to IoT to voter 
    
    The argument for lower transaction cost is that since the seller can have more information about a customer he can reduce his risk and therefore his price.
    An example of this could be a car renting firm, where the customer can show his driving record i.e. the record that shows all received punishments that are driving related if he has it attached to his identity and wants to show it.
    The car renting firm’s employee could now check whether the customer has any major driving violations or if (supposedly) is a safe driver. If the customer appears to be a safe driver, the risk for the car renting firm reduces and therefore it can offer a better price.

    The protection of people’s personal information is also given, since people themselves can choose what to share.
    If some- one does not want to share anything, one is not forced to do so and therefore one’s privacy is not infringed.
    However, it is possible that for example sellers will not sell anything if a user does not expose her name. In this case the user is not entirely forced to reveal it, but in order for her to get the item she needs to do that.

    Lastly, the Sovrin foundation say that Sovrin will simplify identity challenges in various areas. This mainly depends on the amount of people that use Sovrin identities. If it surpasses a critical mass it becomes suitable in those areas to include Sovrin identities to face their challenges. If it only has a relatively low number of users it may not be useful to include it. Nonetheless, one can say that the possibility to store identity attributes that are hidden until their owner chooses to reveal them offer some great possibilities in those areas.

3. JOLOCOM
    Jolocom [10] is an open source project that is currently de- veloping an identity management system that uses hierarchi- cal deterministic keys (HD keys) to offer decentralized iden- tity to its users. Jolocom identities are also self-sovereign.
    Jolocom identities are also self-sovereign


3.1 Design
    The HD keys are generated from a known seed and con- trolled by the users [10] and enable the user to generate further child keys from the parent key [17], which can be recovered later if the seed is known
    This enables users to generate multiple ”personas” which are basically sub identi-ties that can offer anonymity in some interactions.
    In ad- dition, the child keys make it possible to have ownership of IoT devices mapped onto the Jolocom identity.
    However, an implementation of an identity management system that just uses HD keys has usability issues [10], therefore Jolo- com combines HD keys with DIDs
    A DID is derived from the user’s public key and the corresponding DDO is stored on an InterPlanetary File System (IPFS) which is a decen- tralized distributed file storing system Then the mapping of the DID to the hash of the DDO’s IPFS will be stored in a smart contract on the Ethereum blockchain.

    (Claims also have keys that are specific to the claim so that relying parties can validate that the claim is legitimate. Claim keys are linked to the issuer. A claim key can be changed, but old keys are saved, so that a relying party can verify a claim based on the keys that were used to issue it.)

    *To store identity attributes Jolocom uses so-called ”verified credentials” that are files that contain a statement and signa- ture by the verifier identity. 
    An example used in the Jolocom whitepaper for verified credentials is: ”This user is employed by Company X” as a statement and a signature containing metadata about that statement by the verifier identity - in this case Company X.

    Private verified credentials usually re- quire access control and are stored on self-hosted servers when they should be constantly available and on the user’s device when they do not have to be constantly available. Public verified credentials with constant availability should be stored on distributed storage, for example IPFS. In the case of non-constant availability, the authors list no stor- age proposal because there is ”no apparent use case for this configuration”

3.2 Evaluation
    Besides the claim for self-sovereign identity Jolocom does not promise any additional benefits of its technology - nei- ther in the paper nor on its website. Since Jolocom already has a working application it therefore fulfills its claims.
    However, there is one thing that Jolocom does not do (and does not claim to do) that is not entirely clear: In their con- clusion the authors write: ”We offer a truly self-sovereign decentralised digital identity solution” [10]. This could make someone believe that Jolocom eliminates all need for trusted third parties (TTPs).
    But this is not the case since Jolocom does not remove the need for a TTP when it comes to au- thenticating the attributes and getting verified credentials.
    (*verify credentials를 얻을떄 그떄 딱 사진을 찍는게 어떨까? )


4. UPORT
    uPort is an open source identity management system that is used on the decentralized internet
    It claims to en- able users to have a self-sovereign identity registered on the Ethereum blockchain which can then be used for some applications like the usage of credentials or managing of data. Currently, uPort exists only as a mobile application
    (sovrin같은 경우 hyperledger indy jolocom같은 경우 public -> ipfs private -> smartphone 결국 정보를 어디다가 저장할건지를 말하는거네)
    (여기서는 ethereum 블록체인에 자신의 데이터를 저장하고 이런 데이터를 다른 응용프로그램에서 사용하는것?)

4.1 Design
    To implement its self-sovereign identities uPort uses smart contracts on the Ethereum blockchain.
    uPort uses two smart contracts on the Ethereum blockchain that are called controller and proxy.


    *Because the private key is only stored on the user’s mobile phone which can get lost, uPort has a system that enables its users to regain control of their identity with a different key. The system works as follows: The user nominates a group of trustees (with their uPortID) in advance. The trustees can then vote to change the associated public key of the user’s uPortID with a new one and the key will be changed once a quorum is reached. Note, that there is no way for the system to identify whether the private key was truly lost. Therefore, it is possible for malicious trustees to take over a uPortID if they get quorum
    (스마트폰을 잃어버렸을떄의 공개키를 어떻게 바꿔주는가)
    (임시인증, private key 찾는거)
    

Reference: Julian Roos
Advisor: Heiko Niedermayer
Seminar Innovative Internet Technologies and Mobile Communications Chair of Network Architectures and Services Departments of Informatics, Technical University of Munich Email: ga58moy@mytum.de

https://blog.sovrin.org/how-sovrin-works-a1dff156c68e
</pre> 
